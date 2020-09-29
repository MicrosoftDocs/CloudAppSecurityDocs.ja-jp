---
title: フェッチ - Alerts API
description: この記事では、Cloud App Security の Alerts API のフェッチ要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 78ef3b8d2982a6f5228344b35f5d67dca9a6aec1
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90879832"
---
# <a name="fetch---alerts-api"></a>フェッチ - Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定した主キーと一致するアラートをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/alerts/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アラートの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/<pk>/"
```

### <a name="response"></a>[応答]

指定したアラートを JSON 形式で返します。

```json
{
  // alert record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
