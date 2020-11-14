---
title: Cloud Discovery をデプロイする - Cloud App Security
description: この記事では、Cloud Discovery を動作させるためのセットアップ手順について説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: how-to
ms.date: 08/09/2020
ms.collection: M365-security-compliance
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 8a5d2d5ee97677482be80a44b33f832cfaee6ddf
ms.sourcegitcommit: 288f3011c0ce0e5f2d8cbaa9057a63be044465f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94375093"
---
# <a name="set-up-cloud-discovery"></a>Cloud Discovery の設定

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud Discovery では、16,000 以上のクラウド アプリを掲載した Microsoft Cloud App Security のクラウド アプリ カタログに照らしてトラフィック ログが分析されます。 これらのアプリは、80 以上のリスク要因に基づいてランク付けおよびスコア付けされます。これにより、クラウドの使用状況、シャドウ IT、シャドウ IT が組織にもたらすリスクを継続的に把握することができます。

## <a name="snapshot-and-continuous-risk-assessment-reports"></a>スナップショットと継続的なリスク評価レポート

次の種類のレポートを生成できます。

- **スナップショット レポート** - ファイアウォールやプロキシから手動でアップロードするトラフィック ログのセットに対するアドホックな可視性が提供されます。

- **継続的レポート** - Cloud App Security を使用してネットワークから転送されるすべてのログが分析されます。 すべてのデータの可視性が向上し、Machine Learning の異常検出エンジンまたはユーザー定義のカスタム ポリシーを使用して、異常な使用が自動的に識別されます。 これらのレポートは、次の方法で接続することによって作成できます。

  - [**Microsoft Defender for Endpoint 統合**](mde-integration.md):Cloud App Security は、Defender for Endpoint とネイティブに統合されており、Cloud Discovery のロールアウトが簡素化され、企業ネットワークを超えて Cloud Discovery の機能が拡張され、コンピューター ベースの調査が有効になります。
  - [**ログ コレクター**](discovery-docker.md):ログ コレクターを使用すると、ネットワークからのログのアップロードを簡単に自動化することができます。 ログ コレクターをネットワーク上で実行すると、Syslog または FTP でログを受け取ります。
  - **Secure Web Gateway (SWG)** :Cloud App Security と次の SWG のいずれかの両方を使用している場合は、製品を統合して、お使いの Cloud Discovery のセキュリティを強化することができます。 Cloud App Security と SWG を一緒に使用すると、Cloud Discovery のシームレスなデプロイ、承認されていないアプリの自動的なブロック、SWG のポータルでの直接的なリスク評価が提供されます。
    - [Zscaler の統合](zscaler-integration.md)
    - [iboss の統合](iboss-integration.md)
    - [Corrata の統合](corrata-integration.md)
    - [Menlo Security の統合](menlo-integration.md)

- **[Cloud Discovery API](api-discovery.md)** -Cloud App Security の Cloud Discovery API を使用して、トラフィック ログのアップロードを自動化し、Cloud Discovery のレポートとリスク評価を自動で取得します。 また、API を使用して[ブロック スクリプトを生成](api-discovery-script.md)し、ネットワーク アプライアンスに対して直接アプリ制御を合理化することもできます。

## <a name="log-process-flow-from-raw-data-to-risk-assessment"></a>ログ プロセス フロー: 生データからリスク評価へ

リスク評価を生成するプロセスは、次の手順で構成されています。 処理されるデータの量によっては、プロセスには数分から数時間かかります。

- **アップロード** – ネットワークからの Web トラフィック ログがポータルにアップロードされます。

- **解析** – Cloud App Security によりトラフィック ログからトラフィック データが抽出され、データ ソースごとに専用のパーサーを使用して解析されます。

- **分析** – クラウド アプリ カタログに対してトラフィック データが分析され、16,000 を超えるクラウド アプリが識別されて、そのリスク スコアが評価されます。 アクティブなユーザーと IP アドレスも分析の一部として識別されます。

- **レポートの生成** - ログ ファイルから抽出されたデータのリスク評価レポートが生成されます。

>[!NOTE]
> 継続的レポートのデータは 1 日に 4 回分析されます。

## <a name="supported-firewalls-and-proxies"></a>サポートされているファイアウォールとプロキシ <a name="supported-firewalls-and-proxies"></a>

- Barracuda - Web アプリ ファイアウォール (W3C)
- Blue Coat Proxy SG - アクセス ログ (W3C)
- Check Point
- Cisco ASA と FirePOWER
- Cisco ASA Firewall (Cisco ASA Firewall の場合は、情報レベルを 6 に設定する必要があります)
- Cisco Cloud Web Security
- Cisco FWSM
- Cisco IronPort WSA
- Cisco Meraki – URL ログ
- Clavister NGFW (Syslog)
- ContentKeeper
- Corrata
- Digital Arts i-FILTER
- Forcepoint
- Fortinet Fortigate
- iboss Secure Cloud Gateway
- Juniper SRX
- Juniper SSG
- McAfee Secure Web Gateway
- Menlo Security (CEF)
- Microsoft Forefront Threat Management Gateway (W3C)
- Palo Alto シリーズ ファイアウォール
- Sonicwall (旧 Dell)
- Sophos SG
- Sophos XG
- Sophos Cyberoam
- Squid (Common)
- Squid (Native)
- Stormshield
- Websense - Web Security Solutions - 調査詳細レポート (CSV)
- Websense - Web Security Solutions - インターネット アクティビティ ログ (CEF)
- Zscaler

> [!NOTE]
> Cloud Discovery では、IPv4 と IPv6 の両方のアドレスがサポートされます。

ログがサポートされていない場合、またはサポートされているいずれかのデータ ソースから新しくリリースされたログ形式を使用していて、アップロードが失敗する場合は、 **[データ ソース]** として **[その他]** を選択し、アップロードしようとしているアプライアンスとログを指定します。 お使いのログが Cloud App Security クラウド アナリスト チームによってレビューされ、お使いのログの種類に対するサポートが追加される場合は、通知が届きます。 または、お使いの形式と一致するカスタム パーサーを定義することもできます。 詳細については、「[カスタム ログ パーサーを使用する](custom-log-parser.md)」を参照してください。

> [!NOTE]
> 次の一覧のサポートされているアプライアンスは、新しくリリースされたログ形式では動作しない場合があります。 新しくリリースされた形式を使用していて、アップロードが失敗する場合は、[カスタム ログ パーサーを使用](custom-log-parser.md)し、必要に応じてサポート ケースを開きます。

データ属性 (ベンダーのドキュメントによる):

| データ ソース | ターゲット アプリの URL | ターゲット アプリの IP | Username | 送信元の IP | 合計トラフィック | アップロードされたバイト数 |
|----------------------------------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|
| Barracuda | **あり** | **はい** | **はい** | **あり** | いいえ | いいえ |
| Blue Coat | **あり** | いいえ | **あり** | **はい** | **あり** | **あり** |
| Check Point | いいえ | **あり** | いいえ | **あり** | いいえ | いいえ |
| Cisco ASA (Syslog) | いいえ | **あり** | いいえ | **はい** | **あり** | いいえ |
| Cisco ASA と FirePOWER | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| Cisco Cloud Web Security |**あり**|**あり**|**あり**|**はい**|**あり**|**あり**|
| Cisco FWSM | いいえ | **あり** | いいえ | **はい** | **あり** | いいえ |
| Cisco Ironport WSA | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| Cisco Meraki | **はい** | **あり** | いいえ | **あり** | いいえ | いいえ |
| Clavister NGFW (Syslog) | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| ContentKeeper | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| Corrata | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| SonicWall (旧 Dell) | **はい** | **あり** | いいえ | **はい** | **あり** | **あり** |
| Digital Arts i-FILTER | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| ForcePoint LEEF |**あり**|**あり**|**あり**|**はい**|**あり**|**あり**|
| ForcePoint Web Security Cloud\* |**あり**|**あり**|**あり**|**はい**|**あり**|**あり**|
| Fortigate | いいえ | **あり** | いいえ | **はい** | **あり** | **あり** |
| Fortinet FortiOS |**はい**|**あり**|いいえ|**はい**|**あり**|**あり**|
| iboss |**あり**|**あり**|**あり**|**はい**|**あり**|**あり**|
| Juniper SRX | いいえ | **あり** | いいえ | **はい** | **あり** | **あり** |
| Juniper SSG | いいえ | **あり** | **あり** | **はい** | **あり** | **あり** |
| McAfee SWG | **あり** | いいえ | いいえ | **はい** | **はい** | **あり** |
| Menlo Security (CEF) | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| MS TMG | **あり** | いいえ | **あり** | **はい** | **あり** | **あり** |
| Palo Alto Networks | いいえ | **あり** | **あり** | **はい** | **あり** | **あり** |
| Sophos | **あり** | **あり** | **はい** | **はい** | **あり** | いいえ |
| Squid (Common) | **あり** | いいえ | **はい** | **はい** | **あり** | いいえ |
| Squid (Native) | **あり** | いいえ | **はい** | **あり** | いいえ | いいえ |
| Stormshield | いいえ | **あり** | **あり** | **はい** | **あり** | **あり** |
| Websense - 調査詳細レポート (CSV) | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| Websense - インターネット アクティビティ ログ (CEF) | **あり** | **あり** | **あり** | **はい** | **あり** | **あり** |
| Zscaler | **はい** | **はい** | **はい** | **はい** | **はい** | **あり** |

\* Forcepoint Web Security Cloud のバージョン 8.5 以降はサポートされていません

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery のスナップショット レポートを作成する](create-snapshot-cloud-discovery-reports.md)

> [!div class="nextstepaction"]
> [継続的なレポートのために自動ログ アップロードを構成する](discovery-docker.md)

> [!div class="nextstepaction"]
> [Cloud Discovery データでの作業](working-with-cloud-discovery-data.md)
