---
title: ファイル アップロードの実行 - Cloud Discovery API
description: この記事では、Cloud App Security の Cloud Discovery API のファイル アップロード要求の実行について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: a943bf41934a6f90bd8d23b1b6bb358d673f35e7
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880567"
---
# <a name="perform-file-upload---cloud-discovery-api"></a>ファイル アップロードの実行 - Cloud Discovery API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

HTTP PUT 要求を実行して、ファイルの内容をアップロードします。 [ファイルのアップロードの開始](api-discovery-initiate.md)要求から返された URL を使用する必要があります。

Azure と AWS では、ターゲット URL にファイルをアップロードするときのヘッダーと制限が異なります。

> [!NOTE]
>
> - 最大 5 GB の個々のファイルをアップロードできます。 大きなファイルをアップロードする必要がある場合は、Cloud Discovery データを複数のチャンクに分割します。
> - 実行している環境がわからない場合は、この情報を返す[ファイルのアップロードの開始](api-discovery-initiate.md)要求を確認します。

## <a name="http-request"></a>HTTP 要求

```rest
PUT https://<initiate_file_upload_response_url>
```

> [!NOTE]
>
> Azure の場合:
> - ファイル サイズが 64 MB 未満の場合は、ヘッダー "x-ms-blob-type:BlockBlob " を要求に追加します。
> - ファイル サイズが 64 MB を超える場合は、複数のチャンクに分けてアップロードします。 これを行う最も簡単な方法は、[Azure SDK](https://azure.microsoft.com/downloads/) を使用することです。

## <a name="example"></a>例

### <a name="request"></a>要求

Azure の要求の例を次に示します。

```rest
curl --request PUT --upload-file <file_to_upload> -H "x-ms-blob-type: BlockBlob" "https://<initiate_file_upload_response_url>"
```

Azure Java SDK の要求の例を次に示します。

```java
File fileReference = new File("file.name");
// Create a blob using the URI that contains the shared access signature.
CloudBlockBlob sasBlob = new CloudBlockBlob(uri);

// Upload the file to the blob.
sasBlob.upload(new FileInputStream(fileReference), fileReference.length());
```

[!INCLUDE [Open support ticket](includes/support.md)]
