---
title: Cloud App Security を iboss と統合する
description: この記事では、Microsoft Cloud App Security を iboss Secure Cloud Gateway と統合し、シームレスな Cloud Discovery と、承認されていないアプリの自動ブロックを実現する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 2/2/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 8d849ed2b95577a805355eaae744ff81d2eb8176
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781720"
---
# <a name="integrate-cloud-app-security-with-iboss"></a>Cloud App Security を iboss と統合する

*適用対象:Microsoft Cloud App Security*

Cloud App Security と iboss の両方を使用している場合は、この 2 つの製品を統合して、お使いの Cloud Discovery のセキュリティを強化することができます。 iboss は、あなたの組織のトラフィックを監視し、トランザクションをブロックするポリシーを設定できる、スタンドアロンのセキュリティで保護されたクラウド ゲートウェイです。 Cloud App Security と iboss を共に使用すると、次の機能が提供されます。

- Cloud Discovery をシームレスにデプロイすることができます。iboss を使用してご自分のトラフィックをプロキシし、それを Cloud App Security に送信できます。 これにより、Cloud Discovery を有効にするために、お使いのネットワーク エンドポイントにログ コレクターをインストールする必要がなくなります。
- iboss のブロック機能は、Cloud App Security で未承認として設定したアプリに自動的に適用されます。
- ご自分の iboss の管理ポータルを、Cloud App Security のご自分の組織の上位 100 のクラウド アプリに対するリスク評価を使用して拡張することができます。これは、iboss 管理ポータルで直接表示できます。

## <a name="prerequisites"></a>[前提条件]

- Microsoft Cloud App Security 用の有効なライセンス
- iboss Secure Cloud Gateway (リリース 9.1.100.0 以降) 用の有効なライセンス

## <a name="deployment"></a>展開

1. Cloud App Security ポータルで、次の統合手順を行います。
    1. 設定の歯車アイコンをクリックし、 **[Cloud Discovery 設定]** を選択します。
    2. **[自動ログ アップロード]** タブ、 **[データ ソースの追加]** を順に選択します。
    3. **[データ ソースの追加]** ページで、次の設定を入力します。

        - 名前 = iboss
        - ソース = iboss Secure Cloud Gateway
        - レシーバーの種類 = Syslog - UDP

        ![データ ソース iboss](media/iboss-integration.png)

    4. **[期待されるログ ファイルのサンプルを表示]** をクリックします。 次に、 **[サンプル ログのダウンロード]** をクリックしてサンプルの検出ログを表示し、それがお使いのログと一致していることを確認します。<br />

1. ご自分のネットワークで検出されたクラウド アプリを調査します。 詳細および調査手順については、[Cloud Discovery の操作](working-with-cloud-discovery-data.md)に関するページを参照してください。

1. iboss により、Cloud App Security に設定した承認されていないすべてのアプリが、10 分ごとに ping され、自動的にブロックされます。 承認されないアプリの詳細については、[アプリの承認と却下](governance-discovery.md#BKMK_SanctionApp)に関するページを参照してください。

1. iboss を、Microsoft Cloud App Security にトラフィック ログを送信するように構成したい場合は、iboss のサポートにお問い合わせください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
