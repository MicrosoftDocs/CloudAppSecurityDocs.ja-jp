---
title: Dropbox を Cloud App Security に接続する
description: この記事では、お使いの Dropbox アプリを、使用状況を表示および制御する API コネクタを使用して、Cloud App Security に接続する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: a2cc37a22d339b721111948b277135382a2c7c8a
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781091"
---
# <a name="connect-dropbox-to-microsoft-cloud-app-security"></a>Dropbox を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の Dropbox アカウントに接続する方法を説明します。 この接続を使用すると、Dropbox の使用状況を表示したり制御したりできます。 Cloud App Security での Dropbox の保護方法の詳細については、[Dropbox の保護](protect-dropbox.md)に関する記事を参照してください。

Dropbox では、サインインせずに共有リンクからファイルにアクセスできるため、これらのユーザーは Cloud App Security によって認証されていないユーザーとして登録されます。 認証されていない Dropbox ユーザーが見つかった場合、組織外のユーザーであることを示している可能性があります。または、組織内のサインインしていない認識済みユーザーである可能性もあります。

## <a name="how-to-connect-dropbox-to-cloud-app-security"></a>Dropbox を Cloud App Security に接続する方法

1. Cloud App Security コンソールで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

2. **[アプリ コネクタ]** ページで、[+] ボタン、 **[Dropbox]** の順にクリックします。

    ![Dropbox の接続](media/connect-dropbox.png "Dropbox の接続")

3. ポップアップで、管理者アカウントの電子メール アドレスを入力します。

4. **[リンクを生成]** をクリックします。

5. **[このリンクに従ってください]** をクリックします。

    Dropbox のサインイン ページが開きます。 ご自分の資格情報を入力して、Cloud App Security がご自分のチームの Dropbox インスタンスにアクセスできるようにします。

6. Dropbox に、Cloud App Security があなたのチームの情報やアクティビティ ログにアクセスし、チーム メンバーとしてアクティビティを実行することを許可するかどうかを確認するメッセージが示されます。 続行するには、 **[許可]** をクリックします。

7. Cloud App Security コンソールに戻ると、Dropbox と正常に接続されたことを示すメッセージが届きます。

8. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

Dropbox に接続すると、接続前の 60 日間のイベントを受け取ります。

> [!NOTE]
> ファイルを追加するための Dropbox イベントはすべて、Cloud App Security に接続されている他のすべてのアプリに合わせるため、アップロード ファイルとして Cloud App Security に表示されます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
