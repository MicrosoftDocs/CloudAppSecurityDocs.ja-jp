---
title: フェッチ - Entities API
description: この記事では、Cloud App Security の Entities API のフェッチ要求について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: 34db1003dd3ac23f7bc4d5f14100b6c1ff4f6a2e
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314275"
---
# <a name="fetch---entities-api"></a>フェッチ - Entities API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

指定した主キーと一致するエンティティをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/entities/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | base64 文字列としてエンコードされた、エンティティ ID、SaaS、およびインスタンスの詳細を含むディクショナリ。 例: base64 文字列としてエンコードされた `{"id":"3fa9f28b-eb0e-463a-ba7b-8089fe9991e2","saas":11161,"inst":0}`。 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/entities/<pk>/"
```

### <a name="response"></a>[応答]

指定したエンティティを JSON 形式で返します。

```json
{
  // entity record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
