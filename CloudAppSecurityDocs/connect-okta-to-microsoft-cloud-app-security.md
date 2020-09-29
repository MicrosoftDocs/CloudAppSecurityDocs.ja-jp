---
title: Okta を Cloud App Security に接続する
description: この記事では、API コネクタを使用して Okta を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 9/1/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 6d5765c89498df4f7140ad9adbbab949b8970cbb
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881317"
---
# <a name="connect-okta-to-microsoft-cloud-app-security"></a>Okta を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の Okta アカウントに接続する手順について説明します。 この接続を使用すると、Okta の使用状況を表示したり制御したりできます。 Cloud App Security で Okta を保護する方法の詳細については、[Okta の保護](protect-okta.md)に関する記事を参照してください。

## <a name="how-to-connect-okta-to-cloud-app-security"></a>Okta を Cloud App Security に接続する方法

1. Okta で Cloud App Security 向けの管理者サービス アカウントを作成することをお勧めします。

    スーパー管理者のアクセス許可を持つアカウントを使用していることを確認します。

    Okta アカウントが検証済みであることを確認します。

1. Okta コンソールで、 **[Admin]** をクリックします。

    - **[Security]** 、 **[API]** の順にクリックします。

         ![Okta の [API]](media/okta-api.png "Okta の [API]")

    - **[Create Token]** をクリックします。

         ![Okta の [Create Token]](media/okta-createtoken.jpg "Okta の [Create Token]")

    - **[Create Token]** ポップアップで、Cloud App Security トークンに名前を付けて、 **[Create Token]** をクリックします。

         ![Okta のトークンのポップアップ](media/okta-token-pop-up.png)

    - **[Token created successfully]** ポップアップで、**Token value** をコピーします。

         ![Okta の [Token value]](media/okta-token-value.png "Okta の [Token value]")

1. Cloud App Security コンソールで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. **[アプリ コネクタ]** ページで、[+] ボタンをクリックして、 **[Okta]** を選択します。

    ![Okta の接続](media/connect-okta.png "Okta の接続")

1. ポップアップで、 **[ドメイン]** フィールドに Okta ドメインを入力し、 **[トークン]** フィールドにトークンを貼り付けます。

1. **[接続]** をクリックして、Cloud App Security に Okta のトークンを作成します。

1. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

Okta に接続すると、接続前の 60日間のイベントが表示されます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
