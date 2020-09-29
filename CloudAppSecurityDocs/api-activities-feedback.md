---
title: フィードバック - Activities API
description: この記事では、Cloud App Security の Activities API のフィードバック要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: b9d073d3b39fbfeee7ee43b18ab05ddf2969c7bf
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880086"
---
# <a name="feedback-on-activity---activities-api"></a>アクティビティに関するフィードバック - Activities API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

指定した主キーと一致するアクティビティに関するフィードバックを送信する POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/activities/<pk>/feedback
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アクティビティの ID |

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| feedback | アクティビティに関するフィードバック |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/activities/<pk>/feedback" -d '{
  "feedbackValue": "0",
  "feedbackText": "Irrelevant",
  "allowContact": false,
  "contactEmail": "some.contact.address"
}'
```

### <a name="response"></a>[応答]

アクティビティの一覧を JSON 形式で返します。

```json
{
  "total": 5 // total number of records
  "hasNext": true // whether there is more data to show or not.
  "data": [
    // returned records
  ]
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
