---
title: ログ コレクターの FTP 構成
description: この記事では、Cloud App Security Cloud Discovery docker の構成を変更する手順について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/7/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 53eaa7b96a22c7574a63b6051dce64076fafaa39
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781669"
---
# <a name="log-collector-ftp-configuration"></a>ログ コレクターの FTP 構成

*適用対象:Microsoft Cloud App Security*

この記事では、Cloud App Security Cloud Discovery docker の構成を変更する方法について説明します。

## <a name="docker-deployment"></a>Docker のデプロイ

Cloud App Security Cloud Discovery docker の構成を変更する必要がある場合があります。

### <a name="changing-the-ftp-password"></a>FTP のパスワードの変更

1. ログ コレクターのホストに接続します。

2. `docker exec -it <collector name> pure-pw passwd <ftp user>` を実行します。

    1. 新しいパスワードを入力します。
    2. 確認のために、もう一度新しいパスワードを入力します。

3. `docker exec -it <collector name> pure-pw mkdb` を実行して、変更を適用します。

    ![FTP のパスワードの変更](media/ftp-connect.png)

### <a name="customize-certificate-files"></a>証明書ファイルのカスタマイズ

次の手順に従うと、Cloud Discovery docker へのセキュリティで保護された接続に使用する証明書ファイルをカスタマイズできます。

1. FTP クライアントを開き、ログ コレクターに接続します。

    ![FTP クライアントへの接続](media/ftp-connect.png)

2. `ssl_update` ディレクトリに移動します。
3. 新しい証明書ファイルを `ssl_update` ディレクトリにアップロードします (名前は必須です)。

    ![証明書ファイルのアップロード](media/new-certs.png)

    - **FTP の場合:** 1 つファイルが必要です。 このファイルには、キーと資格証明書のデータが (この順番で) あり、**pure-ftpd.pem** という名前です。
    - **Syslog の場合:** **ca.pem**、**server-key.pem、**server-cert.pem** の 3 つのファイルが必要です。 これらのいずれかのファイルが見つからない場合、更新はされません。

4. ターミナルで実行する場合: `docker exec -t <collector name> update_certs` このコマンドを実行すると、次のスクリーンショットのような出力が生成されます。

    ![証明書ファイルの更新](media/update-certs.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery の展開](set-up-cloud-discovery.md)

[!INCLUDE [Open support ticket](includes/support.md)]
