---
title: Cloud App Security を Menlo Security と統合する
description: この記事では、Microsoft Cloud App Security を Menlo Security と統合し、シームレスな Cloud Discovery と、承認されていないアプリの自動ブロックを実現する方法について説明します。
ms.date: 11/09/2020
ms.topic: how-to
ms.openlocfilehash: 675a45375ef1e4a09c9a1369698512d9eac1f92f
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96311147"
---
# <a name="integrate-cloud-app-security-with-menlo-security"></a>Cloud App Security を Menlo Security と統合する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud App Security と Menlo Security の両方を使用している場合は、この 2 つの製品を統合して、お使いの Cloud Discovery のセキュリティを強化することができます。 スタンドアロンの Secure Web Gateway として Menlo Security を使用すると、組織のトラフィックを監視し、トランザクションをブロックするポリシーを設定できます。 Cloud App Security と Menlo Security を共に使用すると、次の機能が提供されます。

- Cloud Discovery をシームレスにデプロイすることができます。Menlo Security を使用してご自分のトラフィックをプロキシし、それを Cloud App Security に送信できます。 これにより、Cloud Discovery を有効にするために、ネットワーク エンドポイントにログ コレクターをインストールする必要がなくなります。
- Menlo Security のブロック機能は、Cloud App Security で未承認として設定したアプリに自動的に適用されます。

## <a name="prerequisites"></a>[前提条件]

- Microsoft Cloud App Security の有効なライセンス、または Azure Active Directory Premium P1 の有効なライセンス
- Menlo Security の有効なライセンス

## <a name="deployment"></a>配置

1. Menlo Admin ポータルにログインし、「[Menlo Security Integration with Microsoft Cloud Access Security Setup Guide](https://admin.menlosecurity.com/docs/guides/web_admin_settings_casb.html?highlight=microsoft)」(Menlo Security と Microsoft Cloud Access Security の統合のセットアップ ガイド) を使用して、製品を統合します。

1. ネットワークで検出されたクラウド アプリを調査します。 詳細および調査手順については、[Cloud Discovery の操作](working-with-cloud-discovery-data.md)に関するページを参照してください。
1. Menlo Security により、Cloud App Security で設定した承認されていないすべてのアプリが、2 時間ごとに ping されて、自動的にブロックされます。 承認されないアプリの詳細については、「[アプリの承認/却下](governance-discovery.md#BKMK_SanctionApp)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
