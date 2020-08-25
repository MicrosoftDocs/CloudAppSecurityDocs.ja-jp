---
title: 一覧表示 - Files API
description: この記事では、Cloud App Security の Files API の一覧表示要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 7399ae14416afd1627b70c1eac27674a5cb2127f
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657709"
---
# <a name="list---files-api"></a>一覧表示 - Files API

*適用対象:Microsoft Cloud App Security*

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

指定したフィルターと一致するファイルの一覧をフェッチする GET または POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/files/
```

```rest
POST /api/v1/files/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求に対してすべての検索フィルターを使用してオブジェクトをフィルター処理します。詳細については、[ファイルのフィルター](api-files.md#filters)に関するページを参照してください |
| skip | 指定した数のレコードをスキップします |
| limit | 要求から返されるレコードの最大数 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/files/" -d '{
  "filters": {
    // some filters
  },
  "skip": 5,
  "limit": 10
  ...
}'
```

### <a name="response"></a>[応答]

JSON 形式のファイルの一覧を返します。

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
