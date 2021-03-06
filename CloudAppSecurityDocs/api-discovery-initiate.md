---
title: ファイルのアップロードの開始 - Cloud Discovery API
description: この記事では、Cloud App Security の Cloud Discovery API の upload_url 要求について説明します。
ms.date: 10/21/2020
ms.topic: reference
ms.openlocfilehash: bc46d4c1fcfd88c751e94eb06c0d858ff2b2c4ba
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314445"
---
# <a name="initiate-file-upload---cloud-discovery-api"></a>ファイルのアップロードの開始 - Cloud Discovery API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

アップロード プロセスを開始する GET 要求を実行します。 3 つのうちの 1 つ目のこの呼び出しからは、後でアップロード (PUT) 要求を実行するために使用される URL が返されます。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/discovery/upload_url/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | 説明 |
| --- |--- |
| filename | Cloud Discovery の処理にアップロードするファイルの名前 |
| ソース | アップロードされる Cloud Discovery ログ ファイルの種類 |

現在、次のソースの種類がサポートされています。

- BARRACUDA
- BLUECOAT
- CHECKPOINT
- CHECKPOINT_CEF_SYSLOG
- CHECKPOINT_SMART_VIEW_TRACKER
- CHECKPOINT_XML
- CISCO_ASA
- CISCO_ASA_FIREPOWER
- CISCO_FIREPOWER_V6_SYSLOG
- CISCO_FWSM
- CISCO_IRONPORT_PROXY
- CISCO_IRONPORT_WSA_II
- CISCO_SCAN_SAFE
- CLAVISTER
- CORRATA
- CUSTOM_PARSER
- FORCEPOINT
- FORCEPOINT_LEEF
- FORTIGATE
- GENERIC_CEF
- GENERIC_LEEF
- GENERIC_W3C
- I_FILTER
- IBOSS
- JUNIPER_SRX
- JUNIPER_SRX_SD
- JUNIPER_SRX_WELF
- JUNIPER_SSG
- MACHINE_ZONE_MERAKI
- MCAFEE_SWG
- MICROSOFT_ISA_W3C
- PALO_ALTO
- PALO_ALTO_LEEF
- SONICWALL_SYSLOG
- SOPHOS_CYBEROAM
- SOPHOS_SG
- SOPHOS_XG
- SQUID
- SQUID_NATIVE
- STORMSHIELD
- WEBSENSE_SIEM_CEF
- WEBSENSE_V7_5
- ZSCALER
- ZSCALER_CEF
- ZSCALER_QRADAR

> [!NOTE]
>
> - カスタム パーサーを使用する場合、Cloud App Security では、選択したデータ ソースにアタッチされたカスタム パーサーが使用されます。
> - ファイル形式が見つからない場合は、ポータルを使用して手動アップロードを実行します。

## <a name="response-parameters"></a>応答のパラメーター

| パラメーター | 説明 |
| --- | --- |
| url | Cloud Discovery のアップロードを実行するターゲット URL。 |
| provider | "azure" または "aws" のいずれか。アップロードが Windows Azure Storage と AWS S3 ストレージのどちらを対象としているかを示します。 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/discovery/upload_url/?filename=my_discovery_file.txt&source=LOG_3COM"
```

### <a name="response"></a>[応答]

JSON 応答の例を次に示します。

```json
{
  "url": "https://<initiate_file_upload_response_url>",
  "provider": "azure"
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
