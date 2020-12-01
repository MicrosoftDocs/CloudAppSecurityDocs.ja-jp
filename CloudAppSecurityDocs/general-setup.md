---
title: Cloud App Security で組織の設定をセットアップする
description: この記事では、Cloud App Security で組織に関する情報を提供する方法について説明します。
ms.date: 11/08/2020
ms.topic: how-to
ms.openlocfilehash: d070b45db464c5789446dc87c4216b1e4e3370c8
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314904"
---
# <a name="basic-setup-for-cloud-app-security"></a>Cloud App Security の基本的なセットアップ

[!INCLUDE [Banner for top of topics](includes/banner.md)]

次の手順では、Microsoft Cloud App Security ポータルをカスタマイズする手順について説明します。

## <a name="prerequisites"></a>[前提条件]

ポータルにアクセスするには、次の IP アドレスをファイアウォールの許可一覧に追加して、Cloud App Security ポータルにアクセスできるようにする必要があります。

* 104.42.231.28

US Government GCC High のお客様の場合は、次の IP アドレスもファイアウォールの許可一覧に追加して、Cloud App Security GCC High ポータルにアクセスできるようにする必要があります。

* 52.227.143.223
* 13.72.19.4

> [!NOTE]
> URL および IP アドレスが変更されときに更新されるようにするには、次の記事で説明されているように RSS をサブスクライブします: 「[Office 365 の URL と IP アドレスの範囲](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」。

## <a name="set-up-the-portal"></a>ポータルを設定する

1. Cloud App Security ポータルのメニュー バーで、設定歯車 ![設定アイコン](media/settings-icon.png "設定アイコン") をクリックし、 **[設定]** を選択して、組織の詳細を構成します。

1. **[組織の詳細]** では、組織に対する **[組織の表示名]** を指定することが重要です。 それは、システムから送信されるメールや Web ページに表示されます。

1. **[環境名]** (テナント) を指定します。 この情報は、複数のテナントを管理する場合に特に重要です。

1. また、システムから送信されるメール通知や Web ページに表示される **[ロゴ]** を指定することもできます。 ロゴは、背景が透明で最大サイズが 150 x 50 ピクセルの png ファイルにする必要があります。

1. 内部ユーザーを識別するため、 **[マネージド ドメイン]** のリストを追加したことを確認します。 マネージド ドメインの追加は、非常に重要なステップです。 Cloud App Security では、マネージド ドメインを使用して、内部ユーザーと外部ユーザー、およびファイルを共有する必要がある場所と共有してはならない場所が決定されます。 この情報は、レポートとアラートに使用されます。

    * 内部として構成されていないドメイン内のユーザーは、外部としてマークされます。 外部ユーザーは、アクティビティまたはファイルのスキャンの対象になりません。

1. **[自動サインアウト]** で、セッションが自動的にサインアウトされずに非アクティブ状態を維持できる時間を指定します。

1. Azure Information Protection 統合と統合する場合は、「[Azure Information Protection の統合](azip-integration.md)」を参照してください。

    * Azure Information Protection の統合を進めるには、[Office 365 のアプリ コネクタ](connect-office-365-to-microsoft-cloud-app-security.md)を有効にする必要があります。

1. Microsoft Defender for Identity 統合と統合する場合は、「[Microsoft Defender for Identity の統合](azip-integration.md)」を参照してください。

1. ポータルの設定をバックアップしたい場合は、この画面で行うことができます。 **[ポータル設定のエクスポート]** をクリックして、ポリシー ルール、ユーザー グループ、IP アドレス範囲など、すべてのポータル設定の JSON ファイルを作成します。

> [!NOTE]
> ExpressRoute を使用している場合、Cloud App Security は Azure にデプロイされて、[ExpressRoute](/azure/expressroute/expressroute-introduction) に完全に統合されます。 検出ログのアップロードを含む、Cloud App Security アプリとのすべての通信、および Cloud App Security に送信されるトラフィックは、ExpressRoute の **パブリック ピアリング** 経由でルーティングされるため、待機時間、パフォーマンス、およびセキュリティが改善されます。 お客様側で設定を行う必要はありません。
>
> パブリック ピアリングの詳細については、「[ExpressRoute 回線とルーティング ドメイン](/azure/expressroute/expressroute-circuit-peerings)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery を設定する](set-up-cloud-discovery.md)

[!INCLUDE [Open support ticket](includes/support.md)]