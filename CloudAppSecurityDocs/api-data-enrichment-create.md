---
title: IP アドレス範囲を作成する - Data Enrichment API
description: この記事では、Cloud App Security の Data Enrichment API での IP アドレス範囲作成要求について説明します。
ms.date: 12/13/2020
ms.topic: reference
ms.openlocfilehash: 39cb7fc47146aec690b9418da28a2caa636749d0
ms.sourcegitcommit: 90df07ce9cd64fd9c46fb6563f0249079204e174
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97859064"
---
# <a name="create-ip-address-range---data-enrichment-api"></a>IP アドレス範囲を作成する - Data Enrichment API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

新しい IP アドレス範囲を追加する POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/subnet/create_rule/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | 説明 |
| --- | --- |
| name | 範囲の一意の名前 |
| category | 範囲カテゴリの ID。 カテゴリを指定すると、対象の IP アドレスからのアクティビティを簡単に識別できます。 次の値を指定できます。<br /><br />**1**:企業<br />**2**:管理<br />**3**:危険<br />**4**:VPN<br />**5**:クラウド プロバイダー<br />**6**: その他 |
| サブネット | 文字列としてのマスクの配列 (IPv4/IPv6) |
| 組織 (省略可能) | 登録された ISP |
| タグ (省略可能) | タグ名、ID、説明、名前テンプレート、テナント ID が格納されている、新規または既存のオブジェクトの配列 |

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
