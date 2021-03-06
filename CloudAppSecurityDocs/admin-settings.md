---
title: 管理者設定の設定
description: この記事では、Cloud App Security で、管理者設定を設定する手順について説明します。
ms.date: 04/19/2020
ms.topic: how-to
ms.openlocfilehash: 18b5940ad4365a31b7e344860c0f791e306d8890
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314785"
---
# <a name="admin-user-settings"></a>管理者ユーザー設定

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security では、管理者ユーザー設定をカスタマイズできます。 通知設定により、管理者は、アラートについて、電子メールまたはテキスト通知を受け取るかどうかを指定できます。

## <a name="customize-your-admin-settings"></a><a name="Adminsettings"></a>管理者設定のカスタマイズ

Microsoft Cloud App Security の管理者として設定をセットアップするには、ポータルのメニュー バーでユーザー名をクリックして **[ユーザー設定]** を選択し、次の設定を設定します。

1. **[言語]** をクリックします。 ここで、Cloud App Security ポータルで使用する言語を選択できます。

    ![カスタム ユーザー設定](media/custom-language-settings.png)

2. **[通知]** をクリックし、システムから受信する電子メールと電子メールのテキスト通知設定を設定します。 電子メールを受け取るアラートや違反を判断する重要度を設定できます。 重要度はポリシーごとに設定します。 違反がトリガーされると、ここでの設定と違反したポリシーの重要度設定に応じて、電子メール通知を受け取ります。 電子メールは、Cloud App Security へのサインインに使用した管理者ユーザー アカウントに関連付けられているエイリアスに送信されます。 電話番号を入力して、Cloud App Security から、アラートや通知が送信されるときに、テキスト メッセージが送信されるようにし、テキスト メッセージによって通知を受け取る重要度レベルを設定します。

    > [!NOTE]
    >
    > - テキスト メッセージによって送信されるアラートの最大数は、1 日に 1 電話番号につき 10 個です。 日は UTC タイムゾーンに従って計算されます。
    > - Azure Active Directory IPC イベントについての通知は送信されません。

    ![通知設定](media/notification-settings.png)

3. 終了したら、 **[保存]** をクリックします。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery を設定する](set-up-cloud-discovery.md)

[!INCLUDE [Open support ticket](includes/support.md)]
