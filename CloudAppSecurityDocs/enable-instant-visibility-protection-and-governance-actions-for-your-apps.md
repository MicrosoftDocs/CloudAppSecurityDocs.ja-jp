---
title: アプリを接続して可視化および管理する
description: この記事では、API コネクタを使用して、アプリを組織のクラウド内のアプリに接続するプロセスについて説明します。
ms.date: 07/14/2020
ms.topic: how-to
ms.openlocfilehash: 3b6733e0addabf8db1064ff8b5f4e20a8eb76c93
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314947"
---
# <a name="connect-apps"></a>アプリを接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

アプリ コネクタを使用するとアプリ プロバイダーの API を利用できるため、Microsoft Cloud App Security による接続先アプリの表示および制御がしやすくなります。

Microsoft Cloud App Security では、クラウド プロバイダーによって提供される API が使用されます。 各サービスには、独自のフレームワークがあり、調整、API の制限、動的なタイム シフト API ウィンドウなどの API の制限があります。 Microsoft Cloud App Security はサービスを利用して、API の使用を最適化し、最高のパフォーマンスを実現できるようになりました。 Cloud App Security エンジンは、サービスによって API に適用されるさまざまな制限を考慮して、許可される機能を使用します。 テナント内のすべてのファイルのスキャンなどの一部の操作では、多数の API が必要になるため、長期間にわたって分散されます。 ポリシーによっては、数時間または数日間にわたって実行される場合があります。

## <a name="multi-instance-support"></a>複数インスタンスのサポート

Cloud App Security では、同じ接続されたアプリの複数のインスタンスがサポートされます。 たとえば、Salesforce のインスタンスが複数ある場合 (1 つは営業用、もう 1 つはマーケティング用)、両方を Cloud App Security に接続できます。 同じコンソールからさまざまなインスタンスを管理して、細かいポリシーを作成し、より詳細な調査を行うことができます。 このサポートは、クラウドで検出されたアプリやプロキシで接続されたアプリではなく、API で接続されたアプリにのみ適用されます。

> [!NOTE]
> Office 365 および Azure では、複数インスタンスはサポートされていません。

## <a name="how-it-works"></a>しくみ

Cloud App Security はシステム管理者権限で展開されているため、環境内のすべてのオブジェクトへのフル アクセスができます。

アプリ コネクタのフローは次のとおりです:

1. Cloud App Security は認証のためのアクセス許可をスキャンして保存します。
2. Cloud App Security はユーザー リストを要求します。 この処理を初めて要求した場合は、スキャンが完了するまでにいくらか時間がかかることがあります。 ユーザーのスキャンが完了すると、Cloud App Security はアクティビティとファイルに進みます。 スキャンが開始されるとすぐに、いくつかのアクティビティが Cloud App Security で利用できるようになります。
3. ユーザーの要求が完了すると、Cloud App Security はユーザー、グループ、アクティビティ、ファイルを定期的にスキャンします。 最初のフル スキャンが完了すると、すべてのアクティビティが利用できるようになります。

スキャンする必要があるテナントのサイズ、ユーザーの数、ファイルのサイズと数によっては、この接続にいくらか時間がかかる場合があります。

接続先のアプリに応じて、API 接続で次の項目が有効になります。

- **アカウント情報** - ユーザー、アカウント、プロファイル情報、状態 (中断、アクティブ、無効) グループ、および特権を表示できます。

- **監査証跡** - ユーザー アクティビティ、管理者アクティビティ、サインイン アクティビティを表示できます。

- **データのスキャン** - 定期的 (12 時間ごと) およびリアルタイム (変更が検出されるたびに開始) の 2 つの処理を使用して、非構造化データをスキャンできます。

- **アプリのアクセス許可** - 発行済みトークンとそのアクセス許可を表示できます。

- **アカウント ガバナンス** - ユーザーによる使用の中断やパスワードの取り消しなどを行います。

- **データ ガバナンス** - ファイルの検疫 (ごみ箱のファイルを含む) やファイルの上書きを行います。

- **アプリのアクセス許可のガバナンス** - トークンを削除します。

次の表は、クラウド アプリごとの、アプリのコネクタによって使用できるようになる機能のリストです。

| | AWS | ボックス | ドロップボックス | GCP | G Suite | Office 365 | Okta | Service Now | Salesforce | Webex | Workday |
|-|-|-|-|-|-|-|-|-|-|-|-|
| **アカウントの一覧表示** | ✔ | ✔ | ✔ | G Suite 接続による | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| **グループの一覧表示** | ✔ | ✔ | ✔ | G Suite 接続による | ✔ | ✔ | ✔ | ✔ | ✔ | | プロバイダーはサポートしていません |
| **権限の一覧表示** | | ✔ | ✔ | G Suite 接続による | ✔ | ✔ | プロバイダーはサポートしていません | ✔ | ✔ | ✔ | プロバイダーはサポートしていません |
| **ユーザー ガバナンス** | | ✔ | 近日中にご利用になれます | G Suite 接続による | ✔ | ✔ | | 近日中にご利用になれます | ✔ | 近日中にご利用になれます | プロバイダーはサポートしていません |
| **ログオン アクティビティ** | ✔ | ✔ | ✔ | G Suite 接続による | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| **ユーザーの利用状況** | 適用できません | ✔ | ✔ | ✔ | ✔ - Google Business または Enterprise が必要です | ✔ | ✔ | 一部サポート | Salesforce Shield でサポート | ✔ | ✔ |
| **管理者アクティビティ** | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | 一部サポート | ✔ | ✔ | プロバイダーはサポートしていません |
| **DLP - 定期的なスキャン** | | ✔ | ✔ | 適用できません | ✔ | ✔ | 適用できません | ✔ | ✔ | ✔ | プロバイダーはサポートしていません |
| **DLP - ほぼリアルタイムのスキャン** | | ✔ | | 適用できません | ✔ - Google Business または Enterprise が必要です | ✔ | 適用できません | | | ✔ | プロバイダーはサポートしていません |
| **コントロールの共有** | ✔ | ✔ | ✔ | 適用できません | ✔ | ✔ | 適用できません | 適用できません | | ✔ | プロバイダーはサポートしていません |
| **ファイル ガバナンス** | ✔ | ✔ | ✔ | 適用できません | ✔ | ✔ | 適用できません | | ✔ | | プロバイダーはサポートしていません |
| **アプリのアクセス許可の表示** | 適用できません | プロバイダーはサポートしていません | 対応予定 | 適用できません | ✔ | ✔ | 適用できません | | ✔ | 適用できません | 適用できません |
| **アプリのアクセス許可の取り消し** | 適用できません | プロバイダーはサポートしていません | 近日対応予定 | 適用できません | ✔ | ✔ | 適用できません | | ✔ | 適用できません | 適用できません |
| **Azure Information Protection ラベルの適用** | 適用できません | ✔ | | 適用できません | ✔ | ✔ | 適用できません | | | 適用できません | 適用できません |

## <a name="prerequisites"></a>[前提条件]

- アプリによっては、Cloud App Security によるログ収集や、Cloud App Security コンソールへのアクセスを可能にするために、リストの IP アドレスを許可することが必要な場合があります。 詳細については、「[ネットワークの要件](network-requirements.md)」を参照してください。

- Cloud App Security API の統合によって接続するアプリごとに Cloud App Security 専用の管理サービス アカウントを作成することをお勧めします。

> [!NOTE]
> URL および IP アドレスが変更されたときに更新されるようにするには、「[Office 365 の URL と IP アドレスの範囲](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」で説明されているように RSS を購読します。

アプリ コネクタを使用するには、特定アプリケーションごとに、次に示すものが含まれるかどうかを確認する必要があります。

| アプリ | ライセンスの種類 | ユーザー |
|-----|--------------|------|
| Azure | | グローバル管理者 |
| AWS | | 新しく作成されたユーザー |
| ボックス | Enterprise | 管理者として Box に接続することを強くお勧めします。共同管理者として接続すると、部分的なデータしか表示されません。 共同管理者として接続する場合は、すべての権限を選択してください。 |
| ドロップボックス | Business/Enterprise | 管理者 |
| GitHub | GitHub Enterprise Cloud | Owner |
| GCP | | [GCP 接続の前提条件](connect-google-gcp-to-microsoft-cloud-app-security.md#prerequisites)に関するページを参照してください |
| G Suite | G Suite Business または Enterprise (推奨)<br /><br />G Suite Enterprise (最低必要) | スーパー管理者 |
| Office 365 | | グローバル管理者 |
| Okta | Enterprise (評価版ではない) | 管理者 |
| Salesforce | | 管理者 |
| ServiceNow | Eureka 以降 | 管理者 + RestAPI のロール |
| Webex | | 管理者 + コンプライアンス管理者 |
| Workday | | [Workday 接続の前提条件](connect-workday-to-microsoft-cloud-app-security.md#prerequisites)に関するページを参照してください |

### <a name="expressroute"></a>ExpressRoute

Cloud App Security は Azure に展開され、[ExpressRoute](/azure/expressroute/expressroute-introduction) に完全に統合されます。 検出ログのアップロードを含む、Cloud App Security アプリとのすべての通信、および Cloud App Security に送信されるトラフィックは、ExpressRoute の **パブリック ピアリング** 経由でルーティングされるため、待機時間、パフォーマンス、およびセキュリティが改善されます。 お客様側で設定を行う必要はありません。
パブリック ピアリングの詳細については、「[ExpressRoute 回線とルーティング ドメイン](/azure/expressroute/expressroute-circuit-peerings)」を参照してください。

## <a name="disable-app-connectors"></a>アプリ コネクタを無効にする

> [!NOTE]
>
> - アプリ コネクタを無効にする前に、接続の詳細を用意してください。コネクタを再有効化する場合に必要になります。
> - これらの手順を使用して Azure コネクタを無効にすることはできません。
> - これらのステップを使用してアプリの条件付きアクセス制御アプリとセキュリティ構成アプリを無効にすることはできません。

接続されているアプリを無効にするには

1. **[接続されているアプリ]** ページで、関連する行の 3 つのドットをクリックし、 **[Disable App connector]\(アプリ コネクタを無効にする\)** を選択します。
1. ポップアップで、 **[Disable App connector instance]\(アプリ コネクタ インスタンスを無効にする\)** をクリックして、操作の確認を行います。

無効にすると、コネクタ インスタンスによって、そのコネクタからのデータの使用が停止されます。

## <a name="re-enable-app-connectors"></a>アプリ コネクタを再有効化する

接続されているアプリを再有効化するには:

1. **[接続されているアプリ]** ページで、関連する行の 3 つのドットをクリックし、 **[アプリの編集]** を選択します。 これでコネクタの追加プロセスが開始します。
1. 関連する API コネクタ ガイドの手順に従ってコネクタを追加します。 たとえば、GitHub を再有効化する場合、[GitHub Enterprise Cloud を Cloud App Security に接続する](connect-github-ec-to-microsoft-cloud-app-security.md)方法に関するページにある手順を使用してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]

## <a name="check-out-this-video"></a>こちらのビデオをご覧ください。

> [!div class="nextstepaction"]
> [Microsoft Cloud App Security - REST API とトークン](https://channel9.msdn.com/Shows/Microsoft-Security/Microsoft-Cloud-App-Security--REST-APIs-and-Tokens)