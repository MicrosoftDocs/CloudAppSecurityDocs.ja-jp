---
title: ログ コレクターの詳細な管理
description: この記事では、Cloud App Security の Cloud Discovery ログ コレクターの高度な管理タスクを実行する方法について説明します。
ms.date: 12/14/2020
ms.topic: how-to
ms.openlocfilehash: dd8ab619f7284bde404bbe90a44d346595e2b99a
ms.sourcegitcommit: d3f243593f86e0f13a1fbc67702a99c23af5a45a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386562"
---
# <a name="advanced-log-collector-management"></a>ログ コレクターの詳細な管理

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事には、Cloud App Security の Cloud Discovery ログ コレクターの以下の高度な構成オプションに関する情報が記載されています。

- [ログ コレクターの FTP 構成を変更する](#modify-the-log-collector-ftp-configuration)
- [プロキシの背後にあるログ コレクターを有効にする](#enable-the-log-collector-behind-a-proxy)
- [Linux 上の別のデータ パーティションにログ コレクターを移動する](#move-the-log-collector-to-a-different-data-partition-on-linux)
- [Linux 上のログ コレクターのディスク使用率を調べる](#inspect-the-log-collector-disk-usage-on-linux)
- [アクセス可能なホストにログ コレクターを移動する](#move-the-log-collector-to-an-accessible-host)
- [Linux 上のログ コレクターの Syslog および FTP レシーバー用のカスタム ポートを定義する](#define-custom-ports-for-syslog-and-ftp-receivers-for-log-collectors-on-linux)
- [Linux 上でログ コレクターが受信したトラフィックとログの形式を検証する](#validate-the-traffic-and-log-format-received-by-log-collector-on-linux)

## <a name="modify-the-log-collector-ftp-configuration"></a>ログ コレクターの FTP 構成を変更する

以下の手順を使用して、Cloud App Security の Cloud Discovery Docker の構成を変更します。

### <a name="docker-deployment"></a>Docker のデプロイ

Cloud App Security Cloud Discovery Docker の構成を変更する必要がある場合があります。

#### <a name="changing-the-ftp-password"></a>FTP のパスワードの変更

1. ログ コレクターのホストに接続します。

1. `docker exec -it <collector name> pure-pw passwd <ftp user>` を実行します。

    1. 新しいパスワードを入力します。
    1. 確認のために、もう一度新しいパスワードを入力します。

1. `docker exec -it <collector name> pure-pw mkdb` を実行して、変更を適用します。

    ![FTP のパスワードの変更](media/log-collector-advanced-tasks/ftp-connect.png)

#### <a name="customize-certificate-files"></a>証明書ファイルのカスタマイズ

次の手順に従って、Cloud Discovery Docker へのセキュリティで保護された接続に使用する証明書ファイルをカスタマイズします。

1. FTP クライアントを開き、ログ コレクターに接続します。

    ![FTP クライアントへの接続](media/log-collector-advanced-tasks/ftp-connect.png)

1. `ssl_update` ディレクトリに移動します。
1. 新しい証明書ファイルを `ssl_update` ディレクトリにアップロードします (名前は必須です)。

    ![証明書ファイルのアップロード](media/log-collector-advanced-tasks/new-certs.png)

    - **FTP の場合:** 1 つファイルが必要です。 このファイルには、キーと資格証明書のデータが (この順番で) あり、**pure-ftpd.pem** という名前です。
    - **Syslog の場合:** **ca.pem**、**server-key.pem、**server-cert.pem** の 3 つのファイルが必要です。 これらのいずれかのファイルが見つからない場合、更新はされません。

1. ターミナル ウィンドウで、`docker exec -t <collector name> update_certs` を実行します。 このコマンドを実行すると、次のスクリーンショットのような出力が生成されます。

    ![証明書ファイルの更新](media/log-collector-advanced-tasks/update-certs.png)

1. ターミナル ウィンドウで、`docker exec <collector name> chmod -R 700 /etc/ssl/private/` を実行します。

## <a name="enable-the-log-collector-behind-a-proxy"></a>プロキシの背後にあるログ コレクターを有効にする

ログ コレクターを構成した後、プロキシの背後で実行する場合は、ログ コレクターから Cloud App Security へのデータ送信時に問題が発生する可能性があります。 これが発生する理由として考えられるのは、ログ コレクターがプロキシのルート証明機関を信頼しておらず、Microsoft Cloud App Security に接続してその構成を取得したり、受信したログをアップロードしたりできないことです。

プロキシの背後にあるログ コレクター有効にするには、次の手順に従います。

>[!NOTE]
> Syslog または FTP のログ コレクターによって使用される証明書を変更する方法と、ファイアウォールおよびプロキシからログ コレクターへの接続に関する問題を解決する方法の詳細については、「[ログ コレクターの FTP 構成を変更する](#modify-the-log-collector-ftp-configuration)」を参照してください。
>

### <a name="set-up-the-log-collector-behind-a-proxy"></a>プロキシの背後にあるログ コレクターの設定

Windows または Linux コンピューターで Docker を実行するために必要な手順を完了したことを確認し、コンピューターに Cloud App Security の Docker イメージを正しくダウンロードします。 詳細については、「[継続的なレポートのために自動ログ アップロードを構成する](discovery-docker.md)」を参照してください。

#### <a name="validate-docker-log-collector-container-creation"></a>Docker ログ コレクター コンテナーの作成を検証する

シェルで次のコマンドを使用して、コンテナーが作成されて実行中であることを確認します。

```bash
docker ps
```

![docker ps](media/log-collector-advanced-tasks/docker-1.png)

#### <a name="copy-proxy-root-ca-certificate-to-the-container"></a>プロキシのルート CA 証明書をコンテナーにコピーする

仮想マシンから Cloud App Security コンテナーに CA 証明書をコピーします。 次の例では、コンテナーの名前は *Ubuntu-LogCollector* であり、CA 証明書の名前は *Proxy-CA.crt* です。
Ubuntu ホスト上でコマンドを実行します。 次のように、実行中のコンテナー内のフォルダーに証明書をコピーします。

```bash
docker cp Proxy-CA.crt Ubuntu-LogCollector:/var/adallom/ftp/discovery
```

#### <a name="set-the-configuration-to-work-with-the-ca-certificate"></a>CA 証明書を使用するように構成を設定する

1. 次のコマンドを使用して、コンテナーに移ります。 ログ コレクター コンテナーで bash が開きます。

    ```bash
    docker exec -it Ubuntu-LogCollector /bin/bash
    ```

1. コンテナー内の bash ウィンドウから、Java `jre` フォルダーに移動します。 バージョンに関連するパスのエラーを回避するために、次のコマンドを使用します。

    ```bash
    cd "$(find /opt/jdk/*/jre -name "bin" -printf '%h' -quit)"
    cd bin
    ```

1. 先ほどコピーしたルート証明書を *discovery* フォルダーから Java キーストアにインポートし、パスワードを定義します。 既定のパスワードは "changeit" です。 パスワード変更の詳細については、「[Java キーストアのパスワードを変更する方法](#how-to-change-the-java-keystore-password)」を参照してください。

    ```bash
    ./keytool --import --noprompt --trustcacerts --alias SelfSignedCert --file /var/adallom/ftp/discovery/Proxy-CA.crt --keystore ../lib/security/cacerts --storepass <password>
    ```

1. 次のコマンドを使用して、インポート時に指定したエイリアス (*SelfSignedCert*) を検索し、証明書が CA キーストアに正しくインポートされたことを確認します。

    ```bash
    ./keytool --list --keystore ../lib/security/cacerts | grep self
    ```

    ![keytool](media/log-collector-advanced-tasks/docker-2.png "keytool")

インポートしたプロキシ CA 証明書が表示されます。

#### <a name="set-the-log-collector-to-run-with-the-new-configuration"></a>新しい構成で実行するようにログ コレクターを設定する

これでコンテナーの準備ができました。

ログ コレクターの作成時に使用した API トークンを使って、**collector_config** コマンドを実行します。

![API トークン](media/log-collector-advanced-tasks/docker-3.png "API トークン")

このコマンドを実行するときに、実際の API トークンを指定します。

```bash
collector_config abcd1234abcd1234abcd1234abcd1234 ${CONSOLE} ${COLLECTOR}
```

![構成の更新](media/log-collector-advanced-tasks/docker-4.png "構成の更新")

これでログ コレクターと Cloud App Security の通信ができるようになりました。 データを送信すると、Cloud App Security ポータル上の状態が "**正常**" から "**接続済み**" に変わります。

![状態](media/log-collector-advanced-tasks/docker-5.png "状態")

>[!NOTE]
> ログ コレクターの構成を更新する必要がある場合、たとえばデータ ソースを追加または削除するには、通常はコンテナーを **削除** し、以前の手順を再度行う必要があります。 これを回避するには、Cloud App Security ポータルで生成された新しい API トークンを使用して、*collector_config* ツールを再実行します。

### <a name="how-to-change-the-java-keystore-password"></a>Java キーストアのパスワードを変更する方法

1. Java キーストア サーバーを停止します。

<!-- /opt/jdk/amazon-corretto-8.222.10.1-linux-x64/jre/lib/security -->

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

## <a name="move-the-log-collector-to-a-different-data-partition-on-linux"></a>Linux 上の別のデータ パーティションにログ コレクターを移動する

多くの企業で、別のパーティションにデータを移動する要件が発生します。 以下の手順を使用して、Cloud App Security の Docker ログ コレクター イメージを Linux ホスト上のデータ パーティションに移動します。

以下の手順では、*datastore* という名前のパーティションにデータを移動する方法を説明します。パーティションは既にマウントされていることを前提としています。

> [!NOTE]
> Linux ホストに新しいパーティションを追加して構成する方法については、このガイドでは説明しません。

![Linux パーティションの一覧](media/log-collector-advanced-tasks/move-lc-new-partition-linux-disk-list.png)

1. 次のコマンドを使用して、Docker サービスを停止します。

    ```bash
    service docker stop
    ```

1. 次のコマンドを使用して、ログ コレクターのデータを新しいパーティションに移動します。

    ```bash
    mv /var/lib/docker /datastore/docker
    ```

1. 古い Docker ストレージ ディレクトリ (/var/lib/docker) を削除し、新しいディレクトリ (/datastore/docker) へのシンボリック リンクを作成します。

    ```bash
    rm -rf /var/lib/docker && ln -s /datastore/docker /var/lib/
    ```

1. 次のコマンドを使用して、Docker サービスを開始します。

    ```bash
    service docker start
    ```

1. 必要に応じて、次のコマンドを使用して、ログ コレクターの状態を確認します。

    ```bash
    docker ps
    ```

## <a name="inspect-the-log-collector-disk-usage-on-linux"></a>Linux 上のログ コレクターのディスク使用率を調べる

ログ コレクターのディスク使用率と場所を確認するには、次の手順に従います。

1. 次のコマンドを使用して、ログ コレクターのデータが格納されているディレクトリへのパスを特定します。

    ```bash
    docker inspect <collector_name> | grep WorkDir
    ```

    ![ログ コレクターのディレクトリを特定する](media/log-collector-advanced-tasks/inspect-lc-linux-disk-usage-directory.png)

1. 特定したパスを "/work" サフィックスなしで使用して、ログ コレクターのディスク上のサイズを取得します。

    ```bash
    du -sh /var/lib/docker/overlay2/<log_collector_id>/
    ```

    ![ディスク上のログ コレクターのサイズを取得する](media/log-collector-advanced-tasks/inspect-lc-linux-disk-usage-size.png)

    > [!NOTE]
    > ディスク上のサイズを知る必要があるだけの場合は、次のコマンドを使用できます: `docker ps -s`

## <a name="move-the-log-collector-to-an-accessible-host"></a>アクセス可能なホストにログ コレクターを移動する

規制された環境では、ログ コレクターのイメージがホストされている Docker Hub へのアクセスがブロックされる可能性があります。 その場合、Cloud App Security によってログ コレクターからデータをインポートできなくなります。これはログ コレクターのイメージをアクセス可能なホストに移動することで解決できます。

以下の手順に従って、Docker Hub にアクセスできるコンピューターを使用してログ コレクターのイメージをダウンロードし、移動先のホストにインポートします。

> [!NOTE]
>
> - ダウンロードしたイメージは、プライベート リポジトリにインポートするか、ホストに直接インポートすることができます。 次の手順では、ログ コレクターのイメージを Windows コンピューターにダウンロードした後、WinSCP を使用してログ コレクターを移動先のホストに移動します。
> - ホストに Docker をインストールするには、必要なオペレーティング システムをダウンロードします。
>   - https://download.docker.com/linux/ubuntu
>   - https://download.docker.com/linux/centos/
>   - https://download.docker.com/linux/rhel/
>
> ダウンロードが完了したら、[オフライン インストール ガイド](https://docs.docker.com/engine/install/binaries/)を使用してオペレーティング システムをインストールします。

まずは[ログ コレクターのイメージをエクスポート](#export-the-log-collector-image-from-your-docker-hub)し、次に[イメージを移動先のホストにインポート](#import-and-load-the-log-collector-image-to-your-destination-host)します。

### <a name="export-the-log-collector-image-from-your-docker-hub"></a>Docker Hub からログ コレクターのイメージをエクスポートする

ログ コレクターのイメージが配置されている Docker Hub のオペレーティング システムに関連する手順を使用します。

#### <a name="exporting-the-image-on-linux"></a>Linux でのイメージのエクスポート

1. Docker Hub にアクセスできる Linux コンピューターで、次のコマンドを実行します。 これにより、Docker がインストールされ、ログ コレクターのイメージがダウンロードされます。

    ```bash
    curl -o /tmp/MCASInstallDocker.sh https://adaprodconsole.blob.core.windows.net/public-files/MCASInstallDocker.sh && chmod +x /tmp/MCASInstallDocker.sh; /tmp/MCASInstallDocker.sh
    ```

1. ログ コレクターのイメージをエクスポートします。

    ```bash
    docker save --output /tmp/mcasLC.targ mcr.microsoft.com/mcas/logcollector
    chmod +r /tmp/mcasLC.tar
    ```

    > [!NOTE]
    > **output** パラメーターを使用して、*STDOUT* ではなくファイルに書き込むことが重要です。

1. WinSCP を使用して、Windows コンピューターの `C:\mcasLogCollector\` にログ コレクターのイメージをダウンロードします。

    ![Windows コンピューターにログ コレクターをダウンロードする](media/log-collector-advanced-tasks/move-lc-to-accessible-host-download-linux-winscp.png)

#### <a name="exporting-the-image-on-windows"></a>Windows でのイメージのエクスポート

1. Docker Hub にアクセスできる Windows 10 コンピューターで、[Docker Desktop](https://docs.docker.com/docker-for-windows/install/) をインストールします。

1. ログ コレクターのイメージをダウンロードします。

    ```dos
    docker login -u caslogcollector -p C0llector3nthusiast
    docker pull mcr.microsoft/mcas/logcollector
    ```

1. ログ コレクターのイメージをエクスポートします。

    ```dos
    docker save --output C:\mcasLogCollector\mcasLC.targ mcr.microsoft.com/mcas/logcollector
    ```

    > [!NOTE]
    > **output** パラメーターを使用して、*STDOUT* ではなくファイルに書き込むことが重要です。

### <a name="import-and-load-the-log-collector-image-to-your-destination-host"></a>ログ コレクターのイメージを移動先のホストにインポートして読み込む

次の手順に従って、エクスポートしたイメージを移動先のホストに転送します。

1. ログ コレクターのイメージを移動先のホストの `/tmp/` にアップロードします。

    ![移動先のホストにログ コレクターをアップロードする](media/log-collector-advanced-tasks/move-lc-to-accessible-host-upload-host-winscp.png)

1. 移動先のホストで、次のコマンドを使用して、ログ コレクターのイメージを Docker イメージのリポジトリにインポートします。

    ```bash
    docker load --input /tmp/mcasLC.tar
    ```

    ![ログ コレクターのイメージを Docker リポジトリにインポートする](media/log-collector-advanced-tasks/move-lc-to-accessible-host-import-docker-repo.png)

1. 必要に応じて、次のコマンドを使用してインポートが正常に完了したことを確認します。

    ```bash
    docker image ls
    ```

    ![ログ コレクターのイメージのインポートが成功したことを確認する](media/log-collector-advanced-tasks/move-lc-to-accessible-host-verify-docker-image.png)

    これで、移動先のホストのイメージを使用して[ログ コレクターの作成](discovery-docker.md)に進むことができるようになりました。

## <a name="define-custom-ports-for-syslog-and-ftp-receivers-for-log-collectors-on-linux"></a>Linux 上のログ コレクターの Syslog および FTP レシーバー用のカスタム ポートを定義する

組織によっては、Syslog および FTP サービス用にカスタム ポートを定義する必要があります。
データ ソースを追加すると、Cloud App Security ログ コレクターによって、1 つまたは複数のデータ ソースからトラフィック ログをリッスンするために特定のポート番号が使用されます。

次の表に、レシーバー用の既定のリッスン ポートを一覧表示します。

| レシーバーの種類 | Port |
| --- | --- |
| syslog | \* UDP/514 - UDP/51x<br />\* TCP/601 - TCP/60x |
| FTP | \* TCP/21 |

カスタム ポートを定義するには、次の手順を使用します。

1. Cloud App Security で、設定アイコンをクリックしてから **[ログ コレクター]** をクリックします。

1. **[ログ コレクター]** タブでログ コレクターを追加または編集し、データ ソースを更新した後、ダイアログから実行コマンドをコピーします。

    ![ログ コレクター ウィザードから実行コマンドをコピーする](media/log-collector-advanced-tasks/define-lc-custom-ports-copy-default-run-command.png)

    > [!NOTE]
    > 以下のウィザードで指定されたコマンドを指定されたとおりに使用すると、ログ コレクターはポート 514/udp と 515/udp を使用するように構成されます。
    >
    > ```bash
    > (echo <credentials>) | docker run --name LogCollector1 -p 514:514/udp -p 515:515/udp -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='10.0.0.100'" -e "PROXY=" -e "SYSLOG=true" -e "CONSOLE=machine.us2.portal.cloudappsecurity.com" -e "COLLECTOR=LogCollector1" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    > ```
    >
    > ![ログ コレクター ウィザードの実行コマンド](media/log-collector-advanced-tasks/define-lc-custom-ports-default-run-command.png)

1. ホスト コンピューター上でコマンドを使用する前に、カスタム ポートを使用するようにコマンドを変更します。 たとえば、UDP ポート 414 および 415 を使用するようにログ コレクターを構成するには、次のようにコマンドを変更します。

    ```bash
    (echo <credentials>) | docker run --name LogCollector1 -p 414:514/udp -p 415:515/udp -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='10.0.0.100'" -e "PROXY=" -e "SYSLOG=true" -e "CONSOLE=machine.us2.portal.cloudappsecurity.com" -e "COLLECTOR=LogCollector1" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```

    ![ホストでカスタム コマンドを実行する](media/log-collector-advanced-tasks/define-lc-custom-ports-custom-run-command.png)

    > [!NOTE]
    > Docker のマッピングのみが変更されます。 内部的に割り当てられたポートは変更されないため、ホスト上の任意のリッスン ポートを選択できます。

## <a name="validate-the-traffic-and-log-format-received-by-log-collector-on-linux"></a>Linux 上でログ コレクターが受信したトラフィックとログの形式を検証する

場合によっては、次のような問題の調査が必要になることがあります。

- **ログ コレクターがデータを受信している**:ログ コレクターがアプライアンスから Syslog メッセージを受信していること、およびファイアウォールによってブロックされていないことを確認します。
- **受信したデータのログの形式が正しい**:Cloud App Security で想定されるログの形式とアプライアンスによって送信されるログの形式を比較することによって、ログの形式を検証し、解析エラーのトラブルシューティングを行います。

ログ コレクターが受信したトラフィックを検証するには、次の手順に従います。

1. Docker コンテナーをホストしているサーバーにサインインします。

1. 次の方法のいずれかを使用して、ログ コレクターが Syslog メッセージを受信していることを確認します。

    - *tcpdump*、または同様のコマンドを使用して、ポート 514 のネットワーク トラフィックを分析します。

        ```bash
        tcpdump -Als0 port 514
        ```

        すべてが正しく構成されていれば、アプライアンスからのネットワーク トラフィックが表示されるはずです。

        ![ネットワーク トラフィックを分析する tcpdump コマンド](media/log-collector-advanced-tasks/validate-traffic-and-log-format-tcpdump-analyze-traffic.png)

    - *netcat*、または同様のコマンドを使用して、ホスト コンピューター上のネットワーク トラフィックを分析します。

        1. *netcat* と *wget* をインストールします。

        1. 次のように、サンプル ログをダウンロードし、必要に応じて解凍します。
            1. Cloud App Security ポータルで **[探索]** をクリックした後、 **[スナップショット レポートの作成]** をクリックします。
            1. ログ ファイルのアップロード元にする **[データソース]** を選択します。
            1. **[表示して検証]** をクリックした後、 **[サンプル ログのダウンロード]** を右クリックして、URL アドレスのリンクをコピーします。
            1. **[閉じる]** をクリックします。
            1. **[キャンセル]** をクリックします。

        ```bash
        wget <URL_address_to_sample_log>
        ```

        1. `netcat` を実行して、データをログ コレクターにストリーミングします。

        ```bash
        cat <path_to_downloaded_sample_log>.log | nc -w 0 localhost <datasource_port>
        ```

        コレクターが正しく構成されている場合、ログ データはメッセージ ファイルに表示され、その後すぐに Cloud App Security ポータルにアップロードされます。

    - Cloud App Security Docker コンテナー内の関連ファイルを調べることで、次を行います。
        1. 次のコマンドを使用して、コンテナーにログインします。

        ```bash
        docker exec -it <Container Name> bash
        ```

        1. 次のコマンドを使用して、Syslog メッセージがメッセージ ファイルに書き込まれているかどうかを確認します。

        ```bash
        cat /var/adallom/syslog/<your_log_collector_port>/messages
        ```

        すべてが正しく構成されていれば、アプライアンスからのネットワーク トラフィックが表示されるはずです。

        > [!NOTE]
        > このファイルは、サイズが 40 KB に達するまで書き込みが続けられます。

        ![ネットワーク トラフィックを分析する cat コマンド](media/log-collector-advanced-tasks/validate-traffic-and-log-format-cat-analyze-traffic.png)

1. Cloud App Security の `/var/adallom/discoverylogsbackup` ディレクトリにアップロードされたログを確認します。

    ![アップロードされたログ ファイルを確認する](media/log-collector-advanced-tasks/validate-traffic-and-log-format-review-uploaded-logs.png)

1. ログ コレクターが受信したログの形式を検証するには、`/var/adallom/discoverylogsbackup` に格納されているメッセージを、Cloud App Security の **[ログ コレクターを作成]** ウィザードで指定されているサンプル ログの形式と比較します。

> [!NOTE]
> 独自のサンプル ログを使用したいがアプライアンスへのアクセス権がない場合は、次のコマンドを使用して、*messages* ファイル (ログ コレクターの syslog ディレクトリにあります) の出力をホスト上のローカル ファイルに書き込みます。
>
> ```bash
> docker exec CustomerLogCollectorName tail -f -q /var/adallom/syslog/<datasource_port>/messages > /tmp/log.log
> ```
>
> 出力ファイル (`/tmp/log.log`) を、`/var/adallom/discoverylogsbackup` に格納されているメッセージと比較します。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery の展開](set-up-cloud-discovery.md)

> [!div class="nextstepaction"]
> [ユーザー アクティビティ ポリシー](user-activity-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
