---
title: 検出されたアプリのブロック - Cloud App Security
description: この記事では、検出されたアプリのブロック スクリプトをエクスポートする手順について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/12/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 73309d7edba1493c941af201aef300deed6b0314
ms.sourcegitcommit: e711727f2f00ee3b54e08337a5040449e352ca46
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2020
ms.locfileid: "93185979"
---
# <a name="govern-discovered-apps"></a>検出されたアプリの管理

[!INCLUDE [Banner for top of topics](includes/banner.md)]

環境内で検出されたアプリの一覧を確認したら、次の方法で、安全なアプリを承認する ( **承認された** ) か、または不要なアプリを禁止する ( **承認されていない** ) ことによって、環境をセキュリティで保護できます。

## <a name="sanctioningunsanctioning-an-app"></a><a name="BKMK_SanctionApp"></a> アプリの承認/非承認

特定の危険なアプリを承認しない場合は、行の末尾にある 3 つのドットをクリックします。 次に、 **[Unsanction]\(非承認\)** を選択します。 アプリを承認しないことによって、使用はブロックしませんが、Cloud Discovery フィルターによって、その使用をより簡単に監視できます。 さらに、承認されていないアプリのユーザーに通知し、それらの使用に対して代替の安全なアプリを提案することができます。

![承認されていないとタグ付けする](media/tag-as-unsanctioned.png)

承認または承認されていないアプリの一覧がある場合は、チェックボックスを使用して、管理するアプリを選択し、さらにアクションを選択します。

承認されていないアプリの一覧をクエリするには、[Cloud App Security API を使用してブロック スクリプトを生成](api-discovery-script.md)できます。

> [!NOTE]
> テナントで Microsoft Defender Advanced Threat Protection (ATP)、Zscaler NSS、または iboss を使用している場合は、承認されていないとマークしたすべてのアプリが Cloud App Security によって自動的にブロックされ、ブロックするスクリプトの作成に関する以下のセクションは不要になります。 詳細については、[Microsoft Defender ATP との統合](mde-integration.md)、[Zscaler との統合](zscaler-integration.md)、[iboss との統合](iboss-integration.md)に関するそれぞれのページをご覧ください。

## <a name="export-a-block-script-to-govern-discovered-apps"></a>検出されたアプリを管理するためにブロック スクリプトをエクスポートする

Cloud App Security により、既存のオンプレミスのセキュリティ アプライアンスを使用して、承認されていないアプリへのアクセスをブロックできます。 専用ブロック スクリプトを生成し、それをアプライアンスにインポートできます。 このソリューションでは、組織のすべての Web トラフィックをプロキシにリダイレクトする必要はありません。

1. Cloud Discovery ダッシュボードで、ブロックするすべてのアプリに、 **承認されていない** とタグ付けします。

    ![承認されていないとタグ付けする](media/tag-as-unsanctioned.png)

2. タイトル バーで、3 つのドットをクリックし、 **[ブロック スクリプトの生成...]** を選択します。

    ![ブロック スクリプトの生成](media/generate-block-script.png)

3. **[ブロック スクリプトの生成]** で、ブロック スクリプトを生成するアプライアンスを選択します。

    ![ブロック スクリプトの生成ポップアップ](media/generate-block-script-pop-up.png)

4. 次に、[スクリプトの生成] ボタンをクリックして、承認されていないすべてのアプリのブロック スクリプトを作成します。 既定で、ファイルには、エクスポートされた日付と選択したアプライアンスの種類で名前が付けられます。 *2017-02-19_CAS_Fortigate_block_script.txt* はファイル名の例です

   ![ブロック スクリプトの生成ボタン](media/generate-block-script-button.png)

5. 作成したファイルをアプライアンスにインポートします。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
