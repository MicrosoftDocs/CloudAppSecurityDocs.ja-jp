---
title: Microsoft Defender for Endpoint を Cloud App Security と統合する
description: この記事では、Microsoft Defender for Endpoint と Cloud App Security を統合して、シャドウ IT とリスク管理の可視性を向上させる方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 95e8271a26828ad4e3adb73727e2692cac3a8d23
ms.sourcegitcommit: 5367d8fdf99d61719a395728f2ef4b014604e3bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2020
ms.locfileid: "94371150"
---
# <a name="microsoft-defender-for-endpoint-integration-with-microsoft-cloud-app-security"></a>Microsoft Defender for Endpoint と Microsoft Cloud App Security の統合

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security は、Microsoft Defender for Endpoint とネイティブに統合されます。 統合により、Cloud Discovery のロールアウトが簡単になり、Cloud Discovery の機能が企業ネットワークを超えて拡張され、デバイス ベースの調査が可能になります。 [Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) は、インテリジェントな保護、検出、調査、対応を行うためのセキュリティ プラットフォームです。 Defender for Endpoint を使うと、エンドポイントがサイバー脅威から保護され、高度な攻撃とデータ侵害が検出され、セキュリティ インシデントが自動化されて、セキュリティ体制が強化されます。

Cloud App Security では、IT によって管理される Windows 10 デバイスからアクセスされているクラウド アプリとサービスについての、Defender for Endpoint によって収集されたトラフィック情報が使用されます。 ネイティブ統合により、パブリック Wi-Fi を使用して、ローミング中に、およびリモート アクセス経由で、企業ネットワーク内の任意のデバイスで Cloud Discovery を実行できます。 また、デバイス ベースの調査も可能になります。

統合では、追加のデプロイは不要であり、すぐに使用できます。 エンドポイントからトラフィックをルーティングまたはミラー化したり、複雑な統合手順を実行したりする必要はありません。 エンドポイントから Cloud App Security に送信されるログでは、トラフィック アクティビティに関するユーザー情報が提供されます。 Defender for Endpoint のネットワーク アクティビティによって、デバイス コンテキストが提供されます。 デバイス コンテキストとユーザー名を組み合わせることで、ネットワークの全体像が得られ、どのユーザーがどのデバイスからどの操作を行ったかを特定できます。

さらに、危険なユーザーが特定されたら、そのユーザーがアクセスしたすべてのデバイスを調べて、潜在的なリスクを検出することができます。 危険なデバイスがわかったら、それを使用したすべてのユーザーを調べて、さらなる潜在的なリスクを検出します。

トラフィック情報が収集されると、組織での[クラウド アプリの使用を詳細に調べる](discovered-apps.md#deep-dive-into-discovered-apps)ことができるようになります。 Cloud App Security によって Defender for Endpoint のネットワーク保護機能が利用され、エンドポイント デバイスからクラウド アプリへのアクセスがブロックされます。 ポータルで [**承認されていない** とタグを付ける](governance-discovery.md#BKMK_SanctionApp)ことで、アプリをブロックすることができます。 承認されていない各アプリの包括的な使用状況とリスクの評価に基づき、Defender for Endpoint ポータルでアプリのドメインを使用して[ドメイン インジケーター](/windows/security/threat-protection/microsoft-defender-atp/manage-indicators#create-indicators-for-ips-and-urlsdomains-preview)が作成されます。 エンドポイントのデバイスで実行されている Microsoft Defender ウイルス対策では、ドメイン インジケーターを使用して、これらのアプリへのアクセスがブロックされます。

> [!NOTE]
> Microsoft Defender for Endpoint を体験したいですか。 [無料試用版にサインアップしてください](https://www.microsoft.com/WindowsForBusiness/windows-atp?ocid=docs-wdatp-assignaccess-abovefoldlink)。

## <a name="prerequisites"></a>[前提条件]

- Microsoft Cloud App Security のライセンス
- Microsoft Defender for Endpoint のライセンス
- Windows 10 バージョン 1709 (OS ビルド 16299.1085 と KB4493441)、Windows 10 バージョン 1803 (OS ビルド 17134.704 と KB4493464)、Windows 10 バージョン 1809 (OS ビルド 17763.379 と KB4489899)、またはそれ以降のバージョンの Windows 10
- Microsoft Defender ウイルス対策
  - [リアルタイム保護が有効になっていること](/windows/security/threat-protection/windows-defender-antivirus/configure-real-time-protection-windows-defender-antivirus)
  - [クラウドによる保護が有効になっていること](/windows/security/threat-protection/windows-defender-antivirus/enable-cloud-protection-windows-defender-antivirus)
  - [ネットワーク保護が有効になっており、ブロック モードに構成されていること](/windows/security/threat-protection/microsoft-defender-atp/enable-network-protection)

## <a name="how-it-works"></a>しくみ

Cloud App Security 自体では、[ユーザーがアップロードしたログ](create-snapshot-cloud-discovery-reports.md)を使用して、または[自動ログ アップロードを構成する](discovery-docker.md)ことにより、エンドポイントからログが収集されます。 ネイティブ統合を使用すると、Windows で実行されてネットワーク トランザクションを監視する Defender for Endpoint のエージェントによって作成されたログを利用できるようになります。 この情報を使用して、ネットワーク上の Windows デバイス全体でシャドウ IT を検出します。

他のプラットフォームで Cloud Discovery を実行できるようにするには、Cloud App Security の[ログ コレクター](discovery-docker.md)と、Windows 10 デバイスを監視するための Defender for Endpoint 統合の両方を使用することをお勧めします。

Defender for Endpoint と Cloud App Security を使用する利点を示す、[こちらの動画をご覧ください](#related-videos)。

## <a name="how-to-integrate-microsoft-defender-for-endpoint-with-cloud-app-security"></a>Microsoft Defender for Endpoint を Cloud App Security と統合する方法

Defender for Endpoint と Cloud App Security の統合を有効にするには:

1. Microsoft Defender セキュリティ センターのナビゲーション ウィンドウで、 **[設定]** を選択します。
2. **[全般]** で、 **[高度な機能]** を選択します。
3. **[Microsoft Cloud App Security]** を **[オン]** に切り替えます。
4. **[Apply]** をクリックします。

>[!NOTE]
> 統合を有効にしてから、データが Cloud App Security に表示されるようになるまでに、最大で 2 時間かかります。
>

![Defender for Endpoint の設定](media/mde-settings.png)

Microsoft Defender for Endpoint に送信されるアラートの重要度を構成するには:

1. Cloud App Security で、 **[設定]** アイコンをクリックし、 **[Microsoft Defender for Endpoint]** を選択します。
1. **[アラート]** で、アラートのグローバル重要度レベルを選択します。
1. **[保存]** をクリックします。

![Defender for Endpoint のアラート設定](media/mde-alert-severity-settings.png)

## <a name="investigate-devices-in-cloud-app-security"></a>Cloud App Security でデバイスを調査する

Defender for Endpoint を Cloud App Security と統合した後は、Cloud Discovery ダッシュボードで検出されたデバイスのデータを調査できます。

1. Cloud App Security で、 **[Cloud Discovery]** 、 **[Cloud Discovery dashboard]\(Cloud Discovery ダッシュボード\)** の順にクリックします。
2. 上部のナビゲーション バーの **[継続的レポート]** で、 **[Win10 endpoint users]\(Win10 エンドポイント ユーザー\)** を選択します。
  ![Defender for Endpoint のレポート](media/win10-dashboard-report.png)
3. 上部には、統合後に追加されて検出されたデバイスの数が表示されます。
4. [ **デバイス** ] タブをクリックします。
5. 一覧に表示されている各デバイスにドリルダウンし、そのタブを使用して調査データを表示できます。 インシデントに関係していたデバイス、ユーザー、IP アドレス、アプリ間の相関関係を見つけます。

    - **概要**
        - **デバイス リスク レベル** :デバイスのプロファイルが組織内の他のデバイスと比較してどの程度危険か示します。これは重要度 (高、中、低、情報) によって示されます。 Cloud App Security では、高度な分析に基づき、Defender for Endpoint からのデバイス プロファイルがデバイスごとに使用されます。 あるデバイスのベースラインに対して異常なアクティビティが評価され、そのデバイスのリスク レベルが決定されます。 デバイス リスク レベルを使用して、最初に調査するデバイスを決定します。
        - **トランザクション** :選択した期間にデバイスで発生したトランザクションの数に関する情報。
        - **合計トラフィック** :選択した期間のトラフィックの総量 (MB 単位) に関する情報。
        - アップロード: 選択した期間にデバイスによってアップロードされたトラフィックの総量 (MB 単位) に関する情報。
        - **ダウンロード** :選択した期間にデバイスによってダウンロードされたトラフィックの総量 (MB 単位) に関する情報。
    - **検出されたアプリ**  
    デバイスによってアクセスされた、すべての検出されたアプリの一覧が表示されます。
    - **ユーザーの履歴**  
    デバイスにサインインしたすべてのユーザーの一覧が表示されます。
    - **IP アドレスの履歴**  
    デバイスに割り当てられたすべての IP アドレスの一覧が表示されます。
 ![デバイスの概要](media/devices-overview.png)

他の Cloud Discovery ソースと同様に、Win10 エンドポイント ユーザー レポートからデータをエクスポートして、さらに調査を行うことができます。

> [!NOTE]
>
> - Defender for Endpoint により、データは最大 4 MB のチャンクで Cloud App Security に転送されます (最大 4,000 のエンドポイント トランザクション)
> - 1 時間以内に 4 MB の制限に達しない場合、Defender for Endpoint によって、過去 1 時間に実行されたすべてのトランザクションが報告されます。
> - エンドポイント デバイスが転送プロキシの内側にある場合、トラフィック データは Defender for Endpoint に認識されないため、Cloud Discovery のレポートに含まれません。 完全に把握するために、 **自動ログ アップロード** を使用して、転送プロキシのログを Cloud App Security にルーティングすることをお勧めします。 このトラフィックを表示し、転送プロキシの内側にあるデバイスによってアクセスされた URL を調査する別の方法については、[転送プロキシの内側にあるネットワーク接続の監視](https://techcommunity.microsoft.com/t5/Microsoft-Defender-ATP/MDATP-Monitoring-network-connection-behind-forward-proxy-Public/ba-p/758274)に関するページをご覧ください。

## <a name="investigate-device-network-events-in-defender-for-endpoint"></a>Defender for Endpoint でデバイス ネットワーク イベントを調査する

Microsoft Defender for Endpoint でデバイスのネットワーク アクティビティをより詳細に表示するには、次の手順を使用します。

1. Cloud App Security の **[検出]** で **[デバイス]** を選択します。
1. 調査するコンピューターを選択し、右上にある **[View in Microsoft Defender for Endpoint]\(Microsoft Defender for Endpoint で表示する\)** をクリックします。
1. Microsoft Defender セキュリティ センターの **[デバイス]** > {選択されたデバイス} の下で、 **[タイムライン]** を選択します。
1. **[フィルター]** で **[ネットワーク イベント]** を選択します。
1. 必要に応じて、デバイスのネットワーク イベントを調査します。

![Microsoft Defender セキュリティ センターのデバイス タイムラインを示すスクリーンショット](media/mde-selected-device.png)

## <a name="investigate-app-usage-in-defender-for-endpoint-with-advanced-hunting"></a>高度なハンティングを使用して Defender for Endpoint でアプリの使用状況を調査する

Defender for Endpoint でアプリ関連のネットワーク イベントをより詳細に表示するには、次の手順を使用します。

1. Cloud App Security の **[検出]** で、 **[検出]** を選択します。
1. 調査するアプリをクリックして、そのドロアーを開きます。
1. アプリの **[ドメイン]** リストをクリックし、ドメインのリストをコピーします。
1. Microsoft Defender セキュリティ センターの **[デバイス]** で、 **[高度な捜索]** を選択します。
1. 次のクエリを貼り付けて、`<DOMAIN_LIST>` を前にコピーしたドメインのリストに置き換えます。

    ```kusto
    DeviceNetworkEvents
    | where RemoteUrl in ("<DOMAIN_LIST>")
    | order by Timestamp desc
    ```

1. クエリを実行し、このアプリのネットワーク イベントを調査します。

![Microsoft Defender セキュリティ センターの [高度な捜索] を示すスクリーンショット](media/mde-advanced-hunting.png)

## <a name="block-access-to-unsanctioned-cloud-apps"></a>承認されていないクラウド アプリへのアクセスをブロックする

Cloud App Security では、組み込みの [**承認されていない**](governance-discovery.md#BKMK_SanctionApp)アプリ タグを使用して、クラウド アプリが使用禁止としてマークされます。これは、Cloud Discovery と Cloud の両方のアプリ カタログ ページで使用できます。 Defender for Endpoint との統合を有効にすることにより、Cloud App Security ポータルで 1 回クリックするだけで、承認されていないアプリへのアクセスをシームレスにブロックできます。

### <a name="how-blocking-works"></a>ブロックのしくみ

Cloud App Security で **承認されていない** としてマークされたアプリは、通常数分以内に Defender for Endpoint に自動的に同期されます。 具体的には、これらの承認されていないアプリによって使用されているドメインはエンドポイント デバイスに反映され、ネットワーク保護の SLA 内で Microsoft Defender ウイルス対策によってブロックされます。

### <a name="how-to-enable-cloud-app-blocking-with-defender-for-endpoint"></a>Defender for Endpoint でクラウド アプリのブロックを有効にする方法

クラウド アプリのアクセス制御を有効にするには、次の手順のようにします。

1. Cloud App Security の設定歯車で **[設定]** を選択し、 **[Cloud Discovery]** で **[Microsoft Defender for Endpoint]** を選択して、 **[承認されていないアプリのブロック]** を選択します。

    ![Defender for Endpoint でブロックを有効にする方法を示すスクリーンショット](media/mde-integration.png)

1. Microsoft Defender セキュリティ センターで、 **[設定]**  >  **[高度な機能]** に移動し、 **[Custom network indicators]\(カスタム ネットワーク インジケーター\)** を選択します。 ネットワーク インジケーターの詳細については、[IP および URL とドメインに対するインジケーターの作成](/windows/security/threat-protection/microsoft-defender-atp/manage-indicators#create-indicators-for-ips-and-urlsdomains-preview)に関するページを参照してください。

    これにより、Microsoft Defender ウイルス対策ネットワーク保護機能を利用し、Cloud App Security を使用して定義済みの URL セットへのアクセスをブロックすることができます。そのためには、特定のアプリに[アプリ タグ](governance-discovery.md#BKMK_SanctionApp)を手動で割り当てるか、[アプリ検出ポリシー](cloud-discovery-policies.md#creating-an-app-discovery-policy)を自動的に使用します。

    ![Defender for Endpoint でカスタム ネットワーク インジケーターを有効にする方法を示すスクリーンショット](media/mde-custom-network-indicators.png)

## <a name="investigate-unsanctioned-apps-in-microsoft-defender-security-center"></a>Microsoft Defender セキュリティ センターで承認されていないアプリを調査する

承認されていないアプリへのアクセスが試みられるたびに、Microsoft Defender セキュリティ センターでアラートがトリガーされ、セッション全体の詳細が示されます。 これを使用して、承認されていないアプリへのアクセスをさらに詳細に調査したり、エンドポイント デバイスの調査に使用する追加の関連情報を提供したりできます。

エンドポイント デバイスが正しく構成されていないため、または強制ポリシーがエンドポイントにまだ反映されていないために、承認されていないアプリへのアクセスがブロックされないことがあります。 そのような場合、Defender for Endpoint 管理者は、承認されていないアプリがブロックされなかったことを示すアラートを Microsoft Defender セキュリティ センターで受け取ります。

![Defender for Endpoint の承認されていないアプリのアラートを示すスクリーンショット](media/mde-unsanctioned-app-alert.png)

> [!NOTE]
>
> - アプリ ドメインに対して **承認されていない** とアプリにタグを付けてから、エンドポイント デバイスに伝達されるまでに、最大で 2 時間かかります。
> - 既定では、Cloud App Security で **承認されていない** とマークされたアプリとドメインは、組織内のすべてのエンドポイント デバイスに対してブロックされます。
> - 現時点では、承認されていないアプリに対する完全な URL はサポートされていません。 そのため、完全な URL で構成されたアプリを承認されていないものにすると、それらは Defender for Endpoint に反映されず、ブロックされません。 たとえば、`google.com/drive` はサポートされませんが、`drive.google.com` はサポートされます。
> - ブラウザーでの通知は、ブラウザーによって異なる場合があります。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

## <a name="related-videos"></a>関連ビデオ

> [!div class="nextstepaction"]
> [Defender for Endpoint を使用してシャドウ IT を検出し、ブロックする](https://www.youtube.com/watch?v=MsHkTOoqSQo)

> [!div class="nextstepaction"]
> [企業ネットワークを超えたシャドウ IT の検出](https://www.youtube.com/watch?v=f8hbvbY1Hnc)

[!INCLUDE [Open support ticket](includes/support.md)]
