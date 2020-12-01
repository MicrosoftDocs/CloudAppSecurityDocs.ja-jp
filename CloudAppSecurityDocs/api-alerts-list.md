---
title: 一覧表示 - Alerts API
description: この記事では、Cloud App Security の Alerts API の一覧表示要求について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: a4a24db5bab13a12fdeb7ecbe88ad45c41b90577
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314584"
---
# <a name="list---alerts-api"></a>一覧表示 - Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定したフィルターと一致するアラートの一覧をフェッチする GET または POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/alerts/
```

```rest
POST /api/v1/alerts/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求に対してすべての検索フィルターを使用してオブジェクトをフィルター処理します。詳細については、[アラートのフィルター](api-alerts.md#filters)に関するページを参照してください |
| sortDirection | 並べ替えの方向。 指定できる値は `asc` および `desc` です。 |
| sortField | アラートの並べ替えに使用するフィールド。 指定できる値は次のとおりです。<br /><br />**date**:アラートが作成された日付<br /><br />**severity**:アラートの重要度 |
| skip | 指定した数のレコードをスキップします |
| limit | 要求から返されるレコードの最大数 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/" -d '{
  "filters": {
    // some filters
  },
  "skip": 5,
  "limit": 10
  ...
}'
```

### <a name="response"></a>[応答]

アラートの一覧を JSON 形式で返します。

```json
{
  "total": 5 // total number of records
  "hasNext": true // whether there is more data to show or not.
  "data": [
    // returned records
  ]
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
