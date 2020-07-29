---
title: Cloud App Security を Zscaler と統合する
description: この記事では、Microsoft Cloud App Security を Zscaler と統合し、シームレスな Cloud Discovery と、承認されていないアプリの自動ブロックを実現する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 0e7f32bd4f6213b4bce86232e40d15cf06e12c18
ms.sourcegitcommit: c737a1ad67b4f7efa302d1aa92fce50f75c94d2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86926725"
---
# <a name="integrate-cloud-app-security-with-zscaler"></a>Cloud App Security を Zscaler と統合する

*適用対象:Microsoft Cloud App Security*

Cloud App Security と Zscaler の両方を使用している場合は、この 2 つの製品を統合して、Cloud Discovery のセキュリティを強化できます。 スタンドアロン クラウド プロキシとして Zscaler を使用すると、組織のトラフィックを監視し、トランザクションをブロックするポリシーを設定できます。 Cloud App Security と Zscaler を共に使用すると、次の機能が提供されます。

- Cloud Discovery をシームレスにデプロイできます。Zscaler を使用してトラフィックをプロキシし、それを Cloud App Security に送信できます。 これにより、Cloud Discovery を有効にするために、ネットワーク エンドポイントにログ コレクターをインストールする必要がなくなります。
- Zscaler のブロック機能は、Cloud App Security で未承認として設定したアプリに自動的に適用されます。
- 主要な 200 個のクラウド アプリに対する Cloud App Security のリスク評価により、Zscaler ポータルが強化されます。Zscaler ポータルでそれを直接表示できます。

## <a name="prerequisites"></a>[前提条件]

- Microsoft Cloud App Security の有効なライセンス、または Azure Active Directory Premium P1 の有効なライセンス
- Zscaler Cloud 5.6 の有効なライセンス
- Zscaler NSS のアクティブなサブスクリプション

## <a name="deployment"></a>展開

1. Zscaler ポータルで、[Microsoft Cloud App Security との Zscaler パートナー統合](https://help.zscaler.com/zia/configuring-mcas-integration)の手順を完了します。
2. Cloud App Security ポータルで、次の統合手順を行います。
    1. 設定の歯車アイコンをクリックし、 **[Cloud Discovery 設定]** を選択します。
    2. **[自動ログ アップロード]** タブをクリックし、 **[データ ソースの追加]** をクリックします。
    3. **[データ ソースの追加]** ページで、次の設定を入力します。

        - 名前 = NSS
        - ソース = Zscaler QRadar LEEF
        - レシーバーの種類 = Syslog - UDP

        ![データ ソース Zscaler](media/data-source-zscaler.png)

        > [!NOTE]
        > データ ソースの名前が **NSS** であることを確認します。 NSS フィードの設定について詳しくは、[Cloud App Security NSS フィードの追加](https://help.zscaler.com/zia/adding-mcas-nss-feeds)に関するページをご覧ください。

    4. **[期待されるログ ファイルのサンプルを表示]** をクリックします。 次いで、 **[サンプル ログのダウンロード]** をクリックしてサンプルの検出ログを表示し、それがお使いのログと一致していることを確認します。<br />

3. ネットワークで検出されたクラウド アプリを調査します。 詳細および調査手順については、[Cloud Discovery の操作](working-with-cloud-discovery-data.md)に関するページを参照してください。

4. Zscaler により、Cloud App Security で設定した承認されていないすべてのアプリが、2 時間ごとに ping されて、自動的にブロックされます。 承認されないアプリの詳細については、「[アプリの承認/却下](governance-discovery.md#BKMK_SanctionApp)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
