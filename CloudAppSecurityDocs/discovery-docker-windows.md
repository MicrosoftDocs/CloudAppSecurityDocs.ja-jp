---
title: Windows 上の Docker を使用して Cloud App Security の継続的レポートをロールアウトする
description: この記事では、オンプレミス サーバーの Windows 上の Docker を使用して、Cloud App Security の継続的レポートのためにログの自動アップロードを構成する手順について説明します。
ms.date: 11/19/2019
ms.topic: how-to
ms.openlocfilehash: 3fe411948dd2f0fe64917d69047351d835744ac0
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96311810"
---
# <a name="docker-on-windows-on-premises"></a>オンプレミスの Windows 上の Docker

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Windows 上の Docker を使用して、Cloud App Security の継続的レポートに対する自動ログ アップロードを構成できます。

## <a name="prerequisites"></a>[前提条件]

* OS:
  * **Windows 10** (Fall Creators Update)
  * Windows Server **バージョン 1709 以降** (SAC)
  * **Windows Server 2019 (LTSC)**

* ディスク領域: 250 GB

* CPU:2

* RAM:4 GB

* 「[ネットワークの要件](network-requirements.md#log-collector)」で説明されているように、ファイアウォールを設定します

* オペレーティング システムの仮想化を、Hyper-V で有効にする必要があります

> [!IMPORTANT]
>
> * ログを収集するには、ユーザーが Docker にサインインしている必要があります。 Docker ユーザーにサインインしないで切断するよう忠告することをお勧めします。
> * Docker for Windows は、VMWare の仮想化シナリオでは公式にサポートされていません。
> * Docker for Windows は、入れ子になった仮想化のシナリオでは公式にサポートされていません。 入れ子になった仮想化の使用を計画する場合は、[Docker の公式ガイド](https://docs.docker.com/docker-for-windows/troubleshoot/#running-docker-desktop-in-nested-virtualization-scenarios)を参照してください。

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
    ![データ ソースの名前の追加](media/ubuntu1.png)
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

1. 詳細な展開情報が表示されます。 ダイアログ ボックスから実行コマンドを **コピー** します。 クリップボードにコピー アイコン ![クリップボードにコピー アイコン](media/copy-icon.png) を使用できます。 これは後で必要になります。

1. 予想されるデータ ソースの構成を **エクスポート** します。 この構成は、アプライアンスでログのエクスポートをどのように設定するかを示しています。

    ![ログ コレクターを作成する](media/windows7.png)

    > [!NOTE]
    >
    > * 1 つのログ コレクターで複数のデータ ソースを処理できます。
    > * Cloud App Security と通信するようにログ コレクターを構成するときに情報が必要になるため、画面の内容をコピーします。 Syslog を選択した場合、この情報には、Syslog リスナーがリッスンするポートに関する情報が含まれます。
    > * FTP を使用して初めてログ データを送信するユーザーについては、FTP ユーザーのパスワードを変更することをお勧めします。 詳細については、「[FTP のパスワードの変更](log-collector-advanced-management.md#changing-the-ftp-password)」をご覧ください。

### <a name="step-2--on-premises-deployment-of-your-machine"></a>ステップ 2 – マシンのオンプレミス展開

以下の手順では、Windows での展開について説明します。 その他のプラットフォームの展開手順は、少し異なります。

1. Windows コンピューターで管理者として PowerShell ターミナルを開きます。

1. 次のコマンドを実行して、Windows Docker インストーラーの PowerShell スクリプト ファイルをダウンロードします。`Invoke-WebRequest https://adaprodconsole.blob.core.windows.net/public-files/LogCollectorInstaller.ps1 -OutFile (Join-Path $Env:Temp LogCollectorInstaller.ps1)`

    インストーラーが Microsoft によって署名されていることを確認するには、「[インストーラーの署名を検証する](#validate-signature)」を参照してください

1. PowerShell スクリプトの実行を有効にするには、`Set-ExecutionPolicy RemoteSigned` を実行します

1. 次を実行します: `& (Join-Path $Env:Temp LogCollectorInstaller.ps1)`。これにより、Docker クライアントがコンピューターにインストールされます。 ログ コレクター コンテナーがインストールされる間に、コンピューターが 2 回再起動されるため、再度ログインする必要があります。 **Docker クライアントが Linux コンテナーを使用するように設定されていることを確認します。**

1. 各再起動の後、お使いのコンピューターの管理者として PowerShell ターミナルを開き、`& (Join-Path $Env:Temp LogCollectorInstaller.ps1)` を再実行します。

1. インストールが完了する前に、前の手順でコピーした実行コマンドを貼り付ける必要があります。

1. コレクターの構成をインポートして、ホスト コンピューターにコレクターのイメージを展開します。 ポータルに生成される run コマンドをコピーして、構成をインポートします。 プロキシを構成する必要がある場合、プロキシ IP アドレスとポート番号を追加します。 たとえば、プロキシの詳細が 192.168.10.1:8080 の場合、実行コマンドは次のように更新されます。

    ```console
    (echo db3a7c73eb7e91a0db53566c50bab7ed3a755607d90bb348c875825a7d1b2fce) | docker run --name MyLogCollector -p 21:21 -p 20000-20099:20000-20099 -e "PUBLICIP='192.168.1.1'" -e "PROXY=192.168.10.1:8080" -e "CONSOLE=mod244533.us.portal.cloudappsecurity.com" -e "COLLECTOR=MyLogCollector" --security-opt apparmor:unconfined --cap-add=SYS_ADMIN --restart unless-stopped -a stdin -i mcr.microsoft.com/mcas/logcollector starter
    ```

    ![ログ コレクターを作成する](media/windows7.png)

1. 次のコマンドを使用して、コレクターが正常に実行されていることを確認します: `docker logs <collector_name>`

次のメッセージが表示されます: "**正常に完了しました**"

![コレクターが正常に実行されていることを確認する](media/ubuntu8.png)

### <a name="step-3---on-premises-configuration-of-your-network-appliances"></a>手順 3 - ネットワーク アプライアンスのオンプレミス構成

ネットワーク ファイアウォールとプロキシを、ダイアログの指示に従って FTP ディレクトリの専用 Syslog ポートにログが定期的にエクスポートされるように構成します。 次に例を示します。

```console
BlueCoat_HQ - Destination path: \<<machine_name>>\BlueCoat_HQ\
```

### <a name="step-4---verify-the-successful-deployment-in-the-cloud-app-security-portal"></a>手順 4 - Cloud App Security ポータルで正常に展開されたことを確認する

**[ログ コレクター]** の表でコレクターの状態をチェックし、状態が **[接続済み]** であることを確認します。 **[作成済み]** の場合、ログ コレクターの接続と解析が完了していない可能性があります。

![コレクターが正常にデプロイされたことを確認する](media/ubuntu9.png)

**[ガバナンス ログ]** に移動して、ログがポータルに定期的にアップロードされていることを確認することもできます。

展開中に問題が発生した場合は、「[Cloud Discovery のトラブルシューティング](troubleshooting-cloud-discovery.md)」を参照してください。

### <a name="optional---create-custom-continuous-reports"></a>省略可能 - カスタムの継続的レポートを作成する<a name="continuous-reports"></a>

ログが Cloud App Security にアップロードされていることと、レポートが生成されていることを確認します。 確認したら、カスタム レポートを作成します。 Azure Active Directory ユーザー グループに基づいて、カスタム探索レポートを作成できます。 たとえば、マーケティング部門のクラウドの使用状況を確認したい場合は、ユーザー グループのインポート機能を使用してマーケティング グループをインポートします。 次に、このグループのカスタム レポートを作成します。 また、IP アドレス タグや IP アドレスの範囲に基づいてレポートをカスタマイズすることもできます。

1. Cloud App Security ポータルの設定の歯車アイコンの下で、[Cloud Discovery の設定]、 **[継続的レポート]** の順に選択します。
1. **[レポートの作成]** ボタンをクリックし、フィールドに入力します。
1. **[フィルター]** では、データ ソース、[インポートされたユーザー グループ](user-groups.md)、または [IP アドレスのタグと範囲](ip-tags.md)を指定してフィルターすることができます。

    ![カスタムの継続的レポート](media/custom-continuous-report.png)

### <a name="optional---validate-installer-signature"></a>省略可能 - インストーラーの署名を検証する <a name="validate-signature"></a>

Docker のインストーラーが Microsoft によって署名されていることを確認するには:

1. ファイルを右クリックして、 **[プロパティ]** を選択します。
1. **[デジタル署名]** をクリックし、 **[このデジタル署名は問題ありません]** と表示されることを確認します。
1. **Microsoft Corporation** が、 **[署名者名]** に唯一のエントリとして表示されることを確認します。

    ![有効なデジタル署名](media/digital-signature-successful.png)

デジタル署名が有効でない場合は、 **[このデジタル署名は有効ではありません]** と表示されます。

![無効なデジタル署名](media/digital-signature-unsuccessful.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ログ コレクターの FTP 構成を変更する](log-collector-advanced-management.md)

[!INCLUDE [Open support ticket](includes/support.md)]
