---
title: Azure のセキュリティ構成に関する推奨事項を取得する
description: この記事では、Azure Security Center と統合することによって Cloud App Security のセキュリティ構成に関する推奨事項を取得する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 6f1b55e3675b9419ca1e53ddeea9189e260b8022
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880195"
---
# <a name="security-configuration-for-azure"></a>Azure のセキュリティ構成

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security では、お客様の Azure 環境のセキュリティ構成の評価を得ることができます。 この評価では、Azure Security Center を利用して、不足している構成とセキュリティ制御に関する推奨事項が提供されます。

## <a name="prerequisites"></a>前提条件

組織は、Azure のセキュリティ構成を評価する対象となるすべてのサブスクリプションに対して Azure Security Center ライセンスを持っている必要があります。

## <a name="how-to-enable-azure-security-recommendations"></a>Azure のセキュリティに関する推奨事項を有効にする方法

Cloud App Security でセキュリティ構成に関する推奨事項を有効にするには、<a href="https://ms.portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/0" target="_blank">ポータル</a>に移動して、Azure Security Center サブスクリプションをアクティブ化します。

## <a name="how-to-view-azure-security-recommendations"></a>Azure のセキュリティに関する推奨事項を表示する方法

1. Cloud App Security で、 **[調査]**  >  **[セキュリティの構成]** の順に参照し、 **[Azure]** タブを選択します。

    > [!NOTE]
    > 変更が有効になるまでに最大 15 分かかる場合があります。

    ![セキュリティの構成メニュー](media/security-configuration-menu.png)

1. 推奨事項は、種類、リソース、サブスクリプションごとにフィルター処理できます。 また、[セキュリティの構成] アイコン ![ASC アイコン](media/asc-icon.png) をクリックして Azure Security Center で推奨事項を開いて詳細情報を確認し、推奨事項についてさらに詳しく調べることができます。

    > [!NOTE]
    > 調査をさらに簡単にするために、カスタム クエリを作成して、後で使用できるように保存することができます。 クエリの作成が完了したら、フィルターの右上隅にある **[名前を付けて保存]** ボタンをクリックします。  **[クエリの保存]** ポップアップで、クエリに名前を付けます。

    ![セキュリティの構成](media/security-configuration-azure.png)

セキュリティに関する推奨事項の実装方法の詳細については、[Azure Security Center でのセキュリティに関する推奨事項の管理](/azure/security-center/security-center-recommendations)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]