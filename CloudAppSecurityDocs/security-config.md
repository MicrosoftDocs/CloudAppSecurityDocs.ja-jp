---
title: パブリック クラウド プラットフォームのセキュリティ構成に関する推奨事項を取得する
description: この記事では、組織のパブリック クラウド プラットフォーム用に、Cloud App Security のセキュリティ構成に関する推奨事項を取得する方法について説明します。
ms.date: 06/28/2020
ms.topic: how-to
ms.openlocfilehash: 95147a89a331da7acda75f595cee1c30bb67e5f7
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96315444"
---
# <a name="security-configuration-overview"></a>セキュリティ構成の概要

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security では、Azure、Amazon Web Services (AWS)、Google Cloud Platform (GCP) のセキュリティ構成の評価を得ることができます。 推奨事項の対象となるのは、あらゆる Azure サブスクリプション、メンバー アカウントを含む AWS アカウント、組織に接続されているあらゆる GCP プロジェクトです。 複数のクラウドを対象にクラウド プラットフォーム セキュリティ構成のあらゆる推奨事項をこのように表示できることで、セキュリティ管理者は、Cloud App Security におけるセキュリティ構成のギャップをすべて調査できます。

さまざまな種類の評価に関する詳細は、次のリンクから入手できます。

- **[Azure 推奨事項](security-config-azure.md)** :Azure Security Center から表示される Azure ベスト プラクティス セキュリティ推奨事項。
- **[AWS 推奨事項](security-config-aws.md)** :AWS 向け Center for Internet Security (CIS) ベンチマーク、バージョン 1.2.0 に基づくセキュリティ推奨事項。AWS Security Hub から表示。
- **[GCP 推奨事項](security-config-gcp.md)** :GCP 向け CIS ベンチマーク、バージョン 1.1.0 に基づくセキュリティ推奨事項。Google Security Command Center と Security Health Analytics から表示。

## <a name="security-recommendations-report"></a>セキュリティに関する推奨事項のレポート

Cloud App Security を使用すると、クラウド環境の監視、理解、カスタマイズを行い、組織の保護を強化するために役立つ、セキュリティに関する推奨事項の詳細な一覧をエクスポートできます。

セキュリティに関する推奨事項の一覧をエクスポートするには、次の手順を実行します。

1. Cloud App Security で、 **[調査]**  >  **[セキュリティの構成]** を参照します。

1. 関連するクラウドのセキュリティの推奨事項タブを選択します。
1. 推奨事項テーブルの右上にある **[エクスポート]** をクリックします。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
