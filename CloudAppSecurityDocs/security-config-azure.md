---
title: Azure のセキュリティ構成に関する推奨事項を取得する
description: この記事では、Azure Security Center と統合することによって Cloud App Security のセキュリティ構成に関する推奨事項を取得する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: f92d94c18ba8f91fd616fe00baeeb38b79a4354c
ms.sourcegitcommit: 97563af6076ccbad0d994ac69a85a998a625d06a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87296901"
---
# <a name="security-configuration-for-azure"></a>Azure のセキュリティ構成

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security では、お客様の Azure 環境のセキュリティ構成の評価を得ることができます。 この評価では、Azure Security Center を利用して、不足している構成とセキュリティ制御に関する推奨事項が提供されます。

## <a name="enable-security-configuration-recommendations"></a>セキュリティ構成に関する推奨事項を有効にする

この機能を使用するには、Azure AD と Azure portal での適切なアクセス許可が必要です。 既定では、Azure AD グローバル管理者のロールでは、Azure サブスクリプションにはアクセスできません。 自分や他のユーザーに対して Azure サブスクリプションへのアクセスを許可するには、ご自分のアクセス許可を昇格させます。

> [!IMPORTANT]
> 次のプロセスを完了した後は、この昇格を無効にすることをお勧めします。

## <a name="how-to-enable-azure-security-recommendations"></a>Azure のセキュリティに関する推奨事項を有効にする方法

Microsoft Cloud App Security でセキュリティ構成に関する推奨事項を有効にするには、次を実行します。

1. <a href="https://docs.microsoft.com/azure/security-center/security-center-management-groups" target="_blank">Azure Security Center に対するテナント全体の可視性を確保します</a>。 このプロセスには次のものが含まれます。

    - 自分自身と、このページへのアクセスを許可する他のすべての Microsoft Cloud App Security 管理者に対して、すべてのサブスクリプションの閲覧者のロールを付与する。
    - Azure Security Center のルート管理グループにロールを割り当てる
    - ご自分の Azure AD グローバル管理者を昇格させて、Azure サブスクリプションへのアクセスを許可する。
    - この記事では、セキュリティ管理者になるためのプロセスについて説明しています。 この統合を機能させるために必要な最小限のアクセス許可は、**閲覧者**です。

1. 変更を有効にするために、<a href="https://ms.portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/0" target="_blank">Azure Security Center</a> を必ず開いてください。

## <a name="how-to-view-azure-security-recommendations"></a>Azure のセキュリティに関する推奨事項を表示する方法

1. Cloud App Security で、 **[調査]**  >  **[セキュリティの構成]** の順に参照し、 **[Azure]** タブを選択します。

    > [!NOTE]
    > 変更が有効になるまでに最大 15 分かかる場合があります。

    ![セキュリティの構成メニュー](media/security-configuration-menu.png)

1. 推奨事項は、種類、リソース、サブスクリプションごとにフィルター処理できます。 また、[セキュリティの構成] アイコン ![ASC アイコン](media/asc-icon.png) をクリックして Azure Security Center で推奨事項を開いて詳細情報を確認し、推奨事項についてさらに詳しく調べることができます。

    > [!NOTE]
    > 調査をさらに簡単にするために、カスタム クエリを作成して、後で使用できるように保存することができます。 クエリの作成が完了したら、フィルターの右上隅にある **[名前を付けて保存]** ボタンをクリックします。  **[クエリの保存]** ポップアップで、クエリに名前を付けます。

    ![セキュリティの構成](media/security-configuration-azure.png)

セキュリティに関する推奨事項の実装方法の詳細については、[Azure Security Center でのセキュリティに関する推奨事項の管理](https://docs.microsoft.com/azure/security-center/security-center-recommendations)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
