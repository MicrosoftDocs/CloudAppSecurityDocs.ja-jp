---
title: フェッチ - Alerts API
description: この記事では、Cloud App Security の Alerts API のフェッチ要求について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: 8332805803dc05d991ef153b8402afb39b7b0cc1
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314615"
---
# <a name="fetch---alerts-api"></a>フェッチ - Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定した主キーと一致するアラートをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/alerts/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アラートの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/<pk>/"
```

### <a name="response"></a>[応答]

指定したアラートを JSON 形式で返します。

```json
{
  // alert record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
