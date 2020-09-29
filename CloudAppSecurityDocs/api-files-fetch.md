---
title: フェッチ - Files API
description: この記事では、Cloud App Security の Files API のフェッチ要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 9d1d06e3951322036b4a4344d85f3ba960582637
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880901"
---
# <a name="fetch---files-api"></a>フェッチ - Files API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

指定した主キーと一致するファイルをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/files/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | ファイルの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/files/<pk>/"
```

### <a name="response"></a>[応答]

指定したファイルを返します。

[!INCLUDE [Open support ticket](includes/support.md)]
