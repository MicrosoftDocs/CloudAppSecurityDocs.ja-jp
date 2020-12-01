---
title: 擬陽性を閉じる - Alerts API
description: この記事では、Cloud App Security の Alerts API の、アラートを擬陽性として一括で閉じる要求について説明します。
ms.date: 10/20/2020
ms.topic: reference
ms.openlocfilehash: 309e0fc4b7c89ab4f24ace1dd0b790b73a66bf6f
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314649"
---
# <a name="close-false-positive---alerts-api"></a>擬陽性を閉じる - Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定されたフィルターに一致する複数のアラートを擬陽性 (悪意のないアクティビティに対するアラート) として閉じる POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/alerts/close_false_positive/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求に対してすべての検索フィルターを使用してオブジェクトをフィルター処理します。詳細については、[アラートのフィルター](api-alerts.md#filters)に関するページを参照してください |
| コメント | アラートが無視される理由に関するコメント |
| reasonId | アラートを擬陽性として閉じる理由。 理由を指定することで、時間の経過と共に検出の精度を高めることができます。 指定できる値は、次のとおりです。<br /><br />**0**:関心がない<br />**1**:類似のアラートが多すぎる<br />**3**:アラートが正確ではない<br />**4**:その他 |
| sendFeedback | このアラートに関するフィードバックが提供されることを示すブール値。 既定値: false |
| feedbackText | フィードバックのテキスト |
| allowContact | ユーザーに連絡するための同意が与えられることを示すブール値。 既定値: false |
| contactEmail | ユーザーのメール アドレス |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/close_false_positive/" -d '{
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
  "reasonId": 0,
  "sendFeedback": true,
  "feedbackText": "Feedback text",
  "allowContact": true,
  "contactEmail": " user@contoso.com"
}'
```

[!INCLUDE [Open support ticket](includes/support.md)]
