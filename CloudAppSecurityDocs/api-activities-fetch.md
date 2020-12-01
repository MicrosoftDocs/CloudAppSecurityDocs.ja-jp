---
title: フェッチ - Activities API
description: この記事では、Cloud App Security の Activities API のフェッチ要求について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: dc26c22748aa2a03e7a59208b691c6a3a92527d6
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314717"
---
# <a name="fetch---activities-api"></a>フェッチ - Activities API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定した主キーと一致するアクティビティをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/activities/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アクティビティの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/activities/<pk>/"
```

### <a name="response"></a>[応答]

指定したアクティビティを JSON 形式で返します。

```json
{
  // activity record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
