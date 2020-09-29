---
title: Box を Cloud App Security に接続する
description: この記事では、お使いの Box アプリを、使用状況を表示および制御する API コネクタを使用して、Cloud App Security に接続する方法について説明します。
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
ms.openlocfilehash: c13cf89f2a929046c846289f0065bc29b0e6d578
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881351"
---
# <a name="connect-box-to-microsoft-cloud-app-security"></a>Box を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、アプリ コネクタ API を使用して Microsoft Cloud App Security を Box アカウントに接続する方法を説明します。 この接続を使用すると、Box の使用状況を表示したり制御したりできます。 Cloud App Security での Box の保護方法の詳細については、[Box の保護](protect-box.md)に関する記事を参照してください。

## <a name="how-to-connect-box-to-cloud-app-security"></a>Box を Cloud App Security に接続する方法

> [!NOTE]
> 管理者アカウントではないアカウントで展開すると、API テストでエラーが発生し、Cloud App Security が Box のすべてのファイルをスキャンしません。 これが問題となる場合は、すべての特権を所有する共同管理者に協力を依頼して展開できます。しかし、引き続き API テストではエラーが発生し、他の管理者が所有している Box のファイルはスキャンされません。

1. アプリケーションのアクセス許可を制限する場合は、次の手順に従います。 それ以外の場合は、手順 2 に進みます。

    1. お使いの Box アカウントの管理者アカウントでサインインします。
    1. **[Apps]\(アプリ\)**  >  **[Custom apps]\(カスタム アプリ\)**  >  **[Settings]\(設定\)** をクリックします。

         ![box アプリ](media/box-apps.png "box アプリ")

    1. **[Disable unpublished apps by default]** \(発行されていないアプリを既定で無効にする\) がオンになっている場合、 **[Except for]** \(次を除外\) テキストボックスに Cloud App Security の API キーを追加します。

         |データ センター|Cloud App Security の API キー|
         |----|----|
         |US1|`nduj1o3yavu30dii7e03c3n7p49cj2qh`|
         |US2|`w0ouf1apiii9z8o0r6kpr4nu1pvyec75`|
         |US3|`dmcyvu1s9284i2u6gw9r2kb0hhve4a0r`|
         |EU1|`me9cm6n7kr4mfz135yt0ab9f5k4ze8qp`|
         |EU2|`uwdy5r40t7jprdlzo85v8suw1l4cdsbf`|

        次に、 **[保存]** をクリックします。 接続されている Cloud App Security データ センターを確認する方法の詳細については、「[データ センターを表示する](network-requirements.md#view-your-data-center)」を参照してください。

        ![box での除外設定](media/box-settings-except-for.png)

        > [!NOTE]
        > 既存の Adallom ユーザーの方でお使いのコンソールの URL が Cloud App Security ではなく Adallom のものである場合、アプリのシリアル番号には `bwahmilhdlpbqy2ongkl119o3lrkoshc` を使用します。

2. Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

3. **[アプリ コネクタ]** ページで、[+] ボタンをクリックして、 **[Box]** を選択します。

    ![box の接続](media/connect-box.png "Box の接続")

4. **[Box settings]** \(Box の設定\) のポップアップで、 **[このリンクに従ってください]** をクリックします。

5. Box のサインイン ページが開きます。 ご自分の資格情報を入力して、Cloud App Security がご自分のチームの Box アプリにアクセスできるようにします。

6. Box に、Cloud App Security があなたのチームの情報やアクティビティ ログにアクセスし、チーム メンバーとしてアクティビティを実行することを許可するかどうかを確認するメッセージが示されます。 続行するには、 **[許可]** をクリックします。

7. Cloud App Security ポータルに戻ると、Box と正常に接続されたことを示すメッセージが届きます。

8. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

これで Box が Cloud App Security に接続されます。

Box に接続すると、接続前の 60 日間のイベントを受け取ります。

Box に接続すると、Cloud App Security によってフル スキャンが実行されます。 ファイルとユーザーの数によっては、フル スキャンの完了にしばらく時間がかかります。 凖リアルタイムでのスキャンが有効になると、アクティビティが検出されたファイルはスキャンのキューの先頭に移動されます。 たとえば、編集、更新、または共有されたファイルは、通常のスキャン プロセスを待機するのではなく、直ちにスキャンされます。 本質的に変更されていないファイルは、準リアルタイムのスキャンの対象にはなりません。 たとえば、表示、プレビュー、印刷、またはエクスポートされたファイルは、定期的にスケジュールされているスキャンの一部としてスキャンされます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
