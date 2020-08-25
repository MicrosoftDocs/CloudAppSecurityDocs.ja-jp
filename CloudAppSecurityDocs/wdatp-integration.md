---
title: Microsoft Defender ATP と Cloud App Security を統合する
description: この記事では、Microsoft Defender Advanced Threat Protection と Cloud App Security を統合して、シャドウ IT とリスク管理の可視性を向上させる方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 0ea29fe115c4235f926ae2d64e3a377bc02949f0
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88780054"
---
# <a name="microsoft-defender-advanced-threat-protection-integration-with-microsoft-cloud-app-security"></a>Microsoft Defender Advanced Threat Protection と Microsoft Cloud App Security の統合

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security は、Microsoft Defender Advanced Threat Protection (ATP) とネイティブに統合されます。 統合により、Cloud Discovery のロールアウトが簡単になり、Cloud Discovery の機能が企業ネットワークを超えて拡張され、コンピューター ベースの調査が可能になります。 [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection) は、インテリジェントな保護、検出、調査、対応のためのセキュリティ プラットフォームです。 Microsoft Defender ATP を使うと、エンドポイントがサイバー脅威から保護され、高度な攻撃とデータ侵害が検出され、セキュリティ インシデントが自動化されて、セキュリティ体制が強化されます。

Cloud App Security では、IT によって管理される Windows 10 コンピューターからアクセスされているクラウド アプリとサービスについての、Microsoft Defender ATP によって収集されたトラフィック情報が使用されます。 ネイティブ統合により、パブリック Wi-Fi を使用して、ローミング中に、およびリモート アクセス経由で、企業ネットワーク内の任意のコンピューターで Cloud Discovery を実行できます。 また、コンピューター ベースの調査も有効になります。

統合では、追加のデプロイは不要であり、すぐに使用できます。 エンドポイントからトラフィックをルーティングまたはミラー化したり、複雑な統合手順を実行したりする必要はありません。 エンドポイントから Cloud App Security に送信されるログでは、トラフィック アクティビティに関するユーザー情報が提供されます。 Microsoft Defender ATP のネットワーク アクティビティでは、デバイス コンテキストが提供されます。 デバイス コンテキストとユーザー名を組み合わせることで、ネットワークの全体像が得られ、どのユーザーがどのコンピューターからどの操作を行ったかを特定できます。

さらに、危険なユーザーが特定されたら、ユーザーがアクセスしたすべてのコンピューターを調べて、潜在的なリスクを検出することができます。 危険なコンピューターがわかったら、それを使用したすべてのユーザーを調べて、潜在的なリスクをさらに検出します。

トラフィック情報が収集されると、組織での[クラウド アプリの使用を詳細に調べる](discovered-apps.md#deep-dive-into-discovered-apps)ことができるようになります。 Cloud App Security では、Microsoft Defender ATP のネットワーク保護機能を利用して、エンドポイント デバイスからクラウド アプリへのアクセスがブロックされます。 ポータルで[**承認されていない**とタグを付ける](governance-discovery.md#BKMK_SanctionApp)ことで、アプリをブロックすることができます。 承認されていない各アプリの包括的な使用状況とリスクの評価に基づき、Microsoft Defender ATP ポータルでアプリのドメインを使用して[ドメイン インジケーター](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/manage-indicators#create-indicators-for-ips-and-urlsdomains-preview)が作成されます。 エンドポイントのデバイスで実行されている Microsoft Defender ウイルス対策では、ドメイン インジケーターを使用して、これらのアプリへのアクセスがブロックされます。

> [!NOTE]
> Microsoft Defender ATP を体験したいですか。 [無料試用版にサインアップしてください](https://www.microsoft.com/WindowsForBusiness/windows-atp?ocid=docs-wdatp-assignaccess-abovefoldlink)。

## <a name="prerequisites"></a>[前提条件]

- Microsoft Cloud App Security のライセンス
- Microsoft Defender ATP のライセンス
- Windows 10 バージョン 1709 (OS ビルド 16299.1085 と KB4493441)、Windows 10 バージョン 1803 (OS ビルド 17134.704 と KB4493464)、Windows 10 バージョン 1809 (OS ビルド 17763.379 と KB4489899)、またはそれ以降のバージョンの Windows 10
- Microsoft Defender ウイルス対策
  - [リアルタイム保護が有効になっていること](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/configure-real-time-protection-windows-defender-antivirus)
  - [クラウドによる保護が有効になっていること](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/enable-cloud-protection-windows-defender-antivirus)
  - [ネットワーク保護が有効になっており、ブロック モードに構成されていること](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-network-protection)

## <a name="how-it-works"></a>しくみ

Cloud App Security 自体では、[ユーザーがアップロードしたログ](create-snapshot-cloud-discovery-reports.md)を使用して、または[自動ログ アップロードを構成する](discovery-docker.md)ことにより、エンドポイントからログが収集されます。 ネイティブ統合を使用すると、Windows で実行されてネットワーク トランザクションを監視する Microsoft Defender ATP のエージェントによって作成されたログを利用できるようになります。 この情報を使用して、ネットワーク上の Windows コンピューター全体でシャドウ IT を検出します。

他のプラットフォームで Cloud Discovery を実行できるようにするには、Cloud App Security の[ログ コレクター](discovery-docker.md)と、Windows 10 コンピューターを監視するための Microsoft Defender ATP 統合の両方を使用することをお勧めします。

Microsoft Defender ATP と Cloud App Security を使用する利点を示す、[こちらの動画をご覧ください](#related-videos)。

## <a name="how-to-integrate-microsoft-defender-atp-with-cloud-app-security"></a>Microsoft Defender ATP と Cloud App Security を統合する方法

Cloud App Security との Microsoft Defender ATP 統合を有効にするには:

1. Microsoft Defender ATP ポータルのナビゲーション ペインで、 **[Preferences setup]\(ユーザー設定のセットアップ\)** を選択します。
2. **[設定]** メニューの **[全般]** で **[高度な機能]** を選択します。
3. **[Microsoft Cloud App Security]** を **[オン]** に切り替えます。
4. **[Save preferences]\(ユーザー設定の保存\)** をクリックします。

>[!NOTE]
> 統合を有効にしてから、データが Cloud App Security に表示されるようになるまでに、最大で 2 時間かかります。
>

![WD ATP の設定](media/wdatp-settings.png)

## <a name="investigate-machines-in-cloud-app-security"></a>Cloud App Security でコンピューターを調査する

Microsoft Defender ATP と Cloud App Security を統合した後は、Cloud Discovery ダッシュボードで検出されたコンピューターのデータを調査できます。

1. Cloud App Security ポータルで、 **[Cloud Discovery]** をクリックし、 **[Cloud Discovery dashboard]\(Cloud Discovery ダッシュボード\)** をクリックします。
2. 上部のナビゲーション バーの **[継続的レポート]** で、 **[Win10 endpoint users]\(Win10 エンドポイント ユーザー\)** を選択します。
  ![WD ATP レポート](media/win10-dashboard-report.png)
3. 上部には、統合後に追加されて検出されたコンピューターの数が表示されます。
4. **[マシン]** タブをクリックします。
5. 一覧に表示されている各コンピューターにドリルダウンし、そのタブを使用して調査データを表示できます。 インシデントに関係していたコンピューター、ユーザー、IP アドレス、アプリ間の相関関係を見つけます。

    - **概要**
        - **マシンのリスク レベル**:コンピューターのプロファイルが組織内の他のコンピューターと比較してどの程度危険か示します。これは重大度 (高、中、低、情報) で示されます。 Cloud App Security では、高度な分析に基づき、Microsoft Defender ATP からのコンピューター プロファイルがコンピューターごとに使用されます。 あるコンピューターのベースラインに対して異常なアクティビティが評価され、マシンのリスク レベルが決定されます。 マシンのリスク レベルを使用し、先に調査するコンピューターを決定します。
        - **トランザクション**:選択した期間にコンピューターで発生したトランザクションの数に関する情報。
        - **合計トラフィック**:選択した期間のトラフィックの総量 (MB 単位) に関する情報。
        - アップロード: 選択した期間にコンピューターによってアップロードされたトラフィックの総量 (MB 単位) に関する情報。
        - **ダウンロード**:選択した期間にコンピューターによってダウンロードされたトラフィックの総量 (MB 単位) に関する情報。
    - **検出されたアプリ**  
  コンピューターによってアクセスされた、すべての検出されたアプリの一覧が表示されます。
    - **ユーザーの履歴**  
    コンピューターにサインインしたすべてのユーザーの一覧が表示されます。
    - **IP アドレスの履歴**  
    コンピューターに割り当てられたすべての IP アドレスの一覧が表示されます。
 ![コンピューターの概要](media/machines-overview.png)

他の Cloud Discovery ソースと同様に、Win10 エンドポイント ユーザー レポートからデータをエクスポートして、さらに調査を行うことができます。

> [!NOTE]
>
> - Microsoft Defender ATP により、データは最大 4 MB のチャンクで Cloud App Security に転送されます (最大 4,000 のエンドポイント トランザクション)
> - 1 時間以内に 4 MB の制限に達しない場合、Microsoft Defender ATP では、過去 1 時間に実行されたすべてのトランザクションが報告されます。
> - エンドポイント デバイスがフォワード プロキシの内側にある場合、トラフィック データは Microsoft Defender ATP に認識されないため、Cloud Discovery のレポートに含まれません。 詳細については、「[フォワード プロキシの内側にあるネットワーク接続の監視](https://techcommunity.microsoft.com/t5/Microsoft-Defender-ATP/MDATP-Monitoring-network-connection-behind-forward-proxy-Public/ba-p/758274)」を参照してください。

## <a name="block-access-to-unsanctioned-cloud-apps"></a>承認されていないクラウド アプリへのアクセスをブロックする

Cloud App Security では、組み込みの[**承認されていない**](governance-discovery.md#BKMK_SanctionApp)アプリ タグを使用して、クラウド アプリが使用禁止としてマークされます。これは、Cloud Discovery と Cloud の両方のアプリ カタログ ページで使用できます。 Microsoft Defender ATP との統合を有効にすることにより、Cloud App Security ポータルで 1 回クリックするだけで、承認されていないアプリへのアクセスをシームレスにブロックできます。

### <a name="how-it-works"></a>しくみ

Cloud App Security で**承認されていない**としてマークされたアプリは、通常数分以内に Microsoft Defender ATP に自動的に同期されます。 具体的には、これらの承認されていないアプリによって使用されているドメインはエンドポイント デバイスに反映され、ネットワーク保護の SLA 内で Microsoft Defender ウイルス対策によってブロックされます。

### <a name="how-to-enable-cloud-app-blocking-with-microsoft-defender-atp"></a>Microsoft Defender ATP でクラウド アプリのブロックを有効にする方法

クラウド アプリのアクセス制御を有効にするには、次の手順のようにします。

1. Cloud App Security の設定歯車で **[設定]** を選択し、 **[Cloud Discovery]** で **[Microsoft Defender ATP]** を選択して、 **[承認されていないアプリのブロック]** を選択します。

    ![Microsoft Defender ATP でブロックを有効にする方法を示すスクリーンショット](media/defender-atp-integration.png)

1. Microsoft Defender セキュリティ センターで、 **[設定]**  >  **[高度な機能]** に移動し、 **[Custom network indicators]\(カスタム ネットワーク インジケーター\)** を選択します。 ネットワーク インジケーターの詳細については、[IP および URL とドメインに対するインジケーターの作成](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/manage-indicators#create-indicators-for-ips-and-urlsdomains-preview)に関するページを参照してください。

    これにより、Microsoft Defender ウイルス対策ネットワーク保護機能を利用し、Cloud App Security を使用して定義済みの URL セットへのアクセスをブロックすることができます。そのためには、特定のアプリに[アプリ タグ](governance-discovery.md#BKMK_SanctionApp)を手動で割り当てるか、[アプリ検出ポリシー](cloud-discovery-policies.md#creating-an-app-discovery-policy)を自動的に使用します。

    ![Microsoft Defender ATP でカスタム ネットワーク インジケーターを有効にする方法を示すスクリーンショット](media/defender-atp-custom-network-indicators.png)

## <a name="investigate-unsanctioned-apps-in-microsoft-defender-security-center"></a>Microsoft Defender セキュリティ センターで承認されていないアプリを調査する

承認されていないアプリへのアクセスが試みられるたびに、Microsoft Defender セキュリティ センターでアラートがトリガーされ、セッション全体の詳細が示されます。 これを使用して、承認されていないアプリへのアクセスをさらに詳細に調査したり、エンドポイント デバイスの調査に使用する追加の関連情報を提供したりできます。

エンドポイント デバイスが正しく構成されていないため、または強制ポリシーがエンドポイントにまだ反映されていないために、承認されていないアプリへのアクセスがブロックされないことがあります。 そのような場合、Microsoft Defender ATP 管理者は、承認されていないアプリがブロックされなかったことを示すアラートを Microsoft Defender セキュリティ センターで受け取ります。

![Microsoft Defender ATP の承認されていないアプリのアラートを示すスクリーンショット](media/defender-atp-unsanctioned-app-alert.png)

> [!NOTE]
>
> - アプリ ドメインに対して**承認されていない**とアプリにタグを付けてから、エンドポイント デバイスに伝達されるまでに、最大で 2 時間かかります。
> - 既定では、Cloud App Security で**承認されていない**とマークされたアプリとドメインは、組織内のすべてのエンドポイント デバイスに対してブロックされます。
> - 現時点では、承認されていないアプリに対する完全な URL はサポートされていません。 そのため、完全な URL で構成されたアプリを承認されていないものにすると、それらは Microsoft Defender ATP に反映されず、ブロックされません。 たとえば、`google.com/drive` はサポートされませんが、`drive.google.com` はサポートされます。
> - ブラウザーでの通知は、ブラウザーによって異なる場合があります。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

## <a name="related-videos"></a>関連ビデオ

> [!div class="nextstepaction"]
> [Microsoft Defender ATP を使用してシャドウ IT を検出し、ブロックする](https://www.youtube.com/watch?v=MsHkTOoqSQo)

> [!div class="nextstepaction"]
> [企業ネットワークを超えたシャドウ IT の検出](https://www.youtube.com/watch?v=f8hbvbY1Hnc)

[!INCLUDE [Open support ticket](includes/support.md)]
