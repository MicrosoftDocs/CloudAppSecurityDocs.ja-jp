---
title: IP アドレス範囲を作成する - Data Enrichment API
description: この記事では、Cloud App Security の Data Enrichment API での IP アドレス範囲作成要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 8739566fb2bd9413651c9f1e14257e62e6f4589e
ms.sourcegitcommit: c114a9e04589e1a3e0b5350862b3e6daf18e3d30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88658866"
---
# <a name="create-ip-address-range---data-enrichment-api"></a>IP アドレス範囲を作成する - Data Enrichment API

*適用対象:Microsoft Cloud App Security*

新しい IP アドレス範囲を追加する POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/subnet/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
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
