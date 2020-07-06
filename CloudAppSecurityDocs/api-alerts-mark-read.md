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
ms.openlocfilehash: 1f312bd7929c40efd056adcecd58b9bbd16c6516
ms.sourcegitcommit: 286f8d5d940d1bb9a09daa3070ac4fc3768208f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505451"
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
curl -XPOST -H "Authorization:<your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/<pk>/read/"
```

[!INCLUDE [Open support ticket](includes/support.md)]
