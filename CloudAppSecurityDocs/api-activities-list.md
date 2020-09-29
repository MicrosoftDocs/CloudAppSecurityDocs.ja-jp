---
title: 一覧表示 - Activities API
description: この記事では、Cloud App Security の Activities API の一覧表示要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: f2a0f245994852c0e48f6c334a7172ffa14950a1
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880075"
---
# <a name="list---activities-api"></a>一覧表示 - Activities API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定したフィルターと一致するアクティビティの一覧をフェッチする GET または POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/activities/
```

```rest
POST /api/v1/activities/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求のすべての検索フィルターでオブジェクトをフィルター処理します。詳細については、[アクティビティ フィルター](api-activities.md#filters)に関するページを参照してください |
| sortDirection | 並べ替えの方向。 指定できる値は `asc` および `desc` です。 |
| sortField | アクティビティの並べ替えに使用するフィールド。 指定できる値は次のとおりです。<br /><br />**date**:アクティビティが発生した日付<br /><br />**created**:アクティビティが保存されたときのタイムスタンプ。 |
| skip | 指定した数のレコードをスキップします |
| limit | 要求から返されるレコードの最大数 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/activities/" -d '{
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
