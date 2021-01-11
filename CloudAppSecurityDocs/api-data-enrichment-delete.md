---
title: IP アドレス範囲を削除する - Data Enrichment API
description: この記事では、Cloud App Security の Data Enrichment API での IP アドレス範囲削除要求について説明します。
ms.date: 12/13/2020
ms.topic: reference
ms.openlocfilehash: 0cda04381501283526c77240debd7cfbe4f672fc
ms.sourcegitcommit: 90df07ce9cd64fd9c46fb6563f0249079204e174
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97859069"
---
# <a name="delete-ip-address-range---data-enrichment-api"></a>IP アドレス範囲を削除する - Data Enrichment API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

IP アドレス範囲を削除するには、DELETE 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
DELETE /api/v1/subnet/<ip_range_id>/
```

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -X DELETE -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/subnet/<ip_range_id>/"
```

[!INCLUDE [Open support ticket](includes/support.md)]
