---
title: 継続的レポートのために自動ログ アップロードを構成する - Cloud App Security
description: この記事では、Cloud Discovery の自動レポートを作成するためにログをアップロードする方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 8711209823bdb2ea010dbb734fc67c03561122ed
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881450"
---
# <a name="configure-automatic-log-upload-for-continuous-reports-on-a-virtual-appliance---deprecated"></a>仮想アプライアンスでの継続的なレポートのために自動ログ アップロードを構成する - 非推奨

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!WARNING]
> 柔軟性の高い展開を実現するために、[Docker](discovery-docker.md) を使用してログのアップロードを構成することを強くお勧めします。

## <a name="prerequisites"></a>[前提条件]

- ハイパーバイザー: Hyper-V または VMware
- ディスク領域: 250 GB
- CPU:2
- RAM:4 GB
- [ネットワークの要件](network-requirements.md#log-collector)に関するセクションで説明されているとおりにファイアウォールを設定する

## <a name="log-collector-performance"></a>ログ コレクターのパフォーマンス

ログ コレクターは、1 時間あたり最大 50 GB の容量のログを処理できます。
ログ収集プロセスの主なボトルネックは次のとおりです。

- ネットワーク帯域幅 - ネットワーク帯域幅によって、ログのアップロード速度が決まります。
- 仮想マシンの I/O パフォーマンス - ログ コレクターのディスクにログが書き込まれる速度が決まります。
ログ コレクターには、ログの収集速度を監視して、アップロード速度と比較する安全メカニズムが組み込まれています。 輻輳の場合、ログ コレクターは、ログ ファイルの削除を開始します。 通常、1 時間あたり 50 GB を超える場合は、トラフィックを複数のログ コレクターに分割することをお勧めします。

## <a name="set-up-and-configuration"></a>セットアップと構成

### <a name="step-1--web-portal-configuration-define-data-sources-and-link-them-to-a-log-collector"></a>手順 1 – Web ポータルの構成: データ ソースを定義してログ コレクターにリンクする

1. 自動アップロードの設定ページに移動します。Cloud App Security ポータルで、設定アイコン ![設定アイコン](media/settings-icon.png "設定アイコン") をクリックしてから **[ログ コレクター]** をクリックします。

2. ログをアップロードするファイアウォールまたはプロキシそれぞれに対応するデータ ソースを作成します。

   a. **[データ ソースの追加]** をクリックします。

   b. プロキシまたはファイアウォールの **[名前]** を付けます。

   c. **[ソース]** リストからアプライアンスを選択します。 一覧に表示されていないネットワーク アプライアンスを使用するために **[カスタム ログ形式]** を選択する場合、構成手順の詳細については、[カスタム ログ パーサーの使用](custom-log-parser.md)に関するページを参照してください。

   d. 予想されるログ形式のサンプルとログを比較します。 ログ ファイルの形式がこのサンプルと一致しない場合は、データ ソースを **[その他]** として追加する必要があります。

   e. **[レシーバーの種類]** を **[FTP]** または **[Syslog]** のいずれかに設定します。 **[Syslog]** の場合は、 **[UDP]** 、 **[TCP]** 、または **[TLS]** を選択します。

   f. **[追加]** をクリックして、データ ソースを保存します。 ネットワークのトラフィックを検出するために使用できるログの取得先であるファイアウォールおよびプロキシそれぞれに対して、この手順を繰り返します。

3. 画面上部の **[ログ コレクター]** タブに移動します。

    a. **[ログ コレクターを追加]** をクリックします。

    b. ログ コレクターに **[名前]** を付けます。

    c. コレクターに接続するすべての **[データ ソース]** を選択します。 **[更新]** をクリックし、構成を保存して、アクセス トークンを生成します。

    ![データ ソースの検出](media/discovery-data-sources.png)

    > [!NOTE]
    > - 1 つのログ コレクターで複数のデータ ソースを処理できます。
    > - Cloud App Security と通信するようにログ コレクターを構成するときに使用するため、画面の内容をコピーします。 Syslog を選択した場合、この情報には、Syslog リスナーがリッスンするポートに関する情報が含まれます。
4. [エンドユーザー ライセンス条項](https://go.microsoft.com/fwlink/?linkid=862492)に同意する場合は、[Hyper-V] または [VMWare] をクリックして、新しいログ コレクター仮想マシンを**ダウンロード**します。 次に、ポータルで受け取ったパスワードを使用してファイルを解凍します。

### <a name="step-2--on-premises-deployment-of-the-virtual-machine-and-network-configuration"></a>ステップ 2: 仮想マシンのオンプレミス展開とネットワークの構成

> [!NOTE]
> 次の手順は、Hyper-V での展開について説明したものです。 VM のハイパーバイザーを展開する手順は若干異なります。

1. Hyper-V マネージャーを開きます。

2. **[新規]** を選択してから **[仮想マシン]** を選択し、 **[次へ]** をクリックします。

    ![Hyper-V 仮想マシンの検出](media/discovery-hyperv-virtual-machine.png)

3. 仮想マシンに、たとえば CloudAppSecurityLogCollector01. という **[名前]** を付けてから **[次へ]** をクリックします。

4. **[生成 1]** を選択してから **[次へ]** をクリックします。

5. **[起動メモリ]** を **[4096 MB]** に変更します。

6. この仮想マシンの **[Use Dynamic Memory (動的メモリを使用) ]** をオンにしてから、 **[次へ]** をクリックします。

7. 可能であれば、ネットワークの **[接続]** を選択してから **[次へ]** をクリックします。

8. **[既存の仮想ハード ディスクを使用する]** を選択します。 ダウンロードした Zip ファイルに含まれていた **.vhd** ファイルを選択します。

9. **[次へ]** をクリックしてから、 **[完了]** をクリックします。 マシンが Hyper-V 環境に追加されます。

10. **[仮想マシン]** の表でこのマシンをクリックしてから、 **[スタート]** をクリックします。

11. ログ コレクター仮想マシンに接続して、DHCP アドレスが割り当てられているかどうかを確認します。仮想マシンをクリックして、 **[接続]** を選択します。 サインインのプロンプトが表示されます。 IP アドレスを表示する場合は、ターミナル/SSH ツールを使用して仮想マシンに接続できます。  IP アドレスが表示されない場合は、Hyper-V/VMWare 接続ツールを使用して、前のステップでログ コレクターを作成したときにコピーした資格情報でサインインします。 コマンド `sudo network_config`を実行することで、パスワードを変更し、ネットワーク構成ユーティリティを使用して、仮想マシンを構成することができます。
    > [!NOTE]
    > 仮想マシンは、DHCP サーバーから IP アドレスを取得するように事前に構成されています。 静的 IP アドレス、既定のゲートウェイ、ホスト名、DNS サーバーおよび NTPS を構成する必要がある場合は、**network_config** ユーティリティを使用するか、手動で変更することができます。

この時点で、ログ コレクターはネットワークに接続されているため、Cloud App Security ポータルにアクセスできるようになります。

### <a name="step-3--on-premises-configuration-of-the-log-collection"></a>ステップ 3: ログ収集のオンプレミス構成

初めてログ コレクターにサインインし、ポータルからログ コレクターの構成をインポートする場合は、次の手順を行います。

1. ポータルで提供された対話型の管理者資格情報を使用して SSH 経由でログ コレクターにサインインします (コンソールに初めてログインする場合は、パスワードを変更した後、再度パスワードを変更してサインインする必要があります)。 ターミナル セッションを使用している場合は、ターミナル セッションの再起動が必要になることがあります。 )
2. ログ コレクターの作成時に提供されたアクセス トークンを使用して、コレクターの構成ユーティリティを実行します。 `sudo collector_config <access token>`
3. コンソールのドメイン (例: `contoso.portal.cloudappsecurity.com`) を入力します。これは、Cloud App Security ポータルへのログイン後に表示される URL から入手できます。
4. 構成するログ コレクターの名前を入力します。たとえば、前の図の場合、「**CloudAppSecurityLogCollector01**」または「**NewYork**」と入力します。
5. 次のように、ポータルからログ コレクターの構成をインポートします。

    a. ポータルで提供された対話型の管理者資格情報を使用して SSH 経由でログ コレクターにサインインします。

    b. 次のコマンドで提供されたアクセス トークンを使用して、コレクターの構成ユーティリティを実行します。`sudo collector_config \<access token>`

    c. たとえば、次に示すようなコンソールのドメインを入力します。`contoso.portal.cloudappsecurity.com`

    d. 構成するログ コレクターの名前 (例: `CloudAppSecurityLogCollector01`) を入力します。

### <a name="step-4---on-premises-configuration-of-your-network-appliances"></a>ステップ 4: ネットワーク機器のオンプレミス構成

ネットワーク ファイアウォールとプロキシを、ダイアログの指示に従って FTP ディレクトリの専用 Syslog ポートにログが定期的にエクスポートされるように構成します。以下に例を示します。

`London Zscaler - Destination path: 614`

BlueCoat_HQ - 宛先のパス: \<<machine_name>>\BlueCoat_HQ\

### <a name="step-5---verify-the-successful-deployment-in-the-cloud-app-security-portal"></a>ステップ 5: Cloud App Security ポータルで正常に展開されたことを確認する

**[ログ コレクター]** の表でコレクターの状態をチェックし、状態が **[接続済み]** であることを確認します。 **[作成済み]** の場合、ログ コレクターの接続と解析が完了していない可能性があります。

![ログ コレクターの状態](media/log-collector-status.png)

ガバナンス ログに移動して、ログがポータルに定期的にアップロードされていることを確認します。

展開中に問題が発生した場合は、「[Cloud Discovery のトラブルシューティング](troubleshooting-cloud-discovery.md)」を参照してください。

### <a name="optional---create-custom-continuous-reports"></a>省略可能 - カスタムの継続的レポートを作成する

ログが Cloud App Security にアップロードされ、レポートが生成されていることを確認したら、カスタム レポートを作成できます。 Azure Active Directory ユーザー グループに基づいて、カスタム検出レポートを作成できるようになりました。 たとえば、マーケティング部門のクラウドの使用状況を確認したい場合は、ユーザー グループのインポート機能を使用してマーケティング グループをインポートして、このグループにカスタム レポートを作成できます。 また、IP アドレス タグや IP アドレスの範囲に基づいてレポートをカスタマイズすることもできます。

1. Cloud App Security ポータルの設定の歯車アイコンをクリックし、 **[Cloud Discovery の設定]** 、 **[継続的レポート]** の順に選択します。
2. **[レポートの作成]** ボタンをクリックし、フィールドに入力します。
3. **[フィルター]** では、データ ソース、[インポートされたユーザー グループ](user-groups.md)、または [IP アドレスのタグと範囲](ip-tags.md)を指定してフィルターすることができます。

> [!NOTE]
> すべてのカスタム レポートは、最大 1 GB の圧縮されていないデータに制限されます。 1 GB を超えるデータがある場合は、最初の 1 GB のデータがレポートにエクスポートされます。

![カスタムの継続的レポート](media/custom-continuous-report.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery データでの作業](working-with-cloud-discovery-data.md)

[!INCLUDE [Open support ticket](includes/support.md)]
