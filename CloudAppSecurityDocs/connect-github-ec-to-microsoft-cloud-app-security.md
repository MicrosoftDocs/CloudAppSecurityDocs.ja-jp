---
title: GitHub Enterprise Cloud を Cloud App Security に接続する
description: この記事では、API コネクタを使用して GitHub Enterprise Cloud を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/28/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ROBOTS: NOINDEX
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: bb3196fb47641fad788fda6c98777bbe2ce70a8c
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781142"
---
# <a name="connect-github-enterprise-cloud-to-microsoft-cloud-app-security"></a>GitHub Enterprise Cloud を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、既存の GitHub Enterprise Cloud 組織を、App Connector API を使用して Microsoft Cloud App Security に接続する方法を説明します。 この接続により、組織の GitHub Enterprise Cloud の使用を可視化し、制御することができます。 Cloud App Security によって GitHub Enterprise Cloud が保護される方法の詳細については、[GitHub Enterprise の保護](protect-github.md)に関するページを参照してください。

## <a name="prerequisites"></a>[前提条件]

- 組織に GitHub Enterprise Cloud のライセンスがある必要があります。
- Cloud App Security に接続するために使用する GitHub アカウントには、組織の "*所有者*" アクセス許可が必要です。
- 組織の所有者を確認するには、組織のページに移動し、 **[ユーザー]** を選択して、"*所有者*" でフィルター処理します。

## <a name="how-to-connect-github-enterprise-cloud-to-cloud-app-security"></a>GitHub Enterprise Cloud を Cloud App Security に接続する方法

### <a name="verify-your-github-domains"></a>GitHub ドメインを確認する

ドメインの確認は任意です。 ただし、Cloud App Security によって GitHub 組織のメンバーのドメイン メールを対応する Azure Active Directory ユーザーと照合できるように、ドメインを確認することを強くお勧めします。

これらの手順は、「[GitHub Enterprise Cloud を構成する](#configure-github-enterprise-cloud)」の手順とは関係なく完了でき、ドメインを既に確認してある場合はスキップできます。

1. 組織を[企業利用規約](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/upgrading-to-the-corporate-terms-of-service)にアップグレードします。
1. [組織のドメイン](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/verifying-your-organizations-domain)を確認します。

    > [!NOTE]
    > Cloud App Security ポータルの一覧に表示されている各マネージド ドメインを確認します。 マネージド ドメインを表示するには、Cloud App Security で **[設定]**  >  **[組織の詳細]**  >  **[マネージド ドメイン]** を参照します。

### <a name="configure-github-enterprise-cloud"></a>GitHub Enterprise Cloud を構成する

1. **組織のログイン名を検索する**  
GitHub で組織のページを参照し、URL から、組織のログイン名を記録しておきます。後で必要になります。

    > [!NOTE]
    > ページの URL は `https://github.com/<your-organization>` のようなものです。 たとえば、組織のページが `https://github.com/sample-organization` である場合、組織のログイン名は *sample-organization* になります。

    ![組織のログイン名の取得を示すスクリーンショット](media/connect-github-org-login-name.png)

1. **GitHub 組織に接続するための Cloud App Security 用の OAuth アプリを作成します。**  
接続する追加の組織ごとに、この手順を繰り返します。

    1. **[設定]**  >  **[開発者向け設定]** に移動し、 **[OAuth アプリ]** を選択して、 **[アプリケーションの登録]** をクリックします。 または、既存の OAuth アプリがある場合は、 **[New OAuth App]\(新しい OAuth アプリ\)** をクリックします。

        ![OAuth アプリの作成を示すスクリーンショット](media/connect-github-create-oauth-app.png)

    1. **[Register a new OAuth app]\(新しい OAuth アプリを登録\)** で詳細を入力し、 **[アプリケーションの登録]** をクリックします。
        - **[アプリケーション名]** ボックスに、アプリの名前を入力します。
        - **[ホームページ URL]** ボックスに、アプリのホーム ページの URL を入力します。
        - **[認証コールバックの URL]** ボックスに、「`https://portal.cloudappsecurity.com/api/oauth/connect`」という値を入力します。

        ![OAuth アプリの登録を示すスクリーンショット](media/connect-github-register-oauth-app.png)

    > [!NOTE]
    >
    > - 既定では、OAuth アプリのアクセスは組織に限定されています。 アクセスを有効にするには、 **[設定]**  >  **[Third-party access]\(サードパーティのアクセス\)** に移動し、 **[Remove restrictions]\(制限の削除\)** をクリックして、 **[Yes, remove application restrictions]\(はい、アプリケーションの制限を削除します\)** をクリックします。
    > - 組織が所有するアプリでは、組織のアプリにアクセスできます。 詳細については、「[OAuth アプリケーションのアクセス制限について](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/about-oauth-app-access-restrictions)」を参照してください。

1. **[設定]**  >  **[OAuth アプリ]** に移動し、作成した OAuth アプリを選択して、その **[クライアント ID]** と **[クライアント シークレット]** を記録しておきます。

    ![OAuth アプリの詳細を示すスクリーンショット](media/connect-github-oauth-app-details.png)

### <a name="configure-cloud-app-security"></a>Cloud App Security を構成する

1. Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. **[アプリ コネクタ]** ページで、[+] ボタン、 **[GitHub]** の順にクリックします。

1. ポップアップで、 **[クライアント ID]** 、 **[クライアント シークレット]** 、 **[Organization Login Name]\(組織のログイン名\)** に記録しておいた値を入力して、 **[Connect in GitHub]\(GitHub で接続\)** をクリックします。

    ![GitHub API の接続を示すスクリーンショット](media/connect-github-connect-app.png)

    GitHub のサインイン ページが開きます。 必要に応じて、GitHub 管理者の資格情報を入力して、チームの GitHub Enterprise Cloud インスタンスへの Cloud App Security のアクセスを許可します。

1. GitHub 組織へのアクセス権を Cloud App Security に付与することをアプリに許可します。

    > [!NOTE]
    > Cloud App Security には、次の OAuth スコープが必要です。
    >
    > - **admin:org** - 組織の監査ログを同期するために必要です
    > - **read:user** と **user:email** - 組織のメンバーを同期するために必要です
    > - **repo:status** - 監査ログでリポジトリ関連のイベントを同期するために必要です。OAuth のスコープの詳細については、「[OAuth アプリのスコープについて](https://developer.github.com/apps/building-oauth-apps/understanding-scopes-for-oauth-apps/)」を参照してください。

    ![GitHub の OAuth の承認を示すスクリーンショット](media/connect-github-authorize-app.png)

1. Cloud App Security コンソールに戻ると、GitHub と正常に接続されたことを示すメッセージが届きます。

1. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

GitHub Enterprise Cloud に接続すると、接続前の 7 日間のイベントが表示されます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
