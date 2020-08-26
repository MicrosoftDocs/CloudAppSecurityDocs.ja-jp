---
title: Google Cloud Platform を Cloud App Security に接続する
description: この記事では、API コネクタを使用して Google Cloud Platform を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/28/2020
ms.topic: how-to
ms.service: cloud-app-security
ms.collection: M365-security-compliance
ms.openlocfilehash: 6639761e2be3ef2f5a0bd9d5367bad44f0d12895
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781159"
---
# <a name="connect-google-cloud-platform-to-microsoft-cloud-app-security"></a>Google Cloud Platform を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の Google Cloud Platform (GCP) アカウントに接続する手順について説明します。 この接続を使用すると、GCP の使用状況を表示したり制御したりできます。 Cloud App Security で GCP を保護する方法の詳細については、[GCP の保護](protect-gcp.md)に関するページを参照してください。

安定した統合を維持し、セットアップ プロセスが削除または変更されるのを防ぐために、統合に専用のプロジェクトを使用し、プロジェクトへのアクセスを制限することをお勧めします。 また、GCP インスタンスが、Cloud App Security に既に接続されている G Suite インスタンスの一部である場合は、GCP 接続の詳細を追加するときに、「**接続されている G Suite 組織の一部である GCP インスタンスの場合**」の手順に従うことをお勧めします。

## <a name="prerequisites"></a>[前提条件]

統合 GCP ユーザーには、次のアクセス許可が必要です。

- **IAM と管理者の編集** - 組織レベル
- **プロジェクトの作成と編集**

Cloud App Security 接続には、次の GCP の一方または両方を接続できます。

- **セキュリティ監査**: この接続を使用すると、GCP アプリの使用状況を表示したり制御したりすることができます。
- **セキュリティ構成**: この接続では、GCP の Center for Internet Security (CIS) ベンチマークに基づいたセキュリティに関する基本的な推奨事項が提供されます。

接続のいずれか一方または両方を追加できるため、この記事では、各接続の手順を個別の手順として説明します。 接続のいずれか一方を既に追加している場合は、必要に応じて既存の構成を編集してください。

## <a name="how-to-connect-gcp-security-auditing-to-cloud-app-security"></a>GCP のセキュリティ監査を Cloud App Security に接続する方法

GCP のセキュリティ監査を接続すると、GCP アプリの使用状況を表示したり制御したりすることができます。

AWS のセキュリティ監査を Cloud App Security に接続するには、次の手順に従います。

> [!div class="checklist"]
>
> - [Google Cloud Platform の構成](#configure-google-cloud-platform)
> - [Google Cloud Platform 監査の Cloud App Security への接続](#connect-google-cloud-platform-auditing-to-cloud-app-security)
> - [集計エクスポート シンク](#aggregated-export-sink)

### <a name="configure-google-cloud-platform"></a>Google Cloud Platform の構成

> [!NOTE]
> 監査のために GCP 環境に接続するための手順は、集計ログを使用するための [Google の推奨事項](https://cloud.google.com/blog/products/gcp/best-practices-for-working-with-google-cloud-audit-logging)に従っています。 統合では Google StackDriver が活用され、課金に影響する可能性のある追加のリソースが消費されます。 消費されるリソースは次のとおりです。
>
> - [集計エクスポート シンク - 組織レベル](https://cloud.google.com/logging/docs/export/aggregated_exports#concept)
> - [Pub/Sub トピック – GCP プロジェクト レベル](https://cloud.google.com/logging/docs/export/using_exported_logs#pubsub-overview)
> - [Pub/Sub サブスクリプション – GCP プロジェクト レベル](https://cloud.google.com/logging/docs/export/using_exported_logs#pubsub-overview)
>
> Cloud App Security の監査接続では管理アクティビティの監査ログのみがインポートされます。データ アクセスとシステム イベントの監査ログはインポートされません。 GCP ログの詳細については、「[Cloud 監査ログ](https://go.microsoft.com/fwlink/?linkid=2109230)」を参照してください。

#### <a name="create-a-dedicated-project"></a>専用プロジェクトを作成する

組織の GCP で専用プロジェクトを作成して、統合の分離と安定性を実現します。

1. 統合 GCP ユーザー アカウントを使用して、GCP ポータルにサインインします。
1. **[Create Project]\(プロジェクトの作成\)** をクリックして、新規作成を開始します。
1. **[New project]\(新しいプロジェクト\)** 画面で、プロジェクトに名前を指定し、 **[Create]** をクリックします。

    ![GCP のプロジェクトの作成ダイアログを示すスクリーンショット](media/connect-gcp-create-project.png)

#### <a name="enable-required-apis"></a>必要な API を有効にする

1. 専用プロジェクトに切り替えます。
1. **[ライブラリ]** タブに移動します。
1. **[Cloud Logging API]** を検索して選択し、API ページで **[有効にする]** をクリックします。
1. **[Cloud Pub/Sub API]** を検索して選択し、API ページで **[有効にする]** をクリックします。

    > [!NOTE]
    > **[Pub/Sub Lite API]** は選択しないでください。

#### <a name="create-a-dedicated-service-account-for-the-security-auditing-integration"></a>セキュリティ監査統合用の専用サービス アカウントを作成する

1. **[IAM & admin]\(IAM & 管理\)** で、 **[Service accounts]\(サービス アカウント\)** をクリックします。
1. **[CREATE SERVICE ACCOUNT]\(サービス アカウントの作成\)** をクリックして、専用のサービス アカウントを作成します。
1. アカウント名を入力し、 **[Create]\(作成\)** をクリックします。
1. **[Role]\(ロール\)** を **[Pub/Sub Admin]\(Pub/Sub 管理者\)** として指定し、 **[Save]\(保存\)** をクリックします。

    ![GCP の IAM ロールの追加機能を示すスクリーンショット](media/connect-gcp-iam-role.PNG)

1. **[Email]\(電子メール\)** の値をコピーします。この値は後で必要になります。

    ![GCP の [Service accounts]\(サービス アカウント\) ダイアログを示すスクリーンショット](media/connect-gcp-create-service-account.png)

1. **[IAM & admin]\(IAM & 管理\)** で、 **[IAM]** をクリックします。

    1. 組織レベルに切り替えます。
    1. **[ADD]** をクリックします。
    1. **[New members]\(新しいメンバー\)** ボックスに、先ほどコピーした **[Email]\(電子メール\)** の値を貼り付けます。
    1. **[Role]\(ロール\)** を **[Logs Configuration Writer]\(ログ構成ライター\)** として指定し、 **[Save]\(保存\)** をクリックします。

        ![メンバーの追加ダイアログを示すスクリーンショット](media/connect-gcp-add-member.png)

#### <a name="create-a-private-key-for-the-dedicated-service-account"></a>専用サービス アカウントの秘密キーを作成する

1. プロジェクト レベルに切り替えます。
1. **[IAM & admin]\(IAM & 管理\)** で、 **[Service accounts]\(サービス アカウント\)** をクリックします。
1. 専用サービス アカウントを開き、 **[Edit]\(編集\)** をクリックします。
1. **[CREATE KEY]\(キーの作成\)** をクリックします。
1. **[Create private key]\(秘密キーの作成\)** 画面で **[JSON]** を選択し、 **[Create]\(作成\)** をクリックします。

    ![秘密キーの作成ダイアログを示すスクリーンショット](media/connect-gcp-create-private-key.png)

    > [!NOTE]
    > 後でコンピューターにダウンロードされる JSON ファイルが必要になります。

#### <a name="retrieve-your-organization-id"></a>組織 ID を取得する

**組織 ID** をメモしておきます。後で必要になります。 詳細については、「[組織 ID の取得](https://cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id)」を参照してください。

![組織 ID ダイアログを示すスクリーンショット](media/connect-gcp-org-id.png)

### <a name="connect-google-cloud-platform-auditing-to-cloud-app-security"></a>Google Cloud Platform 監査の Cloud App Security への接続

#### <a name="add-the-gcp-connection-details"></a>GCP 接続の詳細を追加する

1. Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. **[アプリ コネクタ]** ページで、次のいずれかの手順を行って、AWS コネクタの資格情報を入力します。

    > [!NOTE]
    > G Suite インスタンスを接続して、統合ユーザー管理およびガバナンスを実現することをお勧めします。 これは、G Suite 製品を使用せず、GCP ユーザーが G Suite ユーザー管理システムを介して管理されている場合でも推奨されます。

    **新しいコネクタの場合**

    1. プラス記号をクリックし、 **[Google Cloud Platform]** をクリックします。

        ![GCP の接続](media/connect-gcp-add.png)

    1. ポップアップでコネクタの名前を指定し、 **[Connect Google Cloud Platform]\(Google Cloud Platform に接続する\)** をクリックします。

        ![GCP コネクタ名](media/connect-gcp-name.png)

    1. **[プロジェクトの詳細]** ページで、次の操作を行い、 **[Connect Google Cloud Platform]\(Google Cloud Platform に接続する\)** をクリックします。
        1. **[Organization ID]\(組織 ID\)** ボックスに、前にメモしておいた組織を入力します。
        1. **[Private key file]\(秘密キー ファイル\)** ボックスで、前の手順でダウンロードした JSON ファイルに移動します。

        ![新しいコネクタ用に GCP アプリのセキュリティ監査を接続する](media/connect-gcp-app-audit.png)

    **既存のコネクタの場合**

    1. コネクタの一覧で、AWS コネクタが表示されている行の **[Connect security auditing]\(セキュリティ監査を接続\)** をクリックします。

        ![セキュリティ監査の編集リンクを示す [接続アプリ] ページのスクリーンショット](media/connect-gcp-app-edit-audit.png)

    1. **[プロジェクトの詳細]** ページで、次の操作を行い、 **[Connect Google Cloud Platform]\(Google Cloud Platform に接続する\)** をクリックします。
        1. **[Organization ID]\(組織 ID\)** ボックスに、前にメモしておいた組織を入力します。
        1. **[Private key file]\(秘密キー ファイル\)** ボックスで、前の手順でダウンロードした JSON ファイルに移動します。

        ![既存のコネクタ用に GCP アプリのセキュリティ監査を接続する](media/connect-gcp-app-edit-audit-creds.png)

1. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 完了すると、成功または失敗の通知が表示されます。 成功の通知を受信したら、 **[完了]** をクリックします。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

### <a name="aggregated-export-sink"></a>集計エクスポート シンク

現時点では、集計エクスポート シンクの無効化は Google Cloud Shell 経由でのみ可能です。

#### <a name="to-disable-aggregated-export-sink"></a>集計エクスポート シンクを無効にするには

| 手順 | スクリプト | 詳細情報 |
|-|-|-|
| 1.Google Cloud Shell セッションを開始します。 | | [Cloud Shell の使用](https://cloud.google.com/shell/docs/using-cloud-shell) |
| 2.現在のプロジェクトを設定します。 | `gcloud config set project {PROJECT_ID}` | [gcloud config set](https://cloud.google.com/sdk/gcloud/reference/config/set) |
| 3.組織レベルのシンクを一覧表示します。 | `gcloud logging sinks list --organization={ORGANIZATION_ID}` | [gcloud ログ シンクの一覧](https://cloud.google.com/sdk/gcloud/reference/logging/sinks/list) |
| 4.関連するシンクを削除します。 | `gcloud logging sinks delete {SINK_NAME} --organization={ORGANIZATION_ID}` | [gcloud ログ シンクの削除](https://cloud.google.com/sdk/gcloud/reference/logging/sinks/delete) |

## <a name="how-to-connect-gcp-security-configuration-to-cloud-app-security"></a>GCP のセキュリティ構成を Cloud App Security に接続する方法

GCP のセキュリティ構成を接続すると、GCP の Center for Internet Security (CIS) ベンチマークに基づいたセキュリティに関する基本的な推奨事項の分析情報が提供されます。

GCP のセキュリティ構成を Cloud App Security に接続するには、次の手順に従います。

> [!div class="checklist"]
>
> - [Security Health Analytics を使用して GCP Security Command Center を設定する](#set-up-gcp-security-command-center-with-security-health-analytics)
> - [Security Command Center API を有効にする](#enable-security-command-center-api)
> - [セキュリティ構成統合用の専用サービス アカウントを作成する](#create-a-dedicated-service-account-for-the-security-configuration-integration)
> - [Google Cloud Platform のセキュリティ構成を Cloud App Security に接続する](#connect-google-cloud-platform-security-configuration-to-cloud-app-security)

### <a name="set-up-gcp-security-command-center-with-security-health-analytics"></a>Security Health Analytics を使用して GCP Security Command Center を設定する

1. [Security Command Center](https://cloud.google.com/security-command-center/docs/quickstart-security-command-center) を設定します。
1. [GCP Security Health Analytics を有効にします](https://cloud.google.com/security-command-center/docs/how-to-use-security-health-analytics)。
1. Security Command Center にデータが流れていることを確認します。

    > [!NOTE]
    >
    > - セキュリティ構成のために GCP 環境に接続するための手順は、セキュリティ構成の推奨事項を利用するための [Google の推奨事項](https://cloud.google.com/security-command-center/docs/how-to-notifications#enable-scc-api)に従っています。 統合では Google Security Command Center が活用され、課金に影響する可能性のある追加のリソースが消費されます。
    > - Security Health Analytics を初めて有効にする場合は、データが使用可能になるまで数時間かかることがあります。

### <a name="enable-security-command-center-api"></a>Security Command Center API を有効にする

1. Cloud Console API ライブラリで、Cloud App Security に接続するプロジェクトを選択します。
1. API ライブラリで、「Security Command Center API」を検索して選択します。
1. [API] ページで、 **[有効にする]** をクリックします。

### <a name="create-a-dedicated-service-account-for-the-security-configuration-integration"></a>セキュリティ構成統合用の専用サービス アカウントを作成する

1. GCP Security Command Center で、Cloud App Security に接続するプロジェクトを選択します。
1. **[IAM & admin]\(IAM & 管理\)** で、 **[Service accounts]\(サービス アカウント\)** をクリックします。
1. **[CREATE SERVICE ACCOUNT]\(サービス アカウントの作成\)** をクリックして、専用のサービス アカウントを作成します。
1. アカウント名を入力し、 **[Create]\(作成\)** をクリックします。
1. **[ロール]** を **[Security Center Admin Viewer]\(Security Center 管理者ビューアー\)** として指定し、 **[保存]** をクリックします。

    ![Security Center 管理者ビューアー用の GCP のメニュー項目の追加を示すスクリーンショット](media/connect-gcp-security-configuration-1.png)

1. **[Email]\(電子メール\)** の値をコピーします。この値は後で必要になります。

    ![GCP サービス アカウントのコピーを示すスクリーンショット](media/connect-gcp-security-configuration-2.png)

1. **[IAM & admin]\(IAM & 管理\)** で、 **[IAM]** をクリックします。

    1. 組織レベルに切り替えます。
    1. **[ADD]** をクリックします。
    1. **[New members]\(新しいメンバー\)** ボックスに、先ほどコピーした **[Email]\(電子メール\)** の値を貼り付けます。
    1. **[ロール]** を **[Security Center Admin Viewer]\(Security Center 管理者ビューアー\)** として指定し、 **[保存]** をクリックします。

        ![プロジェクトへのメンバーの追加ダイアログを示すスクリーンショット](media/connect-gcp-security-configuration-3.png)

#### <a name="create-a-private-key-for-the-dedicated-service-account"></a>専用サービス アカウントの秘密キーを作成する

1. プロジェクト レベルに切り替えます。
1. **[IAM & admin]\(IAM & 管理\)** で、 **[Service accounts]\(サービス アカウント\)** をクリックします。
1. 専用サービス アカウントを開き、 **[Edit]\(編集\)** をクリックします。
1. **[CREATE KEY]\(キーの作成\)** をクリックします。
1. **[Create private key]\(秘密キーの作成\)** 画面で **[JSON]** を選択し、 **[Create]\(作成\)** をクリックします。

    ![専用サービス アカウントの秘密キーの作成ダイアログを示すスクリーンショット](media/connect-gcp-security-configuration-4.png)

    > [!NOTE]
    > 後でコンピューターにダウンロードされる JSON ファイルが必要になります。

#### <a name="retrieve-your-organization-id"></a>組織 ID を取得する

**組織 ID** をメモしておきます。後で必要になります。 詳細については、「[組織 ID の取得](https://cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id)」を参照してください。
    ![組織 ID ダイアログを示すスクリーンショット](media/connect-gcp-org-id.png)

### <a name="connect-google-cloud-platform-security-configuration-to-cloud-app-security"></a>Google Cloud Platform のセキュリティ構成を Cloud App Security に接続する

1. Cloud App Security で、 **[調査]** をクリックし、 **[接続アプリ]** を選択します。

1. **[Security configuration apps]\(セキュリティ構成アプリ\)** タブで、[+] ボタンをクリックして、 **[Google Cloud Platform]** を選択します。

    ![GCP メニュー オプションの追加を示すスクリーンショット](media/connect-gcp-security-configuration-5.png)

1. **[インスタンス名]** ページで、インスタンスの種類を選択して、 **[次へ]** をクリックします。

    - 既存のコネクタの場合は、関連するインスタンスを選択します。

        ![GCP インスタンスの選択](media/connect-gcp-existing-instance.png)

    - 新しいコネクタの場合は、インスタンスの名前を指定します。

        ![GCP の新しいコネクタ名](media/connect-gcp-new-instance.png)

1. **[プロジェクトの詳細]** ページで、次の操作を行い、 **[次へ]** をクリックします。
    1. **[Organization ID]\(組織 ID\)** ボックスに、前にメモしておいた組織を入力します。
    1. **[Private key file]\(秘密キー ファイル\)** ボックスで、前の手順でダウンロードした JSON ファイルに移動します。

    ![GCP プロジェクトの詳細の追加](media/connect-gcp-security-configuration-6.png)

1. **[完了]** ページで、接続が成功したことを確認し、 **[完了]** をクリックします。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
