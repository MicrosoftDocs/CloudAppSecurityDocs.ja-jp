---
title: Webex Teams を Cloud App Security に接続する
description: この記事では、お使いの Webex Teams アプリを、使用状況を表示および制御する API コネクタを使用して、Cloud App Security に接続する方法について説明します。
ms.date: 12/27/2020
ms.topic: how-to
ms.openlocfilehash: 7cc58ee71f57c82aae87332d292fad8cf08894d4
ms.sourcegitcommit: cfa59a538167bd126d64dbd05f04a1957bc035c8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/27/2020
ms.locfileid: "97792698"
---
# <a name="connect-cisco-webex-teams-to-microsoft-cloud-app-security"></a>Cisco Webex Teams を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の Cisco Webex アカウントに接続する方法を説明します。 この接続を使用すると、Webex のユーザー、アクティビティ、ファイルについて、表示したり制御したりできます。 Cloud App Security での Cisco Webex Teams の保護方法の詳細については、[Cisco Webex Teams の保護](protect-webex.md)に関する記事を参照してください。

## <a name="prerequisites"></a>[前提条件]

- 接続専用のサービス アカウントを作成することをお勧めします。 これにより、Webex で送信されたメッセージの削除など、Webex で実行されるガバナンス アクションがこのアカウントから実行されていることを確認できます。 それ以外の場合は、Webex に Cloud App Security を接続した管理者の名前が、アクションを実行したユーザーとして表示されます。
- Webex で、完全な権限を持つ管理者とコンプライアンス オフィサーの **両方** の役割を持っている必要があります ( **[Roles and Security]\(役割とセキュリティ\)**  >  **[Administrator Roles]\(管理者の役割\)** で)。

    ![前提条件の Webex の役割](media/connect-webex-roles.png)

## <a name="how-to-connect-webex-to-cloud-app-security"></a>Webex を Cloud App Security に接続する方法

1. Cloud App Security コンソールで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. **[アプリ コネクタ]** ページで、[+] ボタン、 **[Cisco Webex]** の順にクリックします。

    ![WebEx の接続](media/cisco-webex.png)

1. ポップアップで、このコネクタのインスタンス名を入力します。

1. **[Connect Cisco Webex]\(Cisco Webex を接続する\)** をクリックします。 Webex のサインイン ページが開きます。 ご自分の資格情報を入力して、Cloud App Security によるチームの Webex インスタンスにアクセスできるようにします。

1. Webex に、Cloud App Security があなたのチームの情報やアクティビティ ログにアクセスし、チーム メンバーとしてアクティビティを実行することを許可するかどうかを確認するメッセージが示されます。 続行するには、 **[許可]** をクリックします。

1. Cloud App Security コンソールに戻ると、Webex と正常に接続されたことを示すメッセージが届きます。

1. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

Webex に接続すると、接続前の 7 日間のイベントを受け取ります。 Cloud App Security では、イベントが過去 3 か月にわたってスキャンされます。 これを増やすには、Cisco Webex の Pro ライセンスを所有し、Cloud App Security サポートでチケットを開く必要があります。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
