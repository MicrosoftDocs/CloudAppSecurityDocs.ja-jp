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
ms.openlocfilehash: 5127f1e09fc5cd34ce0a45fd05ed1714e94cd94a
ms.sourcegitcommit: 288f3011c0ce0e5f2d8cbaa9057a63be044465f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94375068"
---
# <a name="fetch---files-api"></a>フェッチ - Files API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
>
> - この API はまもなく非推奨になります。 Microsoft Cloud App Security により、ポリシーに違反するファイルを識別して対処するための新しいソリューションが開発されています。
> - この API は、Office 365 Cloud App Security では使用できません。

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
