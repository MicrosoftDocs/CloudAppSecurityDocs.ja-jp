---
title: Cloud App Security の新機能
description: この記事は、Cloud App Security の最新リリースの新機能がわかるように頻繁に更新されます。
ms.date: 02/7/2021
ms.topic: overview
ms.openlocfilehash: 394e0fe3a6aa7287a9b60fbd15d26f999009a9eb
ms.sourcegitcommit: e3c960256e951ac2349ce92a6320326af8435bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2021
ms.locfileid: "100568117"
---
# <a name="whats-new-with-microsoft-cloud-app-security"></a>Microsoft Cloud App Security の新機能

*適用対象:Microsoft Cloud App Security*

この記事は、Cloud App Security の最新リリースの新機能がわかるように頻繁に更新されます。

RSS フィード:ご自身のフィード リーダーに次の URL をコピーして貼り付けることで、このページの更新時に通知を受け取ることができます。`https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Cloud+App+Security%22&locale=en-us`

> [!IMPORTANT]
>
> Microsoft による脅威の防止用製品の名前が変更されています。 この点や他の更新の詳細については、[こちら](https://www.microsoft.com/security/blog/?p=91813)をご覧ください。 今後のリリースでは、新しい名前が使用される予定です。

## <a name="cloud-app-security-release-192-193-and-194"></a>Cloud App Security リリース 192、193、および 194

リリース日: 2021 年 2 月 7 日

- **[ポリシーの更新] ページ**  
**[ポリシー]** ページが更新され、ポリシー カテゴリごとにタブが追加されました。 すべてのポリシーの完全な一覧を提供するために、 **[すべてのポリシー]** タブも追加しました。 ポリシーの分類の詳細については、「[ポリシーの種類](control-cloud-apps-with-policies.md#policy-types)」を参照してください。

- **Office 365 OAuth アプリのエクスポートの強化**  
OAuth アプリの *[リダイレクト URL]* を使用して、CSV ファイルにエクスポートする Office 365 Oauth アプリのアクティビティを拡張しました。 OAuth アプリのアクティビティのエクスポートの詳細については、「[Oauth アプリの監査](manage-app-permissions.md#oauth-app-auditing)」を参照してください。

- **ポータル インターフェイスの更新**  
今後数か月の間に、Microsoft 365 セキュリティ ポータル全体でより一貫したエクスペリエンスを提供するために、Cloud App Security のユーザー インターフェイスが更新されます。 [詳細情報](https://techcommunity.microsoft.com/t5/microsoft-security-and/microsoft-cloud-app-security-user-interface-updates/ba-p/2083113)

## <a name="cloud-app-security-release-189-190-and-191"></a>Cloud App Security リリース 189、190、および 191

リリース日: 2021 年 1 月 10 日

- **新しい異常検出:OAuth アプリへの資格情報の疑わしい追加**  
OAuth アプリへの特権資格情報の疑わしい追加を含めるよう、異常検出を拡張しました。 現在、新しい検出はすぐに使用でき、自動的に有効になります。 この検出は、攻撃者によってアプリが侵害され、悪意のあるアクティビティに使用されていることを示している可能性があります。 詳細については、「[OAuth アプリへの通常とは異なる資格情報の追加](investigate-anomaly-alerts.md#unusual-addition-of-credentials-to-an-oauth-app)」を参照してください。

- **シャドウ IT 検出アクティビティの監査の強化**  
管理者が実行するアクションを含めるように、[シャドウ IT](tutorial-shadow-it.md) アクティビティの監査が更新されました。 次の新しいアクティビティは、現在アクティビティ ログで使用でき、また Cloud App Security [調査エクスペリエンス](investigate.md#use-the-investigation-tools)の一部として使用できます。
  - アプリのタグ付けまたはタグの解除
  - ログ コレクターの作成、更新、または削除
  - データ ソースの作成、更新、または削除

- **新しい Data Enrichment REST API エンドポイント**  
API を使用して IP アドレス範囲を完全に管理できるようにする、次の [Data Enrichment API エンドポイント](api-data-enrichment.md)が追加されました。 作業の開始に役立つ[サンプル管理スクリプト](api-data-enrichment-manage-script.md)をお使いください。 範囲の詳細については、「[IP 範囲とタグの使用](ip-tags.md)」を参照してください。
  - [IP アドレス範囲の一覧表示](api-data-enrichment-list.md)
  - [IP アドレス範囲の更新](api-data-enrichment-update.md)
  - [IP アドレス範囲の削除](api-data-enrichment-delete.md)

## <a name="cloud-app-security-release-187-and-188"></a>Cloud App Security リリース 187 および 188

リリース日: 2020 年 11 月 22 日

- **新しい Shadow IT と Menlo Security の統合**  
Menlo Security とのネイティブ統合を追加しました。これにより、Shadow IT でアプリの利用状況を確認したり、アプリ アクセスを制御したりできます。 詳細については、「[Cloud App Security を Menlo Security と統合する](menlo-integration.md)」を参照してください。

- **新しい Cloud Discovery WatchGuard ログ パーサー**  
Cloud App Security の Cloud Discovery では、さまざまなトラフィック ログを分析して、アプリの順位付けとスコア付けを行います。 今回、WatchGuard 形式をサポートする組み込みのログ パーサーが Cloud Discovery に追加されました。 サポートされているログ パーサーの一覧については、「[サポートされているファイアウォールとプロキシ](set-up-cloud-discovery.md#supported-firewalls-and-proxies)」をご覧ください。

- **Cloud Discovery のグローバル管理者ロールに対する新しい権限**  
Cloud App Security では、Cloud Discovery のグローバル管理者ロールを持つユーザーが API トークンを作成し、Cloud Discovery 関連の全 API を使用できるようになりました。 ロールの詳細については、「[組み込みの Cloud App Security 管理者ロール](manage-admins.md#built-in-cloud-app-security-admin-roles)」を参照してください。

- **強化された感度スライダー:あり得ない移動**  
ユーザー スコープごとに異なる秘密度レベルを構成できるように、あり得ない移動の感度スライダーを更新しました。これにより、ユーザー スコープのアラートの忠実性をより細かく制御できます。 たとえば、管理者の秘密度レベルを、組織内の他のユーザーよりも高く定義することができます。この異常検出の詳細については、「[あり得ない移動](anomaly-detection-policy.md#impossible-travel)」を参照してください。

- **セッション制御の拡張プロキシ URL サフィックス (段階的なロールアウト)**  
2020 年 6 月 7 日に、名前付きリージョンを含まない 1 つの統合サフィックスを使用する、拡張プロキシ セッション制御の段階的なロールアウトを開始しました。 たとえば、ユーザーには `<AppName>.<Region>.cas.ms` の代わりに `<AppName>.mcas.ms` サフィックスが表示されます。 ネットワーク アプライアンスまたはゲートウェイのドメインを定期的にブロックする場合は、「[アクセス制御とセッション制御](network-requirements.md#access-and-session-controls)」に一覧表示されているすべてのドメインを許可リストに登録してください。

## <a name="cloud-app-security-release-184-185-and-186"></a>Cloud App Security リリース 184、185、および 186

リリース日: 2020 年 10 月 25 日

- **新たに強化されたアラートの監視と管理エクスペリエンス**  
アラートの監視と管理に関する継続的な改善の一環として、フィードバックに基づいて Cloud App Security のアラートのページが改善されました。 強化されたエクスペリエンスでは、 **[解決済み]** と **[破棄]** の状態が、 **[終了]** 状態と解決の種類に置き換えられます。 [詳細情報](monitor-alerts.md#deployment-of-our-enhanced-alert-monitoring-and-management-experience)

- **Microsoft Defender for Endpoint に送信されるシグナルの新しいグローバル重要度設定**  
Microsoft Defender for Endpoint に送信されるシグナルのグローバル重要度設定を指定する機能が追加されました。 詳細については、「[Microsoft Defender for Endpoint を Cloud App Security と統合する方法](mde-integration.md#how-to-integrate-microsoft-defender-for-endpoint-with-cloud-app-security)」を参照してください。

- **新しいセキュリティに関する推奨事項のレポート**  
Cloud App Security を使用すると、Azure、アマゾン ウェブ サービス (AWS)、および Google Cloud Platform (GCP) のセキュリティ構成に関する評価が提供され、マルチクラウド環境におけるセキュリティ構成のギャップについての分析情報を得られます。 クラウド環境の監視、理解、カスタマイズを行い、組織の保護を強化するために役立つ、セキュリティに関する推奨事項の詳細なレポートをエクスポートできるようになりました。 レポートのエクスポートについて詳しくは、「[セキュリティに関する推奨事項のレポート](security-config.md#security-recommendations-report)」をご覧ください。

- **セッション制御の拡張プロキシ URL サフィックス (段階的なロールアウト)**  
2020 年 6 月 7 日に、名前付きリージョンを含まない 1 つの統合サフィックスを使用する、拡張プロキシ セッション制御の段階的なロールアウトを開始しました。 たとえば、ユーザーには `<AppName>.<Region>.cas.ms` の代わりに `<AppName>.mcas.ms` サフィックスが表示されます。 ネットワーク アプライアンスまたはゲートウェイのドメインを定期的にブロックする場合は、「[アクセス制御とセッション制御](network-requirements.md#access-and-session-controls)」に一覧表示されているすべてのドメインを許可リストに登録してください。

- **クラウド アプリ カタログの更新**  
クラウド アプリ カタログに対して次の更新が行われました。

  - Teams 管理センターがスタンドアロン アプリとして更新されました
  - Microsoft Office 365 管理センターの名前が Office ポータルに変更されました

- **用語の更新**  
製品全体で用語を統一する Microsoft の全般的な取り組みの一環として、**コンピューター** という用語が **デバイス** に更新されました。

## <a name="cloud-app-security-release-182-and-183"></a>Cloud App Security リリース 182 と 183

リリース日: 2020 年 9 月 6 日

- **Azure portal GA のアクセスとセッションの制御**  
Azure portal のアプリの条件付きアクセス制御の一般提供が開始されました。 これらの制御の構成に関する詳細については、[デプロイに関するこちらのガイド](proxy-deployment-aad.md)を参照してください。

## <a name="cloud-app-security-release-181"></a>Cloud App Security リリース 181

リリース日: 2020 年 8 月 9 日

- **新しい Cloud Discovery Menlo Security ログパーサー**  
Cloud App Security の Cloud Discovery では、さまざまなトラフィック ログを分析して、アプリの順位付けとスコア付けを行います。 今回、Menlo Security CEF 形式をサポートする組み込みのログ パーサーが Cloud Discovery に追加されました。 サポートされているログ パーサーの一覧については、「[サポートされているファイアウォールとプロキシ](set-up-cloud-discovery.md#supported-firewalls-and-proxies)」をご覧ください。

- **ポータルでの Azure Active Directory (AD) の Cloud App Discovery 名の表示**  
Azure AD P1 と P2 のライセンスについて、ポータルでの製品名を **Cloud App Discovery** に更新しました。 [Cloud App Discovery](editions-cloud-app-security-aad.md) の詳細をご確認ください。

## <a name="cloud-app-security-release-179-and-180"></a>Cloud App Security リリース 179 と 180

リリース日: 2020 年 7 月 26 日

- **新しい異常検出:疑わしい OAuth アプリ ファイルのダウンロード アクティビティ**  
OAuth アプリによる疑わしいダウンロード アクティビティを含めるよう、異常検出を拡張しました。 すぐに使用できるこの新しい検出は、自動的に有効になり、OAuth アプリによってユーザーにとって異常な方法で Microsoft SharePoint または Microsoft OneDrive から複数のファイルがダウンロードされると、アラートが生成されます。

- **プロキシ キャッシュを使用したセッション制御のパフォーマンスの向上 (段階的なロールアウト)**  
コンテンツのキャッシュ メカニズムを強化することで、セッション制御のパフォーマンスをさらに向上させました。 改善されたサービスはさらに合理化され、セッション制御を使用する際の応答性が向上します。 セッション制御では、共有 (パブリック) コンテンツのみをキャッシュするための適切な標準に合わせて、プライベート コンテンツはキャッシュされないことに注意してください。 詳細については、「[セッション制御のしくみ](proxy-intro-aad.md#how-session-control-works)」を参照してください。

- **新機能:セキュリティ構成クエリの保存**  
Azure、アマゾン ウェブ サービス (AWS)、Google Cloud Platform (GCP) 用のセキュリティ構成ダッシュボード フィルターのクエリを保存する機能が追加されました。 これにより、一般的なクエリを再利用することで、今後の調査をさらに簡単に行うことができます。 [セキュリティ構成の推奨事項](security-config.md)に関する記事を参照してください。

- **強化された異常検出アラート**  
異常検出アラートに関して提供している情報を拡張し、対応する MITRE ATT\&CK の方策に対するマッピングを含めました。 このマッピングは、攻撃のフェーズと影響を理解し、調査することに役立ちます。 詳細については、「[異常検出アラートを調査する方法](investigate-anomaly-alerts.md)」を参照してください。

- **強化された検出ロジック: ランサムウェアのアクティビティ**  
ランサムウェアのアクティビティに関する検出ロジックを更新し、精度を向上させ、アラート量を減らしました。 この異常検出ポリシーの詳細については、「[ランサムウェアのアクティビティ](anomaly-detection-policy.md#ransomware-activity)」を参照してください。

- **ID セキュリティ態勢のレポート: タグの表示**  
エンティティに関する追加の分析情報を提供する ID セキュリティ態勢のレポートに、エンティティ タグを追加しました。 たとえば、 **[機密]** タグは、危険なユーザーを特定し、調査の優先順位を付けるのに役立ちます。 [危険なユーザーの調査](tutorial-ueba.md)に関する記事を参照してください。

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
Cloud App Security では、シャドウ IT 検出調査の一環としてリスクの高いコンピューターを特定できます。 このたび、**コンピューター** ページに Microsoft Defender Advanced Threat Protection の **マシンのリスク レベル** を追加しました。組織内でコンピューターを調査するとき、アナリストに与えられる背景情報が増えます。 詳細については、「[Cloud App Security でデバイスを調査する](mde-integration.md#investigate-devices-in-cloud-app-security)」を参照してください。

- **新機能:アプリ コネクタのセルフサービス無効化 (段階的ロールアウト)**  
Cloud App Security で直接、アプリ コネクタを無効にする機能を追加しました。 詳細については、「[アプリ コネクタの無効化](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md#disable-app-connectors)」を参照してください。

## <a name="cloud-app-security-release-177"></a>Cloud App Security リリース 177

リリース日: 2020 年 6 月 14 日

- **新しいリアルタイム マルウェア検出 (プレビュー、段階的なロールアウト)**  
ファイルのアップロードまたはダウンロード時に Microsoft 脅威インテリジェンスを使用して潜在的なマルウェアを検出するように、セッション制御を拡張しました。 新しい検出をすぐに使用できるようになりました。これは潜在的なマルウェアとして識別されたファイルを自動的にブロックするように構成できます。 詳細については、「[アップロード時にマルウェアをブロックする](session-policy-aad.md#block-malware-on-upload)」を参照してください。

- **アクセスとセッションの制御のための新しいアクセス トークンのサポート**  
アクセスとセッションの制御に対してアプリをオンボードするときに、アクセス トークンとコードの要求をログインとして扱う機能を追加しました。 トークンを使用するには、設定の歯車アイコンをクリックし、 **[アプリの条件付きアクセス制御]** を選択して、関連するアプリを編集し (3 つの点のメニュー > **[アプリの編集]** )、 **[Treat access token and code requests as app logins]\(アクセス トークンとコードの要求をアプリのログインとして扱う\)** を選択して、 **[保存]** をクリックします。 アプリのオンボードの詳細については、[アプリのオンボードとデプロイ](proxy-deployment-any-app.md)に関するページと[おすすめアプリのデプロイ](proxy-deployment-aad.md)に関するページを参照してください。

- **セッション制御の拡張プロキシ URL サフィックス (段階的なロールアウト)**  
2020 年 6 月 7 日に、名前付きリージョンを含まない 1 つの統合サフィックスを使用する、拡張プロキシ セッション制御の段階的なロールアウトを開始しました。 たとえば、ユーザーには `<AppName>.<Region>.cas.ms` の代わりに `<AppName>.mcas.ms` サフィックスが表示されます。 ネットワーク アプライアンスまたはゲートウェイのドメインを定期的にブロックする場合は、「[アクセス制御とセッション制御](network-requirements.md#access-and-session-controls)」に一覧表示されているすべてのドメインを許可リストに登録してください。

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
2020 年 6 月 7 日から、名前付きリージョンを含まない 1 つの統合サフィックスを使用する、拡張プロキシ セッション制御が段階的にロールアウトされます。 たとえば、ユーザーには `<AppName>.<Region>.cas.ms` の代わりに `<AppName>.mcas.ms` サフィックスが表示されます。 ネットワーク アプライアンスまたはゲートウェイのドメインを定期的にブロック リストに登録する場合は、「[アクセス制御とセッション制御](network-requirements.md#access-and-session-controls)」に一覧表示されているすべてのドメインを許可リストに登録してください。

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
異常に関するポリシーの現行のガバナンス アクションを拡張し、**ユーザーに対するセキュリティ侵害を確認** を追加しました。疑わしいユーザー活動からご自分の環境を積極的に保護することができます。 詳細については、「[アクティビティ ガバナンス アクション](governance-actions.md#activity-governance-actions)」を参照してください。

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
Cloud App Security に取り込まれた Azure AD Identity Protection アラートの重要度を制御できるようになりました。 また、**Azure AD の危険なサインイン** の検出をまだ有効にしていない場合は、重要度の高いアラートを取り込むためにこの検出が自動的に有効になります。 詳細については、「[Azure Active Directory Identity Protection の統合](aadip-integration.md)」を参照してください。

## <a name="cloud-app-security-release-169"></a>Cloud App Security リリース 169

リリース日: 2020 年 3 月 1 日

- **Workday の新しい検出**  
Workday の異常な動作に関するアラートを拡張しました。 新しいアラートには、次のユーザー位置情報の検出が含まれます。
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
Cloud App Security により、Microsoft Defender Advanced Threat Protection (ATP) とのネイティブ統合が拡張されました。 Microsoft Defender ATP のネットワーク保護機能を使用して、承認されていないものとマークされているアプリへのアクセスをブロックできるようになりました。 詳しくは、「[承認されていないクラウドアプリへのアクセスをブロックする](mde-integration.md#block-access-to-unsanctioned-cloud-apps)」をご覧ください。

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

## <a name="see-also"></a>関連項目

ここに記載されているものより前のリリースの説明については、[Microsoft Cloud App Security の過去のリリース](release-note-archive.md)に関する記事をご覧ください。

[!INCLUDE [Open support ticket](includes/support.md)]