---
title: Azure AD のユーザー名を使用して Cloud App Security Discovery のデータを強化する
description: この記事では、Azure AD のユーザー名を使用して Cloud App Security Discovery のデータを強化する方法について説明します。
ms.date: 12/10/2018
ms.topic: how-to
ms.openlocfilehash: bcedf73defb825bf3188592f719814755de89a25
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96313476"
---
# <a name="cloud-discovery-enrichment"></a>Cloud Discovery の強化

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud Discovery のデータを、Azure Active Directory のユーザー名データを使用して強化できるようになりました。 この機能を有効にすると、検出トラフィック ログで受け取ったユーザー名が Azure AD のユーザー名と照合され、置き換えられます。 Cloud Discovery の強化により、次の機能が有効になります。

- Azure Active Directory のユーザーによるシャドウ IT の使用を調査できます。
- 検出されたクラウド アプリの使用と API で収集されたアクティビティを関連付けることができます。
- Azure AD ユーザー グループに基づくカスタム ログを作成できるようになります。 たとえば、特定のマーケティング部門のシャドウ IT レポートなどです。

## <a name="prerequisites"></a>[前提条件]

- ユーザー名情報がデータ ソースから提供されること
- [Office 365 アプリ コネクタ](connect-office-365-to-microsoft-cloud-app-security.md)に接続されていること

## <a name="enabling-user-data-enrichment"></a>ユーザー データの強化を有効にする

1. 「設定」 (歯車アイコン) の **[Cloud Discovery 設定]** を選択します。

2. **[ユーザー エンリッチメント]** タブで、 **[検出されたユーザー識別子を Azure Active Directory ユーザー名で強化します。]** を選択します。 このオプションを使用すると、既定により、Cloud App Security で Azure Active Directory のデータを使用してユーザー名を強化できます。

3. **[Save]** (保存) をクリックします。

![Azure AD のユーザー名を使用して Cloud App Security Discovery を強化する](media/discovery-enrichment.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
