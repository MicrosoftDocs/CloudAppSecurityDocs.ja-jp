---
title: ブロック スクリプトの生成 - Cloud Discovery API
description: この記事では、Cloud App Security の Cloud Discovery API の discovery_block_scripts 要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 55a5d50f8dbe0dbbe1a34fcca913bc25d3292e42
ms.sourcegitcommit: 6e47d0348283d105614d81db4e7737fc837ed20b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88657760"
---
# <a name="generate-block-script---cloud-discovery-api"></a>ブロック スクリプトの生成 - Cloud Discovery API

*適用対象:Microsoft Cloud App Security*

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

ネットワーク アプライアンスに対するブロック スクリプトを取得する GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/discovery/discovery_block_scripts/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| format | ネットワーク アプライアンスの形式。 |

現在サポートされている形式は次のとおりです。

| アプライアンス | フォーマット |
| --- | --- |
| BlueCoat ProxySG | 102 |
| Cisco ASA | 104 |
| Fortinet FortiGate | 108 |
| Juniper SRX | 129 |
| Palo Alto | 112 |
| Websense | 135 |
| Zscaler | 120 |

> [!NOTE]
> アプライアンスが見つからない場合は、ポータルを使用して手動でブロック スクリプトを生成してください。

## <a name="response"></a>[応答]

この要求からはテキスト形式でブロック スクリプトが返されます。

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/discovery/discovery_block_scripts/?format=102&type=banned"
```

### <a name="response"></a>[応答]

```text
url.domain=application.com deny
url.domain=application.be deny
url.domain=application.co deny
```

[!INCLUDE [Open support ticket](includes/support.md)]
