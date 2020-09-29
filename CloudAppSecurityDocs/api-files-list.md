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
ms.openlocfilehash: 2dac75e59e95e01f11e0dc2af0d4dc44ffb9a284
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90879657"
---
# <a name="list---files-api"></a>一覧表示 - Files API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

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
