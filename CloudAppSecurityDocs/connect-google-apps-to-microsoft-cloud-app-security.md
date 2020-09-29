---
title: G Suite を Cloud App Security に接続する
description: この記事では、API コネクタを使用して G Suite を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/27/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 89342994a408ae1b03bd50c3c1fa4adc9dd12bc4
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881432"
---
# <a name="connect-g-suite-to-microsoft-cloud-app-security"></a>G Suite を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の G Suite アカウントに接続する手順について説明します。 この接続を使用すると、G Suite の使用状況を表示したり制御したりできます。 Cloud App Security で G Suite を保護する方法の詳細については、[G Suite の保護](protect-gsuite.md)に関するページを参照してください。

## <a name="configure-g-suite"></a>G Suite の構成

1. G Suite スーパー管理者として、<a href="https://cloud.google.com/console/project" target="_blank">https://cloud.google.com/console/project</a> にサインインします。

1. **[プロジェクトを作成]** をクリックして、新しいプロジェクトを開始します。

    ![Google プロジェクトの作成](media/google1.png)

1. **[新しいプロジェクト]** 画面で、プロジェクトに次のように名前を指定します。「**Cloud App Security**」。 **[作成]** をクリックします。

    ![Google 新規プロジェクトのポップアップ](media/google2.png)

1. プロジェクトが作成されたら、ツールバーの **[Google Cloud Platform]** をクリックします。 上部のドロップダウンで、適切なプロジェクトが選択されていることを確認します。

    ![ツール バーの [Google Cloud Platform] をクリック](media/googleverify-project.png)

1. メニューを選択し、 **[API とサービス]**  >  **[ライブラリ]** に移動して、次の API を有効にします (API が一覧表示されない場合は、検索行を使用します)。

    * Admin SDK

    * Audit API

    * Google Drive API

    * G Suite Marketplace SDK  
![Google API](media/google4.png)

    > [!NOTE]
    > 各 API について、 **[有効にする]** をクリックしてアクティブにします。
    >
    > ![Google API を有効にする](media/google-api.png)
    >
    > 現時点では、**認証情報**の警告を無視します。

1. メニューを選択し、 **[API とサービス]**  >  **[ダッシュボード]** に移動して、次の API が有効になっていることを確認します。

    ![Google の有効になっている API](media/google5.png)

1. **[OAuth 同意画面]** タブにアクセスします。

    * **[アプリケーション名]** に「**Microsoft Cloud App Security**」と入力します。

    * その他のフィールドはすべて省略可能です。

    * **[Save]** (保存) をクリックします。

    ![Google OAuth 同意](media/google-oauth-consent.png)

1. **[認証情報]** 画面で、 **[認証情報を作成]** の横の矢印をクリックし、 **[サービス アカウント キー]** を選択します。

    ![Google 認証情報](media/google7.png)

1. **[サービス アカウント]** で、 **[新しいサービス アカウント]** を選択し、「**Service account 1**」などのアカウントの名前を指定します。 **[役割]** で、 **[プロジェクト]** 、 **[エディタ]** の順に選択します。 **[キーのタイプ]** で、 **[P12]** を選択し、 **[作成]** をクリックします。 P12 証明書ファイルがコンピューターに保存されます。

    ![Google でのサービス アカウント キーの作成](media/google9.png)

1. **[認証情報]** 画面で、右端にある **[サービス アカウントを管理]** をクリックします。 サービス アカウントに割り当てられている**メール アドレス**をコピーしておきます。これは後で必要になります。

    ![G Suite 認証情報サービス アカウント](media/google10.png)

1. 作成したサービス アカウントの右側にある 3 つのドットをクリックし、 **[編集]** を選択します。

    ![Google 編集](media/google11.png "Google 編集")

1. **[ドメイン全体の委任の表示]** をクリックし、 **[G Suite ドメイン全体の委任を有効にする]** を選択します。

    ![Google クライアント ID](media/google12.png "google12")

    1. **クライアント ID** をコピーします。これは後で必要になります。
    ![API クライアント アクセスの管理](media/google12-2.png "google12-2")

    1. **[保存]** をクリックします

    1. [admin.google.com](https://admin.google.com/) に移動し、 **[セキュリティ]** を選択します。

    1. **[詳細設定]** を展開し、 **[認証]** で **[API クライアント アクセスを管理する]** を選択します。

    1. **[クライアント名]** ボックスに、前にコピーした**クライアント ID** を入力します。  

    1. **[1 つ以上の API スコープ]** ボックスに、次の必要なスコープの一覧を入力します (テキストをコピーしてボックスに貼り付けます)。  
`https://www.googleapis.com/auth/admin.reports.audit.readonly,https://www.googleapis.com/auth/admin.reports.usage.readonly,https://www.googleapis.com/auth/drive,https://www.googleapis.com/auth/drive.appdata,https://www.googleapis.com/auth/drive.apps.readonly,https://www.googleapis.com/auth/drive.file,https://www.googleapis.com/auth/drive.metadata.readonly,https://www.googleapis.com/auth/drive.readonly,https://www.googleapis.com/auth/drive.scripts,https://www.googleapis.com/auth/admin.directory.user.readonly,https://www.googleapis.com/auth/admin.directory.user.security,https://www.googleapis.com/auth/admin.directory.user.alias,https://www.googleapis.com/auth/admin.directory.orgunit,https://www.googleapis.com/auth/admin.directory.notifications,https://www.googleapis.com/auth/admin.directory.group.member,https://www.googleapis.com/auth/admin.directory.group,https://www.googleapis.com/auth/admin.directory.device.mobile.action,https://www.googleapis.com/auth/admin.directory.device.mobile,https://www.googleapis.com/auth/admin.directory.user`

    1. **[承認]** をクリックします。

1. [Google Cloud Platform](https://console.cloud.google.com/) で、メニューを選択し、 **[API とサービス]**  >  **[ダッシュボード]** に移動します。

1. ダッシュボードで、有効になっている API の一覧を下にスクロールし、 **[Google Drive API]** をクリックします。
    ![Google Drive の選択](media/google14.png)

1. **[ドライブの管理画面の統合]** タブをクリックし、次の情報を入力します。

    * **アプリケーション名**:Microsoft Cloud App Security。

    * **簡単な説明と詳しい説明** (省略可能):Microsoft Cloud App Security はクラウド アプリケーションを可視化し、クラウド アプリケーションの使用を制御、調査、および管理するのに役立ちます。企業データをセキュリティ保護します。任意のクラウド アプリケーションの疑わしいアクティビティを検出します。

    * Google では、少なくとも 1 つのアプリケーション アイコンをアップロードする必要があります。 [https://go.microsoft.com/fwlink/?linkid=862826](https://go.microsoft.com/fwlink/?linkid=862826) に移動して、Cloud App Security アイコンを格納する zip ファイルをダウンロードします。 次に、 **[アプリケーション アイコン]** で、128 x 128 イメージの横にある **[選択]** をクリックして、それをポップアップ画面にドラッグします。 32 x 32 イメージの横にある **[選択]** をクリックして、それをポップアップ画面にドラッグします。

    * **[Drive Integration]** セクションで、 **[URL を開く]** の下に次の URL を入力します。
    `https://portal.cloudappsecurity.com/#/services/11770?tab=files`

    ![Google Drive の編集](media/google15.png)

1. **[送信]** をクリックします。

1. **[有効な API]** 一覧に戻ります。 **[G Suite Marketplace SDK]** をクリックします。

1. **[設定]** タブを選択します。

    1. 画面上部に表示される**プロジェクト番号 (アプリ ID)** を、後で使用するためにコピーします。

    1. **[アプリケーション名]** に「**Microsoft Cloud App Security**」と入力します。  
**[アプリケーションの説明]** に、「Microsoft Cloud App Security はクラウド アプリケーションを可視化し、クラウド アプリケーションの使用を制御、調査、および管理するのに役立ちます。企業データをセキュリティ保護します。任意のクラウド アプリケーションの疑わしいアクティビティを検出します。」と入力します。

    1. **[新しいアイテム]** ウィンドウで **[完了]** をクリックしてください。

    ![Google の新しいアイテム](media/google-new-item.png)

    * **[個別インストールを有効にする]** チェック ボックスをオフにします。

    * **[アプリケーションのアイコン]** で必要な 4 つのイメージを構成します。

    イメージは次の場所にあります。[https://go.microsoft.com/fwlink/?linkid=862826](https://go.microsoft.com/fwlink/?linkid=862826)

    * 次の **[サポートの URL]** を入力します。

    * **サービス利用規約の URL**: https://go.microsoft.com/fwlink/?LinkID=733268

    * **プライバシー ポリシーの URL**: https://go.microsoft.com/fwlink/?LinkId=512132

    * **[OAuth 2.0 スコープ]** で、次の URL をコピーして貼り付けます (一度に 1 つずつコピーし、それぞれの後に Enter キーを押します)。  
`https://www.googleapis.com/auth/admin.reports.audit.readonly`  
`https://www.googleapis.com/auth/admin.reports.usage.readonly`  
`https://www.googleapis.com/auth/drive`  
`https://www.googleapis.com/auth/drive.appdata`  
`https://www.googleapis.com/auth/drive.apps.readonly`  
`https://www.googleapis.com/auth/drive.file`  
`https://www.googleapis.com/auth/drive.metadata.readonly`  
`https://www.googleapis.com/auth/drive.readonly`  
`https://www.googleapis.com/auth/drive.scripts`  
`https://www.googleapis.com/auth/admin.directory.user.readonly`  
`https://www.googleapis.com/auth/admin.directory.user.security`  
`https://www.googleapis.com/auth/admin.directory.user.alias`  
`https://www.googleapis.com/auth/admin.directory.orgunit`  
`https://www.googleapis.com/auth/admin.directory.notifications`  
`https://www.googleapis.com/auth/admin.directory.group.member`  
`https://www.googleapis.com/auth/admin.directory.group`  
`https://www.googleapis.com/auth/admin.directory.device.mobile.action`  
`https://www.googleapis.com/auth/admin.directory.device.mobile`  
`https://www.googleapis.com/auth/admin.directory.user`

    * **[公開設定]** で、 **[マイ ドメイン]** (パブリックではない) を選択します。
    * **[変更を保存]** をクリックします。
        ![Google の公開設定](media/google-visibility.png)
1. Google 管理コンソールで、[[アプリのアクセス制御を管理]](https://admin.google.com/) に移動します。 **[G Suite 管理者]** 行を探し、 **[制限なし]** アクセスが設定されていることを確認します。

    ![Google セキュリティ](media/googlesec.png)

## <a name="configure-cloud-app-security"></a>Cloud App Security を構成する

1. Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. G Suite 接続の詳細を指定するには、 **[アプリ コネクタ]** で次のいずれかの操作を行います。

    **既に接続されている GCP インスタンスがある G Suite 組織の場合**

    * コネクタの一覧で、GCP インスタンスが表示されている行の末尾にある 3 つのドットをクリックし、 **[Add G Suite]\(G Suite の追加\)** をクリックします。

    **既に接続されている GCP インスタンスがない G Suite 組織の場合**

    * **[接続アプリ]** ページで、プラス記号をクリックし、 **[G Suite]** を選択します。

1. ポップアップで、次の情報を入力します。

    ![Cloud App Security での G Suite 構成](media/gsuite-config-cas.png "Cloud App Security での G Suite 構成")

    1. 前にコピーした**サービス アカウント ID**、**メール アドレス**を入力します。

    1. 前にコピーした **プロジェクト番号 (アプリ ID)** を入力します。

    1. 前に保存した P12 **証明書**ファイルをアップロードします。

    1. G Suite 管理者の 1 つの**管理者アカウントのメール アドレス**を入力します。

    1. G Suite Business または Enterprise アカウントを使用している場合は、このチェック ボックスをオンにします。 G Suite Business または Enterprise の場合の Cloud App Security で使用できる機能の詳細については、[アプリの表示、保護、およびガバナンス アクションをすぐに有効にする](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)方法に関するページを参照してください。

    1. **[設定の保存]** をクリックします。

    1. **[リンクに移動]** をクリックして G Suite に接続します。 これにより、G Suite が開き、Cloud App Security へのアクセスを承認するように求められます。

    1. **[今すぐテストする]** をクリックして、正常に接続されたことを確認します。  
    テストには数分かかる場合があります。  
    成功の通知を受信したら、 **[完了]** をクリックし、G Suite ページを閉じます。

G Suite に接続すると、接続前の 60 日間のイベントが表示されます。

G Suite に接続すると、Cloud App Security によってフル スキャンが実行されます。 ファイルとユーザーの数によっては、フル スキャンの完了にしばらく時間がかかります。 ほぼリアルタイムでのスキャンを可能にするため、アクティビティが検出されたファイルがスキャン キューの先頭に移動されます。 たとえば、編集、更新、または共有されたファイルは、ただちにスキャンされます。 これは、本質的に変更されていないファイルには当てはまりません。 たとえば、表示、プレビュー、印刷、またはエクスポートされたファイルは、定期的なスキャン中にスキャンされます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
