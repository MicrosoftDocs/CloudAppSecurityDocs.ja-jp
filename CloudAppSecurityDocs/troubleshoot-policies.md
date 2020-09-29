---
title: Cloud App Security ポリシーのトラブルシューティング
description: この記事では、Cloud App Security でのポリシー作成のトラブルシューティングのプロセスについて説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: ca7eb8ec3a770991ffc3a0bcd8f39f70c2a65a7b
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90877106"
---
# <a name="troubleshooting-microsoft-cloud-app-security-policies"></a>Microsoft Cloud App Security ポリシーのトラブルシューティング

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、Cloud App Security でのポリシー作成のトラブルシューティングのプロセスについて説明します。

## <a name="troubleshooting"></a>トラブルシューティング

次の表に、ポリシーに関して発生する可能性があるエラーの説明と解決方法を示します。

|エラー|[説明]|解決策|
|----|----|----|
| **構成エラーのため、ポリシー <*name*> が自動的に無効になりました**|Microsoft Cloud App Security でこのエラーが発生した場合は、指定されたポリシーの構成を修正する必要があることを意味します。 Microsoft Cloud App Security ポリシーを作成するときは、多くの場合、IP タグやカスタムの機密の種類など、Cloud App Security またはセキュリティ/コンプライアンス センター内で作成された他のオブジェクトを使用します。 ポリシーで使用した IP タグまたはカスタムの機密の種類が削除されると、ポリシーが自動的に無効になり、このエラーが表示されます。 このメッセージは、複雑すぎるフィルターなど、より一般的な構成エラーを示す場合もあります。 |ポリシーを復元するには、ポリシーを編集し、示されているすべての構成エラーを修正します。 このエラーは通常、削除されたすべてのオブジェクトをポリシー フィルターから削除して、ポリシーを保存する必要があることを意味します。|

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
