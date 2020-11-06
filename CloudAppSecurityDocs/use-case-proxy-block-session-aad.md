---
title: Cloud App Security アプリの条件付きアクセス制御によりアンマネージド デバイスからのダウンロードをブロックする
description: このチュートリアルでは、Azure AD リバース プロキシ機能を使用して、アンマネージド デバイスによる機密データのダウンロードから組織を保護するシナリオについて説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/31/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 3dec3c1729d63649a754098ace7f638ccc3029bc
ms.sourcegitcommit: e711727f2f00ee3b54e08337a5040449e352ca46
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2020
ms.locfileid: "93185939"
---
# <a name="tutorial-block-download-of-sensitive-information"></a>チュートリアル:機密情報のダウンロードをブロックする

[!INCLUDE [Banner for top of topics](includes/banner.md)]

今日の IT 管理者は、ジレンマを感じています。 従業員の生産性を高めたい。 これは、任意のデバイスからいつでも作業できるように、従業員にアプリへのアクセスを許可することを意味します。 それでいて、会社独自の機密情報を含めた資産を保護したいと考えています。 データを保護しながら、従業員がクラウド アプリにアクセスできるようにするにはどうすればよいでしょうか。 **このチュートリアルでは、アンマネージド デバイスまたは社外のネットワークの場所からエンタープライズ クラウド アプリの機密データにアクセスできるユーザーによるダウンロードをブロックできるようになります。**

> [!div class="checklist"]
>
> * アンマネージド デバイスのブロック ダウンロード ポリシーを作成する
> * ポリシーを検証する

## <a name="the-threat"></a>脅威

組織内のアカウント マネージャーが、個人のノート PC で、週末に自宅から Salesforce の情報を確認したいと考えています。 Salesforce のデータには、クライアントのクレジット カード情報や個人情報が含まれる可能性があります。 自宅の PC は管理されていません。 Salesforce からドキュメントを PC にダウンロードすると、マルウェアに感染する可能性があります。 デバイスを紛失したり、盗難にあった場合、それがパスワードで保護されておらず、誰でも機密情報にアクセスできる可能性があります。

## <a name="the-solution"></a>解決策

IdP ソリューションと Cloud App Security のアプリの条件付きアクセス制御を使用し、クラウド アプリの使用を監視し、制御することにより組織を保護します。

## <a name="prerequisites"></a>[前提条件]

* Azure AD Premium P1 の有効なライセンスまたは ID プロバイダー (IdP) ソリューションから要求されるライセンス
* 次のいずれかの認証プロトコルを使用し、SSO のクラウド アプリを構成します。

    |IdP|プロトコル|
    |---|---|
    |Azure AD|SAML 2.0 または OpenID Connect|
    |その他|SAML 2.0|
* [アプリが Cloud App Security にデプロイされている](proxy-deployment-aad.md)ことを確認する

## <a name="create-a-block-download-policy-for-unmanaged-devices"></a>アンマネージド デバイスのブロック ダウンロード ポリシーを作成する

Cloud App Security セッション ポリシーを使用すると、デバイスの状態に基づいてセッションを制限できます。 デバイスを条件として使用してセッションの制御を実現するには、条件付きアクセスポリシーとセッション ポリシーの両方を作成します。

### <a name="step-1-configure-your-idp-to-work-with-cloud-app-security"></a>手順 1:Cloud App Security と連動するように IdP を構成する

次のように、Cloud App Security と連動するように IdP ソリューションを構成します。

* [Azure AD 条件付きアクセス](/azure/active-directory/active-directory-conditional-access-azure-portal)については、[Azure AD との統合を構成する](proxy-deployment-aad.md#configure-integration-with-azure-ad)方法に関するページを参照してください
* その他の IdP ソリューションについては、[その他の IdP ソリューションとの統合を構成する](proxy-deployment-aad.md#configure-integration-with-other-idp-solutions)方法に関するページを参照してください。

このタスクを完了したら、Cloud App Security ポータルにアクセスし、セッションのファイルのダウンロードを監視および制御するためのセッション ポリシーを作成します。

### <a name="step-2-create-a-session-policy"></a>手順 2:セッション ポリシーを作成する

1. Cloud App Security ポータルで、 **[Control]\(制御\)** に続けて **[ポリシー]** を選択します。

2. **[ポリシー]** ページで、 **[Create policy]\(ポリシーを作成する\)** に続けて **[セッション ポリシー]** をクリックします。

3. **[セッション ポリシーの作成]** ページで、ポリシーの名前と説明を入力します。 たとえば、 **アンマネージド デバイスで Salesforce からのダウンロードをブロックする** などです。

4. **[ポリシー重要度]** および **[カテゴリ]** を割り当てます。

5. **[セッション制御の種類]** で、 **[Control file download (with inspection)]\(ファイル ダウンロードの制御 (検査を含む)\)** を選択します。 この設定を使用すると、Salesforce セッション内でユーザーが実行するすべての処理を監視することができ、リアルタイムでのダウンロードをブロックしたり保護したりできます。

6. **[Activities matching all of the following]\(次のすべてに一致するアクティビティ\)** セクションの **[アクティビティ ソース]** で、次のフィルターを選択します。

   * **[デバイス タグ]** : **[次の値と等しくない]** を選択します。 次に、 **[Intune 準拠]** 、 **[ハイブリッド Azure AD 参加]** 、または **[有効なクライアント証明書]** を選択します。 選択内容は、組織がマネージド デバイスの識別で使用する方法によって異なります。

   * **[アプリ]** :制御するアプリを選びます。

   * **[ユーザー]** :監視するユーザーを選びます。

7. また、企業ネットワークの一部ではない場所でのダウンロードをブロックすることもできます。 **[Activities matching all of the following]\(次のすべてに一致するアクティビティ\)** セクションの **[アクティビティ ソース]** で、次のフィルターを設定します。

   * **[IP アドレス]** または **[場所]** :この 2 つのパラメーターのどちらかを使用して、ユーザーが機密データへのアクセスを試みている企業以外の場所、または不明な場所を特定することができます。

     > [!NOTE]
     > アンマネージド デバイスと企業以外の場所の両方からのダウンロードをブロックする場合は、2 つのセッション ポリシーを作成する必要があります。 一方のポリシーでは、その場所を使用する **[アクティビティ ソース]** が設定されます。 もう一方のポリシーでは、 **[アクティビティ ソース]** がアンマネージド デバイスに設定されます。

   * **[アプリ]** :制御するアプリを選びます。

   * **[ユーザー]** :監視するユーザーを選びます。

8. **[Files matching all of the following]\(次のすべてに一致するファイル\)** セクションの **[アクティビティ ソース]** で、次のフィルターを設定します。

   * **[分類ラベル]** :Azure Information Protection の分類ラベルを使用する場合は、特定の Azure Information Protection 分類ラベルに基づいてファイルをフィルター処理します。

   * ファイルの名前または種類に基づいて制限を適用するには、 **[ファイル名]** または **[ファイルの種類]** を選択します。
9. **[コンテンツ検査]** を有効にすると、内部 DLP でファイルの機密コンテンツをスキャンできるようになります。

10. **[アクション]** で、 **[ブロック]** を選択します。 ユーザーがファイルをダウンロードできないときに表示するブロック メッセージをカスタマイズします。

11. ポリシーが一致したときに受信するアラートを設定します。 アラートが多くなりすぎないように制限を設定できます。 アラートを電子メール メッセージ、テキスト メッセージ、またはその両方のどれで取得するかを選択します。

12. **[作成]** をクリックします。

## <a name="validate-your-policy"></a>ポリシーを検証する

1. アンマネージド デバイスまたは企業以外のネットワークの場所からブロックされたファイルのダウンロードをシミュレートするには、アプリにサインインします。 次に、ファイルのダウンロードを試行します。

2. ファイルはブロックされ、 **[ブロック メッセージのカスタマイズ]** に設定したメッセージが表示されるはずです。

3. Cloud App Security ポータルで、 **[制御]** 、 **[ポリシー]** の順にクリックしてから、作成したポリシーをクリックしてポリシー レポートを表示します。 セッション ポリシーの一致がすぐに表示されるはずです。

4. ポリシー レポートでは、セッション制御のために Microsoft Cloud App Security にリダイレクトされたログインと、監視対象セッションからダウンロードまたはブロックされたファイルを確認できます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [アクセス ポリシーを作成する方法](access-policy-aad.md)

> [!div class="nextstepaction"]
> [セッション ポリシーを作成する方法](session-policy-aad.md)

[!INCLUDE [Open support ticket](includes/support.md)]