---
title: Azure の Docker を使用したログの自動アップロードを構成する
description: この記事では、Azure の Linux 上の Docker を使用して、Cloud App Security での継続的レポートのためにログの自動アップロードを構成する手順について説明します。
ms.date: 06/02/2020
ms.topic: how-to
ms.openlocfilehash: 0e34ebfc6d4afcb8ecf0967ddecc7b8dbd0b885f
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96311878"
---
# <a name="docker-on-linux-in-azure"></a>Azure の Linux 上の Docker

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Azure の Ubuntu、Red Hat Enterprise Linux (RHEL)、または CentOS 上の Docker を使用して、Cloud App Security での継続的レポートのためにログの自動アップロードを構成できます。

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

ログ コレクターでは、最大 10 個のデータ ソースで構成される、1 時間あたり最大 50 GB の容量のログを正常に処理できます。 ログ収集プロセスの主なボトルネックは次のとおりです。

* ネットワーク帯域幅 - ネットワーク帯域幅によって、ログのアップロード速度が決まります。

* 仮想マシンの I/O パフォーマンス - ログ コレクターのディスクにログが書き込まれる速度が決まります。 ログ コレクターには、ログの収集速度を監視して、アップロード速度と比較する安全メカニズムが組み込まれています。 輻輳の場合、ログ コレクターは、ログ ファイルの削除を開始します。 お使いのセットアップにおいて通常 1 時間あたり 50 GB を超える場合は、複数のログ コレクターにトラフィックを分割することをお勧めします。

> [!NOTE]
> 10 個を超えるデータ ソースが必要な場合は、複数のログ コレクターにデータ ソースを分割することをお勧めします。

## <a name="set-up-and-configuration"></a>セットアップと構成  

### <a name="step-1--web-portal-configuration-define-data-sources-and-link-them-to-a-log-collector"></a>手順 1 – Web ポータルの構成: データ ソースを定義してログ コレクターにリンクする

1. **[自動ログ アップロード]** 設定ページにアクセスします。

    1. Cloud App Security ポータルで、設定アイコンをクリックしてから **[ログ コレクター]** をクリックします。

    ![設定アイコン](media/settings-icon.png)

1. ログをアップロードするファイアウォールまたはプロキシそれぞれに対応するデータ ソースを作成します。

    1. **[データ ソースの追加]** をクリックします。  
    ![データ ソースの追加](media/add-data-source.png)
    1. プロキシまたはファイアウォールの **[名前]** を付けます。  
      ![プロキシまたはファイアウォールの名前](media/ubuntu1.png)
    1. **[ソース]** リストからアプライアンスを選択します。 一覧に表示されていないネットワーク アプライアンスを使用するために **[カスタム ログ形式]** を選択する場合、構成手順の詳細については、[カスタム ログ パーサーの使用](custom-log-parser.md)に関するページを参照してください。
    1. 予想されるログ形式のサンプルとログを比較します。 ログ ファイルの形式がこのサンプルと一致しない場合は、データ ソースを **[その他]** として追加する必要があります。
    1. **[レシーバーの種類]** に **[FTP]** 、 **[FTPS]** 、 **[Syslog – UDP]** 、 **[Syslog – TCP]** 、 **[Syslog – TLS]** のいずれかを設定します。

    >[!NOTE]
    >多くの場合、セキュリティで保護された転送プロトコル (FTPS および Syslog – TLS) と統合するには、追加の設定またはファイアウォールやプロキシが必要です。

    f. ネットワークのトラフィックを検出するために使用できるログの取得先であるファイアウォールおよびプロキシそれぞれに対して、この手順を繰り返します。 次のことを可能にするために、ネットワーク デバイスごとに専用のデータ ソースを設定することをお勧めします。

    * 調査のために、各デバイスの状態を個別に監視する。
    * デバイスごとに Shadow IT Discovery を探索する (各デバイスが異なるユーザー セグメントによって使用されている場合)。

1. 画面上部の **[ログ コレクター]** タブに移動します。

    1. **[ログ コレクターを追加]** をクリックします。
    1. ログ コレクターに **[名前]** を付けます。
    1. Docker のデプロイに使用するマシンの **ホスト IP アドレス** を入力します。 ホスト名を解決する DNS サーバー (またはそれと同等のもの) がある場合は、ホスト IP アドレスをマシンの名前に置き換えることができます。
    1. コレクターに接続するすべての **データ ソース** を選択し、 **[更新]** をクリックして構成内容を保存します。  
    ![データ ソースの選択](media/ubuntu2.png)

1. 詳細な展開情報が表示されます。 ダイアログ ボックスから実行コマンドを **コピー** します。 クリップボードにコピー アイコンを使用できます。 ![クリップボードにコピー アイコン](media/copy-icon.png)

1. 予想されるデータ ソースの構成を **エクスポート** します。 この構成は、アプライアンスでログのエクスポートをどのように設定するかを示しています。

    ![ログ コレクターを作成する](media/windows7.png)

    > [!NOTE]
    >
    > * 1 つのログ コレクターで複数のデータ ソースを処理できます。
    > * Cloud App Security と通信するようにログ コレクターを構成するときに情報が必要になるため、画面の内容をコピーします。 Syslog を選択した場合、この情報には、Syslog リスナーがリッスンするポートに関する情報が含まれます。
    > * FTP を使用して初めてログ データを送信するユーザーについては、FTP ユーザーのパスワードを変更することをお勧めします。 詳細については、「[FTP のパスワードの変更](log-collector-advanced-management.md#changing-the-ftp-password)」をご覧ください。

### <a name="step-2--deployment-of-your-machine-in-azure"></a>手順 2 – Azure でのマシンのデプロイ

> [!NOTE]
> 次のステップは、Ubuntu での展開を説明しています。 その他のプラットフォームの展開手順は、少し異なります。

1. ご自身の Azure 環境に新しい Ubuntu マシンを作成します。
1. マシンが起動したら、次の方法でポートを開きます。

    1. マシンのビューで、 **[ネットワーク]** にアクセスし、関連するインターフェイスをダブルクリックして選択します。
    1. **[ネットワーク セキュリティ グループ]** にアクセスして、関連するネットワーク セキュリティ グループを選択します。
    1. **[受信セキュリティ規則]** にアクセスし、 **[追加]** をクリックします。![受信セキュリティ規則の追加](media/ubuntu-azure.png)
    1. 次の規則を ( **[詳細設定]** モードで) 追加します。

    |名前|宛先ポート範囲|Protocol|source|Destination|
    |----|----|----|----|----|
    |caslogcollector_ftp|21|TCP|<アプライアンスの IP アドレスのサブネット>|任意|
    |caslogcollector_ftp_passive|20000-20099|TCP|<アプライアンスの IP アドレスのサブネット>|任意|
    |caslogcollector_syslogs_tcp|601-700|TCP|<アプライアンスの IP アドレスのサブネット>|任意|
    |caslogcollector_syslogs_udp|514-600|UDP|<アプライアンスの IP アドレスのサブネット>|任意|

    ![Ubuntu Azure の規則](media/inbound-rule.png)

1. マシンに戻り、 **[接続]** をクリックして、マシン上のターミナルを開きます。

1. `sudo -i` を使用して、ルート権限に変更します。

1. [ソフトウェア ライセンス条項](https://go.microsoft.com/fwlink/?linkid=862492)に同意する場合は、次のコマンドを実行して、古いバージョンをアンインストールし、Docker CE をインストールします。

    ```bash
    curl -o /tmp/MCASInstallDocker.sh https://adaprodconsole.blob.core.windows.net/public-files/MCASInstallDocker.sh && chmod +x /tmp/MCASInstallDocker.sh; /tmp/MCASInstallDocker.sh
    ```

    ![Ubuntu Azure のコマンド](media/ubuntu-azure-command.png)

1. Cloud App Security ポータルの **[Create new log collector]\(新しいログ コレクターの作成\)** ウィンドウで、ホスティング マシンでコレクターの構成をインポートするためのコマンドをコピーします。

    ![ホスティング マシンでコレクターの構成をインポートするためのコマンドをコピーする](media/windows7.png)

1. コマンドを実行して、ログ コレクターを展開します。

    ```bash
    (echo db3a7c73eb7e91a0db53566c50bab7ed3a755607d90bb348c875825a7d1b2fce) | docker run --name MyLogCollector -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='192.168.1.1'" -e "PROXY=192.168.10.1:8080" -e "CONSOLE=mod244533.us.portal.cloudappsecurity.com" -e "COLLECTOR=MyLogCollector" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```

    ![Ubuntu プロキシ](media/ubuntu-proxy.png)

1. ログ コレクターが正常に実行されていることを確認するには、次のコマンドを実行します: `Docker logs <collector_name>`。 次の結果が得られるはずです:"**正常に完了しました**"

    ![ログ コレクターが正常に実行されていることを確認するコマンド](media/ubuntu8.png)

### <a name="step-3---on-premises-configuration-of-your-network-appliances"></a>手順 3 - ネットワーク アプライアンスのオンプレミス構成

ネットワーク ファイアウォールとプロキシを、ダイアログの指示に従って FTP ディレクトリの専用 Syslog ポートにログが定期的にエクスポートされるように構成します。 次に例を示します。

```bash
BlueCoat_HQ - Destination path: \<<machine_name>>\BlueCoat_HQ\
```

### <a name="step-4---verify-the-successful-deployment-in-the-cloud-app-security-portal"></a>手順 4 - Cloud App Security ポータルで正常に展開されたことを確認する

**[ログ コレクター]** の表でコレクターの状態をチェックし、状態が **[接続済み]** であることを確認します。 **[作成済み]** の場合、ログ コレクターの接続と解析が完了していない可能性があります。

![ログ コレクターでコレクターの状態を確認する](media/ubuntu9.png)

**[ガバナンス ログ]** に移動して、ログがポータルに定期的にアップロードされていることを確認することもできます。

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
