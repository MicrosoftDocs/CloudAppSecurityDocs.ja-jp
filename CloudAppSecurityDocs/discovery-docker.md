---
title: Cloud App Security で継続的なレポートのために自動ログ アップロードを構成する
description: この記事では、Cloud App Security での継続的なレポートのために、自動ログ アップロードを構成する手順について説明します。
ms.date: 7/22/2019
ms.topic: how-to
ms.openlocfilehash: f627ae6c1174e84958a09c1d0dfe0645c63d8dda
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96311572"
---
# <a name="configure-automatic-log-upload-for-continuous-reports"></a>継続的なレポートのために自動ログ アップロードを構成する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

ログ コレクターを使用すると、ネットワークからのログのアップロードを簡単に自動化することができます。 ログ コレクターをネットワーク上で実行すると、Syslog または FTP でログを受け取ります。 各ログは自動的に処理および圧縮されてから、ポータルに送信されます。 ファイルがログ コレクターに FTP 転送された後、FTP ログが Microsoft Cloud App Security にアップロードされます。 Syslog の場合、ログ コレクターに受信されたログがディスクに書き込まれます。 その後、ファイル サイズが 40 KB を超えると、コレクターから Cloud App Security にファイルがアップロードされます。

Cloud App Security にアップロードされたログは、バックアップ ディレクトリに移動されます。 バックアップ ディレクトリには、最後の 20 個のログが格納されます。 新しいログが移動されると、古いログは削除されます。 ログ コレクターのディスク領域がいっぱいになると、空きディスク領域が増えるまで、ログ コレクターでは新しいログが削除されます。 この場合、 **[ログを自動的にアップロード]** 設定の **[ログ コレクター]** タブに警告が表示されます。

自動ログ ファイル収集を設定する前に、想定するログの種類とログが一致していることを確認します。 実際に使うファイルを Cloud App Security で解析できることを確認することをお勧めします。 詳細については、「[Cloud Discovery に対するトラフィック ログの使用](create-snapshot-cloud-discovery-reports.md#log-format)」を参照してください。

> [!NOTE]
>
> * ログが元々の形式で転送されると仮定した場合、Cloud App Security は、SIEM サーバーからログ コレクターへのログの転送をサポートします。 ただし、ログ コレクターをファイアウォールまたはプロキシに直接統合することを強くお勧めします。
> * ログ コレクターでは、アップロード前にデータが圧縮されます。 ログ コレクターの送信トラフィックは、受信したトラフィック ログのサイズの 10% になります。
> * ログ コレクターで問題が発生した場合、データを受信しなくなってから 48 時間経過した後にアラートが送信されます。

## <a name="deployment-modes"></a>展開モード

ログ コレクターでは、次の 2 つの展開モードがサポートされます。

* **コンテナー**:[Windows](discovery-docker-windows.md)、[オンプレミスの Ubuntu](discovery-docker-ubuntu.md)、[Azure の Ubuntu](discovery-docker-ubuntu-azure.md)、[オンプレミスの RHEL](discovery-docker-ubuntu.md)、または CentOS 上で Docker イメージとして実行します。

* **仮想アプライアンス**:Hyper-V または VMware ハイパーバイザーを介してイメージとして実行します (非推奨)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery データでの作業](working-with-cloud-discovery-data.md)
