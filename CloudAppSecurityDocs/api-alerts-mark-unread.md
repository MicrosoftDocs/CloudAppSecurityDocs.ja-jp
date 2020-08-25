---
title: 未読としてマークする - Alerts API
description: この記事では、Cloud App Security の Alerts API で未読の要求としてマークする方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 262163c5063e856957477166c6989a9bc5ae8e72
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657811"
---
# <a name="mark-as-unread---alerts-api"></a>未読としてマークする - Alerts API

*適用対象:Microsoft Cloud App Security*

指定した主キーと一致するアラートを未読とマークする POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/alerts/<pk>/unread/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アラートの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/<pk>/unread/"
```

[!INCLUDE [Open support ticket](includes/support.md)]
