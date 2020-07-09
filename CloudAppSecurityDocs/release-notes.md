---
title: Cloud App Security の新機能
description: この記事は、Cloud App Security の最新リリースの新機能がわかるように頻繁に更新されます。
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/28/2020
ms.topic: overview
ms.service: cloud-app-security
ms.collection: M365-security-compliance
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: ff7ac3fb2a6cda0a411ac02f161ce32f5b037a9e
ms.sourcegitcommit: b15034dd50142afd8e95de22a9232f711b1eae6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85625073"
---
# <a name="whats-new-with-microsoft-cloud-app-security"></a>Microsoft Cloud App Security の新機能

*適用対象:Microsoft Cloud App Security*

この記事は、Cloud App Security の最新リリースの新機能がわかるように頻繁に更新されます。

RSS フィード:ご自身のフィード リーダーに次の URL をコピーして貼り付けることで、このページの更新時に通知を受け取ることができます。`https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Cloud+App+Security%22&locale=en-us`

## <a name="cloud-app-security-release-178"></a>Cloud App Security リリース 178

リリース日: 2020 年 6 月 28 日

- **Google Cloud Platform の新しいセキュリティ構成 (段階的なロールアウト)**  
GCP CIS ベンチマークに基づき、Google Cloud Platform 向けのセキュリティを推奨する目的でマルチクラウド セキュリティ構成を拡張しました。 この新しい機能によって、Cloud App Security をご利用の組織はあらゆるクラウド プラットフォームを対象にコンプライアンス状態を 1 つの画面で監視できます。これには [Azure サブスクリプション](security-config-azure.md)や [AWS アカウント](security-config-aws.md)が含まれますが、新たに [GCP プロジェクト](security-config-gcp.md)が加わりました。

- **新しいアプリ コネクタの一般提供**  
次のアプリ コネクタを Microsoft の一般提供 API コネクタ ポートフォリオに追加しました。組織内におけるアプリの利用状況が把握しやすくなり、制御しやすくなります。
  - [GitHub Enterprise Cloud](protect-github.md)
  - [Google Cloud Platform](protect-gcp.md)
  - [Workday](protect-workday.md)

- **新しいリアルタイム マルウェア検出の一般提供**  
ファイルのアップロードまたはダウンロード時に Microsoft 脅威インテリジェンスを使用して潜在的なマルウェアを検出するように、セッション制御を拡張しました。 新しい検出をすぐに使用できる一般提供が始まりました。潜在的なマルウェアとして識別されたファイルを自動的にブロックするように構成できます。 詳細については、「[アップロード時にマルウェアをブロックする](session-policy-aad.md#block-malware-on-upload)」を参照してください。

- **あらゆる IdP でのアクセス制御とセッション制御強化の一般提供**  
アクセス制御とセッション制御では、任意の ID プロバイダーが設定されている SAML アプリのサポートが一般提供になりました。 これらの制御の構成に関する詳細については、[デプロイに関するこちらのガイド](proxy-deployment-aad.md)を参照してください。

- **リスクの高いコンピューターの調査の機能強化**  
Cloud App Security では、シャドウ IT 検出調査の一環としてリスクの高いコンピューターを特定できます。 このたび、**コンピューター** ページに Microsoft Defender Advanced Threat Protection の**マシンのリスク レベル**を追加しました。組織内でコンピューターを調査するとき、アナリストに与えられる背景情報が増えます。 詳細については、「[Cloud App Security でコンピューターを調査する](wdatp-integration.md#investigate-machines-in-cloud-app-security)」を参照してください。

- **新機能:アプリ コネクタのセルフサービス無効化 (段階的ロールアウト)**  
Cloud App Security で直接、アプリ コネクタを無効にする機能を追加しました。 詳細については、「[アプリ コネクタの無効化](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md#disable-app-connectors)」を参照してください。

<!--
- **Enhanced detection logic: Ransomware activity (gradual rollout)**  
We've updated the detection logic for Ransomware activity to provide improved accuracy and reduced alert volume. For more information about this anomaly detection policy, see [Ransomware activity](anomaly-detection-policy.md#ransomware-activity).

- **New OAuth app policy templates**  
Cloud App Security now provides the following new OAuth app policy templates enabling you to detect potentially malicious apps:

  - **OAuth apps authorized by external users**: Alert when an app was authorized by an external user.
  - **OAuth apps with high permissions and rare community use – Google**: Alert for apps with high permissions and rare community use in Google.
  - **OAuth apps with high permissions and rare community use – Office**: Alert for apps with high permissions and rare community use in Office
  - **OAuth apps with rare community use - Salesforce**: Alert for apps with rare community use in Salesforce.
-->

## <a name="cloud-app-security-release-177"></a>Cloud App Security リリース 177

リリース日: 2020 年 6 月 14 日

- **新しいリアルタイム マルウェア検出 (プレビュー、段階的なロールアウト)**  
ファイルのアップロードまたはダウンロード時に Microsoft 脅威インテリジェンスを使用して潜在的なマルウェアを検出するように、セッション制御を拡張しました。 新しい検出をすぐに使用できるようになりました。これは潜在的なマルウェアとして識別されたファイルを自動的にブロックするように構成できます。 詳細については、「[アップロード時にマルウェアをブロックする](session-policy-aad.md#block-malware-on-upload)」を参照してください。

- **アクセスとセッションの制御のための新しいアクセス トークンのサポート**  
アクセスとセッションの制御に対してアプリをオンボードするときに、アクセス トークンとコードの要求をログインとして扱う機能を追加しました。 トークンを使用するには、設定の歯車アイコンをクリックし、 **[アプリの条件付きアクセス制御]** を選択して、関連するアプリを編集し (3 つの点のメニュー > **[アプリの編集]** )、 **[Treat access token and code requests as app logins]\(アクセス トークンとコードの要求をアプリのログインとして扱う\)** を選択して、 **[保存]** をクリックします。 アプリのオンボードの詳細については、[アプリのオンボードとデプロイ](proxy-deployment-any-app.md)に関するページと[おすすめアプリのデプロイ](proxy-deployment-aad.md)に関するページを参照してください。

- **セッション制御の拡張プロキシ URL サフィックス (段階的なロールアウト)**  
2020 年 6 月 7 日に、名前付きリージョンを含まない 1 つの統合サフィックスを使用する、拡張プロキシ セッション制御の段階的なロールアウトを開始しました。 たとえば、ユーザーには `<AppName>.<Region>.cas.ms` の代わりに `<AppName>.mcas.ms` サフィックスが表示されます。 ネットワーク アプライアンスまたはゲートウェイのドメインを定期的にブラックリストに登録する場合は、「[アクセス制御とセッション制御](network-requirements.md#access-and-session-controls)」に一覧表示されているすべてのドメインをホワイトリストに登録してください。

- **新しいドキュメント**  
Cloud App Security ドキュメントは、次の新しいコンテンツを含むように拡張されています。

  - **[Cloud App Security の REST API を使用する](api-introduction.md)** : API の機能について学習し、アプリケーションと Cloud App Security の統合を開始します。
  - **[異常検出アラートの調査](investigate-anomaly-alerts.md)** : 利用可能な UEBA アラート、それらの意味について理解し、発生するリスクを特定して、侵害の範囲、状況を修復するための措置を把握します。

## <a name="cloud-app-security-release-176"></a>Cloud App Security リリース 176

リリース日: 2020 年 5 月 31 日

- **新しいアクティビティのプライバシー機能**  
アクティビティをプライベートにする機能を使用して監視するユーザーを細かく決定する機能が強化されました。 この新機能を使用すると、アクティビティが既定で非表示になるグループ メンバーシップに基づいてユーザーを指定できます。 承認された管理者のみがこれらのプライベート アクティビティを表示することを選択できます。各インスタンスはガバナンス ログで監査されます。 詳細については、「[アクティビティのプライバシー](activity-privacy.md)」をご覧ください。

- **Azure Active Directory (Azure AD) ギャラリーとの新しい統合**  
Azure AD とのネイティブ統合を活用することで、クラウド アプリ カタログ内のアプリから対応する Azure AD ギャラリーのアプリに直接移動し、それをギャラリー内で管理できるようになりました。 詳細については、[Azure AD ギャラリーを使用したアプリの管理](tutorial-shadow-it.md#gallery-apps)に関する記事をご覧ください。

- **選択したポリシーで新しいフィードバック オプションが利用可能に**  
私たちは、皆様からフィードバックをお寄せいただき、どのように皆様を支援できるか把握したいと考えています。 そこで、ファイル、異常検出、またはセッション ポリシーを作成、変更、または削除するときに、新しいフィードバック ダイアログを利用して Cloud App Security の改善にご協力いただけるようになりました。

- **セッション制御の拡張プロキシ URL サフィックス (段階的なロールアウト)**  
2020 年 6 月 7 日から、名前付きリージョンを含まない 1 つの統合サフィックスを使用する、拡張プロキシ セッション制御が段階的にロールアウトされます。 たとえば、ユーザーには `<AppName>.<Region>.cas.ms` の代わりに `<AppName>.mcas.ms` サフィックスが表示されます。 ネットワーク アプライアンスまたはゲートウェイのドメインを定期的にブラックリストに登録する場合は、「[アクセス制御とセッション制御](network-requirements.md#access-and-session-controls)」に一覧表示されているすべてのドメインをホワイトリストに登録してください。

- **セッション制御のパフォーマンスの向上 (段階的なロールアウト)**  
プロキシ サービスのネットワーク パフォーマンスが大幅に改善されました。 改善されたサービスはさらに合理化され、セッション制御を使用する際の応答性が向上します。

- **新しい危険なアクティビティの検出:失敗した異常なログオン**  
危険な動作を検出する現在の機能を拡張しました。 新しい検出をすぐに使用できるようになりました。これは自動的に有効になり、失敗した異常なログイン試行が特定されるとアラートが送信されます。 失敗した異常なログイン試行は、"*パスワード スプレー*" ブルート フォース攻撃 (*low and slow* 方法とも呼ばれます) を示している可能性があります。 この検出は、ユーザーの[調査の優先順位のスコア](tutorial-ueba.md)全体に影響を与えます。

- **強化されたテーブル エクスペリエンス**  
テーブル列の幅のサイズを変更する機能が追加されました。これにより、列の幅を拡大または縮小して、テーブルの表示方法をカスタマイズおよび改善できるようになりました。 また、元のレイアウトを復元することもできるようになりました。それには、テーブルの設定メニューを選択し、 **[既定の幅]** を選択します。

## <a name="cloud-app-security-release-175"></a>Cloud App Security リリース 175

リリース日: 2020 年 5 月 17 日

- **新しい Shadow IT Discovery と Corrata の統合 (プレビュー)**  
Corrata とのネイティブ統合を追加しました。これにより、アプリの利用状況やアプリ アクセスの制御状況を Shadow IT で確認することができます。 詳細については、「[Cloud App Security と Corrata の統合](corrata-integration.md)」を参照してください。

- **新しい Cloud Discovery ログ パーサー**  
Cloud App Security の Cloud Discovery では、さまざまなトラフィック ログを分析して、アプリの順位付けとスコア付けを行います。 今回、Corrata と Cisco ASA で FirePOWER 6.4 ログ形式がサポートされる組み込みのログ パーサーが Cloud Discovery に追加されました。 サポートされているログ パーサーの一覧については、「[サポートされているファイアウォールとプロキシ](set-up-cloud-discovery.md#supported-firewalls-and-proxies)」をご覧ください。

- **強化されたダッシュボード (段階的ロールアウト)** ポータル デザインを継続的に改善する取り組みの一環として、機能が強化された Cloud App Security ダッシュボードを段階的にロールアウトしています。 このダッシュボードには皆様からのフィードバックを基づいて最新技術を取り入れています。コンテンツやデータを一新しており、使いやすさが向上しています。 詳細については、[強化ダッシュボードの段階的デプロイ](daily-activities-to-protect-your-cloud-environment.md)に関するページをご覧ください。

- **強化されたガバナンス:ユーザーに対するセキュリティ侵害を確認 (異常検出)**  
異常に関するポリシーの現行のガバナンス アクションを拡張し、**ユーザーに対するセキュリティ侵害を確認**を追加しました。疑わしいユーザー活動からご自分の環境を積極的に保護することができます。 詳細については、「[アクティビティ ガバナンス アクション](governance-actions.md#activity-governance-actions)」を参照してください。

## <a name="cloud-app-security-release-173-and-174"></a>Cloud App Security リリース 173 と 174

リリース日: 2020 年 4 月 26 日

- **アラートの新しい SIEM エージェント CEF 形式**  
汎用 SIEM サーバーで使用される CEF ファイルで提供されるアラート情報を強化する取り組みの一環として、形式を拡張し、次のクライアント フィールドを含めました。
  - IPv4 アドレス
  - IPv6 アドレス
  - IP アドレスの場所

    詳細については、「[CEF ファイル形式](siem.md#sample-cloud-app-security-alerts-in-cef-format)」を参照してください。
- **強化された検出ロジック: あり得ない移動**  
あり得ない移動に関する検出ロジックが更新されて、精度が上がり、アラート量が減りました。 この異常検出の詳細については、「[あり得ない移動](anomaly-detection-policy.md#impossible-travel)」を参照してください。

## <a name="cloud-app-security-release-172"></a>Cloud App Security リリース 172

リリース日: 2020 年 4 月 5 日

- **あらゆる IdP でアクセス制御とセッション制御を強化 (プレビュー)**  
アクセス制御とセッション制御では、任意の ID プロバイダーが設定されている SAML アプリがサポートされるようになりました。 この新機能のパブリック プレビューが段階的にロールアウトされています。制御を構成するには、「[デプロイ ガイド](proxy-deployment-aad.md)」を参照してください。
- **ユーザーとコンピューターの新しい匿名化一括解除**  
調査中の 1 つまたは複数のユーザーとコンピューターの匿名化を解除するプロセスを拡張し、簡単にしました。 匿名化の一括解除に関する詳細については、「[データの匿名化のしくみ](cloud-discovery-anonymizer.md#how-data-anonymization-works)」を参照してください。

## <a name="cloud-app-security-release-170-and-171"></a>Cloud App Security リリース 170 と 171

リリース日: 2020 年 3 月 22 日

- **新しい異常検出:クラウド リソースの通常とは異なるリージョン (プレビュー)**  
現在の機能が拡張されて、AWS に関する異常な動作が検出されるようになりました。 すぐに使用できるこの新しい検出は、自動的に有効になり、通常はリソースが作成されない AWS リージョンでそのアクティビティが実行された場合にアラートが生成されます。 多くの場合、攻撃者は組織の AWS クレジットを利用して、暗号化マイニングなどの悪意のあるアクティビティを実行します。 このような異常な動作を検出することは、攻撃を軽減するのに役立ちます。

- **Microsoft Teams 用の新しいアクティビティ ポリシー テンプレート**  
Cloud App Security では、Microsoft Teams での不審なアクティビティの検出を可能にする、次の新しいアクティビティ ポリシー テンプレートを使用できるようになりました。
  - **アクセス レベルの変更 (Teams):** チームのアクセス レベルがプライベートからパブリックに変更されたときにアラートを生成します。
  - **追加された外部ユーザー (Teams):** 外部ユーザーがチームに追加されたときにアラートを生成します。
  - **大量の削除 (Teams):** ユーザーが多数のチームを削除したときにアラートを生成します。

- **Azure Active Directory (Azure AD) Identity Protection の統合**  
Cloud App Security に取り込まれた Azure AD Identity Protection アラートの重要度を制御できるようになりました。 また、**Azure AD の危険なサインイン**の検出をまだ有効にしていない場合は、重要度の高いアラートを取り込むためにこの検出が自動的に有効になります。 詳細については、「[Azure Active Directory Identity Protection の統合](aadip-integration.md)」を参照してください。

## <a name="cloud-app-security-release-169"></a>Cloud App Security リリース 169

リリース日: 2020 年 3 月 1 日

- **Workday の新しい検出**  
Workday の異常な動作に関するアラートを拡張しました。 新しいアラートには、次のユーザーの地理的な場所の検出が含まれます。
  - [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)
  - [頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)
  - [不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)
  - [あり得ない移動](anomaly-detection-policy.md#impossible-travel)

- **拡張された Salesforce ログ コレクション**  
Cloud App Security は、Salesforce の時間単位のイベント ログをサポートするようになりました。 時間単位のイベント ログを使用すると、ユーザー アクティビティをほぼリアルタイムでいち早く監視することができます。 詳細については、[Salesforce の接続](connect-salesforce-to-microsoft-cloud-app-security.md)に関する記事を参照してください。

- **マスター アカウントを使用した AWS セキュリティ構成のサポート**  
Cloud App Security で、マスター アカウントの使用をサポートするようになりました。 マスター アカウントを接続すると、すべてのリージョンのすべてのメンバー アカウントのセキュリティに関する推奨事項を受け取ることができます。 マスター アカウントとの接続の詳細については、「[AWS セキュリティ監査を Cloud App Security に接続する方法](connect-aws-to-microsoft-cloud-app-security.md#how-to-connect-aws-security-configuration-to-cloud-app-security)」を参照してください。

- **最新のブラウザーでのセッション制御のサポート**  
Cloud App Security セッション制御に、Chromium に基づく新しい Microsoft Edge ブラウザーのサポートが追加されました。 最新バージョンの Internet Explorer と以前のバージョンの Microsoft Edge は引き続きサポートされますが、サポートは制限されるため、新しい Microsoft Edge ブラウザーを使用することをお勧めします。

## <a name="cloud-app-security-release-165-166-167-and-168"></a>Cloud App Security リリース 165、166、167、168

リリース日: 2020 年 2 月 16 日

- **Microsoft Defender ATP での承認されていないアプリの新しいブロック**  
Cloud App Security により、Microsoft Defender Advanced Threat Protection (ATP) とのネイティブ統合が拡張されました。 Microsoft Defender ATP のネットワーク保護機能を使用して、承認されていないものとマークされているアプリへのアクセスをブロックできるようになりました。 詳しくは、「[承認されていないクラウドアプリへのアクセスをブロックする](wdatp-integration.md#block-access-to-unsanctioned-cloud-apps)」をご覧ください。

- **OAuth アプリの新しい異常検出**  
現在の機能が拡張されて、悪意のある OAuth アプリの同意が検出されるようになりました。 新しい検出はすぐに使用できて自動的に有効になり、ユーザーの環境内で悪意のある OAuth アプリが承認されるとアラートが発生します。 この検出では、Microsoft のセキュリティ研究と脅威インテリジェンスの専門知識が利用されて、悪意のあるアプリが特定されます。

- **ログ コレクターの更新**  
Docker ベースのログ コレクターは、次の重要な更新で強化されました。

  - コンテナー OS のバージョンのアップグレード

  - Java セキュリティの脆弱性の修正プログラム

  - Syslog サービスのアップグレード

  - 安定性とパフォーマンスの向上

    お使いの環境をこの新しいバージョンにアップグレードすることを強くお勧めします。 詳しくは、[ログ コレクターの展開モード](discovery-docker.md#deployment-modes)に関する記事をご覧ください。

- **ServiceNow New York のサポート**  
Cloud App Security では、ServiceNow の最新バージョン (New York) がサポートされるようになりました。 ServiceNow のセキュリティ保護については、「[ServiceNow を Microsoft Cloud App Security に接続する](connect-servicenow-to-microsoft-cloud-app-security.md)」をご覧ください。

- **強化された検出ロジック: あり得ない移動**  
あり得ない移動に関する検出ロジックが更新されて、対象範囲と精度が向上しました。 この更新の一環として、[会社のネットワークからのあり得ない移動](anomaly-detection-policy.md#impossible-travel)の検出ロジックも更新されました。

- **アクティビティ ポリシーの新しいしきい値**  
アラートの量を管理するのに役立つ[アクティビティ ポリシー](user-activity-policies.md)のしきい値が追加されました。 数日間にわたって大量の一致がトリガーされるポリシーは、自動的に無効になります。 これに関するシステム アラートを受け取った場合は、さらにフィルターを追加してポリシーを絞り込むか、またはレポートのためにポリシーを使用している場合は、代わりにクエリとして保存することを検討してください。

## <a name="cloud-app-security-release-162-163-and-164"></a>Cloud App Security リリース 162、163、および 164

2019 年 12 月 8 日リリース

- **CEF 形式の SIEM アクティビティおよびアラートに変更する**  
Cloud App Security によって SIEM に送信されるアクティビティおよびアラート情報の[ポータル URL 形式 (CS1)](siem.md#sample-cloud-app-security-alerts-in-cef-format) は `https://<tenant_name>.portal.cloudappsecurity.com` に変更され、データセンターの場所は含まれなくなりました。 ポータル URL にパターン一致を使用している顧客は、この変更を反映するようにパターンを更新する必要があります。

## <a name="cloud-app-security-release-160-and-161"></a>Cloud App Security リリース 160 と 161

リリース日: 2019 年 11 月 3 日

- **Azure Sentinel でのデータの検出 (プレビュー)**  
Cloud App Security は、Azure Sentinel と統合されました。 アラートと検出データを Azure Sentinel と共有することで、次のような利点があります。

  - より詳細な分析のために、検出データと他のデータ ソースとの相関関係を有効にする。

  - Power BI で、すぐに使えるダッシュボードを使ってデータを表示したり、独自の視覚化を作成したりする。

  - Log Analytics の保持期間が長くなる。

  詳細については、[Azure Sentinel の統合](siem-sentinel.md)に関する記事をご覧ください。

- **Google Cloud Platform コネクタ (プレビュー)**  
Cloud App Security による IaaS 監視機能は拡張中であり、アマゾン ウェブ サービスと Azure だけでなく、Google Cloud Platform がサポートされるようになりました。 これにより、Cloud App Security ですべての GCP ワークロードをシームレスに接続し、監視できます。 この接続では、次のような、GCP 環境を保護するための一連の強力なツールが提供されます。

  - 管理コンソールと API 呼び出しを通じて実行されるすべてのアクティビティの表示。

  - カスタム ポリシーを作成し、定義済みのテンプレートを使って危険なイベントに対してアラートを生成する機能。

  - 異常検出エンジンは GCP のすべてのアクティビティをカバーしており、あり得ない移動、大量の不審なアクティビティ、新しい国からのアクティビティなど、疑わしい動作を検出すると自動的にアラートが生成されます。

  詳細については、[Microsoft Cloud App Security への Google Cloud Platform の接続](connect-google-gcp-to-microsoft-cloud-app-security.md)に関する記事をご覧ください。

- **新しいポリシー テンプレート**  
Cloud App Security に、Google Cloud Platform のセキュリティ ベスト プラクティスのためのアクティビティ ポリシー テンプレートが新しく組み込まれました。

- **強化された Cloud Discovery ログ パーサー**  
Cloud App Security の Cloud Discovery では、さまざまなトラフィック ログを分析して、アプリの順位付けとスコア付けを行います。 Cloud Discovery の組み込みログ パーサーで、Ironport WSA 10.5.1 ログ形式がサポートされるようになりました。

- **セッション制御のカスタマイズ可能なユーザー ランディング ページ**  
セッション ポリシーが適用されているアプリにユーザーが移動したときに表示されるランディング ページを、管理者がカスタマイズする機能が発表されました。 ご自分の組織のロゴを表示し、表示されるメッセージをカスタマイズできるようになりました。 カスタマイズを開始するには、 **[設定]** ページにアクセスし、 **[Cloud Access App Control]\(クラウド アクセス アプリの制御\)** で **[ユーザーの監視]** を選択します。

- **新しい検出**  

  - **疑わしい AWS ログ サービスの変更 (プレビュー)** : CloudTrail ログ サービスに対してユーザーが変更を加えたときに、アラートを生成します。 たとえば、攻撃者は、その攻撃の痕跡を隠すために、CloudTrail の監査を無効にすることがよくあります。

  - **複数の VM 作成アクティビティ**:ユーザーが、学習済みのベースラインと比較して異常な数の VM 作成アクティビティを実行した場合にアラートが生成されます。 AWS に適用されるようになりました。

## <a name="cloud-app-security-release-159"></a>Cloud App Security リリース 159

リリース日: 2019 年 10 月 6 日

- **新しい Cloud Discovery の ContentKeeper ログ パーサー**  
Cloud App Security の Cloud Discovery では、さまざまなトラフィック ログを分析して、アプリの順位付けとスコア付けを行います。 今回、ContentKeeper のログ形式をサポートする組み込みのログ パーサーが Cloud Discovery に追加されました。 サポートされているログ パーサーの一覧については、「[サポートされているファイアウォールとプロキシ](set-up-cloud-discovery.md#supported-firewalls-and-proxies)」をご覧ください。

- **新しい検出**  
次の新しい異常検出ポリシーは、すぐに使用でき、自動的に有効になります。

  - **疑わしいメール削除アクティビティ (プレビュー)**  
    ユーザーが異常なメール削除アクティビティを実行したときにアラートが生成されます。 このポリシーは、メールを使ったコマンド アンド コントロール通信 (C&C/C2) などの潜在的な攻撃ベクトルによって侵害された可能性のあるユーザーのメールボックスを検出するのに役立ちます。

  - **複数の Power BI レポートの共有 (プレビュー)**  
    ユーザーが、学習済みのベースラインと比較して異常な数の Power BI レポート共有アクティビティを実行した場合にアラートが生成されます。

  - **複数の VM 作成アクティビティ (プレビュー)**  
    ユーザーが、学習済みのベースラインと比較して異常な数の VM 作成アクティビティを実行した場合にアラートが生成されます。 現時点では、Azure に適用されます。

  - **複数のストレージ削除アクティビティ (プレビュー)**  
    ユーザーが、学習済みのベースラインと比較して異常な数のストレージ削除アクティビティを実行した場合にアラートが生成されます。 現時点では、Azure に適用されます。

## <a name="cloud-app-security-release-158"></a>Cloud App Security リリース 158

リリース日: 2019 年 9 月 15 日

- **Cloud Discovery エグゼクティブ レポートの名前をカスタマイズ**  
Cloud Discovery エグゼクティブ レポートにより、組織全体にわたるシャドウ IT の使用状況の概要を得ることができます。 レポートを生成する前に、その名前をカスタマイズできるようになりました。 詳細については、「[Cloud Discovery エグゼクティブ レポートの生成](discovered-apps.md#generate-cloud-discovery-executive-report)」をご覧ください。

- **新しいポリシーの概要レポート**  
Cloud App Security によってポリシーの一致が検出され、定義済みの場合はアラートがログに記録されます。これを使って、お客様のクラウド環境をより深く理解することができます。 お客様は、ポリシーごとに集計されたアラートのメトリックを示す、ポリシーの概要レポートをエクスポートして、ポリシーの監視、理解、およびカスタマイズに役立て、組織の保護を強化できるようになりました。 レポートのエクスポートについて詳しくは、「[ポリシーの概要レポート](control-cloud-apps-with-policies.md#policies-overview-report)」をご覧ください。

## <a name="cloud-app-security-release-157"></a>Cloud App Security リリース 157

リリース日: 2019 年 9 月 1 日

- **リマインダー:TLS 1.0 と 1.1 のサポートは 9 月 8 日に終了します**  
Microsoft は、クラス最高レベルの暗号化を提供するため、すべてのオンライン サービスをトランスポート層セキュリティ (TLS) 1.2 以降に移行しています。 そのため、2019 年 9 月 8 日以降、Cloud App Security では TLS 1.0 と 1.1 がサポートされなくなり、これらのプロトコルを使用した接続はサポートされません。 変更による影響の詳細については、[Microsoft のブログ記事](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/End-of-support-for-TLS-1-0-and-1-1-in-Microsoft-Cloud-App/ba-p/770507)を参照してください。

- **新しい検出 ‐ Microsoft Power BI の疑わしい共有 (プレビュー)**  
新しい Power BI レポートの疑わしい共有ポリシーが既定で利用できるようになり、自動的に有効になっています。これでは、機密である可能性のある Power BI レポートが組織外に不審に共有されている可能性がある場合に、アラートを行います。

- **OAuth アプリの監査の新しいエクスポート機能**  
Cloud App Security では、実行されたアクティビティの包括的な監視および調査を提供できるよう、すべての OAuth 承認アクティビティを監査しています。 現在、特定の OAuth アプリを承認したユーザーの詳細もエクスポートできるので、そのユーザーの追加情報を入手して、さらに分析することできます。

- **強化された Okta のイベント監査**  
Cloud App Security で、Okta によってリリースされた新しいシステム ログ API がサポートされるようになりました。 Okta の接続方法の詳細については、[Okta の接続](connect-okta-to-microsoft-cloud-app-security.md)に関するページを参照してください。

- **Workday コネクタ (プレビュー)**  
Workday 用の新しいアプリ コネクタが利用できるようになりました。 Cloud App Security を Workday に接続して、アクティビティを監視したり、そのユーザーとアクティビティを保護できます。 詳細については、[Workday の接続](connect-workday-to-microsoft-cloud-app-security.md)に関するページをご覧ください。

- **"パスワード ポリシー" のリスク要因の評価の強化**  
クラウド アプリ カタログで、**パスワード ポリシー**のリスク要因をより詳細に評価できるようになりました。 これの情報アイコン上をポイントすると、アプリによって適用される特定のポリシーの詳細を表示できます。

## <a name="cloud-app-security-release-156"></a>Cloud App Security リリース 156

リリース日: 2019 年 8 月 18 日

- **新しい Cloud Discovery ログ パーサー**  
Cloud App Security の Cloud Discovery では、さまざまなトラフィック ログを分析して、アプリの順位付けとスコア付けを行います。 現在 Cloud Discovery には、Stormshield および Forcepoint LEEF のログ形式をサポートする組み込みのログパーサーが含まれています。

- **アクティビティ ログの機能強化**  
Cloud App Security で、環境内のアプリによって実行される未分類のアクティビティをより詳細に把握できるようになりました。 これらのアクティビティは、アクティビティ ログだけでなくアクティビティ ポリシーでも使用できます。 未分類のアクティビティを表示するには、 **[種類]** フィルターで **[指定なし]** を選択します。 アクティビティ フィルターの詳細については、「[アクティビティ フィルターとクエリ](activity-filters-queries.md)」を参照してください。

- **リスクの高いユーザーの調査の機能強化**  
Cloud App Security では、 **[ユーザーとアカウント]** のページに、特定のグループ、アプリ、さらにロールごとにリスクの高いユーザーを特定する機能が用意されています。 **調査の優先順位**のスコアに基づいて、組織内のユーザーを調査することもできます。 詳細については、「[調査の優先順位のスコアを理解する](tutorial-ueba.md#risk-score)」を参照してください。

- **アクティビティ ポリシーの機能強化**  
アクティビティ オブジェクトに基づいてアクティビティ ポリシーのアラートを作成できるようになりました。 たとえば、この機能を使用すると、Azure Active Directory 管理者ロールへの変更に関するアラートを作成できます。 アクティビティ オブジェクトの詳細については、「[アクティビティ フィルター](activity-filters-queries.md#activity-filters)」を参照してください。

## <a name="cloud-app-security-release-155"></a>Cloud App Security リリース 155

リリース日: 2019 年 8 月 4 日

- **新しいポリシー テンプレート**  
Cloud App Security に、AWS のセキュリティ ベスト プラクティスのためのアクティビティ ポリシー テンプレートが新しく組み込まれました。

- **注意: TLS 1.0 と 1.1 のサポートは 9 月 8 日に終了します**  
Microsoft は、クラス最高レベルの暗号化を提供するため、すべてのオンライン サービスをトランスポート層セキュリティ (TLS) 1.2 以降に移行しています。 そのため、2019 年 9 月 8 日以降、Cloud App Security では TLS 1.0 と 1.1 がサポートされなくなり、これらのプロトコルを使用した接続はサポートされません。 変更による影響の詳細については、[Microsoft のブログ記事](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/End-of-support-for-TLS-1-0-and-1-1-in-Microsoft-Cloud-App/ba-p/770507)を参照してください。

- **強化された対話型サインイン アクティビティのロジック (段階的なロールアウト)**  
Azure Active Directory のサインイン アクティビティが対話型であるかどうかを識別する新しいロジックを段階的にロールアウトしています。 新しいロジックでは、Cloud App Security の機能が強化され、ユーザーが開始したサインイン アクティビティのみを表示するようになっています。

## <a name="cloud-app-security-release-154"></a>Cloud App Security リリース 154

リリース日: 2019 年 7 月 21 日

- **任意のアプリの条件付きアクセス制御のオンボードと展開が GA に**  
先月の任意のアプリについてのアプリの条件付きアクセス制御をプレビューしたことにより、非常に多くのフィードバックを受け取り、GA を発表できることを楽しみにしています。 この新機能により、セッションやアクセス ポリシーを処理する Web アプリを展開して強力なリアルタイムの監視と制御ができるようになります。

- **AWS のセキュリティの構成評価**  
Cloud App Security では、お客様の CIS コンプライアンスのアマゾン ウェブ サービス環境のセキュリティ構成の評価を取得し、不足している構成およびセキュリティ制御に関する推奨事項を提供する機能を段階的にロールアウトしています。 この機能により、組織は、接続されているすべての AWS アカウントのコンプライアンス状態を 1 つのビューで監視できます。

- **OAuth アプリの異常検出**  
現在の機能を拡張して、疑わしい OAuth アプリを検出しました。 4 つの新しい検出が、組織で承認されている OAuth アプリのメタデータをプロファイルして、悪意のある可能性があるものを識別するために使用できるようになりました。

## <a name="cloud-app-security-release-153"></a>Cloud App Security リリース 153

リリース日: 2019 年 7 月 7 日

- **Dropbox のサポートの強化**  
Cloud App Security で Dropbox の**ごみ箱**ガバナンス アクションがサポートされるようになりました。このガバナンス アクションは、ファイル ポリシーの一部として、手動または自動で使用できます。
- **アプリのクラウド アクセス制御のための新しいおすすめアプリ**  
以下のおすすめアプリに対するアプリの条件付きアクセス制御の一般提供が開始されました。

    - OneDrive for Business
    - SharePoint Online
    - Azure DevOps
    - Exchange Online
    - Power BI

- **マルウェアと識別されたファイルの承認**  
Cloud App Security では、接続されているアプリのファイルから DLP 公開とマルウェアがスキャンされます。 ファイルがマルウェアとして特定されていても、調査の結果安全性が確認された場合はそれを承認できるようになりました。 承認したファイルはマルウェアの検出レポートから削除され、このファイルに対する今後の一致が抑制されます。 マルウェアの検出について詳しくは、[Cloud App Security の異常検出](anomaly-detection-policy.md)に関するページをご覧ください。

## <a name="cloud-app-security-release-152"></a>Cloud App Security リリース 152

リリース日: 2019 年 6 月 23 日

- **すべてのアプリでのアプリの条件付きアクセス制御の展開 (プレビュー)**  
これまでも[主要なアプリケーション](proxy-intro-aad.md)に対して充実したサポートを提供してきましたが、このたび、ついにアプリの条件付きアクセス制御のサポートがすべての Web アプリに展開されることになりました。 この新機能により、セッションやアクセス ポリシーを処理する Web アプリを展開して強力なリアルタイムの監視と制御ができるようになります。 たとえば、ダウンロードを Azure Information Protection ラベルで保護したり、機密文書のアップロードをブロックしたり、監査を提供したりできます。
- **ポータルのアクティビティの監査**  
Cloud App Security は実行されたアクティビティの包括的な監視と調査を行うために、ポータル内のすべての管理アクティビティの監査を行います。 さらに、特定のユーザーを調査したり、特定のアラートを確認したりする管理者の監査のような追加の調査と分析のために、最大で 90 日間のアクティビティをエクスポートできるようになりました。 ログをエクスポートするには、 **[管理者のアクセス権管理]** 設定ページに移動してください。
- **カスタム セッションが Cloud App Security ポータルからサインアウト**  
指定した期間よりも長くアイドル状態にあるポータルから管理セッションが自動的にサインアウトするように構成できるようになりました。

## <a name="cloud-app-security-release-151"></a>Cloud App Security リリース 151

リリース日: 2019 年 6 月 9 日

- **ハイブリッド UEBA - Azure ATP とのネイティブ統合 (プレビュー)**  
Cloud App Security は Azure ATP とネイティブで統合され、クラウド アプリとオンプレミス ネットワークの両方に ID アクティビティの 1 つのビューが用意されました。 詳細については、「[Azure Advanced Threat Protection integration (Azure Advanced Threat Protection の統合)](aatp-integration.md)」を参照してください。
- **UEBA の機能強化**  
レーダーで検知されない脅威を特定しやすくするために、Cloud App Security では独自のプロファイリングを使用して個々のアクティビティとアラートのリスク スコアを表示できるようになりました。 リスク スコアを使用すると、単体ではアラートをトリガーするほど疑わしくないアクティビティを特定できます。 ただし、Cloud App Security でリスク スコアをユーザーの**調査の優先順位のスコア**に集計することで、危険な行動を特定し、調査に集中することができます。 これらの新機能が、再設計されたユーザー ページで使用できるようになりました。
- **クラウド アプリ カタログに追加された新しいリスク要因**  
クラウド アプリ カタログにディザスター リカバリー プランのリスク要因が追加されたため、クラウド アプリ カタログのアプリのビジネス継続性のサポートを評価できるようになりました。
- **Microsoft Flow コネクタの一般提供**  
昨年、プレビュー段階の Microsoft Cloud App Security で Microsoft Flow コネクタがサポートされ、現在、このコネクタは一般提供になりました。
- **ファイル ポリシーの自動ガバナンスの強化**  
Cloud App Security で、ファイル ポリシーの**ごみ箱**ガバナンス アクションの構成がサポートされるようになりました。このガバナンス アクションを利用すると、ファイルをごみ箱フォルダーに自動的に移動することができます。
- **Google ドライブのサポートの強化**  
Cloud App Security で、Google ドライブの**ごみ箱**ガバナンス アクションがサポートされるようになりました。このガバナンス アクションを利用すると、Google ドライブのファイルをごみ箱フォルダーに移動することができます。
- **アプリ管理者とグループ管理者の役割に対する新しいアクセス許可**  
"*アプリ/インスタンス管理者*" と "*ユーザー グループ管理者*" の役割は読み取り専用アクセスをサポートするようになりました。
- **レガシ認証のサインイン アクティビティ (段階的なロールアウト)**  
Cloud App Security で、ActiveSync などの従来のプロトコルを使用する Azure Active Directory のサインイン アクティビティが表示されるようになりました。 これらのサインイン アクティビティは、アクティビティ ログに表示され、ポリシーの構成時に使用できます。

## <a name="cloud-app-security-release-150"></a>Cloud App Security リリース 150

リリース日: 2019 年 5 月 26 日

- **アラートのエクスポートの機能強化**  
**[アラート]** ページから CSV にアラートをエクスポートするとき、そのアラートが解決または無視された日付が結果に追加されるようになりました。

## <a name="cloud-app-security-release-148-and-149"></a>Cloud App Security リリース 148 と 149

リリース日: 2019 年 5 月 12 日

- **Webex アプリ コネクタの使用**  
Cisco Webex Teams の新しいアプリ コネクタがパブリック プレビューで使用できるようになりました。 Microsoft Cloud App Security を Cisco Webex Teams と接続して、そのユーザー、アクティビティ、およびファイルを監視および保護できるようになりました。 詳細については、[Webex の接続](connect-webex-to-microsoft-cloud-app-security.md)に関するページをご覧ください

- **Microsoft データ分類サービスの新しい場所**  
[Microsoft データ分類サービス](dcs-inspection.md)が、4 つの新しい場所で利用できるようになりました。オーストラリア、インド、カナダ、日本です。 ご自身の Office テナントがこれらの場所にある場合は、Microsoft Cloud App Security のファイル ポリシーのコンテンツ検査方法として Microsoft データ分類サービスを利用できるようになりました。

- **シャドウの PaaS と IaaS の検出**  
Microsoft Cloud App Security の Cloud Discovery 機能が拡張されました。Microsoft Azure、アマゾン ウェブ サービス、Google Cloud Platform などの IaaS および PaaS ソリューション上でホストされるリソースに対して、シャドウ IT も提供されるようになりました。 Cloud Discovery では、IaaS や PaaS 上で実行されるカスタム アプリや、作成されるストレージ アカウントなどを確認できるようになりました。 この新しい機能を使用して、どのようなリソースが存在するか、誰がそれらにアクセスしているか、および転送されるトラフィックの量を検出します。

- **アプリの構成証明**  
Microsoft Cloud App Security のコンプライアンスとリスク評価では、クラウド プロバイダーが、各自のアプリがクラウド アプリ カタログで最新であることを証明できるようになりました。 このパイロットにより、クラウド プロバイダーは、クラウド アプリ カタログのリスク属性に基づいて自分の構成証明アンケートに記入し、Cloud App Security での各自のリスク評価が正確かつ最新であることを確認できます。 次に、ユーザーは、どのリスク属性がプロバイダーによって証明されたか (Cloud App Security チームによる評価ではなく)、および各属性はいつプロバイダーによって送信されたかに関する表示を取得できます。 詳細については、「[アプリを証明する](attest-your-app.md)」をご覧ください。

- **Office 365 ワークロードの細分性**  
Office 365 を Microsoft Cloud App Security に接続するときに、どのワークロードを接続したいか制御できるようになりました。 たとえば、アクティビティの監視用にのみ Office 365 の接続に関心があるお客様は、接続プロセス中に、または既存の Office 365 コネクタを編集することで、これを行えるようになりました。 この変更の一環として、OneDrive と SharePoint Online は個別のコネクタとして表示されるのではなく、"_Office 365 ファイル_" ワークロードとして Office 365 コネクタに含まれるようになります。 既存の Office 365 コネクタを使っているお客様は、この変更の影響を受けません。

- **Teams のサポートの強化**  
機密性の高いコンテンツに基づいてセッション ポリシーを構成することで、Teams Web アプリでのメッセージ送信をリアルタイムで監視およびブロックできるようになりました。

## <a name="cloud-app-security-release-147"></a>Cloud App Security リリース 147

リリース日: 2019 年 4 月 14 日

- **新しい Cloud Discovery ログ パーサー**  
Cloud App Security の Cloud Discovery に、Palo Alto LEEF ログ形式をサポートする組み込みのログ パーサーが含まれるようになりました。

- **セッション ポリシーの更新**  
  - **セッション ポリシーの追加のコンテンツ検査方法**:セッション ポリシーを設定するときに、ファイルのコンテンツ検査方法として、データ分類サービスを選択できるようになりました。 データ分類サービスでは、広範囲の機密の種類が組み込みでユーザーに提供され、機密情報を識別するために使用できます。
  - **セッション ポリシーでのファイルのアクセス許可の制御の強化**:Cloud App Security を使ってダウンロードを制御するセッション ポリシーを作成する場合、自分のクラウド アプリからのダウンロードに関して、ドキュメントに対してユーザーごとにアクセス許可 (読み取り専用など) を自動的に適用できるようになりました。 これにより、柔軟性のレベルが大きく上がり、事前に構成された企業のラベルを超えて情報を保護できるようになります。
  - **大きなファイルのダウンロードの制御**:セッション ポリシーでコンテンツ検査が有効になっている場合、ユーザーが非常に大きなファイルをダウンロードしようとしたときの動作を制御できるようになりました。 ダウンロード時にスキャンするにはファイルが大きすぎる場合は、それをブロックするか、許可するかを選択できます。

## <a name="cloud-app-security-release-146"></a>Cloud App Security リリース 146

リリース日: 2019 年 3 月 31 日

- **あり得ない移動に関する強化**  
隣接する国専用のサポートによって、あり得ない移動の検出が強化されました。
- **汎用 CEF パーサーの追加属性のサポート**  
汎用 CEF 形式の Cloud Discovery ログ パーサー サポートが強化され、追加の属性がサポートされるようになりました。
- **Cloud Discovery レポートに対するアクセスの範囲指定**  
検出管理者ロールに加え、特定の検出レポートに対するアクセスを範囲指定できます。 この機能強化によって、特定のサイトや業務部門のデータに対するアクセス許可を構成できるようになります。
- **新しいロールのサポート:グローバルな閲覧者**  
Microsoft Cloud App Security で、Azure AD のグローバルな閲覧者ロールがサポートされるようになりました。 グローバルな閲覧者は、Microsoft Cloud App Security の全面的な読み取り専用アクセスを保持しますが、設定の変更やアクションの実行はできません。

## <a name="cloud-app-security-release-145"></a>Cloud App Security リリース 145

リリース日: 2019 年 3 月 17 日

- **Microsoft Defender ATP 統合が GA になりました**  
昨年、組織内のシャドウ IT の検出が向上し、会社のネットワークを超えて拡張される、[Windows Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Microsoft-Cloud-App-Security-and-Windows-Defender-ATP-better/ba-p/263265) との統合が発表されました。 [1 回のクリックで有効になる](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RWtNmG)この独自の統合が、一般提供されるようになりました。
- **Dynamics 365 CRM のサポート**  
Cloud App Security に Dynamics 365 CRM のリアルタイムな監視と制御が追加され、ビジネス アプリケーションとそのアプリ内に格納された機密コンテンツを保護できるようになりました。 Dynamics 365 CRM で実行できる操作の詳細については、[こちらの記事](proxy-intro-aad.md#how-it-works)を参照してください。

## <a name="cloud-app-security-release-144"></a>Cloud App Security リリース 144

リリース日: 2019 年 3 月 3 日

- **ハイブリッド環境用の統一された SecOps 調査**  
多くの組織にハイブリッド環境があるため、攻撃はクラウド内で始まってからオンプレミスにピボットします。つまり、SecOps チームは複数の場所からこれらの攻撃を調査する必要があります。 Microsoft Cloud App Security、Azure ATP、Azure AD Identity Protection など、クラウドとオンプレミスのソースからの信号を組み合わせることによって、単一のコンソールに統合された ID とユーザー情報が提供され、セキュリティ アナリストはセキュリティ ソリューションを切り替える必要がなくなります。 これにより、SecOps チームは、より多くの時間と適切な情報が得ることができ、より適切な決定を下し、ID に対する実際の脅威とリスクに積極的に対処できます。 詳細については、「[ハイブリッド環境用の統一された SecOps 調査](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Unified-SecOps-Investigation-for-Hybrid-Environments/ba-p/360850)」を参照してください。

- **マルウェア検出のためのサンドボックス化機能** (段階的ロールアウト)  
Cloud App Security のマルウェア検出機能が拡張され、高度なサンドボックス化テクノロジによってゼロデイ マルウェアを識別できるようになります。  
この機能の一部として、Cloud App Security では疑わしいファイルが自動的に識別され、ファイルに悪意のある意図 (マルウェア) があることを示す疑わしいファイルの動作とインジケーターを探すよう示されます。
この変更の一環として、マルウェア検出ポリシーに、脅威インテリジェンスとサンドボックス化によってフィルター処理できる [検出の種類] フィールドが含まれるようになりました。

- **条件付きアクセスの更新**  
アプリの条件付きアクセス制御に、次のアクティビティを監視およびブロックする機能が追加されました。
  - 任意のアプリでのファイルのアップロード - 既知のマルウェア拡張のアップロードを防止し、ユーザーがアップロードの前に AIP でファイルを保護できるようにします。
  - 任意のアプリでのコピーと貼り付け - ダウンロード、印刷、共有などのカスタム アクティビティの制御が既に含まれていたデータ流出の堅牢な制御を完全なものにします。
  - メッセージの送信 - Slack、Salesforce、Workplace by Facebook などの一般的なコラボレーション ツールで、パスワードなどの PII データが共有されないようにします。
  - セッション ポリシーには組み込みテンプレートが含まれるようになっており、組織では、**リアルタイムのコンテンツ検査に基づくアップロードのブロック**など、承認されたアプリに対する一般的なリアルタイムの監視と制御を簡単に有効にすることができます。

## <a name="cloud-app-security-release-143"></a>Cloud App Security リリース 143

リリース日: 2019 年 2 月 17 日

- **アプリ インスタンスの展開のスコープ設定**  
スコープ付きの展開をアプリ インスタンス レベルで構成できるようになり、粒度と制御をさらに高めることができます。
- **ロールの機能強化**  
  - データ管理者とセキュリティ オペレーターの Office 365 ロールが、Cloud App Security でサポートされるようになりました。 データ管理者ロールのユーザーは、ファイルに関連するすべてのことを管理したり、Cloud Discovery レポートを表示したりできます。 セキュリティ オペレーターには、アラートを管理し、ポリシーの構成を表示するアクセス許可があります。
  - セキュリティ閲覧者ロールは、SIEM エージェントを構成できるようになり、アクセス許可のスコープ設定が向上しています。

- **Microsoft Flow のサポート**  
Cloud App Security で Microsoft Flow 内のユーザー アクティビティを監視できるようになりました。 Flow によって Office 365 の監査ログに報告されるアクティビティがサポートされます。

- **アラート エンティティのグループ化**  
調査を支援するために、 **[アラート]** ページで、アラートに関係していた関連エンティティがグループ化されるようになりました。

## <a name="cloud-app-security-release-142"></a>Cloud App Security リリース 142

リリース日: 2019 年 2 月 3 日

- **Azure AD でのセッション ポリシーの構成**  
Azure AD 条件付きアクセスで直接セッション ポリシーを構成し、ユーザーを監視したり、リアルタイムでダウンロードをブロックしたりできるようになりました。 Cloud App Security で、高度なセッション ポリシーを直接構成することもできます。 この展開の手順については、[Azure AD アプリに対するアプリの条件付きアクセス制御の展開](proxy-deployment-aad.md)に関する記事をご覧ください。

- **OAuth アプリのクエリ候補と保存されたクエリ**  
推奨されるクエリが OAuth アプリのページに追加されました。OAuth アプリをフィルター処理するためのすぐに使用できる調査用テンプレートが用意されています。 推奨されるクエリには、管理者が承認したアプリなど、危険なアプリを識別するためのカスタム フィルターが含まれています。 保存されたクエリを使用すると、カスタム クエリを保存して後で使用できます。これは、現在 [アクティビティ ログ] ページや [検出] ページで利用できる保存されたクエリと同様です。

- **Office 365 の既定の構成の監査**  
Cloud App Security で Office 365 のアクティビティの監視を有効にする必要がある場合は、[Office セキュリティ/コンプライアンス センター](/office365/securitycompliance/turn-audit-log-search-on-or-off#turn-on-audit-log-search)で監査を有効にする必要があります。これは、[Office 365 の監査が変更された](/office/office-365-management-api/office-365-management-activity-api-faq#what-happens-if-i-disable-auditing-for-my-office-365-organization-will-i-still-get-events-via-the-management-activity-api)結果です。 この変更は、Cloud App Security で Office 365 のアクティビティの監視をまだ有効にしていない場合にのみ、実行する必要があります。

- **強化された Box のサポート**  
Cloud App Security では、Box に対する 2 つの新しいガバナンス アクションがサポートされるようになりました。

  - **共有リンクの期限切れ** – このガバナンス アクションでは、共有リンクの有効期限を設定できます。これを過ぎると、アクティブにならなくなります。

  - **共有リンクのアクセス レベルを変更** – このガバナンス アクションでは、会社のみ、コラボレーターのみ、パブリックのいずれかに、共有リンクのアクセス レベルを変更できます。

- **OneDrive での複数の場所のサポート**  
Cloud App Security は、OneDrive のファイルが複数の地理的な場所に分散している場合でも、それらを完全に表示できるようになりました。 メインの場所だけでなく追加の場所にあるファイルでも、保護を利用できます。

- **ポータル ナビゲーションの強化**  
Cloud App Security ポータルが強化されて、ナビゲーションが改善され、Microsoft の他のセキュリティ サービスとの Cloud App Security の整合性が向上し、使用が合理化されて簡単になりました。

## <a name="cloud-app-security-release-141"></a>Cloud App Security リリース 141

2019 年 1 月 20 日リリース

- **クラウド リスク評価の機能強化**  
  - クラウド アプリのリスク評価が、2 つの新しいエクスペリエンスによって強化されました。
    - 新しい**データの種類**属性では、ユーザーがアプリにアップロードできるコンテンツの種類が評価されます。 この属性を使用すると、組織内の各データの種類の機密度に基づいて、アプリを評価することができます。
    - アプリのさらに包括的なリスクの概要を見るには、 **[ホスティング企業]** 属性をクリックすることで、アプリのリスク評価からホスティング会社のリスク評価に簡単に切り替えることができます。

- **異常検出アラート調査のためのファイル コンテキストの拡張**  
  - 異常検出の調査が強化され、アラートに関係するファイルに関連のある他の分析情報を見ることができるようになりました。 異常なアクティビティのアラート (ダウンロード、共有、削除) に関係するファイルに対してアラートがトリガーされた場合に、このドリル ダウンを使用できます。 たとえば、影響を受けたファイルのほとんどが同じフォルダーのものである場合、または同じファイル拡張子を共有している場合は、アラートの追加のリスク セクションにこれらの分析情報が表示されます。

- **ファイル調査のためのクエリ**  
  - カスタム クエリを作成して保存する Cloud App Security の機能が、 **[ファイル]** ページに拡張されました。 **[ファイル]** ページのクエリを使用すると、詳細な調査のために再利用できるクエリ テンプレートを作成できます。

## <a name="cloud-app-security-release-139-140"></a>Cloud App Security リリース 139、140

2019 年 1 月 6 日リリース

- **ファイル検出での変更**  
[SharePoint と OneDrive に対して行われた変更のため](https://support.microsoft.com/help/4089534/how-to-grant-the-everyone-claim-to-external-users-in-office-365)、SharePoint および OneDrive ですべてのユーザーと共有されているファイルは**内部**と見なされるようになりました。 そのため、すべてのユーザーと共有されているファイルが検出されると、そのファイルは内部ファイルとして扱われるようになります。これは、ファイルのポリシーによる処理方法と、ファイル ページでの表示方法に影響します。

- **ファイル監視での変更**  
新規およびアイドル状態のお客様に対する既定のファイル監視動作が変更されました。 機能を有効にするには、 **[設定]**  >  **[ファイル]** でファイル監視をオンにすることが必要になります。 既存のアクティブなお客様は、この変更の影響を受けません。

- **異常検出ポリシーの高度なチューニング**  
ユーザーの設定に応じて、異常検出エンジンでアラートを抑制または表示できるようになりました。
  - あり得ない移動ポリシーでは、感度スライダーを設定して、アラートがトリガーされるために必要な異常な動作のレベルを決定できます。
  - また、頻度の低い国、匿名 IP アドレス、疑わしい IP アドレス、およびあり得ない移動からのアクティビティに対するアラートで、失敗と成功両方のログインを分析するか、成功したログインだけを分析するかを、構成することもできます。

- **複数の信頼チェーンのサポート**  
アプリの条件付きアクセス制御では、複数の信頼済みのルート証明書または中間証明書をデバイス管理の形式として追加および使用する機能がサポートされるようになりました。

- **新しい Cloud Discovery ロール** (段階的なロールアウト)  
Cloud App Security では、Cloud Discovery ユーザーに新しい管理者ロールを提供できるようになりました。 このロールを使用すると、管理者ユーザーがアクセスできる範囲を、Cloud App Security ポータル内の Cloud Discovery の設定とデータのみに限定できます。

- **Microsoft Information Protection の統合ラベルのサポート** (段階的なロールアウト)  
Cloud App Security で、Microsoft Information Protection の統合ラベルがサポートされるようになりました。 既に [Office 365 Security およびコンプライアンス センターに分類ラベルを移行](/azure/information-protection/configure-policy-migrate-labels)した顧客に対して、Cloud App Security では、「[Azure Information Protection の統合](azip-integration.md)」に説明されているように、これらのラベルが特定されて処理されます。

**PDF ファイルのラベル付けのサポート** (段階的なロールアウト)  
統合ラベルを使用している顧客に対して、Cloud App Security では PDF ファイルの自動ラベル付けがサポートされるようになりました。

## <a name="cloud-app-security-release-138"></a>Cloud App Security リリース 138

2018 年 12 月 9 日リリース

- **Windows での Docker を使用したログの自動アップロード**  
Cloud App Security で、Windows 10 (Fall Creators Update) および Windows Server バージョン 1709 以降に対して、Docker for Windows を使用したログの自動アップロードがサポートされるようになりました。 この構成の詳細および手順については、「[オンプレミスの Windows の Docker](discovery-docker-windows.md)」を参照してください。

- Cloud App Security と [Microsoft Flow](/flow/getting-started) を統合すると、カスタム アラートの自動化とオーケストレーションのプレイブックが提供されます。 詳細および統合手順については、[Microsoft Flow との統合](flow-integration.md)に関する記事をご覧ください。

## <a name="cloud-app-security-release-137"></a>Cloud App Security リリース 137

リリース日: 2018 年 11 月 25 日

- **Dynamics のサポートの追加**  
Cloud App Security で、Office 365 監査ログでサポートされている Microsoft Dynamics のアクティビティがサポートされるようになりました。

- **暗号化されたコンテンツのスキャン (プレビュー)**  
Cloud App Security では、Azure Information Protection の保護ラベルによって保護されているコンテンツをスキャンできるようになりました。 これにより、Azure Information Protection によって既に暗号化されているファイルでも、機密性の高いコンテンツを検索できるようになります。

- **ヘッドアップ – 新しい用語**  
わかりやすくするため、アプリのアクセス許可という名前が変更され、**OAuth アプリ**と呼ばれるようになりました。

## <a name="cloud-app-security-release-136"></a>Cloud App Security リリース 136

リリース日: 2018 年 11 月 11 日

- **Cloud Discovery の更新内容**  
カスタム ログ パーサーが拡張され、新しい、いっそう複雑な Web トラフィック ログ形式がサポートされるようになりました。 これらの強化の一環として、ユーザーは、ヘッダーレス CSV ログ ファイルに対するカスタム ヘッダーの入力、キーと値のファイルに対する特殊な区切り記号の使用、Syslog ファイル形式の処理などができるようになりました。

- **新しい異常検出ポリシー**  
受信トレイに対する疑わしい操作ルール: このポリシーでは、ユーザーの受信トレイでメッセージまたはフォルダーを削除または移動する疑わしいルールが設定されている場合に、環境がプロファイリングされて、アラートがトリガーされます。 これは、ユーザーのアカウントが侵害されていること、メッセージが意図的に隠ぺいされていること、および組織内でスパムやマルウェアを配信するためにメールボックスが使用されていることを示している可能性があります。

- **アプリのアクセス許可ポリシーでのグループのサポート**  
Cloud App Security では、アプリを承認したユーザーのグループ メンバーシップに基づいて、アプリのアクセス許可ポリシーをより詳細に定義できるようになりました。 たとえば、管理者は、アクセス許可を承認したユーザーが Administrators グループのメンバーである場合にのみ、一般的ではないアプリが高いアクセス許可を要求した場合にそれらを失効させるポリシーを設定することができます。

- **アプリの条件付きアクセス制御を、Azure Active Directory アプリケーション プロキシを介してオンプレミスのアプリと統合できるようになった**  
  - [Azure AD アプリケーション プロキシ](/azure/active-directory/manage-apps/application-proxy)では、シングル サインオンと、オンプレミスでホストされている Web アプリへのセキュリティ保護されたリモート アクセスが提供されます。
  - [アクセス](access-policy-aad.md)および[セッション](session-policy-aad.md)のポリシーにより、これらのオンプレミス Web アプリを Azure AD の条件付きアクセス経由で Microsoft Cloud App Security にルーティングして、リアルタイムの監視と制御を提供できるようになりました。

## <a name="cloud-app-security-release-133-134-135"></a>Cloud App Security リリース 133、134、135

リリース日: 2018 年 10 月

- **新しい異常検出ポリシーの段階的展開**  
  - 新しい "承認されていないアプリへのデータ抜き取り" ポリシーが、自動的に有効になります。このポリシーでは、ユーザーまたは IP アドレスが組織からの情報流出の試みに似たアクティビティを実行することを承認されていないアプリを使用すると、アラートが生成されます。
    - 新しい "複数の VM 削除アクティビティ" ポリシーでは、ユーザーの環境がプロファイリングされ、組織内のベースラインを基準として、ユーザーが 1 つのセッションで複数の VM を削除すると、アラートがトリガーされます。

- **APAC に使用できるデータ分類サービス**  
  - APAC のお客様は、データ分類サービスのコンテンツ検査を利用できるようになりました。 リージョンごとのサポートの完全な一覧については、「[Microsoft データ分類サービスの統合](dcs-inspection.md)」をご覧ください。

- **Cloud Discovery での i-Filter のサポート**  
  - Cloud App Security の Cloud Discovery 機能で、i-Filter syslog パーサーのサポートが強化されました。

## <a name="cloud-app-security-release-132"></a>Cloud App Security リリース 132

リリース日: 2018 年 9 月 25 日

- **パブリックプ レビューになった Office 365 向けアプリの条件付きアクセス制御**  
  - アプリの条件付きアクセス制御で、Office 365 と、Open ID Connect で構成されているすべてのアプリも、サポートされるようになりました。
  - セッション内からフィードバックを提供する: この新しいツールを使用すると、セッションの制御下にあるアプリケーションのパフォーマンスに関するフィードバックを、セッション内から直接 Cloud App Security チームに提供できます。

- **企業の範囲を超えた Shadow IT Discovery のための Microsoft Defender ATP とのネイティブ統合**  
  - Microsoft Cloud App Security は、Windows Defender Advanced Threat Protection (ATP) とネイティブに統合されるようになりました。これにより、企業ネットワーク上およびその外でのクラウド アプリの使用に対する展開不要のシャドウ IT 検出機能が提供されます。  これにより、企業ネットワーク内にないコンピューター上でも Cloud Discovery を実行できます。 また、コンピューター ベースの調査も可能です。危険なユーザーが特定されたら、そのユーザーがアクセスしたすべてのコンピューターを調べて、潜在的なリスクを検出できます。危険なコンピューターが特定されたら、それを使用したすべてのユーザーを調べて、潜在的なリスクを調査できます。 詳しくは、Windows Defender Advanced Threat Protection と [Microsoft Cloud App Security](wdatp-integration.md) の統合に関する記事をご覧ください。

- **暗号化されたファイルのコンテンツ検査**  
  - Cloud App Security では、Azure Information Protection を使用して保護されていた、暗号化されて保護されたファイルのコンテンツ検査がサポートされるようになりました。 これらの暗号化されたファイルで再分類の提案を検査し、追加の DLP 公開とセキュリティ ポリシー違反を識別できます。

## <a name="cloud-app-security-release-131"></a>Cloud App Security リリース 131

リリース日: 2018 年 9 月 2 日

- **危険な OAuth アプリに対するアクセス許可の自動取り消し**  
Office、Google、または Salesforce で OAuth アプリに対するアプリのアクセス許可を取り消すことによって、ユーザーがアクセスできる OAuth アプリを制御できるようになりました。 **アプリのアクセス許可ポリシー**を作成するときに、アプリのアクセス許可を取り消すようにポリシーを設定できるようになりました。

- **Cloud Discovery でサポートされる組み込みパーサーの追加**  
Cloud Discovery で、Forcepoint Web Security Cloud のログ形式がサポートされるようになりました。

## <a name="cloud-app-security-release-130"></a>Cloud App Security リリース 130

リリース日: 2018 年 8 月 22 日

- **新しいメニュー バー**  
Microsoft 365 製品全体で管理者エクスペリエンスの一貫性を高め、Microsoft のセキュリティ ソリューション間の切り替えを間単にするため、Cloud App Security ポータルのメニュー バーが画面の左側に移動されました。 この一貫したナビゲーション エクスペリエンスによって、ある Microsoft セキュリティ ポータルから別のセキュリティ ポータルへの移動が容易になります。

- **OAuth アプリ スコアへの影響**  
Cloud App Security チームにフィードバックを送信して、悪意があると思われる OAuth アプリが組織内で検出されたことを通知できます。 この新機能により、ユーザーはセキュリティ コミュニティの一員となり、OAuth アプリのリスク スコアと分析を強化することができます。 詳細については、[OAuth アプリのアクセス許可の管理](manage-app-permissions.md)に関するページを参照してください。

- **新しい Cloud Discovery パーサー**  
Cloud Discovery パーサーで、iboss Secure Cloud Gateway と Sophos XG がサポートされるようになりました。

## <a name="cloud-app-security-release-129"></a>Cloud App Security リリース 129

リリース日: 2018 年 8 月 5 日

- **新しい異常検出ポリシー - 疑わしい電子メール ルール**  
疑わしい電子メール転送ルールを検出する新しい異常検出ポリシーが追加されました。たとえば、ユーザーが、すべての電子メールのコピーを外部アドレスに転送する受信トレイのルールを作成した場合などです。

- このリリースには、複数の問題に対する修正プログラムと機能強化が含まれています。

## <a name="cloud-app-security-release-128"></a>Cloud App Security リリース 128

リリース日: 2018 年 7 月 22 日

- **複数のアプリ間での OAuth アプリ操作**  
アプリのアクセス許可が付与されている OAuth アプリの場合、1 回の操作で複数のアプリを対象にすることを禁止または承認できるようになりました。 たとえば、組織内のユーザーによるアクセス許可が付与されているすべてのアプリを確認し、禁止するすべてのアプリを選択した後、[アプリを禁止] をクリックして、許可されたすべての同意を取り消すと、ユーザーはそれらのアプリにアクセス許可を付与できなくなります。  詳しくは、「[OAuth アプリの管理](manage-app-permissions.md)」をご覧ください。

- **Azure アプリケーションのサポートの強化**  
Azure では、ユーザー アカウント アクティビティが Azure アプリケーション (内部と外部の両方) によって実行されたアプリケーションを検出する機能が、段階的にロールアウトされています。 これにより、アプリケーションで予期されないアクティビティや承認されていないアクティビティが実行された場合にアラートを生成するポリシーを作成できます。 詳しくは、「[Azure を Microsoft Cloud App Security に接続する](connect-azure-to-microsoft-cloud-app-security.md)」をご覧ください。

- **新しい GDPR の機密情報の種類で更新されたデータ分類エンジン**  
[Cloud App Security のデータ分類サービス](dcs-inspection.md)で、GDPR の新しい機密情報の種類がデータ分類エンジンに追加され、ファイル内の GDPR 関連コンテンツを検出できるようになりました。

- **クラウド アプリ カタログの更新**  
クラウド アプリ カタログに、GDPR への対応など、データのプライバシーと所有権のコンプライアンスを管理するのに役立つ法的リスク カテゴリが (一般、セキュリティ、コンプライアンスに加えて) 含まれるようになりました。
各クラウド アプリの GDPR 対応を評価するため、新しいリスク カテゴリには、クラウド サービスの GDPR 対応ステートメントと、各 GDPR フレームワーク制御の状態が含まれています。
この改善の一環として、次のリスク属性が他のリスク カテゴリから法的カテゴリに移動されたことに注意してください。
  - DMCA
  - データ所有権
  - データ保持期間ポリシー

  さらに、新しいリスク カテゴリは個別にスコア付けされるので、ユーザーの設定と優先度に応じてスコアの重み付けを構成することができます。 詳しくは、[リスク スコア](risk-score.md)に関する記事をご覧ください。

- **新しい推奨クエリ: GDPR 対応**  
検出された GDPR 対応アプリを識別できるように、新しい推奨クエリが追加されました。 最近、GDPR はセキュリティ管理者の最優先事項になったため、このクエリを使用すると、GDPR 対応のアプリを簡単に識別し、対応していないアプリのリスクを評価することで、脅威を軽減できます。

## <a name="cloud-app-security-release-127"></a>Cloud App Security リリース 127

リリース日: 2018 年 7 月 8 日

- Office 365 の全般的なアクティビティを表示する機能が提供されました。 **アクティビティ ログ**と**アクティビティ ポリシー**で、Office 365 のアクティビティをフィルター処理して**指定なし**のアクティビティを抽出できるようになりました。 これらのアクティビティを確認することで、Cloud App Security の種類によってまだ分類されていない、実行されたアクティビティに関する情報を調査できます。また、これらのアクティビティを使用して、Cloud App Security チームに要求を送り、これらのアクティビティに基づく新しいアクティビティの種類を作成することができます。

## <a name="cloud-app-security-release-126"></a>Cloud App Security リリース 126

リリース日: 2018 年 6 月 24 日

- **アプリの条件付きアクセス制御の一般提供**  
Microsoft Cloud App Security のアプリの条件付きアクセス制御 (リバース プロキシ) が、すべての SAML アプリケーションで一般提供されました。 アプリの条件付きアクセス制御は Azure AD の条件付きアクセス ポリシーと直接統合されて、**ユーザーのセッションがリアルタイムで監視および制御**されるので、ユーザーの生産性を高めることができます。 最初のプレビュー機能から、次のような多くの機能が作成され、機能強化が行われています。
  - ブラウザー トラフィック用のセッション ポリシーの作成に加えて、ネイティブ クライアントから同じアプリへのアクセスを管理するための[アクセス ポリシー](access-policy-aad.md)を作成する機能。
  - アプリのオンボード プロセスは、組織内のカスタム SAML アプリケーションをサポートするために合理化されました。
  - Azure の世界規模のネットワークの一部として、ユーザーが世界中のどこにいてもシームレスなエクスペリエンスを使用できるよう、統合とインターフェイスが強化されました。

- **Microsoft データ分類サービスによるコンテンツ検査の一般提供**  
Microsoft Cloud App Security と Microsoft データ分類サービスの統合が一般提供されました。 この統合により、Microsoft データ分類サービスをネイティブに利用して、クラウド アプリ内のファイルを分類できます。 詳細については、「[Microsoft データ分類サービスの統合](dcs-inspection.md)」を参照してください。 この機能は現在、米国とヨーロッパ (フランスを除く) でのみ利用できます。

- **Cloud Discovery エグゼクティブ レポート**  
Microsoft Cloud App Security では、Cloud Discovery エグゼクティブ PDF レポートを生成する機能が段階的にロールアウトされています。 このレポートでは、組織内で明らかになったシャドウ IT の使用の概要が示され (全体および主要なカテゴリで使用されている上位のアプリとユーザーが強調されています)、シャドウ IT によって組織に発生するリスクに焦点が当てられています。 また、レポートでは、組織内でのシャドウ IT の視覚化と制御を向上させるための推奨事項の一覧が提供されます。 このレポートを使用して、潜在的なリスクと脅威が排除され、組織が安全でセキュリティ保護されていることを確認します。

- **マルウェアの検出**  
ファイルの種類に関係なく、**クラウド ストレージ内の悪意のあるファイルを自動的に検出する**マルウェア検出機能が、段階的にロールアウトされています。 Microsoft Cloud App Security では、Microsoft の脅威インテリジェンスを使用して、特定のファイルが既知のマルウェア攻撃に関連付けられているかどうか、または悪意を持つ可能性があるかどうかが認識されます。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

- **疑わしいアクティビティの自動修復**  
異常検出ポリシーによってトリガーされる疑わしいセッションに対して、自動修復アクションを設定できるようになりました。 この機能強化により、侵害が発生したらすぐにアラートを受け取り、ユーザーの中断などの**ガバナンス アクションを自動的に適用する**ことができます。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md#adp-automated-gov)に関する記事をご覧ください。

- **Azure のセキュリティ構成の評価**  
Microsoft Cloud App Security では、お客様の Azure 環境のセキュリティ構成の評価を取得し、不足している構成およびセキュリティ制御に関する推奨事項を提供する機能が、段階的にロールアウトされています。 たとえば、管理ユーザーに対する MFA が不足しているかどうかを知ることができます。 詳しくは、[クラウドのセキュリティ体制の管理の統合](security-config.md)に関する記事をご覧ください。

- **危険な OAuth アプリの自動検出**  
環境に接続されている OAuth アプリの既存の調査に加えて、Microsoft Cloud App Security では、OAuth アプリが特定の条件を満たした場合に通知を受け取れるように自動通知を設定する機能が、段階的にロールアウトされています。 たとえば、高いアクセス許可レベルを必要とし、50 人を超えるユーザーによって承認されたアプリがある場合、自動的にアラートを受け取ることができます。 詳しくは、[アプリのアクセス許可ポリシー](app-permission-policy.md)に関する記事をご覧ください。

- **Managed Security Service Provider (MSSP) の管理のサポート**  
Microsoft Cloud App Security では、MSSP の管理エクスペリエンスが改善されました。 外部ユーザーを管理者として構成し、[Microsoft Cloud App Security で現在使用可能な任意のロール](manage-admins.md)を割り当てることができるようになりました。 さらに、MSSP で複数の顧客テナントにサービスを提供できるようにするため、複数のテナントへのアクセス権を持つ管理者は、ポータル内でテナントを簡単に切り替えることができるようになりました。 管理者の管理については、[管理者の管理](manage-admins.md)に関する記事をご覧ください。

- **外部 DLP との統合の一般提供**  
Microsoft Cloud App Security では、データ損失防止 (DLP) ソリューションのような[サードパーティ製分類システムの既存の投資を利用](icap-stunnel.md)できるようになり、環境内で実行されている既存の展開を使用してクラウドのアプリケーションの内容をスキャンできるようになりました。 詳しくは、「[外部 DLP 統合](icap-stunnel.md)」をご覧ください。

## <a name="cloud-app-security-release-125"></a>Cloud App Security リリース 125

リリース日: 2018 年 6 月 10 日

- **上位ユーザーによる新しい調査機能:**  
Microsoft Cloud App Security では、脅威検出のオープン アラートの数で上位のユーザーが表示される新しい調査ウィジェットが、ダッシュボードに追加されました。 この調査ウィジェットを使用すると、不審なセッションが最も多いユーザーに、脅威の調査を集中させることができます。

- **AWS S3 バケットのサポート:**  
Microsoft Cloud App Security では、AWS S3 バケットとその共有レベルを検出できるようになりました。 これにより、パブリックにアクセスできる AWS バケットのアラートと可視性が提供されます。 これにより、バケットに基づいてポリシーを作成し、自動ガバナンスを適用することもできます。 また、AWS ストレージを管理するためのポリシーを簡単に作成するために使用できる**パブリックにアクセス可能な S3 バケット (AWS)** という名前の新しいポリシー テンプレートもあります。 これらの新機能を有効にするには、[AWS の接続](connect-aws-to-microsoft-cloud-app-security.md)に関する記事で説明されている新しいアクセス許可を追加することにより、AWS 接続アプリを更新します。

- **ユーザー グループに基づく管理特権**:  
Microsoft Cloud App Security 管理者に対する管理アクセス許可を、ユーザー グループごとに設定できるようになりました。 たとえば、ドイツのユーザーだけに対する管理者として、特定のユーザーを設定できます。 これにより、そのユーザーは、"ドイツ - 全ユーザー" というユーザー グループについてだけ、Microsoft Cloud App Security で情報を表示および変更できます。 詳しくは、「[管理者アクセスの管理](manage-admins.md)」をご覧ください。

## <a name="cloud-app-security-release-124"></a>Cloud App Security リリース 124

リリース日: 2018 年 5 月 27 日

- **クラウド アプリ カタログへの GDPR リスク評価の追加**  
13 個の新しいリスク要因が、Microsoft Cloud App Security に追加されました。 これらのリスク要因は GDPR フレームワークのチェックリストに従っており、GDPR の規則に従って、クラウド アプリ カタログ内のアプリを評価できます。

- **Microsoft データ分類サービスとの統合**  
Microsoft Cloud App Security では、Microsoft データ分類サービスをネイティブに利用して、クラウド アプリ内のファイルを分類できるようになりました。   
Microsoft データ分類サービスでは、Office 365、Azure Information Protection、Microsoft Cloud App Security に対して統一された情報保護エクスペリエンスが提供されます。 これにより、Microsoft Cloud App Security によって保護されているサードパーティのクラウド アプリまで同じデータ分類フレームワークを拡張し、さらに多くのアプリに対して既に行った決定を利用できます。

- **Microsoft Azure への接続** (段階的ロールアウト)  
Microsoft Cloud App Security では IaaS 監視機能が拡張されており、アマゾン ウェブ サービスだけでなく、Microsoft Azure もサポートされるようになっています。 これにより、Cloud App Security ですべての Azure サブスクリプションをシームレスに接続し、監視できます。 この接続では、次のような、Azure 環境を保護するための一連の強力なツールが提供されます。

  - ポータルで実行されたすべてのアクティビティの表示

  - 望ましくない動作に対するアラートを生成するためのカスタム ポリシーを作成する機能。および、一時停止したり、再サインインを強制したりすることにより、危険性のあるユーザーを自動的に保護する機能。

  - 異常検出エンジンで Azure のすべてのアクティビティがカバーされており、Azure portal であり得ない移動、大量の不審なアクティビティ、新しい国からのアクティビティなど、疑わしい動作が検出されると、自動的にアラートが生成されます。  

  詳しくは、「[Azure を Microsoft Cloud App Security に接続する](connect-azure-to-microsoft-cloud-app-security.md)」をご覧ください。

- **スコープ付きの展開** (段階的ロールアウト)  
Microsoft Cloud App Security を使用することで、企業では、グループのメンバーシップに基づいて監視および保護するユーザーを細かく決定できます。 この機能を使用すると、保護されているアプリケーションのいずれにもアクティビティが表示されないユーザーを選択できます。 スコープ付きの監視機能は、次の場合に特に役立ちます。
  - コンプライアンス - コンプライアンス規制によって、地域の規制のために特定の国のユーザーを監視しないようにする必要がある場合。
  - ライセンス – Microsoft Cloud App Security ライセンスの制限内に収まっていることを監視する対象のユーザーの数を減らしたい場合。
  詳細については、「[スコープ付きの展開](scoped-deployment.md)」をご覧ください。

- **検出されたアプリに対する侵害されたアプリのアラート**  
 テナントの検出されたアプリのいずれかが侵害されたときに通知する組み込みのアラートが作成されました。 このアラートでは、侵害の日時とアプリを使用したユーザーに関する情報、および侵害に関する情報がわかる公開ソースへのリンクが提供されます。

- **新しいメール サーバー**  
 Cloud App Security のメール サーバーが変更され、異なる IP アドレス範囲が使用されるようになりました。 通知を確実に受け取れるよう、新しい IP アドレスをスパム対策のホワイトリストに追加してください。 通知をカスタマイズするユーザーは、Microsoft Cloud App Security では、サードパーティの電子メール サービスである MailChimp&reg; を使用してこれを行うことができます。 メール サーバーの IP アドレスの一覧、および MailChimp での作業を有効にする手順については、「[ネットワークの要件](network-requirements.md#mail-server)」と「[メールの設定](mail-settings.md)」をご覧ください。

## <a name="cloud-app-security-release-123"></a>Cloud App Security リリース 123

2018 年 5 月 13 日リリース

- **異常検出ポリシーのスコープ設定**  
異常検出ポリシーのスコープを設定できるようになりました。 これにより、各異常検出ポリシーを設定して、特定のユーザーまたはグループのみを含めたり、特定のユーザーまたはグループを除外したりすることができます。 たとえば、頻度の低い地域の検出から、頻繁に移動する特定のユーザーを無視するように、アクティビティを設定できます。

## <a name="cloud-app-security-release-122"></a>Cloud App Security リリース 122

リリース日: 2018 年 4 月 29 日

- 段階的ロールアウト: **Microsoft Cloud App Security 管理者に対する管理アクセス許可を、アプリごとに設定できる**ようになりました。 たとえば、G Suite だけに対する管理者として、特定のユーザーを設定できます。 これにより、そのユーザーは、G Suite だけに関連しているときにのみ、Microsoft Cloud App Security で情報を表示および変更できます。 詳しくは、「[管理者アクセスの管理](manage-admins.md)」をご覧ください。

- 段階的ロールアウト: Microsoft Cloud App Security で **Okta 管理者ロールが表示されるようになり**、 **[設定]**  >  **[ユーザー グループ]** でタグとして各ロールに利用できます。

## <a name="cloud-app-security-release-121"></a>Cloud App Security リリース 121

リリース日: 2018 年 4 月 22 日

- **アプリの条件付きアクセス制御 (旧称 Cloud App Security Proxy)** のパブリック プレビューが、さまざまなアプリケーションをより深く可視化し、制御する機能によって強化されています。 "*アクティビティの種類*" フィルターを使用してセッション ポリシーを作成し、さまざまなアプリ固有のアクティビティを監視してブロックすることができるようになりました。 この新しいフィルターでは、既存のファイル ダウンロード制御機能が強化されて、組織内のアプリケーションを包括的に制御できるようになります。また、Azure Active Directory の条件付きアクセスと連携し、リスクの高いユーザー セッションをリアルタイムで表示および制御できます (たとえば、B2B コラボレーション ユーザーとのセッションや、アンマネージド デバイスからのユーザーなど)。 詳しくは、「[セッション ポリシー](session-policy-aad.md)」をご覧ください。

- 段階的ロールアウト: Cloud App Security の**異常検出ポリシーが改善され**、次の 2 つの新しい脅威検出の種類が含まれるようになりました: ランサムウェア アクティビティと、終了させられたユーザーのアクティビティ。 Cloud App Security のランサムウェア検出機能が異常検出によって強化され、高度なランサムウェア攻撃に対していっそう包括的なカバレッジが保証されるようになりました。 セキュリティ研究の専門知識を活用して、ランサムウェアのアクティビティを反映する行動パターンを識別することにより、Cloud App Security では包括的で堅牢な保護が実現されます。 終了させられたユーザーのアクティビティを使用すると、終了させられたユーザーのアカウントを監視できます。そのようなユーザーは、会社のアプリからプロビジョニング解除された可能性がありますが、多くの場合、特定の企業リソースへのアクセスはまだ保持しています。 詳しくは、「[瞬間的な行動分析と異常検出を取得する](anomaly-detection-policy.md)」をご覧ください。

## <a name="cloud-app-security-release-120"></a>Cloud App Security リリース 120

リリース日: 2018 年 4 月 8 日

- Office 365 と Azure AD では、ユーザー アカウント アクティビティが Office 365 と Azure AD アプリケーション (内部と外部の両方) によって実行された内部アプリケーションを検出する機能が、段階的にロールアウトされています。 これにより、アプリケーションで予期されないアクティビティや承認されていないアクティビティが実行された場合にアラートを生成するポリシーを作成できます。

- アプリのアクセス許可の一覧を csv にエクスポートすると、発行元、アクセス許可レベル、コミュニティの使用状況などの追加フィールドが、コンプライアンスと調査のプロセスを支援するために含まれます。

- ServiceNow 接続アプリが改善され、内部サービス アクティビティが "ゲスト" によって実行されたものとして登録されなくなり、擬陽性アラートがトリガーされなくなりました。 これらのアクティビティは、他のすべての接続されたアプリと同様に N/A として表されるようになりました。

## <a name="cloud-app-security-release-119"></a>Cloud App Security リリース 119

リリース日: 2018 年 3 月 18 日

- IP アドレス範囲のページには、Cloud App Security によって検出された組み込みの IP アドレスが含まれます。 これには、Azure や Office 365 などの識別されたクラウド サービスの IP アドレスだけでなく、既知の危険な IP アドレスに関する情報で IP アドレスを自動的に強化する脅威インテリジェンスのフィードが含まれます。

- Cloud App Security では、ファイルに対するガバナンス アクションを実行しようとして、ファイルがロックされているために失敗した場合、ガバナンス アクションが自動的に再試行されるようになりました。

## <a name="cloud-app-security-release-118"></a>Cloud App Security リリース 118

リリース日: 2018 年 3 月 4 日

- Microsoft Cloud App Security のシャドウ IT 検出および監視機能を、独自のカスタム アプリで利用できるようになりました。 Cloud Discovery にカスタム アプリを追加する新しい機能を使用すると、アプリの使用状況を監視し、使用パターンが変化したらアラートを受け取ることができます。 詳しくは、[カスタム アプリの保護](cloud-discovery-custom-apps.md)に関する記事をご覧ください。 この機能は、徐々にロール アウトされていきます。

- Cloud App Security ポータルの **[設定]** ページのデザインが変更されました。 新しいデザインでは、すべての設定ページが統合され、検索機能が提供されるようになり、デザインが向上しています。

- Cloud Discovery では、Barracuda F シリーズ ファイアウォールと Barracuda F シリーズ ファイアウォール Web ログ ストリーミングがサポートされるようになりました。

- [ユーザー] ページと [IP アドレス] ページの検索機能でオートコンプリートが有効になり、探しているものを見つけやすくなりました。

- [エンティティの除外] ページと [Exclude IP address settings]\(IP アドレス設定の除外\) ページでは、一括操作を実行できるようになりました。 これにより、複数のユーザーとグループまたは IP アドレスを選択し、組織内の Cloud Discovery の一部としての監視対象から、簡単に除外できます。

## <a name="cloud-app-security-release-117"></a>Cloud App Security リリース 117

2018 年 2 月 20 日のリリース

- Cloud App Security と Azure Information Protection との緊密な統合により、G Suite のファイルを保護できるようになりました。 このパブリック プレビュー機能を使用すると、G Suite のファイルをスキャンして分類したり、Azure Information Protection ラベルを保護のために自動的に適用したりできます。 詳しくは、「[Azure Information Protection の統合](azip-integration.md)」をご覧ください。

- Cloud Discovery で [Digital Arts の i-FILTER](https://www.daj.jp/en/products/if/) がサポートされるようになりました。

- SIEM エージェント テーブルで、管理を容易にするための詳細情報を確認できるようになりました。

## <a name="cloud-app-security-release-116"></a>Cloud App Security リリース 116

リリース日: 2018 年 2 月 4 日

- Cloud App Security の異常検出ポリシーが、新しい**シナリオベースの検出**によって強化されました。これには、あり得ない移動、疑わしい IP アドレスからのアクティビティ、ログイン試行の複数の失敗などが含まれます。 新しいポリシーは自動的に有効になり、クラウド環境全体で脅威検出をすぐに使用できます。 さらに、新しいポリシーでは、Cloud App Security 検出エンジンからより多くのデータが公開され、調査プロセスの高速化と、進行中の脅威の阻止に役立ちます。 詳しくは、「[瞬間的な行動分析と異常検出を取得する](/cloud-app-security/anomaly-detection-policy)」をご覧ください。

- 段階的ロールアウト: Cloud App Security により、SaaS アプリ全体でユーザーとそのアカウントが相互に関連付けられるようになりました。 これにより、使用したアプリやアカウントに関係なく、関連するさまざまな SaaS アプリ全体で、ユーザーに対するすべてのアクティビティを簡単に調査できます。

- 段階的ロールアウト: Cloud App Security で、同じ接続されたアプリの複数のインスタンスがサポートされるようになりました。 たとえば、Salesforce の複数のインスタンスがある場合 (1 つは営業用、1 つはマーケティング用)、両方のインスタンスを Cloud App Security に接続して、同じコンソールから管理し、詳細なポリシーやより深い調査を作成できます。

- Cloud Discovery パーサーで、2 つの追加のチェックポイント形式、XML と KPC がサポートされるようになりました。

## <a name="cloud-app-security-release-115"></a>Cloud App Security リリース 115

リリース日: 2018 年 1 月 21 日

- このリリースでは、ファイル ポリシーで特定のフォルダーを選択するときのエクスペリエンスが向上しています。 複数のフォルダーを簡単に表示して選択し、ポリシーに含めることができるようになりました。
- **[検出されたアプリ]** ページでは次のことができます。
  - 一括タグ付け機能により、(承認されたタグと承認されていないタグに加えて) カスタム タグを適用することができます。
  - **IP アドレス レポートを生成する**とき、または**ユーザー レポートを生成する**とき、エクスポートされたレポートに、トラフィックが承認されたアプリまたは承認されていないアプリのどちらからであったかに関する情報が含まれるようになりました。
- ポータルの **[アプリを接続]** ページから、新しい API アプリ コネクタを Microsoft Cloud App Security チームに直接要求できるようになりました。

## <a name="cloud-app-security-release-114"></a>Cloud App Security リリース 114

リリース日: 2018 年 1 月 7 日

- バージョン 114 以降、アクティビティ ログと検出されたアプリのページでカスタム クエリを作成して保存する機能が段階的にロールアウトされています。 カスタム クエリを使用すると、詳細な調査のために再利用できるフィルター テンプレートを作成できます。 さらに、**推奨されるクエリ**が追加され、アクティビティと検出されたアプリをフィルター処理するためのすぐに使用できる調査用テンプレートが提供されるようになりました。 **推奨されるクエリ**には、偽装アクティビティ、管理者アクティビティ、危険な非準拠のクラウド ストレージ アプリ、脆弱な暗号化を使用したエンタープライズ アプリ、セキュリティ リスクなどのリスクを識別するためのカスタム フィルターが含まれます。 **推奨されるクエリ**を基にして、必要に応じて変更し、新しいクエリとして保存することができます。 詳しくは、「[アクティビティ フィルターとクエリ](activity-filters-queries.md)」および「[検出されたアプリのフィルターとクエリ](discovered-app-queries.md)」をご覧ください。

- [status.cloudappsecurity.com](https://status.cloudappsecurity.com) にアクセスするか、ポータル内から **[ヘルプ]** > **[システムの状態]** をクリックすることで直接、Cloud App Security サービスの現在の状態を確認できるようになりました。

## <a name="see-also"></a>関連項目

ここに記載されているものより前のリリースの説明については、[Microsoft Cloud App Security の過去のリリース](release-note-archive.md)に関する記事をご覧ください。

[!INCLUDE [Open support ticket](includes/support.md)]
