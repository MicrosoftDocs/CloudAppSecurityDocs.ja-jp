---
title: 既読としてマークする - Alerts API
description: この記事では、Cloud App Security の Alerts API で既読の要求としてマークする方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 61a8c7edb0533d4b7c6cf2228ef7a83c54541bd7
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657854"
---
# <a name="mark-as-read---alerts-api"></a>既読としてマークする - Alerts API

*適用対象:Microsoft Cloud App Security*

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
