---
title: Cloud Discovery のデプロイ
description: この記事では、Cloud Discovery を動作させるためのセットアップ手順について説明します。
ms.date: 01/17/2021
ms.topic: how-to
ms.openlocfilehash: 2ac879d1cd4ac75aebdf080599f77b0bedba640e
ms.sourcegitcommit: e9d295ba27d0797e970d10b3effaff4961cbf556
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2021
ms.locfileid: "98540898"
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
- WatchGuard
- Zscaler

> [!NOTE]
> Cloud Discovery では、IPv4 と IPv6 の両方のアドレスがサポートされます。

ログがサポートされていない場合、またはサポートされているいずれかのデータ ソースから新しくリリースされたログ形式を使用していて、アップロードが失敗する場合は、 **[データ ソース]** として **[その他]** を選択し、アップロードしようとしているアプライアンスとログを指定します。 お使いのログが Cloud App Security クラウド アナリスト チームによってレビューされ、お使いのログの種類に対するサポートが追加される場合は、通知が届きます。 または、お使いの形式と一致するカスタム パーサーを定義することもできます。 詳細については、「[カスタム ログ パーサーを使用する](custom-log-parser.md)」を参照してください。

> [!NOTE]
> 次の一覧のサポートされているアプライアンスは、新しくリリースされたログ形式では動作しない場合があります。 新しくリリースされた形式を使用していて、アップロードが失敗する場合は、[カスタム ログ パーサーを使用](custom-log-parser.md)し、必要に応じてサポート ケースを開きます。

データ属性 (ベンダーのドキュメントによる):

| データ ソース | ターゲット アプリの URL | ターゲット アプリの IP | Username | 送信元の IP | 合計トラフィック | アップロードされたバイト数 |
|----------------------------------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|
| Barracuda | **あり** | **はい** | **はい** | **はい** | いいえ | いいえ |
| Blue Coat | **あり** | いいえ | **あり** | **あり** | **はい** | **あり** |
| Check Point | いいえ | **はい** | いいえ | **はい** | いいえ | いいえ |
| Cisco ASA (Syslog) | いいえ | **あり** | いいえ | **はい** | **はい** | いいえ |
| Cisco ASA と FirePOWER | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| Cisco Cloud Web Security |**あり**|**あり**|**あり**|**あり**|**はい**|**あり**|
| Cisco FWSM | いいえ | **あり** | いいえ | **はい** | **はい** | いいえ |
| Cisco Ironport WSA | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| Cisco Meraki | **はい** | **はい** | いいえ | **はい** | いいえ | いいえ |
| Clavister NGFW (Syslog) | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| ContentKeeper | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| Corrata | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| SonicWall (旧 Dell) | **はい** | **あり** | いいえ | **あり** | **はい** | **あり** |
| Digital Arts i-FILTER | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| ForcePoint LEEF |**あり**|**あり**|**あり**|**あり**|**はい**|**あり**|
| ForcePoint Web Security Cloud\* |**あり**|**あり**|**あり**|**あり**|**はい**|**あり**|
| Fortinet Fortigate | いいえ | **あり** | いいえ | **あり** | **はい** | **あり** |
| FortiOS |**はい**|**あり**|いいえ|**あり**|**はい**|**あり**|
| iboss |**あり**|**あり**|**あり**|**あり**|**はい**|**あり**|
| Juniper SRX | いいえ | **あり** | いいえ | **あり** | **はい** | **あり** |
| Juniper SSG | いいえ | **あり** | **あり** | **あり** | **はい** | **あり** |
| McAfee SWG | **あり** | いいえ | いいえ | **はい** | **はい** | **はい** |
| Menlo Security (CEF) | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| MS TMG | **あり** | いいえ | **あり** | **あり** | **はい** | **あり** |
| Palo Alto Networks | いいえ | **あり** | **はい** | **あり** | **はい** | **あり** |
| Sophos | **あり** | **はい** | **あり** | **はい** | **はい** | いいえ |
| Squid (Common) | **あり** | いいえ | **あり** | **はい** | **はい** | いいえ |
| Squid (Native) | **あり** | いいえ | **はい** | **はい** | いいえ | いいえ |
| Stormshield | いいえ | **あり** | **あり** | **あり** | **はい** | **あり** |
| Websense - 調査詳細レポート (CSV) | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| Websense - インターネット アクティビティ ログ (CEF) | **あり** | **あり** | **あり** | **あり** | **はい** | **あり** |
| WatchGuard | **はい** | **はい** | **はい** | **あり** | **はい** | **あり** |
| Zscaler | **はい** | **はい** | **はい** | **はい** | **はい** | **はい** |

\* Forcepoint Web Security Cloud のバージョン 8.5 以降はサポートされていません

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery のスナップショット レポートを作成する](create-snapshot-cloud-discovery-reports.md)

> [!div class="nextstepaction"]
> [継続的なレポートのために自動ログ アップロードを構成する](discovery-docker.md)

> [!div class="nextstepaction"]
> [Cloud Discovery データでの作業](working-with-cloud-discovery-data.md)
