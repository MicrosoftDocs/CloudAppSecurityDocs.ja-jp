---
title: Cloud App Security の安全な ICAP による外部 DLP 統合
description: この記事では、Cloud App Security と stunnel セットアップで ICAP 接続を構成するために必要な手順について説明します。
ms.date: 07/09/2020
ms.topic: how-to
ms.openlocfilehash: b33c010233c585ea930de9d1ea9cae738c65eebd
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314972"
---
# <a name="external-dlp-integration"></a>外部 DLP 統合

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security は、既存の DLP ソリューションと統合して、オンプレミスとクラウドのアクティビティ全体で一貫性のある統一されたポリシーを維持しながら、これらのコントロールをクラウドに拡張させることができます。 このプラットフォームは、REST API や ICAP など、使いやすいインターフェイスをエクスポートします。Symantec Data Loss Prevention (以前の Vontu Data Loss Prevention) や Forcepoint DLP など、コンテンツ分類システムと統合できます。

統合は標準 ICAP プロトコルを使用して行われます。これは [RFC 3507](https://tools.ietf.org/html/rfc3507) で説明されている http 型のプロトコルです。 データ転送のために ICAP をセキュリティで保護するには、DLP ソリューションと Cloud App Security の間にセキュリティで保護された TLS トンネル (stunnel) を設定する必要があります。 stunnel を構築することで、DLP サーバーと Cloud App Security の間で送信されるデータが TLS で暗号化されます。

本ガイドでは、Cloud App Security と stunnel セットアップで ICAP 接続を構成し、通信を保護するために必要な手順について説明します。

## <a name="architecture"></a>アーキテクチャ

Cloud App Security によってクラウド環境がスキャンされ、ファイル ポリシー構成に基づき、内部 DLP エンジンと外部 DLP のいずれを利用してファイルをスキャンするかどうかが決定されます。 外部 DLP スキャンが適用される場合、ファイルはセキュリティで保護されたトンネルを経由して顧客環境に送信され、そこで ICAP アプライアンスに中継され、DLP 判定が行われます (許可またはブロック)。 応答は stunnel 経由で Cloud App Security に送り返され、ポリシーによって、通知、隔離、共有コントロールなど、後続のアクションを決定するために使用されます。

![stunnel アーキテクチャ](media/icap-architecture-stunnel.png)

Cloud App Security は Azure で実行されるため、Azure でのデプロイによってパフォーマンスが向上します。 ただし、他のクラウドやオンプレミスでの展開など、他の選択肢もあります。 他の環境で展開する場合、待機時間が長く、スループットが低いため、パフォーマンスが低下することがあります。 トラフィックを暗号化するために、ICAP サーバーと stunnel を同じネットワークに展開する必要があります。

## <a name="prerequisites"></a>[前提条件]

Cloud App Security で stunnel 経由でデータを ICAP サーバーに送信するには、Cloud App Security で使用される外部 IP アドレスに DMZ ファイアウォールを開きます。このとき、動的ソース ポート番号を使用します。

1. ソース アドレス:[「アプリを接続する」の「前提条件」](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md#prerequisites)を参照
2. ソース TCP ポート:動的
3. 宛先アドレス: 次の手順で構成する外部 ICAP サーバーに接続されている stunnel の 1 つまたは 2 つの IP アドレス
4. 宛先 TCP ポート:ネットワークで定義されている

> [!NOTE]
> 既定では、stunnel ポート番号は 11344 に設定されます。 これは必要に応じて別のポートに変更できますが、新しいポート番号を必ず書き留めてください。次の手順で入力する必要があります。

## <a name="step-1--set-up-icap-server"></a>ステップ 1:ICAP サーバーを設定する

ICAP サーバーを設定します。ポート番号をメモして、 **[モード]** を **[ブロック]** に設定します。 ブロック モードでは、分類判定を Cloud App Security に戻すように ICAP サーバーが設定されます。

この設定方法については、外部 DLP 製品のマニュアルを参照してください。 例として、「[付録 A: ForcePoint ICAP サーバー セットアップ](#forcepoint)」と「[付録 B: Symantec への展開ガイド](#symantec)」を参照してください。

## <a name="step-2--set-up-your-stunnel-server"></a>ステップ 2:stunnel サーバーを設定する

この手順では、ICAP サーバーに接続される stunnel を設定します。

>[!NOTE]
> この手順は強く推奨されますが、任意です。テスト ワークロードでは省略できます。

### <a name="install-stunnel-on-a-server"></a>サーバーに stunnel をインストールする

**前提条件**

- **サーバー** - Windows Server または Linux サーバー (メジャー ディストリビューション)。

stunnel インストール対応のサーバーの種類については、[stunnel Web サイト](https://www.stunnel.org/index.html)をご覧ください。 Linux を使用している場合は、Linux ディストリビューション マネージャーを使用してインストールできます。

#### <a name="install-stunnel-on-windows"></a>Windows に stunnel をインストールする

1. [最新の Windows Server インストールをダウンロードします](https://www.stunnel.org/downloads.html) (このアプリケーションは、Windows Server のすべての最新エディションで動作します)。 (既定のインストール)

2. インストール中は、新しい自己署名証明書を作成しないでください。 証明書は、後の手順で作成します。

3. **[Start server after installation]\(インストール後にサーバーを起動する\)** をクリックします。

4. 次のいずれかの方法で証明書を作成します。

    - 証明書管理サーバーを使用して、ICAP サーバーで TLS 証明書を作成します。 次に、stunnel インストール用に準備したサーバーにキーをコピーします。
    - あるいは、stunnel サーバーで、次の OpenSSL コマンドを利用して秘密キーと自己署名証明書を生成します。 次の変数を置き換えます。
        - **key.pem** を秘密キーの名前に変更
        - **cert.pem** を証明書の名前に変更
        - **stunnel-key** を新しく作成したキーの名前に変更

5. stunnel インストール パスの下で、config ディレクトリを開きます。 既定では、c:\Program Files (x86)\stunnel\config\ です。
6. 管理者アクセス許可で次のコマンド ラインを実行します。

    ```bash
    ..\bin\openssl.exe genrsa -out key.pem 2048
    ..\bin\openssl.exe  req -new -x509 -config ".\openssl.cnf" -key key.pem -out .\cert.pem -days 1095
    ```

7. cert.pem と key.pem を連結し、ファイルに保存します。 `type cert.pem key.pem >> stunnel-key.pem`

8. [公開キーをダウンロード](https://adaprodconsole.blob.core.windows.net/icap/publicCert.pem)し、**C:\Program Files (x86)\stunnel\config\MCASca.pem** に保存します。

9. Windows ファイアウォールでポートを開くための次の規則を追加します。

    ```console
    rem Open TCP Port 11344 inbound and outbound
    netsh advfirewall firewall add rule name="Secure ICAP TCP Port 11344" dir=in action=allow protocol=TCP localport=11344
    netsh advfirewall firewall add rule name="Secure ICAP TCP Port 11344" dir=out action=allow protocol=TCP localport=11344
    ```

10. `c:\Program Files (x86)\stunnel\bin\stunnel.exe` を実行し、stunnel アプリケーションを開きます。

11. **[構成]** をクリックし、 **[構成の編集]** をクリックします。

    ![Windows Server 構成を編集する](media/stunnel-windows.png)

12. ファイルを開き、次のサーバー構成行を貼り付けます。 **DLP Server IP** は ICAP サーバーの IP アドレスです。**stunnel-key** は前の手順で作成したキーです。**MCASCAfile** は Cloud App Security stunnel クライアントの公開証明書です。 サンプル テキストがあればそれを削除し (例では Gmail テキストが表示されています)、次のテキストをファイルにコピーします。

    ```ini
    [microsoft-Cloud App Security]
    accept = 0.0.0.0:11344
    connect = **ICAP Server IP**:1344
    cert = C:\Program Files (x86)\stunnel\config\**stunnel-key**.pem
    CAfile = C:\Program Files (x86)\stunnel\config\**MCASCAfile**.pem
    TIMEOUTclose = 0
    client = no
    ```

13. ファイルを保存し、 **[構成の再読み込み]** をクリックします。

14. 予想どおり動作していることを確認するには、コマンド プロンプトから次を実行します。 `netstat -nao  | findstr 11344`

#### <a name="install-stunnel-on-ubuntu"></a>Ubuntu に stunnel をインストールする

次の例は Ubuntu サーバー インストールに基づきます。ルート ユーザーとしてサインインしています。他のサーバーの場合、並列コマンドを使用します。

準備したサーバーで、最新バージョンの stunnel をダウンロードしてインストールします。 Ubuntu サーバーで次のコマンドを実行して、stunnel と OpenSSL の両方をインストールします。

```console
apt-get update
apt-get install openssl -y
apt-get install stunnel4 -y
```

コンソールから次のコマンドを実行し、stunnel がインストールされていることを確認します。 バージョン番号と構成オプションの一覧が表示されるはずです。

stunnel-version

### <a name="generate-certificates"></a>証明書を生成する

ICAP サーバーと Cloud App Security では、stunnel 全体でのサーバーの暗号化と認証に秘密キーと公開証明書が使用されます。
stunnel をバックグラウンド サービスとして実行できるように、パス フレーズなしで秘密キーを作成してください。 また、ファイルのアクセス許可を、stunnel 所有者は **読み取り可能** に、その他のユーザーは **なし** に設定してください。

次のいずれかの方法で証明書を作成できます。

- 証明書管理サーバーを使用して、ICAP サーバーで TLS 証明書を作成します。 次に、stunnel インストール用に準備したサーバーにキーをコピーします。
- あるいは、stunnel サーバーで、次の OpenSSL コマンドを利用して秘密キーと自己署名証明書を生成します。
次の変数を置き換えます。
  - **key.pem** を秘密キーの名前に変更
  - **cert.pem** を証明書の名前に変更
  - **stunnel-key** を新しく作成したキーの名前に変更

    ``` console
    openssl genrsa -out key.pem 2048
    openssl req -new -x509 -key key.pem -out cert.pem -days 1095
    cat key.pem cert.pem >> /etc/ssl/private/stunnel-key.pem
    ```

### <a name="download-the-cloud-app-security-stunnel-client-public-key"></a>Cloud App Security stunnel クライアントの公開キーをダウンロードする

https://adaprodconsole.blob.core.windows.net/icap/publicCert.pem から公開キーをダウンロードし、 **/etc/ssl/certs/MCASCAfile.pem** に保存します。

### <a name="configure-stunnel"></a>stunnel を構成する

stunnel 構成は stunnel.conf ファイルで設定されます。

1. 次のディレクトリで stunnel.conf ファイルを作成します。 **vim /etc/stunnel/stunnel.conf**

2. ファイルを開き、次のサーバー構成行を貼り付けます。  **DLP Server IP** は ICAP サーバーの IP アドレスです。**stunnel-key** は前の手順で作成したキーです。**MCASCAfile** は Cloud App Security stunnel クライアントの公開証明書です。

    ```ini
    [microsoft-Cloud App Security]
    accept = 0.0.0.0:11344
    connect = **ICAP Server IP**:1344
    cert = /etc/ssl/private/**stunnel-key**.pem
    CAfile = /etc/ssl/certs/**MCASCAfile**.pem
    TIMEOUTclose = 1
    client = no
    ```

### <a name="update-your-ip-table"></a>IP テーブルを更新する

次のルート ルールで IP アドレス表を更新します。

```bash
iptables -I INPUT -p tcp --dport 11344 -j ACCEPT
```

IP テーブルの更新を永続的にするには、次のコマンドを使用します。

```bash
sudo apt-get install iptables-persistent
sudo /sbin/iptables-save > /etc/iptables/rules.v4
```

### <a name="run-stunnel"></a>stunnel を実行する

1. stunnel サーバーで、次のコマンドを実行します。

    ```bash
    vim /etc/default/stunnel4
    ```

2. 変数 ENABLED を 1 に変更します。

    ```bash
    ENABLED=1
    ```

3. サービスを再起動し、構成を有効にします。

    ```bash
    /etc/init.d/stunnel4 restart
    ```

4. 次のコマンドを実行し、stunnel が正しく動作していることを確認します。

    ```bash
    ps -A | grep stunnel
    ```

    次のコマンドを実行し、正しいポートでリッスンしていることを確認します。

    ```bash
    netstat -anp | grep 11344
    ```

5. stunnel サーバーが展開されたネットワークが前述のネットワーク前提条件に一致していることを確認します。 これは、Cloud App Security からの着信接続がサーバーに正常に到達できるようにするために必要です。

プロセスが終わらない場合、[stunnel マニュアル](https://www.stunnel.org/docs.html)を参照して問題を解決してください。

## <a name="step-3--connect-to-cloud-app-security"></a>ステップ 3:Cloud App Security に接続する

1. Cloud App Security の **[設定]** で、 **[セキュリティ拡張機能]** を選択し、 **[外部 DLP]** タブを選択します。

2. プラス記号をクリックし、新しい接続を追加します。

3. **[Add new external DLP]\(新しい外部 DLP の追加\)** ウィザードに **[接続名]** を入力します (たとえば、「My Forcepoint connector」と入力します)。この名前はコネクタの識別に利用されます。

4. **[接続の種類]** を選択します。
    - **Symantec Vontu** – Vontu DLP アプライアンスにカスタマイズ統合を使用します。
    - **Forcepoint DLP** – Forcepoint DLP アプライアンスにカスタマイズ統合を使用します。
    - **Generic ICAP – REQMOD** - [要求変更](https://tools.ietf.org/html/rfc3507)を使用するその他の DLP アプライアンスを使用します。
    - **Generic ICAP – RESPMOD** - [応答変更](https://tools.ietf.org/html/rfc3507)を使用するその他の DLP アプライアンスを使用します。

        ![Cloud App Security ICAP 接続の種類](media/icap-wizard1.png)

5. 前の手順で生成したパブリック証明書 "cert.pem" を参照して選択し、stunnel に接続します。 **[次へ]** をクリックします。

   > [!NOTE]
   > **[Use secure ICAP]\(安全な ICAP を使用する\)** ボックスを選択し、stunnel ゲートウェイを暗号化することが推奨されます。 テスト目的の場合、または stunnel サーバーを持っていない場合は、このボックスをオフにして、DLP サーバーと直接統合することができます。

6. **[サーバー構成]** 画面で、手順 2 で設定した stunnel サーバーの **[IP アドレス]** と **[ポート]** を指定します。 負荷分散の目的のために、追加サーバーの **[IP アドレス]** と **[ポート]** を構成できます。 指定する IP アドレスは、サーバーの外部静的 IP アドレスになります。

    ![Cloud App Security ICAP 接続 IP アドレスとポート](media/icap-wizard2.png)

7. **[次へ]** をクリックします。 Cloud App Security により、構成したサーバーへの接続がテストされます。 エラーが発生した場合、マニュアルとネットワーク設定を見直してください。 正常に接続されたら、 **[終了]** をクリックします。

8. 次に、この外部 DLP サーバーにトラフィックを送信するために、 **[コンテンツ検査方法]** で **ファイル ポリシー** を作成するときに、作成した接続を選択します。 ファイル ポリシーの作成方法については[こちら](data-protection-policies.md)をご覧ください。

## <a name="appendix-a-forcepoint-icap-server-setup"></a>付録 A:ForcePoint ICAP サーバー セットアップ <a name="forcepoint"></a>

ForcePoint で、次の手順でアプライアンスを設定します。

1. DLP アプライアンスで、 **[展開]**  >  **[システム モジュール]** の順に移動します。

    ![ICAP 展開](media/icap-system-modules.png)

2. **[全般]** タブで **[ICAP サーバー]** が **[有効]** になっていること、 **[ポート]** が **[1344]** に設定されていることを確認します。 また、 **[Allow connection to this ICAP Server from the following IP addresses]\(次の IP アドレスからこの ICAP サーバーへの接続を許可する\)** で **[任意の IP アドレス]** を選択します。

    ![ICAP 構成](media/icap-ip-address.png)

3. HTTP/HTTPS タブで、 **[モード]** を **[ブロック]** に設定します。

    ![ICAP ブロック](media/icap-blocking.png)

## <a name="appendix-b-symantec-deployment-guide"></a>付録 B:Symantec への展開ガイド <a name="symantec"></a>

サポートされている Symantec DLP のバージョンは、11 以降です。

上述のとおり、検出サーバーは、Cloud App Security テナントがあるのと同じ Azure データセンターに展開する必要があります。 検出サーバーは、専用の IPSec トンネルを使用して Enforce Server と同期します。

### <a name="detection-server-installation"></a>検出サーバーのインストール

Cloud App Security で使用する検出サーバーは、標準の Network Prevent for Web サーバーです。 一部の構成オプションでは変更が必要です。

1. **[Trial Mode]\(トライアル モード\)** を無効にします。
    1. **[System]\(システム\)**  >  **[Servers and Detectors]\(サーバーと検出ツール\)** で、対象の ICAP をクリックします。

        ![ICAP ターゲット](media/icap-target.png)

    1. **[Configure]\(構成\)** をクリックします。

        ![ICAP ターゲットの構成](media/configure-icap-target.png)

    1. **[Trial Mode]\(トライアル モード\)** を無効にします。

        ![トライアル モードの無効化ポップアップ](media/icap-disable-trial-mode.png)

2. **[ICAP]**  >  **[Response Filtering]\(応答のフィルタリング\)** で、 **[Ignore Responses Smaller Than]\(次のサイズより小さい応答を無視する\)** の値を 1 に変更します。

3. "application/\*" を **[Inspect Content Type]\(コンテンツの種類の検査\)</em>** のリストに追加します。

    ![コンテンツの種類の検査](media/icap-inspect-content-type.png)

4. **[Save]\(保存\)** をクリックします。

### <a name="policy-configuration"></a>ポリシーの構成

Cloud App Security は、Symantec DLP と共に含まれる全種類の検出ルールにシームレスに対応しているため、既存のルールを変更する必要はありません。 ただし、完全な統合を可能にするには、既存および新規のすべてのポリシーに適用する必要がある構成変更があります。 この変更により、すべてのポリシーに特定の応答ルールが追加されます。

この構成の変更を、お使いの Vontu に追加します。

1. **[Manage]\(管理\)**  >  **[Policies]\(ポリシー\)**  >  **[Response Rules]\(応答ルール\)** の順に移動し、 **[Add Response Rule]\(応答ルールの追加\)** をクリックします。

    ![応答ルールの追加](media/icap-add-response-rule.png)

2. **[Automated Response]\(自動応答\)** が選択されていることを確認して、 **[Next]\(次へ\)** をクリックします。

    ![自動応答](media/icap-automated-response.png)

3. ルールの名前を入力します (この例では、「**Block HTTP/HTTPS (HTTP/HTTPS のブロック)** 」)。 **[Actions]\(アクション\)** で **[Block HTTP/HTTPS]\(HTTP/HTTPS のブロック\)** を選択して、 **[Save]\(保存\)** をクリックします。

    ![HTTP のブロック](media/icap-block-http.png)

作成したルールを既存の任意のポリシーに追加します。

1. 各ポリシーで、 **[Response]\(応答\)** タブに切り替えます。

2. **[Response rule]\(応答ルール\)** ドロップダウンで、先ほど作成したブロック応答ルールを選択します。

3. ポリシーを保存します。

    ![ポリシーでのトライアル モードの無効化](media/icap-add-policy.png)

このルールは、既存のすべてのポリシーに追加する必要があります。

>[!NOTE]
> Symantec vontu を使用して Dropbox からファイルをスキャンすると、CAS ではファイルが次の URL からのものとして自動的に表示されます。 http://misc/filename このプレースホルダー URL は実際にはどこにもつながっていませんが、ログ記録の目的で使用されます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
