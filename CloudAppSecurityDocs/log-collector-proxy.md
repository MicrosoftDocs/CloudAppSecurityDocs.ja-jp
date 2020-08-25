---
title: プロキシの背後にあるログ コレクターを有効にする - Cloud App Security
description: この記事では、プロキシの背後から Cloud App Security の Cloud Discovery ログ コレクターを有効にする方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/6/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 665d7435399c37a1d9683f004b0996f9ea5d263f
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781703"
---
# <a name="enable-the-log-collector-behind-a-proxy"></a>プロキシの背後にあるログ コレクターを有効にする

ログ コレクターを構成した後、プロキシの背後で実行する場合は、ログ コレクターから Cloud App Security へのデータ送信時に問題が発生する可能性があります。 これが発生する理由として考えられるのは、ログ コレクターがプロキシのルート証明機関を信頼しておらず、Microsoft Cloud App Security に接続してその構成を取得したり、受信したログをアップロードしたりできないことです。

>[!NOTE]
> Syslog または FTP のログ コレクターによって使用される証明書を変更する方法と、ファイアウォールおよびプロキシからログ コレクターへの接続に関する問題を解決する方法の詳細については、「[ログ コレクターの FTP 構成](log-collector-ftp.md)」を参照してください。
>

## <a name="set-up-the-log-collector-behind-a-proxy"></a>プロキシの背後にあるログ コレクターの設定

Windows または Linux コンピューターで Docker を実行するために必要な手順を完了したことを確認し、コンピューターに Cloud App Security の Docker イメージを正しくダウンロードします。 詳細については、「[継続的なレポートのために自動ログ アップロードを構成する](discovery-docker.md)」を参照してください。

### <a name="validate-docker-log-collector-container-creation"></a>Docker ログ コレクター コンテナーの作成を検証する

シェルで次のコマンドを使用して、コンテナーが作成されて実行中であることを確認します。

```bash
docker ps
```

![docker ps](media/docker-1.png)

### <a name="copy-proxy-root-ca-certificate-to-the-container"></a>プロキシのルート CA 証明書をコンテナーにコピーする

仮想マシンから Cloud App Security コンテナーに CA 証明書をコピーします。 次の例では、コンテナーの名前は *Ubuntu-LogCollector* であり、CA 証明書の名前は *Proxy-CA.crt* です。
Ubuntu ホスト上でコマンドを実行します。 次のように、実行中のコンテナー内のフォルダーに証明書をコピーします。

```bash
docker cp Proxy-CA.crt Ubuntu-LogCollector:/var/adallom/ftp/discovery
```

### <a name="set-the-configuration-to-work-with-the-ca-certificate"></a>CA 証明書を使用するように構成を設定する

1. 次のコマンドを使用して、コンテナーに移ります。 ログ コレクター コンテナーで bash が開きます。

    ```bash
    docker exec -it Ubuntu-LogCollector /bin/bash
    ```

2. コンテナー内の bash から、Java *jre* フォルダーに移動します。 バージョンに関連したパスのエラーを回避するには、次のコマンドを使用します。

    ```bash
    cd "$(find /opt/jdk/*/jre -name "bin" -printf '%h' -quit)"
    ```

3. 先ほどコピーしたルート証明書を *discovery* フォルダーから Java キーストアにインポートし、パスワードを定義します。 既定のパスワードは "changeit" です。 パスワード変更の詳細については、「[Java キーストアのパスワードを変更する方法](#how-to-change-the-java-keystore-password)」を参照してください。

    ```bash
    ./keytool --import --noprompt --trustcacerts --alias SelfSignedCert --file /var/adallom/ftp/discovery/Proxy-CA.crt --keystore ../lib/security/cacerts --storepass <password>
    ```

4. 次のコマンドを使用して、インポート時に指定したエイリアス (*SelfSignedCert*) を検索し、証明書が CA キーストアに正しくインポートされたことを確認します。

    ```bash
    ./keytool --list --keystore ../lib/security/cacerts | grep self
    ```

    ![keytool](media/docker-2.png "keytool")

インポートしたプロキシ CA 証明書が表示されます。

### <a name="set-the-log-collector-to-run-with-the-new-configuration"></a>新しい構成で実行するようにログ コレクターを設定する

これでコンテナーの準備ができました。

ログ コレクターの作成時に使用した API トークンを使って、**collector_config** コマンドを実行します。

![API トークン](media/docker-3.png "API トークン")

このコマンドを実行するときに、実際の API トークンを指定します。

```bash
collector_config abcd1234abcd1234abcd1234abcd1234 ${CONSOLE} ${COLLECTOR}
```

![構成の更新](media/docker-4.png "構成の更新")

これでログ コレクターと Cloud App Security の通信ができるようになりました。 データを送信すると、Cloud App Security ポータル上の状態が "**正常**" から "**接続済み**" に変わります。

![状態](media/docker-5.png "状態")

>[!NOTE]
> ログ コレクターの構成を更新する必要がある場合、たとえばデータ ソースを追加または削除するには、通常はコンテナーを**削除**し、以前の手順を再度行う必要があります。 これを回避するには、Cloud App Security ポータルで生成された新しい API トークンを使用して、*collector_config* ツールを再実行します。

## <a name="how-to-change-the-java-keystore-password"></a>Java キーストアのパスワードを変更する方法

1. Java キーストア サーバーを停止します。
1. コンテナー内で bash シェルを開き、*appdata/conf* フォルダーに移動します。
1. 次のコマンドを使用して、サーバー キーストアのパスワードを変更します。

    ```bash
    keytool -storepasswd -new newStorePassword -keystore server.keystore
    -storepass changeit
    ```

    > [!NOTE]
    > 既定のサーバー パスワードは *changeit* です。

1. 次のコマンドを使用して、証明書のパスワードを変更します。

    ```bash
    keytool -keypasswd -alias server -keypass changeit -new newKeyPassword -keystore server.keystore -storepass newStorePassword
    ```

    > [!NOTE]
    > 既定のサーバー エイリアスは *server* です。

1. テキスト エディターで、*server-install\conf\server\secured-installed.properties* ファイルを開き、次のコード行を追加して、変更を保存します。
    1. サーバーの新しい Java キーストア パスワードを指定します: `server.keystore.password=newStorePassword`
    1. サーバーの新しい証明書パスワードを指定します: `server.key.password=newKeyPassword`
1. サーバーを起動します。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ユーザー アクティビティ ポリシー](user-activity-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
