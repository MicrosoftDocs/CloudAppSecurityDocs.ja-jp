---
title: Cloud App Security と汎用 SIEM の統合
description: この記事では、汎用 SIEM と Cloud App Security の統合に関する情報を提供します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/28/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 32a4b3542a7abc7d96ae6ca111fbfba7a6a5fbff
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88779136"
---
# <a name="generic-siem-integration"></a>汎用 SIEM の統合

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security と汎用 SIEM サーバーを統合し、接続アプリから、アラートとアクティビティを一元的に監視できます。 接続アプリでは新しいアクティビティとイベントがサポートされるため、それらの表示が Microsoft Cloud App Security にロールアウトされます。 SIEM サービスとの統合により、通常のセキュリティ ワークフローを維持し、セキュリティ手順を自動化してクラウドベースのイベントとオンプレミス イベントを関連付けた状態で、クラウド アプリケーションの保護を強化できます。 Microsoft Cloud App Security SIEM エージェントはサーバー上で実行され、Microsoft Cloud App Security からアラートとアクティビティを取得し、SIEM サーバーに送ります。

SIEM を Cloud App Security と初めて統合した場合、過去 2 日間のアクティビティとアラートは SIEM に転送され、以降のすべてのアクティビティとアラートも (選択したフィルターに基づいて) 転送されます。 この機能を長期間無効にしてから再び有効にすると、過去 2 日間分のアラートとアクティビティが転送され、次にそれ以降のすべてのアラートとアクティビティが転送されます。

追加の統合ソリューションには次のものがあります。

* **Azure Sentinel** - ネイティブ統合用のスケーラブルでクラウドネイティブの SIEM および SOAR です。 Azure Sentinel との統合の詳細については、「[Azure Sentinel 統合](siem-sentinel.md)」を参照してください。
* **Microsoft セキュリティ グラフ API** - 複数のセキュリティ プロバイダーに接続するための単一のプログラムによるインターフェイスを提供する中間サービス (またはブローカー) です。 詳細については、「[Microsoft Graph Security API を使用したセキュリティ ソリューションの統合](https://docs.microsoft.com/graph/security-integration#list-of-connectors-from-microsoft)」を参照してください。

> [!IMPORTANT]
> Cloud App Security に Azure Advanced Threat Protection を統合し、アラート通知を SIEM に送信するように両方のサービスを構成している場合、同じアラートに対して重複する SIEM 通知が送られてきます。 各サービスからはアラートが 1 つ発行され、異なるアラート ID が与えられます。 重複や混乱を避けるため、このシナリオに対処してください。 たとえば、アラート管理を実行する箇所を決定し、他のサービスからの SIEM 通知の送信を停止します。

## <a name="generic-siem-integration-architecture"></a>汎用 SIEM 統合アーキテクチャ

SIEM エージェントは組織のネットワークに展開されます。 展開と構成が行われると、Cloud App Security RESTful API を使用して構成を行ったデータの種類 (アラートとアクティビティ) がプルされます。
ポーリングされるトラフィックはポート 443 の暗号化された HTTPS チャネルを通じて送信されます。

SIEM エージェントで Cloud App Security からデータが受け取られると、ローカル SIEM に Syslog メッセージが送信されます。 Cloud App Security では、セットアップ時に指定したネットワーク構成 (カスタムポートによる TCP または UDP) が使用されます。

![SIEM 統合アーキテクチャ](media/siem-architecture.png)

## <a name="supported-siems"></a>サポートされている SIEM

Cloud App Security では現在、Micro Focus ArcSight と汎用 CEF がサポートされています。

## <a name="how-to-integrate"></a>統合方法

SIEM との統合は次の 3 つの手順で行われます。

1. Cloud App Security ポータルでセットアップします。
2. JAR ファイルをダウンロードし、サーバーで実行します。
3. SIEM エージェントが動作しているか検証します。

### <a name="prerequisites"></a>[前提条件]

* 標準的な Windows または Linux サーバー (仮想マシンを使用可)。
* OS:Windows または Linux
* CPU:2
* ディスク領域:20 GB
* RAM:2 GB
* サーバーで Java 8 を実行している必要があります。 以前のバージョンはサポートされません。
* 「[ネットワークの要件](network-requirements.md)」で説明されているとおりに、ファイアウォールを設定します

## <a name="integrating-with-your-siem"></a>SIEM との統合

### <a name="step-1-set-it-up-in-the-cloud-app-security-portal"></a>手順 1:Cloud App Security ポータルでセットアップする

1. Cloud App Security ポータルの **[設定]** 歯車で、 **[セキュリティ拡張機能]** をクリックします。

1. **[SIEM エージェント]** タブで、追加 ( **+** ) をクリックし、 **[Generic SIEM]\(汎用 SIEM\)** を選択します。

    ![SIEM 統合の追加メニューを示すスクリーンショット](media/siem0.png)

1. ウィザードで、 **[ウィザード起動]** をクリックします。
1. ウィザードで、名前を入力し、**SIEM 形式を選択**して、その形式に関する**詳細設定**をすべて設定します。 **[次へ]** をクリックします。

    ![SIEM の全般設定](media/siem1.png)

1. **リモートの Syslog ホスト**の IP アドレスまたはホスト名と **Syslog ポート番号**を入力します。 リモートの Syslog プロトコルとして TCP または UDP を選択します。
    これらの詳細がわからない場合は、セキュリティ管理者と協力して取得してださい。 **[次へ]** をクリックします。

    ![リモートの Syslog 設定](media/siem2.png)

1. **アラート**と**アクティビティ**について、SIEM サーバーにエクスポートするデータの種類を選択します。 スライダーを使用してこれらを有効および無効にします。既定では、すべて選択されます。 **[適用先]** ドロップダウンを使用して、SIEM サーバーに特定のアラートとアクティビティのみを送信するようにフィルターを設定することができます。 **[結果の編集とプレビュー]** をクリックし、フィルターが予期したとおりに動作していることを確認します。 **[次へ]** をクリックします。

   ![データの種類の設定](media/siem3.png)

1. トークンをコピーし、保存して後で使用できるようにします。
    [完了] をクリックして、ウィザードを終了します。 SIEM ページに戻り、テーブルに追加した SIEM エージェントを確認します。 後で接続されるまで **[作成済み]** と表示されます。

> [!NOTE]
> 作成したトークンは、それを作成した管理者にバインドされます。 これは、管理者ユーザーが Cloud App Security から削除されると、トークンが有効でなくなることを意味します。

### <a name="step-2-download-the-jar-file-and-run-it-on-your-server"></a>手順 2:JAR ファイルをダウンロードし、サーバーで実行する

1. [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?linkid=838596)で、[ソフトウェア ライセンス条項](https://go.microsoft.com/fwlink/?linkid=862491)に同意したら、.zip ファイルをダウンロードして解凍します。

1. サーバーで抽出したファイルを実行します。

    `java -jar mcas-siemagent-0.87.20-signed.jar [--logsDirectory DIRNAME] [--proxy ADDRESS[:PORT]] --token TOKEN`

> [!NOTE]
>
> * ファイル名は、SIEM エージェントのバージョンによって異なる場合があります。
> * 角かっこ [] で囲まれたパラメーターは省略可能で、関係する場合にのみ使用してください。
> * サーバーの起動時に JAR を実行することが推奨されます。
>   * Windows:スケジュールされたタスクとして実行し、**ユーザーがログオンしているかどうかにかかわらず実行する**ようにタスクを構成し、 **[タスクを停止するまでの時間]** チェックボックスをオフにしていることを確認します。
>   * Linux: **&** を付けた実行コマンドを rc.local ファイルに追加します。 例: `java -jar mcas-siemagent-0.87.20-signed.jar [--logsDirectory DIRNAME] [--proxy ADDRESS[:PORT]] --token TOKEN &`

各変数の使用方法:

* DIRNAME は、ローカル エージェント デバッグ ログで使用するディレクトリのパスです。
* ADDRESS[:PORT] は、サーバーがインターネットに接続する際に使用するプロキシ サーバーのアドレスとポートです。
* TOKEN は、前の手順でコピーした SIEM エージェント トークンです。

「-h」と入力すれば、いつでもヘルプを表示できます。

#### <a name="sample-activity-logs"></a>アクティビティ ログのサンプル<a name="siem-samples"></a>

SIEM に送信されるアクティビティ ログのサンプルを次に示します。

>`2017-11-22T17:50:04.000Z CEF:0|MCAS|SIEM_Agent|0.111.85|EVENT_CATEGORY_LOGOUT|Log out|0|externalId=1511373015679_167ae3eb-ed33-454a-b548-c2ed6cea6ef0 rt=1511373004000 start=1511373004000 end=1511373004000 msg=Log out suser=admin@contoso.com destinationServiceName=ServiceNow dvc=13.82.149.151 requestClientApplication= cs1Label=portalURL cs1=https://contoso.portal.cloudappsecurity.com/#/audits?activity.id\=eq(1511373015679_167ae3eb-ed33-454a-b548-c2ed6cea6ef0,) cs2Label=uniqueServiceAppIds cs2=APPID_SERVICENOW cs3Label=targetObjects cs3=admin@contoso.com,admin@contoso.com,admin@contoso.com cs4Label=policyIDs cs4= c6a1Label="Device IPv6 Address" c6a1=`
>
>`2017-11-28T19:40:15.000Z CEF:0|MCAS|SIEM_Agent|0.112.68|EVENT_CATEGORY_VIEW_REPORT|View report|0|externalId=1511898027370_e272cd5f-31a3-48e3-8a6a-0490c042950a rt=1511898015000 start=1511898015000 end=1511898015000 msg=View report: ServiceNow Report 23 suser=admin@contoso.com destinationServiceName=ServiceNow dvc= requestClientApplication= cs1Label=portalURL cs1=https://contoso.portal.cloudappsecurity.com/#/audits?activity.id\=eq(1511898027370_e272cd5f-31a3-48e3-8a6a-0490c042950a,) cs2Label=uniqueServiceAppIds cs2=APPID_SERVICENOW cs3Label=targetObjects cs3=23,sys_report,admin@contoso.com,admin@contoso.com,admin@contoso.com cs4Label=policyIDs cs4= c6a1Label="Device IPv6 Address" c6a1=`
>
>`2017-11-28T19:25:34.000Z CEF:0|MCAS|SIEM_Agent|0.112.68|EVENT_CATEGORY_DELETE_OBJECT|Delete object|0|externalId=1511897141625_7558b33f-218c-40ff-be5d-47d2bdd6b798 rt=1511897134000 start=1511897134000 end=1511897134000 msg=Delete object: ServiceNow Object f5122008db360300906ff34ebf96198a suser=admin@contoso.com destinationServiceName=ServiceNow dvc= requestClientApplication= cs1Label=portalURL cs1=https://contoso.portal.cloudappsecurity.com/#/audits?activity.id\=eq(1511897141625_7558b33f-218c-40ff-be5d-47d2bdd6b798,) cs2Label=uniqueServiceAppIds cs2=APPID_SERVICENOW cs3Label=targetObjects cs3=,,admin@contoso.com,admin@contoso.com,admin@contoso.com cs4Label=policyIDs cs4= c6a1Label="Device IPv6 Address" c6a1=`
>
>`2017-11-27T20:40:14.000Z CEF:0|MCAS|SIEM_Agent|0.112.49|EVENT_CATEGORY_CREATE_USER|Create user|0|externalId=1511815215873_824f8f8d-2ecd-439b-98b1-99a1adf7ba1c rt=1511815214000 start=1511815214000 end=1511815214000 msg=Create user: user 747518c0db360300906ff34ebf96197c suser=admin@contoso.com destinationServiceName=ServiceNow dvc= requestClientApplication= cs1Label=portalURL cs1=https://contoso.portal.cloudappsecurity.com/#/audits?activity.id\=eq(1511815215873_824f8f8d-2ecd-439b-98b1-99a1adf7ba1c,) cs2Label=uniqueServiceAppIds cs2=APPID_SERVICENOW cs3Label=targetObjects cs3=,747518c0db360300906ff34ebf96197c,sys_user,admin@contoso.com,admin@contoso.com,admin@contoso.com cs4Label=policyIDs cs4= c6a1Label="Device IPv6 Address" c6a1=`
>
>`2017-11-27T20:41:20.000Z CEF:0|MCAS|SIEM_Agent|0.112.49|EVENT_CATEGORY_DELETE_USER|Delete user|0|externalId=1511815287798_bcf60601-ecef-4207-beda-3d2b8d87d383 rt=1511815280000 start=1511815280000 end=1511815280000 msg=Delete user: user 233490c0db360300906ff34ebf9619ef suser=admin@contoso.com destinationServiceName=ServiceNow dvc= requestClientApplication= cs1Label=portalURL cs1=https://contoso.portal.cloudappsecurity.com/#/audits?activity.id\=eq(1511815287798_bcf60601-ecef-4207-beda-3d2b8d87d383,) cs2Label=uniqueServiceAppIds cs2=APPID_SERVICENOW cs3Label=targetObjects cs3=,233490c0db360300906ff34ebf9619ef,,admin@contoso.com,admin@contoso.com,admin@contoso.com cs4Label=policyIDs cs4= c6a1Label="Device IPv6 Address" c6a1=`
>
>`2017-11-28T19:24:55.000Z LAB-EUW-ARCTEST CEF:0|MCAS|SIEM_Agent|0.112.68|EVENT_CATEGORY_DELETE_OBJECT|Delete object|0|externalId=1511897117617_5be018ee-f676-4473-a9b5-5982527409be rt=1511897095000 start=1511897095000 end=1511897095000 msg=Delete object: ServiceNow Object b1709c40db360300906ff34ebf961923 suser=admin@contoso.com destinationServiceName=ServiceNow dvc= requestClientApplication= cs1Label=portalURL cs1=https://contoso.portal.cloudappsecurity.com/#/audits?activity.id\=eq(1511897117617_5be018ee-f676-4473-a9b5-5982527409be,) cs2Label=uniqueServiceAppIds cs2=APPID_SERVICENOW cs3Label=targetObjects cs3=,,admin@contoso.com,admin@contoso.com,admin@contoso.com cs4Label=policyIDs cs4= c6a1Label="Device IPv6 Address" c6a1=`

次のテキストはアラート ログファイルの例です。

>`2017-07-15T20:42:30.531Z CEF:0|MCAS|SIEM_Agent|0.102.17|ALERT_CABINET_EVENT_MATCH_AUDIT|myPolicy|3|externalId=596a7e360c204203a335a3fb start=1500151350531 end=1500151350531 msg=Activity policy ''myPolicy'' was triggered by ''admin@box-contoso.com'' suser=admin@box-contoso.com destinationServiceName=Box cn1Label=riskScore cn1= cs1Label=portalURL cs1=https://cloud-app-security.com/#/alerts/596a7e360c204203a335a3fb cs2Label=uniqueServiceAppIds cs2=APPID_BOX cs3Label=relatedAudits cs3=1500151288183_acc891bf-33e1-424b-a021-0d4370789660 cs4Label=policyIDs cs4=59f0ab82f797fa0681e9b1c7`
>
>`2017-07-16T09:36:26.550Z CEF:0|MCAS|SIEM_Agent|0.102.17|ALERT_CABINET_EVENT_MATCH_AUDIT|test-activity-policy|3|externalId=596b339b0c204203a33a51ae start=1500197786550 end=1500197786550 msg=Activity policy ''test-activity-policy'' was triggered by ''user@contoso.com'' suser=user@contoso.com destinationServiceName=Salesforce cn1Label=riskScore cn1= cs1Label=portalURL cs1=https://cloud-app-security.com/#/alerts/596b339b0c204203a33a51ae cs2Label=uniqueServiceAppIds cs2=APPID_SALESFORCE cs3Label=relatedAudits cs3=1500197720691_b7f6317c-b8de-476a-bc8f-dfa570e00349 cs4Label=policyIDs cs4=`
>
>`2017-07-16T09:17:03.361Z CEF:0|MCAS|SIEM_Agent|0.102.17|ALERT_CABINET_EVENT_MATCH_AUDIT|test-activity-policy3|3|externalId=596b2fd70c204203a33a3eeb start=1500196623361 end=1500196623361 msg=Activity policy ''test-activity-policy3'' was triggered by ''admin@contoso.com'' suser=admin@contoso.com destinationServiceName=Office 365 cn1Label=riskScore cn1= cs1Label=portalURL cs1=https://cloud-app-security.com/#/alerts/596b2fd70c204203a33a3eeb cs2Label=uniqueServiceAppIds cs2=APPID_O365 cs3Label=relatedAudits cs3=1500196549157_a0e01f8a-e29a-43ae-8599-783c1c11597d cs4Label=policyIDs cs4=`
>
>`2017-07-16T09:17:15.426Z CEF:0|MCAS|SIEM_Agent|0.102.17|ALERT_CABINET_EVENT_MATCH_AUDIT|test-activity-policy|3|externalId=596b2fd70c204203a33a3eec start=1500196635426 end=1500196635426 msg=Activity policy ''test-activity-policy'' was triggered by ''admin@contoso.com'' suser=admin@contoso.com destinationServiceName=Microsoft 365 admin center cn1Label=riskScore cn1= cs1Label=portalURL cs1=https://cloud-app-security.com/#/alerts/596b2fd70c204203a33a3eec cs2Label=uniqueServiceAppIds cs2=APPID_O365_PORTAL cs3Label=relatedAudits cs3=1500196557398_3e102b20-d9fa-4f66-b550-8c7a403bb4d8 cs4Label=policyIDs cs4=59f0ab35f797fa9811e9b1c7`
>
>`2017-07-16T09:17:46.290Z CEF:0|MCAS|SIEM_Agent|0.102.17|ALERT_CABINET_EVENT_MATCH_AUDIT|test-activity-policy4|3|externalId=596b30200c204203a33a4765 start=1500196666290 end=1500196666290 msg=Activity policy ''test-activity-policy4'' was triggered by ''admin@contoso.com'' suser=admin@contoso.com destinationServiceName=Microsoft Exchange Online cn1Label=riskScore cn1= cs1Label=portalURL cs1=https://cloud-app-security.com/#/alerts/596b30200c204203a33a4765 cs2Label=uniqueServiceAppIds cs2=APPID_OUTLOOK cs3Label=relatedAudits cs3=1500196587034_a8673602-7e95-46d6-a1fe-c156c4709c5d cs4Label=policyIDs cs4=`
>
>`2017-07-16T09:41:04.369Z CEF:0|MCAS|SIEM_Agent|0.102.17|ALERT_CABINET_EVENT_MATCH_AUDIT|test-activity-policy2|3|externalId=596b34b10c204203a33a5240 start=1500198064369 end=1500198064369 msg=Activity policy ''test-activity-policy2'' was triggered by ''user2@test15-adallom.com'' suser=user2@test15-adallom.com destinationServiceName=Google cn1Label=riskScore cn1= cs1Label=portalURL cs1=https://cloud-app-security.com/#/alerts/596b34b10c204203a33a5240 cs2Label=uniqueServiceAppIds cs2=APPID_33626 cs3Label=relatedAudits cs3=1500197996117_fd71f265-1e46-4f04-b372-2e32ec874cd3 cs4Label=policyIDs cs4=`

#### <a name="sample-cloud-app-security-alerts-in-cef-format"></a>CEF 形式の Cloud App Security アラートのサンプル

| 次に対して適用可能 | CEF フィールド名 | [説明] |
| --- | --- | --- |
| アクティビティ/アラート | start | アクティビティまたはアラートのタイムスタンプ |
| アクティビティ/アラート | end | アクティビティまたはアラートのタイムスタンプ |
| アクティビティ/アラート | rt | アクティビティまたはアラートのタイムスタンプ |
| アクティビティ/アラート | msg | ポータルに表示されるアクティビティまたはアラートの説明 |
| アクティビティ/アラート | suser | アクティビティまたはアラートの対象ユーザー |
| アクティビティ/アラート | destinationServiceName | アクティビティまたはアラートの生成元アプリ (Office 365、SharePoint、Box など)。 |
| アクティビティ/アラート | cs\<X>Label | 各ラベルは異なる意味を持ちますが、targetObjects など、ラベル自体でそれが説明されています。 |
| アクティビティ/アラート | cs\<X> | ラベルに対応する情報 (ラベルの例によると、アクティビティまたはアラートのターゲット ユーザー)。 |
| アクティビティ | EVENT_CATEGORY_* | アクティビティの高レベル カテゴリ |
| アクティビティ | \<ACTION> | ポータルに表示されるアクティビティの種類 |
| アクティビティ | externalId | イベント ID |
| アクティビティ | dvc | クライアント デバイスの IP |
| アクティビティ | requestClientApplication | クライアント デバイスのユーザー エージェント |
| アラート | \<alert type> | たとえば、"ALERT_CABINET_EVENT_MATCH_AUDIT" |
| アラート | \<name> | 一致したポリシー名 |
| アラート | externalId | アラート ID |
| アラート | src | クライアント デバイスの IPv4 アドレス |
| アラート | c6a1 | クライアント デバイスの IPv6 アドレス |

### <a name="step-3-validate-that-the-siem-agent-is-working"></a>手順 3:SIEM エージェントが動作していることを検証する

1. Cloud App Security ポータルで SIEM エージェントの状態が **[接続エラー]** または **[切断]** ではないこと、およびエージェント通知がないことを確認します。 接続が 2 時間以上ダウンしている場合は、 **[接続エラー]** と表示されます。 接続が 12 時間以上ダウンしている場合は、状態が **[切断]** と表示されます。
 ![SIEM が切断されている状態](media/siem-not-connected.png)

    代わりに、次に示すように、状態は接続済みになっているはずです。![SIEM 接続済み](media/siem-connected.png)

1. Syslog/SIEM サーバーで、Cloud App Security から送られたアクティビティとアラートが表示されていることを確認します。

## <a name="regenerating-your-token"></a>トークンの再生成

トークンが失われた場合は、テーブルの SIEM エージェント行の末尾にある 3 つのドットをクリックして、いつでも再生成することができます。 **[トークンの再生成]** を選択して、新しいトークンを取得しますす。

![SIEM - トークンの再生成](media/siem-regenerate-token.png)

## <a name="editing-your-siem-agent"></a>SIEM エージェントの編集

SIEM エージェントを編集するには、テーブルの SIEM エージェント行の末尾にある 3 つのドットをクリックし、 **[編集]** を選択します。 SIEM エージェントを編集する場合、.jar ファイルを再実行する必要はなく、自動的に更新されます。

![SIEM - 編集](media/siem-edit.png)

## <a name="deleting-your-siem-agent"></a>SIEM エージェントの削除

SIEM エージェントを削除する場合は、テーブルの SIEM エージェント行の末尾にある 3 つのドットをクリックし、 **[削除]** を選択します。

![SIEM - 削除](media/siem-delete.png)

> [!NOTE]
> この機能はパブリック プレビューの状態にあります。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [SIEM 統合問題のトラブルシューティング](troubleshooting-siem.md)

[!INCLUDE [Open support ticket](includes/support.md)]
