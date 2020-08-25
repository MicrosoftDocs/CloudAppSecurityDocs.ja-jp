---
title: 一覧表示 - Entities API
description: この記事では、Cloud App Security の Entities API の一覧表示要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: f6cea4b9697489aa979de029ab5d12e897a8f94b
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657645"
---
# <a name="list---entities-api"></a>一覧表示 - Entities API

*適用対象:Microsoft Cloud App Security*

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

指定したフィルターと一致するエンティティの一覧をフェッチする GET または POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/entities/
```

```rest
POST /api/v1/entities/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求のすべての検索フィルターでオブジェクトをフィルター処理します。詳細については、[エンティティ フィルター](api-entities.md#filters)に関するページを参照してください |
| sortDirection | 並べ替えの方向。 指定できる値は `asc` および `desc` です。 |
| sortField | エンティティの並べ替えに使用するフィールド。 指定できる値は次のとおりです。<br /><br />**date**:エンティティが作成された日付。<br /><br />**severity**:エンティティの重要度 |
| skip | 指定した数のレコードをスキップします |
| limit | 要求から返されるレコードの最大数 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/entities/" -d '{
  "filters": {
    // some filters
  },
  "skip": 5,
  "limit": 10
  ...
}'
```

### <a name="response"></a>[応答]

アクティビティの一覧を JSON 形式で返します。

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
