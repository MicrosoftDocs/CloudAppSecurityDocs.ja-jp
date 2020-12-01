---
title: Cloud App Security と Azure Sentinel の統合
description: この記事では、Azure Sentinel と Cloud App Security の統合に関する情報を提供します。
ms.date: 08/23/2020
ms.topic: how-to
ms.openlocfilehash: e30981259f1ee0c6894918f12ebfa2c370e72564
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96315465"
---
# <a name="azure-sentinel-integration-preview"></a>Azure Sentinel の統合 (プレビュー)

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security を Azure Sentinel (スケーラブルでクラウドネイティブな SIEM および SOAR) と統合することにより、アラートと探索データを一元的に監視できます。 Azure Sentinel との統合により、クラウド アプリケーションの保護を強化しながら、通常のセキュリティ ワークフローを維持し、セキュリティ手順を自動化し、クラウドベースのイベントとオンプレミス イベントを関連付けることができます。

Azure Sentinel の使用には、次のような利点があります。

* Log Analytics によって提供されるより長いデータ保有期間。
* すぐに使える視覚化。
* Microsoft Power BI や Azure Sentinel ブックなどのツールを使用して、組織のニーズに合わせた独自の探索データの視覚化を作成できます。

追加の統合ソリューションには次のものがあります。

* **汎用 SIEM** - Cloud App Security を汎用 SIEM サーバーと統合します。 汎用 SIEM との統合の詳細については、「[汎用 SIEM の統合](siem.md)」をご覧ください。
* **Microsoft セキュリティ グラフ API** - 複数のセキュリティ プロバイダーに接続するための単一のプログラムによるインターフェイスを提供する中間サービス (またはブローカー) です。 詳細については、[Microsoft Graph Security API を使用したセキュリティ ソリューションの統合](/graph/security-integration#list-of-connectors-from-microsoft)に関する記事をご覧ください。

## <a name="how-to-integrate"></a>統合方法

SIEM との統合は次の 2 つの手順で行われます。

1. Cloud App Security で設定する。
1. Azure Sentinel で設定する。

> [!NOTE]
> 以前に統合を行っていた場合、Azure Sentinel を追加するオプションは使用できません。

### <a name="prerequisites"></a>[前提条件]

Azure Sentinel と統合するには:

* 有効な Azure Sentinel ライセンスが必要です
* テナントのグローバル管理者またはセキュリティ管理者である必要があります。

### <a name="integrating-with-azure-sentinel"></a>Azure Sentinel との統合

1. Cloud App Security ポータルの **設定** の歯車で、 **[セキュリティ拡張機能]** をクリックします。

1. **[SIEM エージェント]** タブで、追加 ( **+** ) をクリックし、 **[Azure Sentinel]** を選択します。

    ![SIEM 統合の追加メニューを示すスクリーンショット](media/siem0.png)

1. ウィザードで、Azure Sentinel に転送するデータの種類を選択します。 次のように統合を構成できます。
    1. **アラート**: Azure Sentinel が有効になると、アラートが自動的に有効になります。 <!--Use the **Apply to** drop-down to filter which alerts are sent to Azure Sentinel.-->
    1. **探索ログ**: スライダーを使用して、それらを有効または無効にします。既定ではすべて選択されています。次に、 **[適用対象]** ドロップダウンを使用して、Azure Sentinel に送信される探索ログをフィルター処理します。

    ![[Azure Sentinel 統合の構成] の開始ページを示すスクリーンショット](media/siem-sentinel-configuration.png)

1. **[次へ]** をクリックし、Azure Sentinel に進んで統合を完了します。 Azure Sentinel の構成の詳細については、[こちら](/azure/sentinel/connect-cloud-app-security)を参照してください。

    ![[Azure Sentinel 統合の構成] の完了ページを示すスクリーンショット](media/siem-sentinel-configuration-complete.png)

> [!NOTE]
> 新しい探索ログは、Cloud App Security ポータルでの構成から 15 分以内に、Azure Sentinel への転送が開始されます。

## <a name="alerts-and-discovery-logs-in-azure-sentinel"></a>Azure Sentinel のアラートと探索ログ

統合が完了すると、Azure Sentinel で Cloud App Security のアラートと探索ログを表示できます。

Azure Sentinel では、 **[ログ]** の **[Security Insights]\(セキュリティ分析情報\)** の下に、Cloud App Security のデータの種類のログが次のように表示されます。

| データ型 | Table |
| --- | --- |
| 探索ログ | McasShadowItReporting |
| アラート | SecurityAlert |

次の表に、**McasShadowItReporting** スキーマの各フィールドの説明を示します。

| フィールド | Type | 説明 | 例 |
| --- | --- | --- | --- |
| TenantId | 文字列型 | ワークスペース ID | b459b4u5-912x-46d5-9cb1-p43069212nb4 |
| SourceSystem | 文字列型 | ソース システム – 静的な値 | Azure |
| TimeGenerated [UTC] | DateTime | 探索データの日付 | 2019-07-23T11:00:35.858Z |
| StreamName | 文字列型 | 特定のストリームの名前 | マーケティング部門 |
| TotalEvents | 整数型 | セッションあたりのイベントの合計数 | 122 |
| BlockedEvents | 整数型 | ブロックされたイベントの数 | 0 |
| UploadedBytes | 整数型 | アップロードされたデータの量 | 1,514,874 |
| TotalBytes | 整数型 | データの合計量 | 4,067,785 |
| DownloadedBytes | 整数型 | ダウンロードされたデータの量 | 2,552,911 |
| IpAddress | 文字列型 | ソース IP アドレス | 127.0.0.0 |
| UserName | 文字列型 | ユーザー名 | `Raegan@contoso.com` |
| EnrichedUserName | 文字列型 | Azure AD ユーザー名で強化されたユーザー名 | `Raegan@contoso.com` |
| AppName | 文字列型 | クラウド アプリの名前 | Microsoft OneDrive for Business |
| AppId | 整数型 | クラウド アプリ識別子 | 15600 |
| AppCategory | 文字列型 | クラウド アプリのカテゴリ | クラウド ストレージ |
| AppTags | 文字列配列 | アプリに対して定義されている組み込みタグとカスタム タグ | ["sanctioned"] |
| AppScore | 整数型 | 0 から 10 までのアプリのリスク スコア (10 が危険のないアプリのスコア) | 10 |
| Type | 文字列型 | ログの種類 – 静的な値 | McasShadowItReporting |

## <a name="use-power-bi-with-cloud-app-security-data-in-azure-sentinel"></a>Azure Sentinel で Cloud App Security データと共に Power BI を使用する

統合が完了したら、Azure Sentinel に格納されている Cloud App Security データを他のツールで使用することもできます。

このセクションでは、Microsoft Power BI (Power BI) を使用して簡単にデータの整形と結合を行い、組織のニーズを満たすレポートとダッシュボードを構築する方法について説明します。

次の手順に従って、すばやく作業を開始できます。

1. Power BI で、Azure Sentinel から Cloud App Security データ用のクエリをインポートします。 詳細については、「[Azure Monitor ログ データを Power BI にインポートする](/azure/azure-monitor/platform/powerbi)」をご覧ください。
1. [Cloud App Security Shadow IT Discovery アプリをインストール](https://aka.ms/MCASShadowITReporting)し、探索ログ データに[接続](#connect-the-cloud-app-security-app)して、組み込みの Shadow IT Discovery ダッシュボードを表示します。

    > [!NOTE]
    > 現時点では、このアプリは Microsoft AppSource 上で公開されていません。 そのため、アプリをインストールするためのアクセス許可について、ご自分の Power BI 管理者に連絡する必要がある場合があります。

    ![Shadow IT Discovery ダッシュボードを示すスクリーンショット](media/siem-sentinel-configuration-powerbi-dashboard.png)

1. 必要に応じて、Power BI Desktop でカスタム ダッシュボードを作成し、組織のビジュアル分析やレポートの要件に合わせて調整します。

### <a name="connect-the-cloud-app-security-app"></a>Cloud App Security アプリを接続する

1. Power BI で、 **[アプリ]** をクリックし、 **[Shadow IT Discovery]** アプリをクリックします。

1. **[新しいアプリを開始する]** ページで、 **[接続]** をクリックします。

    ![アプリ データの接続ページを示すスクリーンショット](media/siem-sentinel-powerbi-connect.png)

1. ワークスペース ID のページで、ログ分析の概要ページに表示される Azure Sentinel ワークスペース ID を入力し、 **[次へ]** をクリックします。

    ![ワークスペース ID の要求を示すスクリーンショット](media/siem-sentinel-powerbi-workspace-id.png)

1. 認証ページで、認証方法とプライバシー レベルを指定し、 **[サインイン]** をクリックします。

    ![認証ページを示すスクリーンショット](media/siem-sentinel-powerbi-authentication.png)

1. データを接続したら、ワークスペースの **[データセット]** タブにアクセスし、 **[最新の情報に更新]** をクリックします。 これにより、レポートが独自のデータで更新されます。

[!INCLUDE [Open support ticket](includes/support.md)]