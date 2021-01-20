---
title: Cloud App Security を展開する
description: このクイックスタートでは、クラウド アプリの使用状況、分析情報、および制御を得るために Cloud App Security を起動して実行するプロセスについて概説します。
ms.date: 06/07/2020
ms.topic: quickstart
ms.openlocfilehash: 95f4d916fc60db4d8ddbe2a9a87dc1af580e4be9
ms.sourcegitcommit: 7fc4d916a43d188b1aa4e3cee2e8bd1de230d135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98206494"
---
# <a name="quickstart-get-started-with-microsoft-cloud-app-security"></a>クイック スタート:Microsoft Cloud App Security を使ってみる

[!INCLUDE [Banner for top of topics](includes/banner.md)]

このクイックスタートでは、Cloud App Security を起動して実行する手順について説明します。 Microsoft Cloud App Security は、企業リソースの制御を維持しながら、クラウド アプリケーションの利点を活用するのに役立ちます。 これは、クラウド アクティビティの可視性を向上させ、企業データの保護を強化することによって機能します。 この記事では、Microsoft Cloud App Security を設定して使用する手順について説明します。

Cloud App Security を使用するには、組織がライセンスを持っている必要があります。 価格詳細については、[Cloud App Security ライセンス データシート](https://aka.ms/mcaslicensing)を参照してください。

>[!NOTE]
>Cloud App Security では、Office 365 のライセンスは必要ありません。

## <a name="prerequisites"></a>[前提条件]

- Cloud App Security を使用するには、組織がライセンスを持っている必要があります。 価格詳細については、[Cloud App Security ライセンス データシート](https://aka.ms/mcaslicensing)を参照してください。

    テナントのアクティブ化のサポートについては、「[ビジネス製品についてサポートに問い合わせる方法 - 管理者ヘルプ](https://support.office.com/article/Contact-Office-365-for-business-support-Admin-Help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b)」を参照してください。
- Cloud App Security のライセンスを取得すると、ライセンス認証情報と Cloud App Security ポータルへのリンクを含むメールが届きます。

- Cloud App Security をセットアップするには、Azure Active Directory または Office 365 のグローバル管理者またはセキュリティ管理者である必要があります。 管理者ロールが割り当てられているユーザーは、組織がサブスクライブしているすべてのクラウド アプリに対して同じアクセス許可を持つことを理解しておくことが重要です。 これは、ロールを Microsoft 365 管理センターと Azure クラシック ポータルのどちらで割り当てるか、または [Windows PowerShell](/microsoft-365/enterprise/assign-roles-to-user-accounts-with-microsoft-365-powershell?view=o365-worldwide&preserve-view=true) 用 Azure AD モジュールを使用して割り当てるかには関係ありません。 詳細については、[管理者の役割の割り当て](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504)および [Azure Active Directory での管理者の役割の割り当て](/azure/active-directory/users-groups-roles/directory-assign-admin-roles)に関するページ参照してください。

- Cloud App Security ポータルを実行する場合は、Internet Explorer 11、Microsoft Edge (最新版)、Google Chrome (最新版)、Mozilla Firefox (最新版)、Apple Safari (最新版) のいずれかを使用してください。

## <a name="to-access-the-portal"></a>ポータルにアクセスするには

Cloud App Security ポータルにアクセスするには、[https://portal.cloudappsecurity.com](https://portal.cloudappsecurity.com) にアクセスします。 ポータルには、次のように **[Microsoft 365 管理センター](https://security.microsoft.com)** からアクセスすることもできます。

1. Microsoft 365 管理センターのサイド メニューで、 **[すべてを表示]** をクリックし、 **[セキュリティ]** を選択します。

    ![Microsoft 365 管理センターからのアクセス](media/access-from-o365.png)

1. [Microsoft 365 セキュリティ] ページで、 **[その他のリソース]** をクリックしてから **[Cloud App Security]** を選択します。

    ![Cloud App Security の選択](media/access-from-o365-s2.png)

## <a name="step-1-set-instant-visibility-protection-and-governance-actions-for-your-apps"></a>手順 1. [アプリのインスタント表示、保護、およびガバナンス アクションの設定](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)

必須のタスク:アプリを接続する

1. 設定の歯車アイコンから **[アプリ コネクタ]** を選択します。
1. プラス記号 **[+]** をクリックしてアプリを追加し、アプリを選択します。
1. 構成手順に従ってアプリを接続します。

**アプリを接続する理由**
アプリに接続すると、クラウド環境内のアプリのアクティビティ、ファイル、アカウントを調査できるように、より詳細な可視性を得ることができます。

## <a name="step-2-control-cloud-apps-with-policies"></a>手順 2. [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

必須のタスク:ポリシーを作成する

### <a name="to-create-policies"></a>ポリシーを作成するには

1. **[制御]**  >  **[テンプレート]** に移動します。
1. 一覧からポリシー テンプレートを選択し、(+) **[ポリシーの作成]** を選択します。
1. ポリシーをカスタマイズ (フィルター、アクション、およびその他の設定を選択) し、 **[作成]** を選択します。
1. **[ポリシー]** タブでポリシーを選択して、関連する一致項目 (アクティビティ、ファイル、アラート) を確認します。
 ヒント:すべてのクラウド環境のセキュリティ シナリオに対応するには、**リスク カテゴリ** ごとにポリシーを作成します。

### <a name="how-can-policies-help-your-organization"></a>ポリシーは企業でどのように役立つか

ポリシーを使用して、傾向の監視、セキュリティ脅威の確認、カスタマイズされたレポートとアラートの生成を行うことができます。 ポリシーを使用すると、ガバナンス アクションを作成し、データ損失防止とファイル共有制御を設定できます。

## <a name="step-3-set-up-cloud-discovery"></a>手順 3. [Cloud Discovery を設定する](set-up-cloud-discovery.md)

必須のタスク:クラウド アプリの使用状況を表示するには、Cloud App Security を有効にします

1. [Microsoft Defender for Endpoint と統合](mde-integration.md)することで、Cloud App Security が自動的に有効にされ、会社内外のご利用の Windows 10 デバイスを監視できるようになります。
1. [Zscaler](zscaler-integration.md) を使用する場合は、これを Cloud App Security と統合します。
1. 完全なカバレッジを実現するために、継続的な Cloud Discovery レポートを作成する

    1. 設定の歯車アイコンで、 **[Cloud Discovery 設定]** を選択します。
    1. **[自動ログ アップロード]** を選択します。
    1. **[データ ソース]** タブで、ソースを追加します。
    1. **[ログ コレクター]** タブで、ログ コレクターを構成します。

### <a name="to-create-a-snapshot-cloud-discovery-report"></a>Cloud Discovery のスナップショット レポートを作成するには

 **[検出]**  >  **[スナップショット レポート]** に移動し、表示される手順に従います。

### <a name="why-should-you-configure-cloud-discovery-reports"></a>Cloud Discovery レポートを構成する必要がある理由

組織内のシャドウ IT を可視化することは重要です。
ログを分析した後は、どのユーザーが、どのデバイスで、どのクラウド アプリを使用しているかを簡単に確認できます。

## <a name="step-4-personalize-your-experience"></a>手順 4. [エクスペリエンスの個人設定](mail-settings.md)

推奨されるタスク:組織の詳細を追加する

### <a name="to-enter-email-settings"></a>電子メールの設定を入力するには

1. 設定の歯車アイコンで、 **[メールの設定]** を選択します。
1. **[メール送信者の ID]** で、メール アドレスと表示名を入力します。
1. **[メールのデザイン]** で、組織のメール テンプレートをアップロードします。

### <a name="to-set-admin-notifications"></a>管理者通知を設定するには

1. ナビゲーション バーでユーザー名を選択し、 **[ユーザー設定]** に移動します。
1. **[通知]** で、システム通知に設定する方法を構成します。
1. **[保存]** を選びます。

### <a name="to-customize-the-score-metrics"></a>スコアのメトリックをカスタマイズするには

1. 設定の歯車アイコンで、 **[Cloud Discovery 設定]** を選択します。
1. 設定の歯車アイコンで、 **[Cloud Discovery 設定]** を選択します。
1. **[スコア メトリック]** で、さまざまなリスク値の重要度を構成します。
1. **[保存]** を選びます。

これで、検出されたアプリに与えられるリスク スコアが、組織のニーズと優先順位に従って正確に構成されるようになりました。

### <a name="why-personalize-your-environment"></a>環境のカスタマイズが必要な理由

一部の機能は、ニーズに合わせてカスタマイズされている場合に最適に動作します。
独自のメール テンプレートを使用して、ユーザーにより良いエクスペリエンスを提供します。 受信する通知を決定し、ご自分の組織の設定に合わせてご自分のリスク スコア メトリックをカスタマイズします。

## <a name="step-5-organize-the-data-according-to-your-needs"></a>手順 5. [ニーズに応じたデータの編成](ip-tags.md)

推奨されるタスク:重要な設定を構成する

### <a name="to-create-ip-address-tags"></a>IP アドレスのタグを作成するには

1. 設定の歯車アイコンで、 **[Cloud Discovery 設定]** を選択します。
1. 設定の歯車アイコンから **[IP アドレスの範囲]** を選択します。
1. プラス記号 **[+]** をクリックして、IP アドレスの範囲を追加します。
1. IP 範囲の **詳細**、**場所**、**タグ**、および **カテゴリ** を入力します。
1. **[作成]** を選択します。

    これで、ポリシーを作成するときや、継続的なレポートをフィルター処理および作成するときに、IP タグを使用できるようになりました。

### <a name="to-create-continuous-reports"></a>継続的レポートを作成するには

1. 設定の歯車アイコンで、 **[Cloud Discovery 設定]** を選択します。
1. **[継続的レポート]** で、 **[レポートの作成]** を選択します。
1. 構成の手順に従います。
1. **[作成]** を選択します。

これで、ビジネス ユニットや IP 範囲などの独自の設定に基づいて、検出されたデータを表示できるようになりました。

### <a name="to-add-domains"></a>ドメインを追加するには

1. 設定の歯車アイコンで、 **[設定]** を選択します。
1. **[組織の詳細]** で、組織の内部ドメインを追加します。
1. **[保存]** を選びます。

### <a name="why-should-you-configure-these-settings"></a>これらの設定を構成する必要がある理由

これらの設定により、コンソールの機能をより適切に制御できるようになります。 IP タグを使用すると、ニーズに合ったポリシーを作成したり、データを正確にフィルター処理したりできます。 データ ビューを使用して、データを論理カテゴリにグループ化します。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)].
