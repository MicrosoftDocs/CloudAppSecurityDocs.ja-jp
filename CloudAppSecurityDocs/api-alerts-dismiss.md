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
ms.openlocfilehash: efd8ced52fcad8d575242cb702fe6149f3345e20
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90879893"
---
# <a name="dismiss---alerts-api"></a>無視 - Alerts API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

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
