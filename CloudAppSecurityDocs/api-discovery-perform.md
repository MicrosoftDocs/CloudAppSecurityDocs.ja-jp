---
title: ファイル アップロードの実行 - Cloud Discovery API
description: この記事では、Cloud App Security の Cloud Discovery API のファイル アップロード要求の実行について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: 551a8a0434c916f1df7b591638908970712e9d28
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314428"
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
