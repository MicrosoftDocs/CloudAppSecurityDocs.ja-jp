---
title: ファイルのアップロードの最終処理 - Cloud Discovery API
description: この記事では、Cloud App Security の Cloud Discovery API の done_upload 要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: a30fd3f257089d8d3aeda125f63ae2c695d6344c
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880599"
---
# <a name="finalize-file-upload---cloud-discovery-api"></a>ファイルのアップロードの最終処理 - Cloud Discovery API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

ファイル コンテンツのアップロードが正常に完了すると、ファイルの処理を開始するために通知されます。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/discovery/done_upload/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| uploadUrl | ファイルのアップロードを要求する最初の呼び出しで返された URL。 |
| inputStreamName | データの受信元のデータ ソースの名前 (デバイスを表します)。 |
| uploadAsSnapshot | 継続的レポートにアップロードするのではなく、スナップショット レポートとしてデータをアップロードします。 このパラメーターが設定されている場合、inputStreamName で指定した名前を持つレポートが作成されます。 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/discovery/done_upload/" -d "uploadUrl=<initiate_file_upload_response_url>"
```

[!INCLUDE [Open support ticket](includes/support.md)]
