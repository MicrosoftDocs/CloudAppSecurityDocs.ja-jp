---
title: 真陽性を閉じる - Alerts API
description: この記事では、Cloud App Security の Alerts API の、アラートを真陽性として一括で閉じる要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/20/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 1da36127115b2b3204d33a467b01bc7544838936
ms.sourcegitcommit: ee40375712d2cc4090bd4e9cb58df486ec02aa62
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2020
ms.locfileid: "92327066"
---
# <a name="close-true-positive---alerts-api"></a>真陽性を閉じる - Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定されたフィルターに一致する複数のアラートを真陽性 (確認済みの悪意のあるアクティビティに対するアラート) として閉じる POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/alerts/close_true_positive/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求に対してすべての検索フィルターを使用してオブジェクトをフィルター処理します。詳細については、[アラートのフィルター](api-alerts.md#filters)に関するページを参照してください |
| コメント | アラートが無視される理由に関するコメント |
| sendFeedback | このアラートに関するフィードバックが提供されることを示すブール値。 既定値: false |
| feedbackText | フィードバックのテキスト |
| allowContact | ユーザーに連絡するための同意が与えられることを示すブール値。 既定値: false |
| contactEmail | ユーザーのメール アドレス |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/close_true_positive" -d '{
  "filters": {
    "id": {
      "eq": [
        "55af7415f8a0a7a29eef2e1f",
        "55af741cf8a0a7a29eef2e20",
        "5f8d70bfc1ffb25b0a541c7d"
      ]
    }
  },
  "comment": "Irrelevant",
  "sendFeedback": true,
  "feedbackText": "Feedback text",
  "allowContact": true,
  "contactEmail": " user@contoso.com"
}'
```

[!INCLUDE [Open support ticket](includes/support.md)]
