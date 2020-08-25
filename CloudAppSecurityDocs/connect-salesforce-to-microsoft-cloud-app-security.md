---
title: Salesforce を Cloud App Security に接続する
description: この記事では、お使いの Salesforce を、使用状況を表示および制御する API コネクタを使用して Cloud App Security に接続する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/06/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 81ad720b3230ab49a752671bcdc7d45cf789aad7
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88780887"
---
# <a name="connect-salesforce-to-microsoft-cloud-app-security"></a>Salesforce を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、アプリ コネクタ API を使用して Microsoft Cloud App Security を既存の Salesforce アカウントに接続する方法を説明します。 この接続を使用すると、Salesforce の使用状況を表示したり制御したりできます。 Cloud App Security での Salesforce の保護方法の詳細については、[Salesforce の保護](protect-salesforce.md)に関する記事を参照してください。

## <a name="how-to-connect-salesforce-to-cloud-app-security"></a>Salesforce を Cloud App Security に接続する方法

1. Cloud App Security に専用のサービス管理者アカウントを作成することをお勧めします。

1. Salesforce で REST API が有効になっていることを確認します。

    Salesforce アカウントには、REST API のサポートを含むエディション

    **Performance**、**Enterprise**、**Unlimited**、**Developer**。

    **Professional** エディションには、既定では REST API は含まれていませんが、必要に応じて追加することが可能です。

    現在のエディションで REST API を使用可能かどうか、有効化されているかどうかを確認するには、以下の手順を実行します。

    * お使いの Salesforce アカウントにサインインし、 **[設定]** ページに移動します。

    * **[Manage Users]** \(ユーザーの管理\) から **[User Profiles]** \(ユーザー プロファイル\) ページに移動します。

        ![Salesforce でのユーザー プロファイルの管理](media/salesforce-manageusers-profiles.png "Salesforce でのユーザー プロファイルの管理")

    * **[New]** \(新規\) をクリックして、新しいプロファイルを作成します。
    * Cloud App Security を展開するために作成したばかりのプロファイルを選択して、 **[Edit]** \(編集\) をクリックします。 このプロファイルは、Cloud App Security サービス アカウントでアプリ コネクタをセットアップするために使用されます。

         ![Salesforce でのプロファイルの編集](media/salesforce-edit-profile.png "Salesforce でのプロファイルの編集")

    * 次のチェックボックスをオンにします。
      * **[API Enabled]\(API 有効化\)**
      * **[View All Data]\(すべてのデータを表示する\)**
      * **[Manage Salesforce CRM Content]\(Salesforce CRM コンテンツを管理する\)**
      * **[ユーザーを管理する]**
      * **[[Query All Files]](https://go.microsoft.com/fwlink/?linkid=2106480)\(すべてのファイルを照会する\)**

      これらのチェックボックスがオフになっている場合は、Salesforce に連絡してお使いのアカウントに追加してもらう必要があります。

1. 組織で **[Salesforce CRM Content]** を有効化している場合は、現在の管理者アカウントでも有効になっていることを確認します。

    1. Salesforce の設定ページに移動します。

        ![Salesforce の設定](media/salesforce-setup.png "Salesforce の設定")

    1. サイド メニューから **[ユーザーの管理]** を選択し、 **[ユーザー]** をクリックします。

        ![Salesforce のユーザー メニュー](media/salesforce-menu-users.png "Salesforce のユーザー メニュー")

    1. 専用の Cloud App Security ユーザーの現在の管理ユーザーを選択します。

    1. **[Salesforce CRM Content ユーザー]** チェックボックスがオンになっていることを確認します。

        オフになっている場合は、 **[Edit]** \(編集\) をクリックしてチェックボックスをオンにします。

        ![Salesforce CRM コンテンツ ユーザー](media/salesforce-crm-content-user.png "Salesforce CRM コンテンツ ユーザー")

    1. **[Save]** (保存) をクリックします。

1. Cloud App Security コンソールで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. **[アプリ コネクター]** ページで、[+] ボタン、 **[Salesforce]** の順にクリックします。

    ![Salesforce の接続](media/connect-salesforce.png "Salesforce の接続")

1. Salesforce の設定ページの API タブで、インストールするインスタンスに応じて **Follow this link (このリンクに移動)** をクリックします。

1. これにより Salesforce のサインイン ページが開きます。 Cloud App Security がチームの Salesforce アプリにアクセスできるように、資格情報を入力します。

    ![Salesforce のサインイン](media/salesforce-logon.png "Salesforce へのログオン")

1. Cloud App Security からチームの情報やアクティビティ ログにアクセスし、任意のチーム メンバーと同様に任意のアクティビティを実行することを許可するかどうかを確認するメッセージが Salesforce で表示されます。 続行するには、 **[許可]** をクリックします。

1. この時点で、展開の成功または失敗の通知が表示されます。 Cloud App Security が Salesforce.com で承認されました。

1. Cloud App Security コンソールに戻ると、Salesforce が正常に接続されたことを示すメッセージが表示されます。

1. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[完了]** をクリックします。

Salesforce の接続後には、次のイベントを受け取ります。接続した時点からのトリガー、接続前の 60 日間のログイン イベントとセットアップ監査証跡、お使いの Salesforce EventMonitoring のライセンスに応じた 30 日前または 1 日前の EventMonitoring。 Cloud App Security API は Salesforce から利用できる API と直接通信します。 Salesforce はそれが受け取る API 呼び出しの数を制限できるため、Cloud App Security はそれを考慮し、制限を順守します。 Salesforce API は、利用できる合計数や残りの数など、API カウンターのフィールドと共に各応答を送信します。 Cloud App Security はこれを百分率に計算し、利用できる API 呼び出しの 10% が常に残るようにします。

> [!NOTE]
> Cloud App Security の調整は、Salesforce で呼び出した Cloud App Security の API に基づいてのみ計算されます。他のアプリケーションが Salesforce で呼び出した API は計算対象になりません。
> API 呼び出しが制限されることで Cloud App Security にデータが取り込まれる速度が遅くなることがありますが、通常、一晩で追いつきます。

Salesforce イベントは Cloud App Security により次のように処理されます。

* 15 分ごとにサインイン イベント
* 15 分ごとにセットアップ監査証跡
* 1 時間ごとにイベント ログ Salesforce のイベントの詳細については、「[イベント監視の使用](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_resources_event_log_files.htm)」をご覧ください。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
