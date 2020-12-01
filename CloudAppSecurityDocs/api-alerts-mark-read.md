---
title: 既読としてマークする - Alerts API
description: この記事では、Cloud App Security の Alerts API で既読の要求としてマークする方法について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: ecf314300e59371fc6cddaeddc0ab4b78efbaaa0
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314598"
---
# <a name="mark-as-read---alerts-api"></a>既読としてマークする - Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定した主キーと一致するアラートを既読とマークする POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/alerts/<pk>/read/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アラートの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/<pk>/read/"
```

[!INCLUDE [Open support ticket](includes/support.md)]
