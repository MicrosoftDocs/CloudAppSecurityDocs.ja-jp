---
title: 無視 - Alerts API
description: この記事では、Cloud App Security の Alerts API の無視要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: cce286057b244d9a49a43327587c1156a156c999
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657612"
---
# <a name="dismiss---alerts-api"></a>無視 - Alerts API

*適用対象:Microsoft Cloud App Security*

指定した主キーと一致するアラートを無視する POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/alerts/<pk>/dismiss/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アラートの ID |

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | 説明 |
| --- | --- |
| コメント | アラートが無視された理由に関するコメント |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/<pk>/dismiss/" -d '{
  "comment": "Irrelevant"
}'
```

[!INCLUDE [Open support ticket](includes/support.md)]
