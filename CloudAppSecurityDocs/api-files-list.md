---
title: 一覧表示 - Files API
description: この記事では、Cloud App Security の Files API の一覧表示要求について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: 644bfea227212e5b988eebc7e05aca8694a49f92
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314003"
---
# <a name="list---files-api"></a>一覧表示 - Files API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
>
> - この API はまもなく非推奨になります。 Microsoft Cloud App Security により、ポリシーに違反するファイルを識別して対処するための新しいソリューションが開発されています。
> - このエンドポイントは、大規模なコレクションのフィルター処理とページ番号付けを行うとタイムアウトする場合があります。
> - この API は、Office 365 Cloud App Security では使用できません。

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
