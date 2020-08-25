---
title: ServiceNow を Cloud App Security に接続する
description: この記事では、API コネクタを使用して ServiceNow を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/24/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 75bc58df1ea45eb4d00498cb9fb2d7a061dac9b4
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88780853"
---
# <a name="connect-servicenow-to-microsoft-cloud-app-security"></a>ServiceNow を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、アプリ コネクタ API を使用して Microsoft Cloud App Security を既存の ServiceNow アカウントに接続する方法について説明します。 この接続を使用すると、ServiceNow の使用状況を表示したり制御したりできます。 Cloud App Security での ServiceNow の保護方法の詳細については、[ServiceNow の保護](protect-servicenow.md)に関する記事を参照してください。

> [!NOTE]
> Fuji 以降のリリースで使用できる OAuth アプリ トークンを使用して ServiceNow をデプロイすることをお勧めします (関連する [ServiceNow のドキュメント](https://wiki.servicenow.com/index.php?title=OAuth_Applications#gsc.tab=0)を参照してください)。
> 以前のリリースでは、ユーザーとパスワードに基づいて、[レガシ接続モード](#legacy-servicenow-connection)を使用できます。 指定されたユーザー名/パスワードは API トークンの生成にのみ使用され、最初の接続処理の後に保存されることはありません。

> [!NOTE]
> Cloud App Security では、次の ServiceNow バージョンがサポートされています。Eureka、Fiji、Geneva、Helsinki、Istanbul、Jakarta、Kingston、London、Madrid、および New York。 ServiceNow を Cloud App Security に接続するには、**管理者**ロールを保持していることと、ServiceNow インスタンスが API アクセスをサポートしていることを確認する必要があります。 詳細については、[ServiceNow の製品ドキュメント](https://wiki.servicenow.com/index.php?title=Base_System_Roles#gsc.tab=0)を参照してください。

## <a name="how-to-connect-servicenow-to-cloud-app-security-using-oauth"></a>OAuth を使用して ServiceNow を Cloud App Security に接続する方法

1. ServiceNow アカウントに管理者アカウントでサインインします。

    > [!NOTE]
    > 指定されたユーザー名/パスワードは API トークンの生成にのみ使用され、最初の接続処理の後に保存されることはありません。

2. **フィルター ナビゲーター**の検索バーに、「**OAuth**」と入力し、 **[Application Registry]** を選択します。

3. **[Application Registries]** メニュー バーで、 **[New]** をクリックして新しい OAuth プロファイルを作成します。

    ![ServiceNow の新しい OAuth プロファイル](media/servicenow-app-registry.png)

4. **[What kind of OAuth application?]** で、 **[Create an OAuth API endpoint for external clients]** をクリックします。

    ![ServiceNow の OAuth の種類](media/servicenow-oauth-app-type.png)

5. **[Application Registries New record]** で、次のフィールドに入力 ます。

    - **[名前]** フィールドで、新しい OAuth プロファイルの名前を指定します (「CloudAppSecurity」など)。

    - **[クライアント ID]** が自動的に生成されます。 この ID をコピーします。接続を完了するために Cloud App Security に貼り付ける必要があります。

    - **[クライアント シークレット]** フィールドに文字列を入力します。 空のままにすると、ランダムなシークレットが自動的に生成されます。 後で使用するために、コピーして保存します。

    - **[Access Token Lifespan]** を 3,600 以上に増やします。

    - **[送信]** をクリックします。

    ![ServiceNow のプロファイル ID](media/servicenow-profile-ids.png)

6. Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

7. **[アプリ コネクタ]** ページで、[+] ボタンをクリックして、 **[ServiceNow]** を選択します。

    ![ServiceNow の接続](media/connect-servicenow.png "ServiceNow の接続")

8. ポップアップで、ServiceNow のユーザー ID、パスワード、インスタンスの URL、クライアント ID、およびクライアント シークレットを該当するボックスに追加します。 ServiceNow のユーザー ID を見つけるには、ServiceNow ポータルで、 **[Users]** に移動して、表で自分の名前を見つけます。

    ![ServiceNow のユーザー ID](media/servicenow-userid.png)

9. **[接続]** をクリックします。

    ![ServiceNow を CAS に接続する](media/servicenow-portal-connect.png "ポータルでの ServiceNow の接続")

10. **[今すぐテストする]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

ServiceNow に接続すると、接続前の 7 日間のイベントが表示されます。

## <a name="legacy-servicenow-connection"></a>従来の ServiceNow 接続

ServiceNow を Cloud App Security に接続するには、管理者レベルのアクセス許可が必要であるほか、ServiceNow インスタンスが API アクセスをサポートしていることを確認する必要があります。

1. ServiceNow アカウントに管理者アカウントでサインインします。

2. Cloud App Security 用の新しいサービス アカウントを作成し、その新しいアカウントに管理者ロールを付与します。

3. REST API プラグインが有効になっていることを確認します。

    ![ServiceNow アカウント](media/servicenow-account.png "ServiceNow アカウント")

4. Cloud App Security ポータルで、 **[調査]** 、 **[承認されたアプリ]** の順にクリックします。

5. ServiceNow の行の **[アプリ コネクタの状態]** 列 で **[接続]** をクリックするか、 **[アプリを接続]** ボタンをクリックして **[ServiceNow]** を選択します。

   ![ServiceNow の接続](media/connect-servicenow.png "ServiceNow の接続")

6. [ServiceNow の設定] ページの [API] タブで、該当するボックスに ServiceNow のユーザー ID、パスワード、およびインスタンスの URL を追加します。

7. **[接続]** をクリックします。

    ![ServiceNow のパスワードの更新](media/servicenow-update-password.png "ServiceNow のパスワードの更新")

8. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

ServiceNow に接続すると、接続前の 7 日間のイベントが表示されます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
