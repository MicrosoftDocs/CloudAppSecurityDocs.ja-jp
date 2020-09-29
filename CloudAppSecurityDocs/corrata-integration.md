---
title: Cloud App Security を Corrata と統合する
description: この記事では、Microsoft Cloud App Security を Corrata と統合し、シームレスな Cloud Discovery と、承認されていないアプリの自動ブロックを実現する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: borisk
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: be9454c025d0dd2bf7d83954cba48ed349cf08e3
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880806"
---
# <a name="integrate-cloud-app-security-with-corrata"></a>Cloud App Security を Corrata と統合する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud App Security と Corrata の両方を使用している場合は、この 2 つの製品を統合して、モバイル アプリ用途で Cloud Discovery のセキュリティを強化できます。 ローカル モバイル ゲートウェイの Corrata で、モバイル デバイスからの組織のトラフィックを監視し、トランザクションをブロックするポリシーを設定することができます。 Cloud App Security と Corrata を共に使用すると、次の機能が提供されます。

- Cloud Discovery をシームレスにデプロイできます。Corrata を使用してモバイル デバイスのトラフィックを収集し、それを Cloud App Security に送信できます。 これにより、Cloud Discovery を有効にするために、ネットワーク エンドポイントにログ コレクターをインストールする必要がなくなります。
- Corrata のブロック機能は、Cloud App Security で未承認として設定したアプリに自動的に適用されます。
- 主要なクラウド アプリに対する Cloud App Security のリスク評価により、Corrata ポータルが強化されます。Corrata ポータルでそれを直接表示できます。

## <a name="prerequisites"></a>[前提条件]

- Microsoft Cloud App Security 用の有効なライセンス
- Corrata Cloud の有効なライセンス

## <a name="deployment"></a>展開

1. Corrata ポータルで、[Microsoft Cloud App Security との Corrata パートナー統合](https://corrata.com/microsoft-mcas-onboarding)の手順を完了します。
2. Cloud App Security ポータルで、次の統合手順を行います。
    1. 設定の歯車アイコンをクリックし、 **[Cloud Discovery 設定]** を選択します。
    2. **[自動ログ アップロード]** タブをクリックし、 **[データ ソースの追加]** をクリックします。
    3. **[データ ソースの追加]** ページで、次の設定を入力します。

        - [名前] = Corrata
        - [ソース] = Corrata
        - [レシーバーの種類] = FTP

        ![データ ソース Corrata](media/data-source-corrata.png)

    4. **[期待されるログ ファイルのサンプルを表示]** をクリックします。 次いで、 **[サンプル ログのダウンロード]** をクリックしてサンプルの検出ログを表示し、それがお使いのログと一致していることを確認します。

3. ネットワークで検出されたクラウド アプリを調査します。 詳細および調査手順については、[Cloud Discovery の操作](working-with-cloud-discovery-data.md)に関するページを参照してください。

4. 承認されていないものとして Cloud App Security で設定したすべてのアプリが Corrata によって ping され、自動的にブロックされます。 承認されないアプリの詳細については、「[アプリの承認/却下](governance-discovery.md#BKMK_SanctionApp)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
