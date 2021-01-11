---
title: Google Workspace を Cloud App Security に接続する
description: この記事では、API コネクタを使用して Google Workspace を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
ms.date: 11/27/2019
ms.topic: how-to
ms.openlocfilehash: 0d9d99d650ab0d68f8bd6dd129f6b01c78fb2cc5
ms.sourcegitcommit: 16a65ab2c8ca778d0b3cfa97b847af4c812363b2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2021
ms.locfileid: "97855576"
---
# <a name="connect-google-workspace-to-microsoft-cloud-app-security"></a>Google Workspace を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の Google Workspace アカウントに接続する手順について説明します。 この接続を使用すると、Google Workspace の使用状況を表示したり制御したりすることができます。 Cloud App Security で Google Workspace を保護する方法の詳細については、[Google Workspace の保護](protect-google-workspace.md)に関するページを参照してください。

## <a name="configure-google-workspace"></a>Google Workspace を構成する

1. Google Workspace のスーパー管理者として、<a href="https://cloud.google.com/console/project" target="_blank">https://cloud.google.com/console/project</a> にサインインします。

1. **[プロジェクトを作成]** をクリックして、新しいプロジェクトを開始します。

    ![Google プロジェクトの作成](media/connect-google-workspace/google-workspace-create-new-project.png)

1. **[新しいプロジェクト]** ページで、プロジェクトに次のように名前を指定します。「**Cloud App Security**」。 **[作成]** をクリックします。

    ![Google 新規プロジェクトのポップアップ](media/connect-google-workspace/google-workspace-create-new-project-popup.png)

1. プロジェクトが作成されたら、ツールバーの **[Google Cloud Platform]** をクリックします。 上部のドロップダウンで、適切なプロジェクトが選択されていることを確認します。

    ![ツール バーの [Google Cloud Platform] をクリック](media/connect-google-workspace/google-workspace-verify-project.png)

1. メニューを選択し、 **[API とサービス]**  >  **[ライブラリ]** に移動して、次の API を有効にします (API が一覧表示されない場合は、検索行を使用します)。

    - Admin SDK API

    - Audit API
    - Google Drive API
    - Google Workspace Marketplace SDK

    > [!NOTE]
    > 各 API について、 **[有効にする]** をクリックしてアクティブにします。
    >
    > ![Google API を有効にする](media/connect-google-workspace/google-workspace-api.png)
    >
    > 現時点では、**認証情報** の警告を無視します。

1. メニューを選択し、 **[API とサービス]**  >  **[ダッシュボード]** に移動して、次の API が有効になっていることを確認します。

    - Admin SDK API

    - Audit API
    - Google Drive API
    - Google Workspace Marketplace SDK

1. **[OAuth 同意ページ]** のページで、次の操作を行います。
    1. **[ユーザーの種類]** で、 **[外部]** を選択し、 **[作成]** をクリックします。

        ![Google OAuth 同意のユーザーの種類](media/connect-google-workspace/google-workspace-oauth-consent-user-type.png)

    1. 次の情報を入力し、 **[保存]** をクリックします。

        | フィールド名 | 値 |
        | --- | --- |
        | アプリケーションの種類 | パブリック |
        | アプリケーション名 | Microsoft Cloud App Security |
        | サポート メール | `<your_email_address>` |

        その他のフィールドはすべて省略可能です。

        ![Google OAuth 同意のアプリの種類](media/connect-google-workspace/google-workspace-oauth-consent-app-type.png)

1. **[認証情報]** ページで、次の操作を実行します。
    1. **[認証情報の作成]** を選択し、 **[サービス アカウント]** を選択します。
    1. **[サービス アカウントの詳細]** に、名前と説明を入力して、 **[作成]** をクリックします。
    1. [**Grant this service account access to project]\(このサービス アカウントにプロジェクトへのアクセスを許可\)** の **[ロール]** に **[プロジェクト]** を選択し、 **[エディター]** を選択して、 **[完了]** をクリックします。

    ![Google のサービス アカウントの作成](media/connect-google-workspace/google-workspace-create-service-account.png)

1. **[サービス アカウント]** ページで、次の操作を行います。
    1. **[サービス アカウント]** で、前に作成したサービス アカウントを探して編集します。

        ![Google のサービス アカウントの編集](media/connect-google-workspace/google-workspace-edit-service-account.png)

    1. メール アドレスをコピーします。 これは後で必要になります。
    1. **[キー]** の **[キーの追加]** メニューで、 **[新しいキーの作成]** を選択し、 **[P12]** を選択して、 **[作成]** をクリックします。 ダウンロードしたファイルを保存します。これは、後で必要になります。
    1. **[サービス アカウントの状態]** で、 **[G Suite ドメイン全体の委任を有効にする]** を選択し、 **[保存]** をクリックします。

    ![Google のサービス アカウントの更新](media/connect-google-workspace/google-workspace-update-service-account.png)

1. **[認証情報]** ページの、 **[OAuth 2.0 クライアント ID]** の下で、サービス アカウントに割り当てられている **クライアント ID** をコピーします。これは、後で必要になります。

    ![Google Workspace 認証情報サービス アカウント](media/connect-google-workspace/google-workspace-copy-service-account-client-id.png)

1. [admin.google.com](https://admin.google.com/) に移動し、 **[セキュリティ]**  >  **[API 管理]**  >  **[MANAGE DOMAIN WIDE DELEGATION]\(ドメイン全体の委任の管理\)** に移動し、 **[新規追加]** をクリックして、次の操作を行います。

    1. **[クライアント ID]** ボックスに、前にコピーした **クライアント ID** を入力します。
    1. **[OAuth スコープ]** ボックスに、次の必要なスコープの一覧を入力します (テキストをコピーしてボックスに貼り付けます)。  
    `https://www.googleapis.com/auth/admin.reports.audit.readonly,https://www.googleapis.com/auth/admin.reports.usage.readonly,https://www.googleapis.com/auth/drive,https://www.googleapis.com/auth/drive.appdata,https://www.googleapis.com/auth/drive.apps.readonly,https://www.googleapis.com/auth/drive.file,https://www.googleapis.com/auth/drive.metadata.readonly,https://www.googleapis.com/auth/drive.readonly,https://www.googleapis.com/auth/drive.scripts,https://www.googleapis.com/auth/admin.directory.user.readonly,https://www.googleapis.com/auth/admin.directory.user.security,https://www.googleapis.com/auth/admin.directory.user.alias,https://www.googleapis.com/auth/admin.directory.orgunit,https://www.googleapis.com/auth/admin.directory.notifications,https://www.googleapis.com/auth/admin.directory.group.member,https://www.googleapis.com/auth/admin.directory.group,https://www.googleapis.com/auth/admin.directory.device.mobile.action,https://www.googleapis.com/auth/admin.directory.device.mobile,https://www.googleapis.com/auth/admin.directory.user`

    1. **[承認]** をクリックします。

    ![Google Workspace の新しいクライアント ID の追加](media/connect-google-workspace/google-workspace-add-new-client-id.png)

## <a name="configure-cloud-app-security"></a>Cloud App Security を構成する

1. Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. Google Workspace 接続の詳細を指定するには、 **[アプリ コネクタ]** で次のいずれかの操作を行います。

    **既に GCP インスタンスが接続されている Google Workspace 組織の場合**

    - コネクタの一覧で、GCP インスタンスが表示されている行の末尾にある 3 つのドットをクリックし、 **[Google Workspace の追加]** をクリックします。

    **まだ GCP インスタンスが接続されていない Google Workspace 組織の場合**

    - **[接続アプリ]** ページで、プラス記号 **[+]** をクリックし、 **[Google Workspace]** を選択します。

1. ポップアップで、次の情報を入力します。

    ![Cloud App Security での Google Workspace の構成](media/connect-google-workspace/cas-config-google-workspace.png "Cloud App Security での Google Workspace の構成")

    1. 前にコピーした **サービス アカウント ID**、**メール アドレス** を入力します。

    1. 前にコピーした **プロジェクト番号 (アプリ ID)** を入力します。

    1. 前に保存した P12 **証明書** ファイルをアップロードします。

    1. Google Workspace 管理者の **管理者アカウントのメール アドレス** を入力します。

    1. Google Workspace Business または Enterprise アカウントを使用している場合は、このチェック ボックスをオンにします。 Google Workspace Business または Enterprise の場合の Cloud App Security で使用できる機能の詳細については、[アプリの表示、保護、およびガバナンス アクションをすぐに有効にする](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)方法に関するページを参照してください。

    1. **[Save settings]\(設定の保存\)** をクリックします。

    1. **[リンクに移動]** をクリックして Google Workspace に接続します。 これにより、Google Workspace が開き、Cloud App Security へのアクセスを承認するように求められます。

    1. **[今すぐテストする]** をクリックして、正常に接続されたことを確認します。  
    テストには数分かかる場合があります。  
    成功の通知を受信したら、 **[完了]** をクリックし、Google Workspace ページを閉じます。

Google Workspace に接続すると、接続前の 60 日間のイベントが表示されます。

Google Workspace に接続すると、Cloud App Security によってフル スキャンが実行されます。 ファイルとユーザーの数によっては、フル スキャンの完了にしばらく時間がかかります。 ほぼリアルタイムでのスキャンを可能にするため、アクティビティが検出されたファイルがスキャン キューの先頭に移動されます。 たとえば、編集、更新、または共有されたファイルは、ただちにスキャンされます。 これは、本質的に変更されていないファイルには当てはまりません。 たとえば、表示、プレビュー、印刷、またはエクスポートされたファイルは、定期的なスキャン中にスキャンされます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
