---
title: PingOne を使用して Web アプリに対して Cloud App Security のアプリの条件付きアクセス制御を展開する
description: この記事では、PingOne ID プロバイダーを使用して Web アプリに対して Microsoft Cloud App Security のアプリの条件付きアクセス制御を展開する方法について説明します。
ms.date: 09/29/2020
ms.topic: how-to
ms.openlocfilehash: df0ab81e2dcb6140f939caff436d18868daad496
ms.sourcegitcommit: f56a2060b99ab087b8637606a1fb66e5577aded8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98795271"
---
# <a name="onboard-and-deploy-conditional-access-app-control-for-any-web-app-using-pingone-as-the-identity-provider-idp"></a>ID プロバイダー (IdP) として PingOne を使用する任意の Web アプリにアプリの条件付きアクセス制御をオンボードして展開する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security のセッション制御は、任意の Web アプリおよびサード パーティー IdP と連動するように構成できます。 この記事では、リアルタイム セッション制御のために、アプリのセッションを PingOne から Cloud App Security にルーティングする方法について説明します。

この記事では、Cloud App Security セッション制御を使用するように構成されている Web アプリの例として、Salesforce アプリを使用します。

## <a name="prerequisites"></a>[前提条件]

- アプリの条件付きアクセス制御を使用するには、お客様の組織が次のライセンスを持っている必要があります。

  - 関連する PingOne ライセンス (シングル サインオンに必要)
  - Microsoft Cloud App Security

- SAML 2.0 認証プロトコルを使用するアプリの既存の PingOne シングル サインオン構成

## <a name="to-configure-session-controls-for-your-app-using-pingone-as-the-idp"></a>IdP として PingOne を使用してアプリのセッション制御を構成するには

次のステップに従って、PingOne から Cloud App Security に Web アプリのセッションをルーティングします。 Azure AD の構成ステップについては、「[Azure AD との統合を構成する](proxy-deployment-any-app.md#configure-integration-with-azure-ad)」を参照してください。

> [!NOTE]
> 次のいずれかの方法を使用して、PingOne によって提供されるアプリの SAML シングル サインオン情報を構成できます。
>
> - **オプション 1**:アプリの SAML メタデータ ファイルのアップロード。
> - **オプション 2**:アプリの SAML データの手動による提供。
>
> 以降のステップでは、オプション 2 を使用します。

**手順 1: [アプリの SAML シングル サインオン設定を取得する](#idp1-get-your-app-saml-sso-info)**

**手順 2: [アプリの SAML 情報で Cloud App Security を構成する](#idp1-conf-cas-with-your-app-saml-info)**

**手順 3: [PingOne でカスタム アプリを作成する](#idp1-create-custom-app-pingone)**

**手順 4: [PingOne アプリの情報で Cloud App Security を構成する](#idp1-conf-cas-with-pingone-app-info)**

**手順 5: [PingOne でカスタム アプリを完成させる](#idp1-complete-custom-app-in-pingone)**

**手順 6: [Cloud App Security でアプリの変更を取得する](#idp1-get-app-changes-in-cas)**

**手順 7: [アプリの変更を完了する](#idp1-complete-app-changes)**

**手順 8: [Cloud App Security の構成を完了する](#idp1-complete-conf-in-cas)**

<a name="idp1-get-your-app-saml-sso-info"></a>

## <a name="step-1-get-your-apps-saml-single-sign-on-settings"></a>手順 1:アプリの SAML シングル サインオン設定を取得する

1. Salesforce で、 **[設定]**  >  **[設定]**  >  **[ID]**  >  **[シングル サインオン設定]** を参照します。

1. **[シングル サインオン設定]** で、お使いの既存の SAML 2.0 構成の名前をクリックします。

    ![Salesforce の SSO 設定を選択する](media/proxy-idp-pingone/idp-pingone-sf-select-sso-settings.png)

1. **[SAML シングルサインオン設定]** ページで、Salesforce の **ログイン URL** をメモしておきます。 これは後で必要になります。

    > [!NOTE]
    > お使いのアプリで SAML 証明書が提供されている場合は、その証明書ファイルをダウンロードします。

    ![Salesforce の SSO ログイン URL を選択する](media/proxy-idp-pingone/idp-pingone-sf-copy-saml-sso-login-url.png)

<a name="idp1-conf-cas-with-your-app-saml-info"></a>

## <a name="step-2-configure-cloud-app-security-with-your-apps-saml-information"></a>手順 2:アプリの SAML 情報で Cloud App Security を構成する

1. Cloud App Security で、 **[調査]**  >  **[接続アプリ]**  >  **[アプリの条件付きアクセス制御アプリ]** の順に移動します。

1. プラス記号 **[+]** をクリックし、ポップアップでデプロイするアプリを選択してから、 **[ウィザード起動]** をクリックします。
1. **[アプリ情報]** ページで、 **[データを手動で入力する]** を選択し、 **[Assertion consumer service URL]** に、前にメモした Salesforce の **ログイン URL** を入力して、 **[次へ]** をクリックします。

    > [!NOTE]
    > アプリで SAML 証明書が提供されている場合は、 **[<アプリ名> の SAML 証明書を使用する]** を選択して、証明書ファイルをアップロードします。

    ![Salesforce の SAML 情報を手動で入力する](media/proxy-idp-pingone/idp-pingone-cas-sf-app-info.png)

<a name="idp1-create-custom-app-pingone"></a>

## <a name="step-3-create-a-custom-app-in-pingone"></a>手順 3:PingOne でカスタム アプリを作成する

続行する前に、次のステップを使用して、既存の Salesforce アプリから情報を取得します。

1. Ping One で、既存の Salesforce アプリを編集します。

1. **[SSO 属性マッピング]** ページで、SAML_SUBJECT 属性と値をメモし、**署名証明書** と **SAML メタデータ** のファイルをダウンロードします。

    ![既存の Salesforce アプリの属性をメモする](media/proxy-idp-pingone/idp-pingone-sf-app-copy-saml-sso-attributes.png)

1. SAML メタデータ ファイルを開き、PingOne の **SingleSignOnService Location** をメモしておきます。 これは後で必要になります。

    ![既存の Salesforce アプリの SSO サービスの場所をメモする](media/proxy-idp-pingone/idp-pingone-sf-app-copy-saml-sso-service-location.png)

1. **[Group Access]\(グループ アクセス\)** ページの、割り当てられたグループをメモしておきます。

    ![既存の Salesforce アプリの割り当てられたグループをメモする](media/proxy-idp-pingone/idp-pingone-sf-app-copy-saml-sso-user-groups.png)

次に、 **[Add a SAML application with your identity provider]\(ID プロバイダーを使用して SAML アプリケーションを追加する\)** ページの指示に従って、IdP のポータルでカスタム アプリを構成します。

![ID プロバイダーを使用して SAML アプリを追加する](media/proxy-deploy-add-idp-get-conf.png)

> [!NOTE]
> カスタム アプリを構成すると、組織の既存の動作を変更することなく、アクセスとセッションの制御を使用して既存のアプリをテストできます。

1. **[New SAML Application]\(新しい SAML アプリケーション\)** を作成します。

    ![PingOne で、Salesforce の新しいカスタム アプリを作成する](media/proxy-idp-pingone/idp-pingone-sf-custom-app-new.png)

1. **[Application Details]\(アプリケーションの詳細\)** ページで、フォームに入力し、 **[Continue to Next Step]\(次のステップに進む\)** をクリックします。

    > [!TIP]
    > カスタム アプリと既存の Salesforce アプリを区別できるアプリ名を使用します。

    ![カスタム アプリの詳細を入力する](media/proxy-idp-pingone/idp-pingone-sf-custom-app-details.png)

1. **[Application Configuration]\(アプリケーション構成\)** ページで、次の操作を行ってから、 **[Continue to Next Step]\(次のステップに進む\)** をクリックします。
    - **[シングル サインオン サービス URL]** フィールドに、前にメモした Salesforce の **ログイン URL** を入力します。
    - **[エンティティ ID]** フィールドに、*https://* で始まる一意の ID を入力します。 これは、既存の Salesforce PingOne アプリの構成とは違うものにしてください。
    - **[エンティティ ID]** をメモしておきます。 これは後で必要になります。

    ![Salesforce の SAML の詳細を使用してカスタム アプリを構成する](media/proxy-idp-pingone/idp-pingone-sf-custom-app-set-saml-sso-properties.png)

1. **[SSO 属性マッピング]** ページで、前にメモした既存の Salesforce アプリの **SAML_SUBJECT** の属性と値を追加して、 **[Continue to Next Step]\(次のステップに進む\)** をクリックします。

    ![Salesforce のカスタム アプリに属性を追加する](media/proxy-idp-pingone/idp-pingone-sf-custom-app-set-saml-sso-attributes.png)

1. **[Group Access]\(グループ アクセス\)** ページで、先ほどメモした既存の Salesforce アプリのグループを追加し、構成を完了します。

    ![Salesforce のカスタム アプリにグループを割り当てる](media/proxy-idp-pingone/idp-pingone-sf-custom-app-set-saml-sso-user-groups.png)

<a name="idp1-conf-cas-with-pingone-app-info"></a>

## <a name="step-4-configure-cloud-app-security-with-the-pingone-apps-information"></a>手順 4:PingOne アプリの情報で Cloud App Security を構成する

1. Cloud App Security の **[ID プロバイダー]** ページに戻り、 **[次へ]** をクリックして続行します。

1. 次のページで、 **[データを手動で入力する]** を選択し、次の手順を実行して、 **[次へ]** をクリックします。
    - **[Assertion Consumer Service URL]** に、前にメモした Salesforce の **ログイン URL** を入力します。
    - **[Upload identity provider's SAML certificate]\(ID プロバイダーの SAML 証明書をアップロードする\)** を選択し、先ほどダウンロードした証明書ファイルをアップロードします。

    ![SSO サービスの URL と SAML 証明書を追加する](media/proxy-idp-pingone/idp-pingone-cas-sf-app-idp-info.png)

1. 次のページで、以下の情報をメモしてから、 **[次へ]** をクリックします。 この情報は後で必要になります。

    - Cloud App Security のシングル サインオン URL
    - Cloud App Security の属性と値

    ![Cloud App Security の SSO の URL と属性をメモする](media/proxy-idp-pingone/idp-pingone-cas-get-sf-app-external-config.png)

<a name="idp1-complete-custom-app-in-pingone"></a>

## <a name="step-5-complete-the-custom-app-in-pingone"></a>手順 5:PingOne でカスタム アプリを完成させる

1. Ping One で、Salesforce のカスタム アプリを見つけて編集します。

    ![Salesforce のカスタム アプリを検索して編集する](media/proxy-idp-pingone/idp-pingone-sf-custom-app-edit.png)

1. **[Assertion Consumer Service (ACS)]** フィールドで、URL を前にメモした Cloud App Security のシングル サインオン URL に置き換え、 **[次へ]** をクリックします。

    ![Salesforce のカスタム アプリの ACS を置き換える](media/proxy-idp-pingone/idp-pingone-sf-custom-app-replace-saml-sso-properties.png)

1. 前にメモしておいた Cloud App Security の属性と値を、アプリのプロパティに追加します。

    ![Salesforce のカスタム アプリに Cloud App Security 属性を追加する](media/proxy-idp-pingone/idp-pingone-sf-custom-app-replace-saml-sso-attributes.png)

1. 設定を保存します。

<a name="idp1-get-app-changes-in-cas"></a>

## <a name="step-6-get-the-app-changes-in-cloud-app-security"></a>手順 6:Cloud App Security でアプリの変更を取得する

Cloud App Security の **[アプリの変更]** ページに戻り、次を行います。ただし、 **[完了] はクリックしないでください**。 この情報は後で必要になります。

- Cloud App Security の SAML シングル サインオン URL をコピーします
- Cloud App Security の SAML 証明書をダウンロードします

![Cloud App Security の SAML SSO URL をメモして証明書をダウンロードする](media/proxy-idp-pingone/idp-pingone-cas-sf-app-changes.png)

<a name="idp1-complete-app-changes"></a>

## <a name="step-7-complete-the-app-changes"></a>手順 7: アプリの変更を完了する

Salesforce で、 **[設定]**  >  **[設定]**  >  **[ID]**  >  **[シングル サインオン設定]** を参照し、次を行います。

1. 推奨: 現在の設定のバックアップを作成してください。
1. **[ID プロバイダーのログイン URL]** フィールドの値を、前にメモした Cloud App Security SAML シングル サインオンの URL に置き換えます。
1. 前にダウンロードしておいた Cloud App Security の SAML 証明書をアップロードします。
1. **[エンティティ ID]** フィールドの値を、前にメモしておいた PingOne のカスタム アプリ エンティティ ID に置き換えます。
1. **[保存]** をクリックします。

    > [!NOTE]
    > Cloud App Security の SAML 証明書は 1 年間有効です。 有効期限が切れた後は、新しい証明書を生成する必要があります。

    ![Cloud App Security の SAML の詳細を使用して Salesforce のカスタム アプリを更新する](media/proxy-idp-pingone/idp-pingone-sf-custom-app-changes.png)

<a name="idp1-complete-conf-in-cas"></a>

## <a name="step-8-complete-the-configuration-in-cloud-app-security"></a>手順 8:Cloud App Security の構成を完了する

- Cloud App Security の **[アプリの変更]** ページに戻り、 **[完了]** をクリックします。 ウィザードを完了すると、このアプリに関連付けられたすべてのログイン要求が、アプリの条件付きアクセス制御経由でルーティングされます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [« 前へ:すべてのアプリにアプリの条件付きアクセス制御を展開する](proxy-deployment-any-app.md)

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [アプリの条件付きアクセス制御の概要](proxy-intro-aad.md)

> [!div class="nextstepaction"]
> [アクセスおよびセッション制御のトラブルシューティング](troubleshooting-proxy.md)

[!INCLUDE [Open support ticket](includes/support.md)]
