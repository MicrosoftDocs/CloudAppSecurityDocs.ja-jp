---
title: フェッチ - Entities API
description: この記事では、Cloud App Security の Entities API のフェッチ要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 0ff0a93866652a0a4cc2e927593a2a56800c64de
ms.sourcegitcommit: cc283f0ecf8124953f1f71181655603de6846d8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87254668"
---
# <a name="fetch---entities-api"></a>フェッチ - Entities API

*適用対象:Microsoft Cloud App Security*

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

指定した主キーと一致するエンティティをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/entities/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | base64 文字列としてエンコードされた、エンティティ ID、SaaS、およびインスタンスの詳細を含むディクショナリ。 例: base64 文字列としてエンコードされた `{"id":"3fa9f28b-eb0e-463a-ba7b-8089fe9991e2","saas":11161,"inst":0}`。 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:<your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/entities/<pk>/"
```

### <a name="response"></a>[応答]

指定したエンティティを JSON 形式で返します。

```json
{
  // entity record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
