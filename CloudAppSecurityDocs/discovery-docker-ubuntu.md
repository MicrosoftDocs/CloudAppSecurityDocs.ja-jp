---
title: オンプレミスの Docker を使用したログの自動アップロードを構成する
description: この記事では、オンプレミス サーバーの Linux 上の Docker を使用して、Cloud App Security での継続的レポートのためにログの自動アップロードを構成する手順について説明します。
ms.date: 12/02/2020
ms.topic: how-to
ms.openlocfilehash: 710afdc9c50ece74d9040b76e8a55d36651df0fd
ms.sourcegitcommit: 53e485ed8460f1123b3b55277fa5991b427b5302
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96512935"
---
# <a name="docker-on-linux-on-premises"></a>オンプレミスの Linux 上の Docker

[!INCLUDE [Banner for top of topics](includes/banner.md)]

オンプレミスの Ubuntu、Red Hat Enterprise Linux (RHEL)、または CentOS サーバー上の Docker を使用して、Cloud App Security での継続的レポートのためにログの自動アップロードを構成できます。

## <a name="prerequisites"></a>[前提条件]

* OS:
  * Ubuntu 14.04、16.04、および 18.04
  * RHEL 7.2 以降
  * CentOS 7.2 以降

* ディスク領域:250 GB

* CPU:2

* RAM:4 GB

* [ネットワークの要件](network-requirements.md#log-collector)に関する記事の説明に従ってファイアウォールを設定する

> [!NOTE]
> 既存のログ コレクターがあり、それを再度デプロイする前に削除したい場合、または単純に削除したい場合は、次のコマンドを実行します。
>
> ```console
> docker stop <collector_name>
> docker rm <collector_name>
> ```

## <a name="log-collector-performance"></a>ログ コレクターのパフォーマンス

ログ コレクターは、1 時間あたり最大 50 GB の容量のログを処理できます。 ログ収集プロセスの主なボトルネックは次のとおりです。

* ネットワーク帯域幅 - ネットワーク帯域幅によって、ログのアップロード速度が決まります。

* 仮想マシンの I/O パフォーマンス - ログ コレクターのディスクにログが書き込まれる速度が決まります。 ログ コレクターには、ログの収集速度を監視して、アップロード速度と比較する安全メカニズムが組み込まれています。 輻輳の場合、ログ コレクターは、ログ ファイルの削除を開始します。 お使いのセットアップにおいて通常 1 時間あたり 50 GB を超える場合は、複数のログ コレクターにトラフィックを分割することをお勧めします。

## <a name="set-up-and-configuration"></a>セットアップと構成  

### <a name="step-1--web-portal-configuration-define-data-sources-and-link-them-to-a-log-collector"></a>手順 1 – Web ポータルの構成: データ ソースを定義してログ コレクターにリンクする

1. **[自動ログ アップロード]** 設定ページにアクセスします。

    1. Cloud App Security ポータルで、設定アイコンをクリックしてから **[ログ コレクター]** をクリックします。

    ![設定アイコン](media/settings-icon.png)

1. ログをアップロードするファイアウォールまたはプロキシそれぞれに対応するデータ ソースを作成します。

    1. **[データ ソースの追加]** をクリックします。  
    ![データ ソースの追加](media/add-data-source.png)
    1. プロキシまたはファイアウォールの **[名前]** を付けます。  
    ![データ ソースの名前](media/ubuntu1.png)
    1. **[ソース]** リストからアプライアンスを選択します。 一覧に表示されていないネットワーク アプライアンスを使用するために **[カスタム ログ形式]** を選択する場合、構成手順の詳細については、[カスタム ログ パーサーの使用](custom-log-parser.md)に関するページを参照してください。
    1. 予想されるログ形式のサンプルとログを比較します。 ログ ファイルの形式がこのサンプルと一致しない場合は、データ ソースを **[その他]** として追加する必要があります。
    1. **[レシーバーの種類]** に **[FTP]** 、 **[FTPS]** 、 **[Syslog – UDP]** 、 **[Syslog – TCP]** 、 **[Syslog – TLS]** のいずれかを設定します。

    > [!NOTE]
    > 多くの場合、セキュリティで保護された転送プロトコル (FTPS および Syslog – TLS) と統合するには、追加の設定またはファイアウォールやプロキシが必要です。

    f. ネットワークのトラフィックを検出するために使用できるログの取得先であるファイアウォールおよびプロキシそれぞれに対して、この手順を繰り返します。 次のことを可能にするために、ネットワーク デバイスごとに専用のデータ ソースを設定することをお勧めします。

    * 調査のために、各デバイスの状態を個別に監視する。
    * デバイスごとに Shadow IT Discovery を探索する (各デバイスが異なるユーザー セグメントによって使用されている場合)。

1. 画面上部の **[ログ コレクター]** タブに移動します。

    1. **[ログ コレクターを追加]** をクリックします。
    1. ログ コレクターに **[名前]** を付けます。
    1. Docker のデプロイに使用するマシンの **ホスト IP アドレス** を入力します。 ホスト名を解決する DNS サーバー (またはそれと同等のもの) がある場合は、ホスト IP アドレスをマシンの名前に置き換えることができます。
    1. コレクターに接続するすべての **データ ソース** を選択し、 **[更新]** をクリックして構成内容を保存します。

    ![接続するデータ ソースの選択](media/ubuntu2.png)

1. 詳細な展開情報が表示されます。 ダイアログ ボックスから実行コマンドを **コピー** します。 クリップボードにコピー アイコンを使用できます。 ![クリップボードにコピー アイコン](media/copy-icon.png)

1. 予想されるデータ ソースの構成を **エクスポート** します。 この構成は、アプライアンスでログのエクスポートをどのように設定するかを示しています。

    ![ログ コレクターを作成する](media/windows7.png)

    > [!NOTE]
    >
    > * 1 つのログ コレクターで複数のデータ ソースを処理できます。
    > * Cloud App Security と通信するようにログ コレクターを構成するときに情報が必要になるため、画面の内容をコピーします。 Syslog を選択した場合、この情報には、Syslog リスナーがリッスンするポートに関する情報が含まれます。
    > * FTP を使用して初めてログ データを送信するユーザーについては、FTP ユーザーのパスワードを変更することをお勧めします。 詳細については、「[FTP のパスワードの変更](log-collector-advanced-management.md#changing-the-ftp-password)」をご覧ください。

### <a name="step-2--on-premises-deployment-of-your-machine"></a>ステップ 2 – マシンのオンプレミス展開

次のステップは、Ubuntu での展開を説明しています。

> [!NOTE]
> サポートされるその他のプラットフォームの展開手順は、少し異なります。

1. Ubuntu マシンでターミナルを開きます。

1. 次のコマンドを使用して、ルート権限に変更します: `sudo -i`

1. ネットワーク内のプロキシをバイパスするには、次の 2 つのコマンドを実行します。

    ```bash
    export http_proxy='<IP>:<PORT>' (e.g. 168.192.1.1:8888)
    export https_proxy='<IP>:<PORT>'
    ```

1. [ソフトウェア ライセンス条項](https://go.microsoft.com/fwlink/?linkid=862492)に同意する場合は、お使いの環境に適したコマンドを実行して古いバージョンをアンインストールし、Docker CE をインストールします。

#### <a name="centos"></a>[CentOS](#tab/centos)

1. 古いバージョンの Docker を削除します: `yum erase docker docker-engine docker.io`
1. Docker エンジンの前提条件をインストールします: `yum install -y yum-utils`
1. Docker リポジトリを追加します:

    ```bash
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    yum makecache
    ```

1. Docker エンジンをインストールします: `yum -y install docker-ce`
1. Docker を起動します

    ```bash
    systemctl start docker
    systemctl enable docker
    ```

1. Docker のインストールをテストします: `docker run hello-world`

#### <a name="red-hat"></a>[Red Hat](#tab/red-hat)

1. 古いバージョンの Docker を削除します: `yum erase docker docker-engine docker.io`
1. Docker エンジンの前提条件をインストールします:

    ```bash
    yum install -y yum-utils
    yum install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.3.7-3.1.el7.x86_64.rpm
    ```

1. Docker リポジトリを追加します:

    ```bash
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    yum makecache
    ```

1. Docker エンジンをインストールします: `yum -y install docker-ce`
1. Docker を起動します

    ```bash
    systemctl start docker
    systemctl enable docker
    ```

1. Docker のインストールをテストします: `docker run hello-world`

#### <a name="ubuntu"></a>[Ubuntu](#tab/ubuntu)

1. 古いバージョンの Docker を削除します: `apt-get remove docker docker-engine docker.io`
1. Ubuntu 14.04 にインストールする場合は、linux-image-extra パッケージをインストールします。

    ```bash
    apt-get update -y
    apt-get install -y linux-image-extra-$(uname -r) linux-image-extra-virtual
    ```

1. Docker エンジンの前提条件をインストールします:

    ```bash
    apt-get update -y
    (apt-get install -y apt-transport-https ca-certificates curl software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - )
    ```

1. apt-key のフィンガープリント UID が docker@docker.com: `apt-key fingerprint | grep uid` であることを確認します
1. Docker エンジンをインストールします:

    ```bash
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    apt-get update -y
    apt-get install -y docker-ce
    ```

1. Docker のインストールをテストします: `docker run hello-world`

---

5. コレクターの構成をインポートして、ホスト コンピューターにコレクターのイメージを展開します。 ポータルに生成される run コマンドをコピーして、構成をインポートします。 プロキシを構成する必要がある場合、プロキシ IP アドレスとポート番号を追加します。 たとえば、プロキシの詳細が 192.168.10.1:8080 の場合、実行コマンドは次のように更新されます。

    ```bash
    (echo 6f19225ea69cf5f178139551986d3d797c92a5a43bef46469fcc997aec2ccc6f) | docker run --name MyLogCollector -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='192.2.2.2'" -e "PROXY=192.168.10.1:8080" -e "CONSOLE=tenant2.eu1-rs.adallom.com" -e "COLLECTOR=MyLogCollector" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```

    ![ログ コレクターを作成する](media/windows7.png)

1. 次のコマンドを使用して、コレクターが正常に実行されていることを確認します: `docker logs <collector_name>`

次のメッセージが表示されます: **Finished successfully!** (正常に完了しました!)
![Docker が正常に実行されていることを確認するコマンド](media/ubuntu8.png)

### <a name="step-3---on-premises-configuration-of-your-network-appliances"></a>手順 3 - ネットワーク アプライアンスのオンプレミス構成

ネットワーク ファイアウォールとプロキシを、ダイアログの指示に従って専用 Syslog ポートまたは FTP ディレクトリにログが定期的にエクスポートされるように構成します。 次に例を示します。

```bash
BlueCoat_HQ - Destination path: \<<machine_name>>\BlueCoat_HQ\
```

### <a name="step-4---verify-the-successful-deployment-in-the-cloud-app-security-portal"></a>手順 4 - Cloud App Security ポータルで正常に展開されたことを確認する

**[ログ コレクター]** の表でコレクターの状態をチェックし、状態が **[接続済み]** であることを確認します。 **[作成済み]** の場合、ログ コレクターの接続と解析が完了していない可能性があります。

![ログ コレクターの正常な展開の確認](media/ubuntu9.png)

**[ガバナンス ログ]** に移動して、ログがポータルに定期的にアップロードされていることを確認することもできます。

または、次のコマンドを使用して、Docker コンテナー内からログ コレクターの状態を確認することもできます。

1. 次のコマンドを使用して、コンテナーにログインします: `docker exec -it <Container Name> bash`
1. 次のコマンドを使用して、ログ コレクターの状態を確認します: `collector_status -p`

展開中に問題が発生した場合は、「[Cloud Discovery のトラブルシューティング](troubleshooting-cloud-discovery.md)」を参照してください。

### <a name="optional---create-custom-continuous-reports"></a>省略可能 - カスタムの継続的レポートを作成する

ログが Cloud App Security にアップロードされていることと、レポートが生成されていることを確認します。 確認したら、カスタム レポートを作成します。 Azure Active Directory ユーザー グループに基づいて、カスタム探索レポートを作成できます。 たとえば、マーケティング部門のクラウドの使用状況を確認したい場合は、ユーザー グループのインポート機能を使用してマーケティング グループをインポートします。 次に、このグループのカスタム レポートを作成します。 また、IP アドレス タグや IP アドレスの範囲に基づいてレポートをカスタマイズすることもできます。

1. Cloud App Security ポータルの設定の歯車アイコンの下で、[Cloud Discovery の設定]、 **[継続的レポート]** の順に選択します。
1. **[レポートの作成]** ボタンをクリックし、フィールドに入力します。
1. **[フィルター]** では、データ ソース、[インポートされたユーザー グループ](user-groups.md)、または [IP アドレスのタグと範囲](ip-tags.md)を指定してフィルターすることができます。

![カスタムの継続的レポート](media/custom-continuous-report.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ログ コレクターの FTP 構成を変更する](log-collector-advanced-management.md)

[!INCLUDE [Open support ticket](includes/support.md)]
