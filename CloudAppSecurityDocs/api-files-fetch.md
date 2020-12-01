---
title: フェッチ - Files API
description: この記事では、Cloud App Security の Files API のフェッチ要求について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: 7d3faf9630edf3e277b481d5f8bcea87898e67cd
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314054"
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
