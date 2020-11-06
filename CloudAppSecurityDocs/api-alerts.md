---
title: Cloud App Security Alerts API
description: この記事では、Alerts API の使用方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/20/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: f1176967bfcf67a458f55fe9421575df329aabe7
ms.sourcegitcommit: 6ae1c05025a49ad3c8e8cecd0c10dc05edcd9bf8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2020
ms.locfileid: "92929082"
---
# <a name="alerts-api"></a>Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Alerts API を使用すると、Cloud App Security によって特定された、注意が必要な緊急リスクに関する情報を取得できます。 アラートは、不審な使用パターンや、会社のポリシーに違反するコンテンツを含むファイルから生成される可能性があります。

サポートされている要求は次のとおりです。

- [アラートの一覧表示](api-alerts-list.md)
- [問題のないものを閉じる](api-alerts-close-benign.md)
- [偽陽性を閉じる](api-alerts-close-false-positive.md)
- [真陽性を閉じる](api-alerts-close-true-positive.md)
- [アラートのフェッチ](api-alerts-fetch.md)
- [アラートを既読としてマークする](api-alerts-mark-read.md)
- [アラートを未読としてマークする](api-alerts-mark-unread.md)

## <a name="deprecated-requests"></a>非推奨の要求

古いため非推奨とされる要求と、それらを置き換える要求を次の表に一覧表示します。

| 古い要求 | 代替手段 |
| --- | --- |
| 一括破棄 | [偽陽性を閉じる](api-alerts-close-false-positive.md) |
| 一括解決 | [真陽性を閉じる](api-alerts-close-true-positive.md) |
| アラートを無視 | [偽陽性を閉じる](api-alerts-close-false-positive.md) |

> [!NOTE]
> 非推奨の要求は、中断を避けるために、代替手段にマップされています。 ただし、お使いの環境で古い要求を使用している場合は、それらを代替手段に更新することをお勧めします。

## <a name="filters"></a>フィルタ

フィルターの動作の詳細については、「[フィルター](api-introduction.md#filters)」を参照してください。

次の表では、サポートされているフィルターについて説明します。

| フィルター | Type | 演算子 | [説明] |
| --- | --- | --- | --- |
| entity.entity | entity pk | eq、neq | 指定したファイルに関連するアラートをフィルター処理します。 例: `[{ "id": "entity-id", "saas": 11161, "inst": 0 }]` |
| entity.ip | string | eq、neq | 指定した IP アドレスに関連するアラートをフィルター処理します |
| entity.service | integer | eq、neq | 指定したサービス appId に関連するアラートをフィルター処理します。例:11770 |
| entity.instance | integer | eq、neq | 指定したインスタンスに関連するアラートをフィルター処理します。例:11770、1059065 |
| entity.policy | string | eq、neq | 指定したポリシーに関連するアラートをフィルター処理します |
| entity.file | string | eq、neq | 指定したファイルに関連するアラートをフィルター処理します |
| alertOpen | boolean | eq | "true" に設定すると、未処理のアラートのみが返され、"false" に設定すると、閉じられたアラートのみが返されます |
| severity | integer | eq、neq | 重要度でフィルター処理します。 次の値を指定できます。<br /><br />**0** :低<br />**1** :中間<br/>**2** :高 |
| resolutionStatus | integer | eq、neq | アラートの解決状態でフィルター処理します。次の値を指定できます。<br /><br />**0** :オープン <br />**1** :破棄 (レガシ状態)<br />**2** :解決済み (レガシ状態)<br />**3** :擬陽性として閉じられた<br />**4** :無害として閉じられた<br />**5** :真陽性として閉じられた |
| read | boolean | eq | "true" に設定すると、既読のアラートのみが返され、"false" に設定すると、未読のアラートのみが返されます。 |
| date | timestamp | lte、gte、range、lte_ndays、gte_ndays | アラートがトリガーされた時刻でフィルター処理します |
| resolutionDate | timestamp | lte、gte、range | アラートが解決された時刻でフィルター処理します |
| risk | integer | eq、neq | リスクでフィルター処理します |
| alertType | integer | eq、neq | アラートの種類でフィルター処理します |
| ID | string | eq、neq | アラート ID でフィルター処理します |
| ソース | string | eq | アラートの生成元 (組み込みまたはポリシー) |

[!INCLUDE [Open support ticket](includes/support.md)]
