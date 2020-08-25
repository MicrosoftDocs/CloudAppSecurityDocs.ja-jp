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
ms.openlocfilehash: 9d61d4456674632aab09875b6c534593947856cc
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657335"
---
# <a name="fetch---alerts-api"></a>フェッチ - Alerts API

*適用対象:Microsoft Cloud App Security*

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
