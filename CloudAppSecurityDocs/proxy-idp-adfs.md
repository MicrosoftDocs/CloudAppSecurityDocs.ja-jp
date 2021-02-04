---
title: AD FS を使用して任意の Web アプリに対して Cloud App Security のアプリの条件付きアクセス制御を展開する
description: この記事では、ID プロバイダーとして AD FS を使用している任意の Web アプリに Microsoft Cloud App Security のアプリの条件付きアクセス制御を展開する方法について説明します。
ms.date: 01/26/2021
ms.topic: how-to
ms.openlocfilehash: 74a454332125162dbec74f076d150ffe1b9d9b45
ms.sourcegitcommit: f56a2060b99ab087b8637606a1fb66e5577aded8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98795270"
---
# <a name="onboard-and-deploy-conditional-access-app-control-for-any-web-app-using-active-directory-federation-services-ad-fs-as-the-identity-provider-idp"></a>ID プロバイダー (IdP) として Active Directory フェデレーション サービス (AD FS) を使用する任意の Web アプリにアプリの条件付きアクセス制御をオンボードして展開する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security のセッション制御は、任意の Web アプリおよびサード パーティー IdP と連動するように構成できます。 この記事では、アプリのセッションを AD FS から Cloud App Security にルーティングして、セッションをリアルタイムで制御する方法について説明します。

この記事では、Cloud App Security セッション制御を使用するように構成されている Web アプリの例として、Salesforce アプリを使用します。

## <a name="prerequisites"></a>[前提条件]

- アプリの条件付きアクセス制御を使用するには、お客様の組織が次のライセンスを持っている必要があります。

  - 構成済みの AD FS 環境
  - Microsoft Cloud App Security

- SAML 2.0 認証プロトコルを使用するアプリでの既存の AD FS シングル サインオン構成

## <a name="to-configure-session-controls-for-your-app-using-ad-fs-as-the-idp"></a>IdP として AD FS を使用してお使いのアプリのセッション制御を構成するには

AD FS から Cloud App Security にお使いの Web アプリのセッションをルーティングするには、次の手順に従います。 Azure AD の構成ステップについては、「[Azure AD との統合を構成する](proxy-deployment-any-app.md#configure-integration-with-azure-ad)」を参照してください。

> [!NOTE]
> AD FS で提供されるアプリの SAML シングル サインオン情報を構成するには、次のいずれかの方法を使用します。
>
> - **オプション 1**:アプリの SAML メタデータ ファイルのアップロード。
> - **オプション 2**:アプリの SAML データの手動による提供。
>
> 以降のステップでは、オプション 2 を使用します。

**手順 1: [アプリの SAML シングル サインオン設定を取得する](#idp1-get-your-app-saml-sso-info)**

**手順 2: [アプリの SAML 情報で Cloud App Security を構成する](#idp1-conf-cas-with-your-app-saml-info)**

**手順 3: [新規に AD FS 証明書利用者信頼とアプリのシングル サインオン構成を作成する](#idp1-create-custom-app-adfs)**

**手順 4: [AD FS アプリの情報で Cloud App Security を構成する](#idp1-conf-cas-with-adfs-app-info)**

**手順 5: [AD FS 証明書利用者信頼の構成を完了する](#idp1-complete-custom-app-in-adfs)**

**手順 6: [Cloud App Security でアプリの変更を取得する](#idp1-get-app-changes-in-cas)**

**手順 7: [アプリの変更を完了する](#idp1-complete-app-changes)**

**手順 8: [Cloud App Security の構成を完了する](#idp1-complete-conf-in-cas)**

<a name="idp1-get-your-app-saml-sso-info"></a>

## <a name="step-1-get-your-apps-saml-single-sign-on-settings"></a>手順 1:アプリの SAML シングル サインオン設定を取得する

1. Salesforce で、 **[設定]**  >  **[設定]**  >  **[ID]**  >  **[シングル サインオン設定]** を参照します。

1. **[シングル サインオン設定]** で、お使いの既存の AD FS 構成の名前をクリックします。

    ![Salesforce の SSO 設定を選択する](media/proxy-idp-adfs/idp-adfs-sf-select-sso-settings.png)

1. **[SAML シングルサインオン設定]** ページで、Salesforce の **ログイン URL** をメモしておきます。 これは、後で Cloud App Security を構成するときに必要になります。

    > [!NOTE]
    > お使いのアプリで SAML 証明書が提供されている場合は、その証明書ファイルをダウンロードします。

    ![Salesforce の SSO ログイン URL を選択する](media/proxy-idp-adfs/idp-adfs-sf-copy-saml-sso-login-url.png)

<a name="idp1-conf-cas-with-your-app-saml-info"></a>

## <a name="step-2-configure-cloud-app-security-with-your-apps-saml-information"></a>手順 2:アプリの SAML 情報で Cloud App Security を構成する

1. Cloud App Security で、 **[調査]**  >  **[接続アプリ]**  >  **[アプリの条件付きアクセス制御アプリ]** の順に移動します。

1. プラス記号をクリックし、ポップアップでデプロイするアプリを選択してから、 **[ウィザード起動]** をクリックします。
1. **[アプリ情報]** ページで、 **[データを手動で入力する]** を選択し、 **[Assertion consumer service URL]** に、前にメモした Salesforce の **ログイン URL** を入力して、 **[次へ]** をクリックします。

    > [!NOTE]
    > アプリで SAML 証明書が提供されている場合は、 **[<アプリ名> の SAML 証明書を使用する]** を選択して、証明書ファイルをアップロードします。

    ![Salesforce の SAML 情報を手動で入力する](media/proxy-idp-adfs/idp-adfs-cas-sf-app-info.png)

<a name="idp1-create-custom-app-adfs"></a>

## <a name="step-3-create-a-new-ad-fs-relying-party-trust-and-app-single-sign-on-configuration"></a>手順 3:新規に AD FS 証明書利用者信頼とアプリのシングル サインオン構成を作成する

> [!NOTE]
> エンドユーザーのダウンタイムを制限し、お使いの既存の既知の正しい構成を保持するには、新しい **証明書利用者信頼** と **シングル サインオンの構成** を作成することをお勧めします。 これが不可能な場合は、関連する手順をスキップしてください。 たとえば、構成しているアプリで複数の **シングル サインオン構成** の作成がサポートされていない場合は、新しいシングル サインオンの作成手順をスキップします。

1. **[AD FS の管理]** コンソールの **[証明書利用者信頼]** の下で、お使いのアプリの既存の証明書利用者信頼のプロパティを表示し、設定をメモします。

1. **[操作]** の下の **[証明書利用者信頼の追加]** をクリックします。 一意の名前である必要がある **識別子** 値とは別に、前にメモした設定を使用して新しい信頼を構成します。 この信頼は、後で Cloud App Security を構成するときに必要になります。
1. フェデレーション メタデータ ファイルを開き、AD FS の **SingleSignOnService Location** をメモします。 これは後で必要になります。

    > [!NOTE]
    > お使いのフェデレーション メタデータ ファイルには、`https://<Your_Domain>/federationmetadata/2007-06/federationmetadata.xml` のエンドポイントからアクセスできます。

    ![既存の Salesforce アプリの SSO サービスの場所をメモする](media/proxy-idp-adfs/idp-adfs-sf-app-copy-saml-sso-service-location.png)

1. ID プロバイダーの署名証明書をダウンロードします。 これは後で必要になります。
    1. **[サービス]**  >  **[証明書]** で、AD FS 署名証明書を右クリックし、 **[証明書の表示]** を選択します。

        ![IdP 署名証明書のプロパティを表示する](media/proxy-idp-adfs/idp-adfs-view-signing-cert-props.png)

    1. 証明書の [詳細] タブで、 **[ファイルにコピー]** をクリックし、**証明書のエクスポート ウィザード** の手順に従って、お使いの証明書を *Base-64 encoded X.509 (.CER)* ファイルとしてエクスポートします。

        ![IdP 署名証明書ファイルを保存する](media/proxy-idp-adfs/idp-adfs-save-signing-cert-file.png)

1. Salesforce に戻り、既存の AD FS のシングル サインオンの設定ページで、すべての設定をメモします。
1. 新しい SAML シングル サインオン構成を作成します。 証明書利用者信頼の **識別子** と一致している必要がある **エンティティ ID** 値とは別に、前にメモした設定を使用してシングル サインオンを構成します。 これは、後で Cloud App Security を構成するときに必要になります。

<a name="idp1-conf-cas-with-adfs-app-info"></a>

## <a name="step-4-configure-cloud-app-security-with-the-ad-fs-apps-information"></a>手順 4:AD FS アプリの情報で Cloud App Security を構成する

1. Cloud App Security の **[ID プロバイダー]** ページに戻り、 **[次へ]** をクリックして続行します。

1. 次のページで、 **[データを手動で入力する]** を選択し、次の手順を実行して、 **[次へ]** をクリックします。
    - **[シングル サインオン サービス URL]** に、前にメモした Salesforce の **ログイン URL** を入力します。
    - **[Upload identity provider's SAML certificate]\(ID プロバイダーの SAML 証明書をアップロードする\)** を選択し、先ほどダウンロードした証明書ファイルをアップロードします。

    ![SSO サービスの URL と SAML 証明書を追加する](media/proxy-idp-adfs/idp-adfs-cas-sf-app-idp-info.png)

1. 次のページで、以下の情報をメモしてから、 **[次へ]** をクリックします。 この情報は後で必要になります。

    - Cloud App Security のシングル サインオン URL
    - Cloud App Security の属性と値

    > [!NOTE]
    > **ID プロバイダー用の Cloud App Security SAML 証明書** をアップロードするオプションが表示された場合は、リンクをクリックして証明書ファイルをダウンロードします。 これは後で必要になります。

    ![Cloud App Security の SSO の URL と属性をメモする](media/proxy-idp-adfs/idp-adfs-cas-get-sf-app-external-config.png)

<a name="idp1-complete-custom-app-in-adfs"></a>

## <a name="step-5-complete-the-configuration-of-the-ad-fs-relying-party-trust"></a>手順 5:AD FS 証明書利用者信頼の構成を完了する

1. **[AD FS の管理]** コンソールに戻り、先ほど作成した証明書利用者信頼を右クリックし、 **[要求発行ポリシーの編集]** を選択します。

    ![証明書信頼の要求発行を検索および編集する](media/proxy-idp-adfs/idp-adfs-sf-relying-trust-edit.png)

1. **[要求発行ポリシーの編集]** ダイアログ ボックスの **[発行変換規則]** の下の表に記載されている情報を使用して、カスタム規則を作成する手順を完了します。

    | 要求規則名 | カスタム規則 |
    | --- | --- |
    | McasSigningCert | `=> issue(type="McasSigningCert", value="<value>");` の `<value>` は、前にメモした Cloud App Security ウィザードの **McasSigningCert** 値です。 |
    | McasAppId | `=> issue(type="McasAppId", value="<value>");` は、前にメモした Cloud App Security ウィザードの **McasAppId** 値です。 |

    1. **[要求規則テンプレート]** の下の **[規則の追加]** をクリックし、 **[カスタム規則を使用して要求を送信]** を選択し、 **[次へ]** をクリックします。
    1. **[規則の構成]** ページで、提供された **[要求規則名]** と **[カスタム規則]** をそれぞれ入力します。

    > [!NOTE]
    > これらの規則は、構成しているアプリに必要な要求規則や属性に対する追加されます。

1. **[証明書利用者信頼]** ページに戻り、先ほど作成した証明書利用者信頼を右クリックし、 **[プロパティ]** を選択します。
1. **[エンドポイント]** タブで **[SAML アサーション コンシューマー エンドポイント]** を選択し、 **[編集]** をクリックし、 **[信頼された URL]** を先ほどメモした Cloud App Security シングル サインオン URL に置き換え、 **[OK]** をクリックします。

    ![証明書信頼エンドポイント プロパティの信頼された URL を更新する](media/proxy-idp-adfs/idp-adfs-sf-relying-trust-endpoint-properties.png)

1. **ID プロバイダーの Cloud App Security SAML 証明書** をダウンロードした場合、 **[署名]** タブで **[追加]** をクリックして、証明書ファイルをアップロードし、 **[OK]** をクリックします。

    ![証明書信頼署名プロパティの SAML 証明書を更新する](media/proxy-idp-adfs/idp-adfs-sf-relying-trust-signature-properties.png)

1. 設定を保存します。

<a name="idp1-get-app-changes-in-cas"></a>

## <a name="step-6-get-the-app-changes-in-cloud-app-security"></a>手順 6:Cloud App Security でアプリの変更を取得する

Cloud App Security の **[アプリの変更]** ページに戻り、次を行います。ただし、 **[完了] はクリックしないでください**。 この情報は後で必要になります。

- Cloud App Security の SAML シングル サインオン URL をコピーします
- Cloud App Security の SAML 証明書をダウンロードします

![Cloud App Security の SAML SSO URL をメモして証明書をダウンロードする](media/proxy-idp-adfs/idp-adfs-cas-sf-app-changes.png)

<a name="idp1-complete-app-changes"></a>

## <a name="step-7-complete-the-app-changes"></a>手順 7: アプリの変更を完了する

Salesforce で、 **[設定]**  >  **[設定]**  >  **[ID]**  >  **[シングル サインオン設定]** を参照し、次を行います。

1. 推奨: 現在の設定のバックアップを作成してください。
1. **[ID プロバイダーのログイン URL]** フィールドの値を、前にメモした Cloud App Security SAML シングル サインオンの URL に置き換えます。
1. 前にダウンロードしておいた Cloud App Security の SAML 証明書をアップロードします。
1. **[保存]** をクリックします。

    > [!NOTE]
    > Cloud App Security の SAML 証明書は 1 年間有効です。 有効期限が切れた後は、新しい証明書を生成する必要があります。

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
