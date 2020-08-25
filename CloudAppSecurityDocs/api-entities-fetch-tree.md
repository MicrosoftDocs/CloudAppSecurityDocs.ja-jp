---
title: エンティティ ツリーのフェッチ - Entities API
description: この記事では、Cloud App Security の Entities API のエンティティ ツリーのフェッチ要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 2f39f0541569b4f4c127c3c1d9602e097b56a82b
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657743"
---
# <a name="fetch-entity-tree---entities-api"></a>エンティティ ツリーのフェッチ - Entities API

*適用対象:Microsoft Cloud App Security*

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

指定した主キーと一致するエンティティに関連するすべてのエンティティをフェッチする GET 要求を実行します。 エンティティがユーザーの場合、ユーザーに関連付けられているすべてのアカウントをフェッチします。 エンティティがアカウントの場合、エンティティの親と兄弟をフェッチします。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/entities/<pk>/retrieve_tree/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | エンティティの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/entities/<pk>/retrieve_tree/"
```

### <a name="response"></a>[応答]

指定したエンティティ ツリーを JSON 形式で返します。

```json
{
  // entity tree record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
