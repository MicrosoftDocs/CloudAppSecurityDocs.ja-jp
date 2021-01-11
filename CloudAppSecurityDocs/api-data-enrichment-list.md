---
title: 一覧表示 - Data Enrichment API
description: この記事では、Cloud App Security の Data Enrichment API の一覧表示要求について説明します。
ms.date: 12/13/2020
ms.topic: reference
ms.openlocfilehash: a817431dc7788900294b8f6fde26beb326a21d87
ms.sourcegitcommit: 90df07ce9cd64fd9c46fb6563f0249079204e174
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97859066"
---
# <a name="list---data-enrichment-api"></a>一覧表示 - Data Enrichment API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定したフィルターと一致する IP 範囲の一覧をフェッチするには、GET または POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/subnet/
```

```rest
POST /api/v1/subnet/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求のすべての検索フィルターを使用してオブジェクトをフィルター処理します。詳細については、[IP 範囲フィルター](api-data-enrichment.md#filters)に関するページを参照してください |
| sortDirection | 並べ替えの方向。 指定できる値は `asc` および `desc` です。 |
| sortField | IP 範囲の並べ替えに使用するフィールド。 次のいずれかの値になります。<br />- **category**: IP 範囲のカテゴリ<br />- **tags**: IP 範囲のタグ<br />- **name**: IP 範囲の名前 |
| skip | 指定した数のレコードをスキップします |
| limit | 要求から返されるレコードの最大数 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/subnet/" -d '{
  "filters": {
    // some filters
  },
  "skip": 5,
  "limit": 10
  ...
}'
```

### <a name="response"></a>[応答]

IP 範囲の一覧が JSON 形式で返されます。 応答のフィールドの詳細については、「[プロパティ](api-data-enrichment.md#properties)」を参照してください。

```json
{
  "total": 1 // total number of records
  "hasNext": false // whether there is more data to show or not.
  "data": [
    {
      // returned records
      "_id": "5fd767259cd24bb563567d7c",
      "name": "range name",
      "subnets": [
        {
          "mask": 112,
          "address": "0000:0000:0000:0000:0000:ffff:c5c6:0000",
          "originalString": "197.198.192.20/16"
        }
      ],
      "location": {
        "name": "United States",
        "latitude": 39.5035514831543,
        "longitude": -99.01830291748047,
        "countryCode": "US",
        "countryName": "United States"
      },
      "organization": "isp name",
      "tags": [
        {
          "_id": "5ce2aaf42207ad108c76fa3a",
          "id": "000000290000000000000000",
          "target": 1,
          "type": 2,
          "name": "Contoso",
          "nameTemplate": {
            "template": "SAGE_BUILTIN_TAG_CONTOSO_NAME"
          },
          "description": "IP addresses used by Contoso",
          "descriptionTemplate": {
            "template": "SAGE_BUILTIN_TAG_CONTOSO_DESCRIPTION"
          },
          "visibility": 0,
          "status": 0,
          "_tid": 113348336
        }
      ],
      "category": 5,
      "lastModified": 1607952165309.8032,
      "_tid": 113348336
    }
  ]
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
