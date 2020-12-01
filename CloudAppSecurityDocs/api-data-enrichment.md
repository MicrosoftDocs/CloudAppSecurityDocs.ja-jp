---
title: IP アドレス範囲を作成する - Data Enrichment API
description: この記事では、Cloud App Security の Data Enrichment API での IP アドレス範囲作成要求について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: ec84185e0523b8b9f9f172e1940302656f10316b
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314513"
---
# <a name="create-ip-address-range---data-enrichment-api"></a>IP アドレス範囲を作成する - Data Enrichment API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

新しい IP アドレス範囲を追加する POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/subnet/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | 説明 |
| --- | --- |
| category | 範囲カテゴリの ID |
| サブネット | 文字列としてのマスクの配列 (IPv4/IPv6) |
| 組織 (省略可能) | 登録された ISP |
| タグ (省略可能) | タグの配列 ("text" プロパティにタグ名が設定されたオブジェクト) - 新規または既存 |

現在、次のカテゴリがサポートされています。

| カテゴリ | ID |
| --- | -- |
| 企業 | 1 |
| 管理 | 2 |
| 危険 | 3 |
| VPN | 4 |
| クラウド プロバイダー | 5 |
| その他 | 6 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/subnet/create_rule/" -d '{
  "name":"range name",
  "category":5,
  "organization":"Microsoft",
  "subnets":[
    "192.168.1.0/24",
    "192.168.2.0/16"
  ],
  "tags":[
    "existing tag"
  ]
}'
```

### <a name="response"></a>[応答]

新しい範囲の ID を文字列として返します。

[!INCLUDE [Open support ticket](includes/support.md)]
