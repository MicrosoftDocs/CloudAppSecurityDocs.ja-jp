---
title: Microsoft Cloud App Security の Azure セキュリティ ベースライン
description: Microsoft Cloud App Security のセキュリティ ベースラインは、Azure セキュリティ ベンチマークで指定されたセキュリティに関する推奨事項を実装するための手順に関するガイダンスとリソースを提供します。
author: msmbaldwin
ms.service: cloud-app-security
ms.topic: conceptual
ms.date: 12/03/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 0c659e0682cef4239bb5fe6d07b1cea84247b1a5
ms.sourcegitcommit: 0768aa1992819e2651a14a731f79e178fdececc5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "98114685"
---
# <a name="azure-security-baseline-for-microsoft-cloud-app-security"></a>Microsoft Cloud App Security の Azure セキュリティ ベースライン

このセキュリティ ベースラインは、[Azure セキュリティ ベンチマーク バージョン 2.0](/azure/security/benchmarks/overview) のガイダンスを Microsoft Cloud App Security に適用します。 Azure セキュリティ ベンチマークには、Azure 上のクラウド ソリューションをセキュリティで保護する方法に関する推奨事項がまとめてあります。 コンテンツは、Azure セキュリティ ベンチマークで定義されている **セキュリティ コントロール** と、Microsoft Cloud App Security に適用される関連ガイダンスごとにグループ化されています。 Microsoft Cloud App Security に適用できない **コントロール** は除外されています。

Microsoft Cloud App Security と Azure セキュリティ ベンチマークの完全なマッピングについては、[完全な Microsoft Cloud App Security セキュリティ ベースライン マッピング ファイル](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines)を参照してください。

## <a name="network-security"></a>ネットワークのセキュリティ

*詳細については、[Azure セキュリティ ベンチマークの「ネットワークのセキュリティ](/azure/security/benchmarks/security-controls-v2-network-security)」を参照してください。*

### <a name="ns-6-simplify-network-security-rules"></a>NS-6: ネットワーク セキュリティ規則を簡略化する

**ガイダンス**: Azure Virtual Network のサービス タグを使用して、ネットワーク セキュリティ グループまたは Cloud App Security リソース用に構成された Azure Firewall 上にネットワーク アクセスの制御を定義します。 セキュリティ規則を作成するときは、特定の IP アドレスの代わりにサービス タグを使うことができます。 サービス タグ名 (例: "Microsoft Cloudappsecurity") をルールの適切なソースまたは送信先のフィールドに指定すると、対応するサービスのトラフィックを許可または拒否することができます。 サービス タグに含まれるアドレス プレフィックスの管理は Microsoft が行い、アドレスが変化するとサービス タグは自動的に更新されます。

- [サービス タグとその使用方法の概要](/azure/virtual-network/service-tags-overview)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

## <a name="identity-management"></a>ID 管理

*詳細については、[Azure セキュリティ ベンチマークの「ID 管理](/azure/security/benchmarks/security-controls-v2-identity-management).* 」を参照してください。

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1:Azure Active Directory を中央 ID および認証システムとして標準化する

**ガイダンス**: Cloud App Security は、既定の ID とアクセス管理サービスとして Azure Active Directory (Azure AD) を使用します。 Azure AD を標準化して、次のリソースでの組織の ID とアクセス管理を統制する必要があります。

- Azure portal、Azure Storage、Azure 仮想マシン (Linux と Windows)、Azure Key Vault、PaaS、SaaS アプリケーションなどの Microsoft Cloud リソース。

- Azure 上のアプリケーションや企業ネットワーク リソースなどの組織のリソース。

Azure AD を保護することは、組織のクラウド セキュリティ プラクティスの中で高い優先順位を持つ必要があります。 Azure AD では、Microsoft のベスト プラクティスの推奨事項を基準にした、お客様の ID セキュリティ体制を評価するために役立つ ID セキュリティ スコアが提供されます。 スコアを使用して、構成がベスト プラクティスの推奨事項とどの程度一致しているかを測定し、セキュリティ体制を強化します。

注:Azure AD では、外部 ID がサポートされます。これにより、Microsoft アカウントを持たないユーザーが、外部 ID を使用してアプリケーションやリソースにサインインできるようになります。

- [Azure Active Directory のテナント](/azure/active-directory/develop/single-and-multi-tenant-apps) 

- [Azure AD インスタンスを作成して構成する方法](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant) 

- [アプリケーションに外部 ID プロバイダーを使用する](/azure/active-directory/b2b/identity-providers) 

- [Azure Active Directory の ID セキュリティ スコアとは](/azure/active-directory/fundamentals/identity-secure-score)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="im-3-use-azure-ad-single-sign-on-sso-for-application-access"></a>IM-3:アプリケーションのアクセスに Azure AD シングル サインオン (SSO) を使用する

**ガイダンス**: Cloud App Security は Azure Active Directory (Azure AD) を使用して、Azure リソース、クラウド アプリケーション、オンプレミス アプリケーションに ID とアクセス管理を提供します。 これには、従業員などの企業 ID だけでなく、パートナー、ベンダー、サプライヤーなどの外部 ID も含まれます。 これにより、オンプレミスおよびクラウド内の組織のデータとリソースへのアクセスを管理し、セキュリティで保護するためのシングルサインオン (SSO) が可能になります。 すべてのユーザー、アプリケーション、およびデバイスを Azure AD に接続して、シームレスで安全なアクセスを実現し、可視性と制御を向上させることができます。

- [Azure AD を使用したアプリケーションの SSO について理解する](/azure/active-directory/manage-apps/what-is-single-sign-on)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4:すべての Azure Active Directory ベースのアクセスに強力な認証制御を使用する

**ガイダンス**: Cloud App Security は Azure Active Directory (Azure AD) を使用して、多要素認証とパスワードレス認証による強力な認証制御をサポートしています。

- 多要素認証 - Azure AD 多要素認証を有効にし、多要素認証のセットアップに関する Azure Security Center の ID とアクセス管理の推奨事項に従います。 多要素認証は、サインイン条件とリスク要因に基づいて、すべてのユーザー、選択したユーザー、またはユーザーごとのレベルに適用できます。

- パスワードレス認証 - 3 つのパスワードレス認証オプションを使用できます。Windows Hello for Business、Microsoft Authenticator アプリ、スマート カードなどのオンプレミスの認証方法。

管理者と特権ユーザーについて、高いレベルの強力な認証方法が使用されていることを確認し、その後、適切な強力な認証ポリシーを他のユーザーにロールアウトします。

- [Azure で多要素認証を有効にする方法](/azure/active-directory/authentication/howto-mfa-getstarted) 

- [Azure Active Directory のパスワードレス認証オプションの概要](/azure/active-directory/authentication/concept-authentication-passwordless) 

- [Azure AD の規定のパスワード ポリシー](/azure/active-directory/authentication/concept-sspr-policy#password-policies-that-only-apply-to-cloud-user-accounts) 

- [Azure AD のパスワード保護を使用して不適切なパスワードを排除する](/azure/active-directory/authentication/concept-password-ban-bad)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="im-6-restrict-azure-resource-access-based-on-conditions"></a>IM-6:条件に基づいて Azure リソースへのアクセスを制限する

**ガイダンス**: Cloud App Security は、特定の IP 範囲からのユーザー ログインではログインに MFA を使用する必要があるなど、ユーザー定義の条件に基づいて、より詳細なアクセスの制御に関する Azure Active Directory (Azure AD) 条件付きアクセスをサポートします。 さまざまなユース ケースに対して、きめ細かい認証セッション管理ポリシーを使用することもできます。

- [Conditional Access App Control 保護](what-is-cloud-app-security.md#conditional-access-app-control-protection)

- [Azure での条件付きアクセスの概要](/azure/active-directory/conditional-access/overview) 

- [一般的な条件付きアクセス ポリシー](/azure/active-directory/conditional-access/concept-conditional-access-policy-common) 

- [条件付きアクセスを使用して認証セッション管理を構成する](/azure/active-directory/conditional-access/howto-conditional-access-session-lifetime)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="privileged-access"></a>特権アクセス

*詳細については、[Azure セキュリティ ベンチマークの「特権アクセス](/azure/security/benchmarks/security-controls-v2-privileged-access)」を参照してください。*

### <a name="pa-1-protect-and-limit-highly-privileged-users"></a>PA-1:高い特権を持つユーザーを保護および制限する

**ガイダンス**: Cloud App Security には、次の高い特権を持つアカウントがあります。

- 全体管理者、セキュリティ管理者:フル アクセスの権限を持つ管理者には、Cloud App Security での完全なアクセス許可があります。 管理者の追加、ポリシーと設定の追加、ログのアップロード、ガバナンス アクションの実行を行うことができます。
- コンプライアンス管理者: 読み取り専用アクセス許可を持ち、アラートを管理できます。 クラウド プラットフォームのセキュリティに関する推奨事項にはアクセスできません。 ファイル ポリシーの作成と変更、ファイル ガバナンス アクションの許可、データ管理でのすべての組み込みレポートの表示を行うことができます。
- コンプライアンス データ管理者: 読み取り専用アクセス許可を持ち、ファイル ポリシーの作成と変更、ファイル ガバナンス アクションの許可、すべての検出レポートの表示を行うことができます。 クラウド プラットフォームのセキュリティに関する推奨事項にはアクセスできません。
- セキュリティ オペレーター: 読み取り専用アクセス許可を持ち、アラートを管理できます。
- セキュリティ閲覧者: 読み取り専用アクセス許可を持ち、アラートを管理できます。 セキュリティ閲覧者は、以下のアクションを行うことはできません。
  - ポリシーを作成する、または既存のポリシーを編集および変更する
  - ガバナンス アクションを実行する

  - 探索ログをアップロードする

  - サードパーティのアプリの禁止または承認

  - IP アドレス範囲設定ページへのアクセスと表示

  - すべてのシステム設定ページへのアクセスと表示

  - 検出設定へのアクセスと表示

  - アプリ コネクタ ページへのアクセスと表示

  - ガバナンス ログへのアクセスと表示

  - [スナップショット レポートの管理] ページへのアクセスと表示

  - SIEM エージェントへのアクセスと編集

- グローバル閲覧者: Cloud App Security のすべての部分に対する完全な読み取り専用アクセス権を持ちます。 設定を変更したり、アクションを実行したりすることはできません。

高い特権を持つユーザーは、Azure 環境内のすべてのリソースを直接または間接的に読み取り、変更することができるため、この特権を持つアカウントまたはロールの数を制限し、これらのアカウントを高いレベルで保護してください。

Azure Privileged Identity Management (PIM) を使用して、Azure リソースと Azure AD への Just-In-Time (JIT) の特権アクセスを有効にすることができます。 ユーザーが必要とする場合にのみ特権タスクを実行するための一時的なアクセス許可は、JIT によって付与されます。 PIM を使用すると、Azure AD 組織に不審なアクティビティや安全でないアクティビティがある場合に、セキュリティ アラートを生成することもできます。

- [Cloud App Security での管理者アクセスを管理する](manage-admins.md)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2:ビジネス クリティカルなシステムへの管理アクセスを制限する

**ガイダンス**: Cloud App Security は管理者向けにロールベースのアクセス制御を提供しています。

- [Cloud App Security の管理者アクセスを管理する](manage-admins.md)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="pa-3-review-and-reconcile-user-access-regularly"></a>PA-3:ユーザー アクセスを定期的に確認して調整する

**ガイダンス**: Cloud App Security は Azure Active Directory (Azure AD) アカウントを使用してリソースを管理し、ユーザー アカウントを確認し、割り当てに定期的にアクセスして、アカウントとそのアクセスが有効であることを確認します。 Azure AD アクセス レビューを使用して、グループ メンバーシップ、エンタープライズ アプリケーションへのアクセス、およびロールの割り当てをレビューすることができます。 Azure AD レポートによって、古いアカウントの検出に役立つログが提供されます。 また、Azure AD Privileged Identity Management を使用してアクセス レビュー レポート ワークフローを作成し、レビュー プロセスを容易にすることもできます。

さらに、過剰な数の管理者アカウントが作成された場合にアラートを発行したり、古い管理者アカウントや不適切に構成されている管理者アカウントを特定するように Azure Privileged Identity Management を構成することもできます。

注:一部の Azure サービスでは、Azure AD で管理されていないローカル ユーザーとロールがサポートされています。 これらのユーザーは個別に管理する必要があります。

- [Privileged Identity Management (PIM) で Azure リソース ロールのアクセス レビューを作成する](/azure/active-directory/privileged-identity-management/pim-resource-roles-start-access-review) 

- [Azure AD の ID およびアクセス レビューの使用方法](/azure/active-directory/governance/access-reviews-overvie)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="pa-4-set-up-emergency-access-in-azure-ad"></a>PA-4:Azure AD で緊急アクセスを設定する

**ガイダンス**: Cloud App Security は Azure Active Directory (Azure AD) を使用してリソースを管理します。 Azure AD 組織から誤ってロックアウトされるのを防ぐために、通常の管理者アカウントを使用できない場合にアクセスするための緊急アクセス用アカウントを設定します。 緊急アクセス用アカウントは、通常、高い権限を持っているため、特定のユーザーに割り当てることはできません。 緊急アクセス用アカウントは、通常の管理者アカウントを使うことができない "緊急事態" に制限されます。

緊急アクセス用アカウントの資格情報 (パスワード、証明書、スマート カードなど) がセキュリティで保護され、緊急時に使用することが許可されているユーザーのみに通知されるようにする必要があります。

- [Azure AD で緊急アクセス用アカウントを管理する](/azure/active-directory/users-groups-roles/directory-emergency-access)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-5-automate-entitlement-management"></a>PA-5:エンタイトルメント管理を自動化する 

**ガイダンス**: Cloud App Security は Azure Active Directory (Azure AD) との統合によってリソースを管理します。 Azure AD のエンタイトルメント管理機能を使用して、アクセスの割り当て、レビュー、有効期限など、アクセス要求のワークフローを自動化します。 2 段階または複数段階の承認もサポートされています。

- [Azure AD アクセス レビューとは](/azure/active-directory/governance/access-reviews-overview) 

- [Azure AD エンタイトルメント管理とは](/azure/active-directory/governance/entitlement-management-overview)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="pa-7-follow-just-enough-administration-least-privilege-principle"></a>PA-7:Just Enough Administration (最小限の特権の原則) に従う 

**ガイダンス**: Cloud App Security は Azure のロールベースのアクセス制御 (RBAC) との統合によってリソースを管理します。 Azure RBAC を使用すると、ロールの割り当てによって Azure リソースへのアクセスを管理できます。 これらのロールを、ユーザー、グループ サービス プリンシパル、およびマネージド ID に割り当てることができます。 特定のリソースに対して定義済みの組み込みロールがあります。これらのロールは、Azure CLI、Azure PowerShell、Azure portal などのツールを使用してインベントリまたは照会できます。 Azure RBAC を使用してリソースに割り当てる特権は、常に、ロールで必要なものに制限する必要があります。 これは、Azure Active Directory Privileged Identity Management (PIM) のジャスト イン タイム (JIT) アプローチを補完するものであり、定期的に見直す必要があります。

組み込みロールを使用してアクセス許可を割り当て、必要な場合にのみカスタム ロールを作成します。

- [Cloud App Security にアクセスできる Office 365 および Azure AD のロール](manage-admins.md)

Azure ロールベースのアクセス制御 (Azure RBAC) とは https://docs.microsoft.com/azure/role-based-access-control/overview 

- [Azure で RBAC を構成する方法](/azure/role-based-access-control/role-assignments-portal) 

- [Azure AD の ID およびアクセス レビューの使用方法](/azure/active-directory/governance/access-reviews-overview)

**Azure Security Center の監視**: はい

**責任**: Customer

## <a name="data-protection"></a>データ保護

*詳細については、[Azure セキュリティ ベンチマークの「データ保護](/azure/security/benchmarks/security-controls-v2-data-protection)」を参照してください。*

### <a name="dp-2-protect-sensitive-data"></a>DP-2:機密データを保護する

**ガイダンス**: Cloud App Security は、機密データを管理し、Azure AD のロールを使用して、さまざまな種類のデータのアクセス許可を制御します。

- [Cloud App Security にアクセスできる Azure AD のロール](manage-admins.md#office-365-and-azure-ad-roles-with-access-to-cloud-app-security)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="dp-4-encrypt-sensitive-information-in-transit"></a>DP-4:転送中の機密情報を暗号化する

**ガイダンス**: Cloud App Security は、TLS v1.2 以上で転送中のデータの暗号化をサポートしています。

これはプライベート ネットワーク上のトラフィックでは省略できますが、外部ネットワークとパブリック ネットワーク上のトラフィックには重要です。 ご自分の Azure リソースに接続するすべてのクライアントの HTTP トラフィックのネゴシエートには、確実に TLS v1.2 以上を使用してください。 リモート管理には、暗号化されていないプロトコルではなく、(Linux の場合) SSH または (Windows の場合) RDP/TLS を使用します。 無効な SSL、TLS、SSH のバージョンとプロトコル、および弱い暗号は無効にする必要があります。

既定では Azure によって、Azure のデータ センター間の転送データが暗号化されます。

- [Microsoft Cloud App Security のデータ セキュリティとプライバシー](cas-compliance-trust.md#encryption)

- [Azure での転送中の暗号化の概要](/azure/security/fundamentals/encryption-overview#encryption-of-data-in-transit) 

- [TLS セキュリティに関する情報](/security/engineering/solving-tls1-problem) 

- [転送中の Azure データの二重暗号化](/azure/security/fundamentals/double-encryption#data-in-transit)

**Azure Security Center の監視**: 適用なし

**責任**: 共有

## <a name="asset-management"></a>アセット管理

*詳細については、[Azure セキュリティ ベンチマークの「アセット管理](/azure/security/benchmarks/security-controls-v2-asset-management)」を参照してください。*

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>AM-1:セキュリティ チームが資産のリスクを確実に可視化できるようにする

**ガイダンス**:セキュリティ チームに Azure テナントとサブスクリプションのセキュリティ閲覧者アクセス許可を付与して、セキュリティ チームが Azure Security Center を使用してセキュリティ上のリスクを監視できるようにします。 

セキュリティ リスクの監視は、セキュリティ チームの責任の構造に応じて、中央のセキュリティ チームまたはローカル チームの責任になります。 ただし、セキュリティ分析情報とリスクは、常に組織内で一元的に集計する必要があります。 

セキュリティ閲覧者のアクセス許可は、テナント全体 (ルート管理グループ) に幅広く適用することも、管理グループまたは特定のサブスクリプションにスコープ指定することもできます。 

注:ワークロードとサービスを可視化するには、追加のアクセス許可が必要になることがあります。 

- [セキュリティ閲覧者ロールの概要](/azure/role-based-access-control/built-in-roles#security-reader)

- [Azure 管理グループの概要](/azure/governance/management-groups/overview)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

## <a name="logging-and-threat-detection"></a>ログと脅威検出

*詳細については、[Azure セキュリティ ベンチマークの「ログと脅威検出](/azure/security/benchmarks/security-controls-v2-logging-threat-protection)」を参照してください。*

### <a name="lt-1-enable-threat-detection-for-azure-resources"></a>LT-1:Azure リソースの脅威検出を有効にする

**ガイダンス**: Cloud App Security から、カスタム脅威検出の設定に使用できる SIEM にログを転送します。 潜在的な脅威や異常を検出するために、さまざまな種類の Azure 資産を監視していることを確認してください。 アナリストが選別しやすいように、質の高いアラートを取得して誤検知を減らすことに専念します。 アラートは、ログ データ、エージェント、その他のデータを元に生成できます。

- [Azure Sentinel の統合](siem-sentinel.md)
- [汎用 SIEM の統合](siem.md)

- [脅威を検出するためのカスタム分析規則を作成する](/azure/sentinel/tutorial-detect-threats-custom) 

- [Azure Sentinel を使用したサイバー脅威インテリジェンス](/azure/architecture/example-scenario/data/sentinel-threat-intelligence)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="incident-response"></a>インシデント対応

*詳細については、[Azure セキュリティ ベンチマークの「インシデント対応](/azure/security/benchmarks/security-controls-v2-incident-response)」を参照してください。*

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1: 準備 – インシデント対応プロセスを Azure 用に更新する

**ガイダンス**:組織において、セキュリティ インシデントに対応するためのプロセスが用意されていること、Azure のこれらのプロセスが更新されていること、それらのプロセスを定期的に使用して準備されていることを確認します。

- [企業環境全体にセキュリティを実装する](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [インシデント対応のリファレンス ガイド](/microsoft-365/downloads/IR-Reference-Guide.pdf)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2: 準備 – インシデント通知をセットアップする

**ガイダンス**:Azure Security Center でセキュリティ インシデントの連絡先情報を設定します。 この連絡先情報は、Microsoft Security Response Center (MSRC) でユーザーのデータが違法または権限のないユーザーによってアクセスされたことが検出された場合に、Microsoft からの連絡先として使用されます。 インシデント対応のニーズに応じて、さまざまな Azure サービスでインシデント アラートや通知をカスタマイズするオプションもあります。 

- [Azure Security Center のセキュリティ連絡先を設定する方法](/azure/security-center/security-center-provide-security-contact-details)

**Azure Security Center の監視**: はい

**責任**: Customer

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3: 検出と分析 – 高品質のアラートに基づいてインシデントを作成する

**ガイダンス**:高品質のアラートを作成し、アラートの品質を測定するプロセスがあることを確認します。 これにより、過去のインシデントから教訓を学び、アナリストに対するアラートに優先順位を付けることができるので、擬陽性に時間を無駄にすることがありません。 

高品質のアラートは、過去のインシデントからの経験、検証されたコミュニティ ソース、およびさまざまなシグナル ソースの融合と関連付けによってアラートを生成してクリーンアップするように設計されたツールに基づいて構築できます。 

Azure Security Center (ASC) は、多くの Azure 資産にわたって高品質のアラートを提供します。 ASC データ コネクタを使用してアラートを Azure Sentinel にストリーミングできます。 Azure Sentinel を使用すると、高度なアラート ルールを作成し、調査のためにインシデントを自動的に生成できます。 

エクスポート機能を使用して Azure Security Center のアラートと推奨事項をエクスポートし、Azure リソースへのリスクを特定します。 アラートと推奨事項を手動で、または継続した連続的な方法でエクスポートします。

- [エクスポートを構成する方法](/azure/security-center/continuous-export)

- [Azure Sentinel にアラートをストリーミングする方法](/azure/sentinel/connect-azure-security-center)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>IR-4: 検出と分析 – インシデントを調査する

**ガイダンス**:アナリストが潜在的なインシデントを調査するときに、さまざまなデータ ソースを照会して使用し、発生した内容の完全なビューを構築できることを確認します。 キル チェーン全体で潜在的な攻撃者のアクティビティを追跡して死角を回避するには、さまざまなログを収集する必要があります。  また、他のアナリストのため、および将来において履歴が参照される場合のために、確実に分析情報と学習がキャプチャされているようにします。  

調査対象のデータ ソースには、スコープ内のサービスおよび実行中のシステムから既に収集されている一元化されたログ ソースが含まれますが、次のものも含まれます。

- ネットワーク データ - ネットワーク セキュリティ グループのフロー ログ、Azure Network Watcher、Azure Monitor を使用して、ネットワーク フロー ログやその他の分析情報をキャプチャします。 

- 実行中のシステムのスナップショット: 

    - Azure 仮想マシンのスナップショット機能を使用して、実行中のシステムのディスクのスナップショットを作成します。 

    - オペレーティング システムのネイティブ メモリ ダンプ機能を使用して、実行中のシステムのメモリのスナップショットを作成します。

    - Azure サービスのスナップショット機能またはソフトウェア独自の機能を使用して、実行中のシステムのスナップショットを作成します。

Azure Sentinel により、事実上すべてのログソースに対して広範な Data Analytics と、インシデントのライフサイクル全体を管理するためのケース管理ポータルが提供されます。 調査中のインテリジェンス情報を、追跡とレポートのためにインシデントに関連付けることができます。 

- [Windows マシンのディスクのスナップショットを作成する](/azure/virtual-machines/windows/snapshot-copy-managed-disk)

- [Linux マシンのディスクのスナップショットを作成する](/azure/virtual-machines/linux/snapshot-copy-managed-disk)

- [Microsoft Azure サポートの診断情報とメモリ ダンプ コレクション](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [Azure Sentinel でインシデントを調査します](/azure/sentinel/tutorial-investigate-cases)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5: 検出と分析 – インシデントの優先順位を付ける

**ガイダンス**:アラートの重要度と資産の機密性に基づいて、最初に注目するインシデントについてのコンテキストをアナリストに提供します。 

Azure Security Center によって各アラートに重大度が割り当てられるため、最初に調査する必要があるアラートの優先順位付けに役立ちます。 重要度は、アラートの発行に使用された Security Center の信頼度と、アラートの原因となったアクティビティの背後に悪意のある意図があったかどうかの信頼レベルに基づいて決まります。

さらに、タグを使用してリソースをマークし、Azure リソース (特に、機密データを処理するもの) を識別して分類するための命名システムを作成します。  インシデントが発生した Azure リソースと環境の重要度に基づいて、アラートの修復に優先順位を付けることは、お客様の責任です。

- [Security alerts in Azure Security Center](/azure/security-center/security-center-alerts-overview)

- [タグを使用した Azure リソースの整理](/azure/azure-resource-manager/resource-group-using-tags)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6: 包含、根絶、復旧 – インシデントの処理を自動化する

**ガイダンス**:手動による反復タスクを自動化して、応答時間を短縮し、アナリストの負担を軽減します。 手動タスクを実行すると時間がかかり、各インシデントの速度が低下し、アナリストが処理できるインシデントの数が減少します。 手動タスクではアナリストの疲労も増加します。これにより、遅延が発生する人的エラーのリスクが増加し、複雑なタスクに効果的に焦点を当てるアナリストの能力が低下します。 Azure Security Center と Azure Sentinel のワークフロー自動化機能を使用して、自動的にアクションをトリガーしたり、プレイブックを実行して受信したセキュリティ アラートに応答したりします。 プレイブックにより、通知の送信、アカウントの無効化、問題のあるネットワークの特定などのアクションが実行されます。 

- [Security Center でワークフロー自動化を構成する](/azure/security-center/workflow-automation)

- [Azure Security Center で脅威への自動対応を設定する](/azure/security-center/tutorial-security-incident#triage-security-alerts)

- [Azure Sentinel で脅威への自動対応を設定します](/azure/sentinel/tutorial-respond-threats-playbook)

**Azure Security Center の監視**: 現在は使用できません

**責任**: Customer

## <a name="posture-and-vulnerability-management"></a>体制と脆弱性の管理

*詳細については、[Azure セキュリティ ベンチマークの「体制と脆弱性の管理](/azure/security/benchmarks/security-controls-v2-vulnerability-management)」を参照してください。*

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8: 定期的に攻撃シミュレーションを実施する

**ガイダンス**:必要に応じて、Azure リソースの侵入テストまたはレッド チーム アクティビティを実施し、セキュリティに関するすべての重大な調査結果が確実に修復されるようにします。
お客様の侵入テストが Microsoft のポリシーに違反しないように、Microsoft クラウド侵入テストの実施ルールに従ってください。 Microsoft が管理しているクラウド インフラストラクチャ、サービス、アプリケーションに対する Red Teaming およびライブ サイト侵入テストに関する Microsoft の戦略と実施を活用してください。

- [Azure での侵入テスト](/azure/security/fundamentals/pen-testing)

- [侵入テストの実施ルール](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft Cloud Red Teaming](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Azure Security Center の監視**: 適用なし

**責任**: 共有

## <a name="governance-and-strategy"></a>ガバナンスと戦略

*詳細については、[Azure セキュリティ ベンチマークの「ガバナンスと戦略](/azure/security/benchmarks/security-controls-v2-governance-strategy)」を参照してください。*

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1: 資産の管理とデータ保護の戦略を定義する 

**ガイダンス**:システムとデータを継続的に監視および保護するための明確な戦略が文書化および伝達されるようにします。 ビジネスに不可欠なデータとシステムの検出、評価、保護、監視の優先順位を決定します。 

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   ビジネス リスクに応じたデータ分類標準

-   リスクと資産のインベントリに対するセキュリティ組織の可視性 

-   Azure サービスを使用するためのセキュリティ組織の承認 

-   ライフサイクルを通じた資産のセキュリティ

-   組織のデータ分類に従った必要なアクセス制御戦略

-   Azure のネイティブおよびサードパーティのデータ保護機能の使用

-   転送中および保存中のユース ケースのデータ暗号化要件

-   適切な暗号化標準

詳細については、次のリファレンスを参照してください。
- [Azure セキュリティ アーキテクチャに関する推奨事項 - ストレージ、データ、暗号化](/azure/architecture/framework/security/storage-data-encryption?amp;bc=%2fsecurity%2fcompass%2fbreadcrumb%2ftoc.json&toc=%2fsecurity%2fcompass%2ftoc.json)

- [Azure のセキュリティの基礎 - Azure のデータ セキュリティ、暗号化、ストレージ](/azure/security/fundamentals/encryption-overview)

- [クラウド導入フレームワーク - Azure のデータ セキュリティと暗号化のベスト プラクティス](/azure/security/fundamentals/data-encryption-best-practices?amp;bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json)

- [Azure セキュリティ ベンチマーク - アセット管理](/azure/security/benchmarks/security-benchmark-v2-asset-management)

- [Azure セキュリティ ベンチマーク - データ保護](/azure/security/benchmarks/security-benchmark-v2-data-protection)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2: 企業のセグメント化戦略を定義する 

**ガイダンス**:ID、ネットワーク、アプリケーション、サブスクリプション、管理グループ、その他のコントロールを利用し、アセットへのアクセスをセグメント化する企業規模の戦略を確立します。

セキュリティ分離の必要性と、互いと通信し、データにアクセスする必要があるシステムの日常的操作を有効にするという必要性のバランスを慎重に取ります。

セグメント化戦略は、ネットワーク セキュリティ、ID とアクセス モデル、アプリケーション アクセス許可とアクセス モデル、人的プロセスの制御など、あらゆるコントロールの種類を対象として確実に一貫性をもって実装します。

- [Azure のセグメント化戦略に関するガイド (動画)](/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)

- [Azure のセグメント化戦略に関するガイド (ドキュメント)](/security/compass/governance#enterprise-segmentation-strategy)

- [ネットワークのセグメント化を企業のセグメント化戦略に合わせる](/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3: セキュリティ態勢管理の戦略を定義する

**ガイダンス**:個々の資産とそれらがホストされている環境に対するリスクを継続的に測定し、軽減します。 公開されたアプリケーション、ネットワークのイングレスとエグレスのポイント、ユーザーと管理者のエンドポイントなど、価値の高い資産と高度に暴露された攻撃の可能性を優先します。

- [Azure セキュリティ ベンチマーク - 体制と脆弱性の管理](/azure/security/benchmarks/security-benchmark-v2-posture-vulnerability-management)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4: 組織の役割、責任、責務を整合させる

**ガイダンス**:セキュリティ組織における役割と責任に関する明確な戦略が文書化されて伝えられるようにします。 セキュリティに関する決定についてわかりやすく説明すること、共有される責任モデルについて全員に教育すること、クラウドをセキュリティで保護するテクノロジについて技術チームに教育することを優先とします。

- [Azure のセキュリティのベスト プラクティス 1 – 人: クラウド セキュリティに関する取り組みについてチームを教育する](/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey)

- [Azure のセキュリティのベスト プラクティス 2 - 人: クラウド セキュリティ テクノロジについてチームを教育する](/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology)

- [Azure のセキュリティのベスト プラクティス 3 - プロセス: クラウドのセキュリティに関する意思決定のアカウンタビリティを割り当てる](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-5-define-network-security-strategy"></a>GS-5: ネットワーク セキュリティ戦略を定義する

**ガイダンス**:組織全体のセキュリティ アクセス制御戦略の一環として、Azure ネットワーク セキュリティ アプローチを確立します。  

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   一元的なネットワーク管理とセキュリティ責任

-   エンタープライズ セグメント化戦略と一致する仮想ネットワーク セグメント化モデル

-   さまざまな脅威と攻撃のシナリオにおける修復戦略

-   インターネット エッジとイングレスおよびエグレス戦略

-   クラウドとオンプレミスのハイブリッド相互依存戦略

-   最新のネットワーク セキュリティ成果物 (例: ネットワーク図、参照ネットワーク アーキテクチャ)

詳細については、次のリファレンスを参照してください。
- [Azure のセキュリティのベスト プラクティス 11 - アーキテクチャ。単一の統合セキュリティ戦略](/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Azure セキュリティ ベンチマーク - ネットワーク セキュリティ](/azure/security/benchmarks/security-benchmark-v2-network-security)

- [Azure のネットワーク セキュリティの概要](/azure/security/fundamentals/network-overview)

- [エンタープライズ ネットワーク アーキテクチャ戦略](/azure/cloud-adoption-framework/ready/enterprise-scale/architecture)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6: ID と特権アクセス戦略を定義する

**ガイダンス**:組織全体のセキュリティ アクセス制御戦略の一環として、Azure の ID と特権アクセス アプローチを確立します。  

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   一元化された ID と認証システム、および他の内部および外部 ID システムとのその相互接続

-   さまざまなユース ケースおよび条件における強力な認証方法

-   高い特権を持つユーザーの保護

-   異常なユーザー アクティビティの監視と処理  

-   ユーザー ID とアクセスの確認と調整のプロセス

詳細については、次のリファレンスを参照してください。

- [Azure セキュリティ ベンチマーク - ID 管理](/azure/security/benchmarks/security-benchmark-v2-identity-management)

- [Azure セキュリティ ベンチマーク - 特権アクセス](/azure/security/benchmarks/security-benchmark-v2-privileged-access)

- [Azure のセキュリティのベスト プラクティス 11 - アーキテクチャ。単一の統合セキュリティ戦略](/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Azure ID 管理のセキュリティの概要](/azure/security/fundamentals/identity-management-overview)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7: ログ記録と脅威対応戦略を定義する

**ガイダンス**:コンプライアンス要件を満たしながら脅威を迅速に検出して修復するための、ログ記録と脅威対応戦略を確立します。 アナリストが、統合や手動による手順ではなく、脅威の対応に集中できるように、質の高いアラートとシームレスなエクスペリエンスを提供することを優先してください。 

この戦略には、次の要素に関する文書化されたガイダンス、ポリシー、標準が含まれている必要があります。 

-   セキュリティ運用 (SecOps) 組織の役割と責任 

-   NIST または他の業界フレームワークと一致する、明確に定義されたインシデント対応プロセス 

-   脅威の検出、インシデント対応、コンプライアンスのニーズに対応するためのログのキャプチャと保持

-   SIEM、Azure のネイティブ機能、その他のソースを使用した、脅威に関する情報の一元的な可視化と関連付け 

-   顧客、サプライヤー、および関心を持つパブリック パーティに関するコミュニケーションと通知の計画

-   ログ記録と脅威の検出、フォレンジクス、攻撃の修復と根絶など、インシデント処理に対する Azure ネイティブおよびサードパーティのプラットフォームの使用

-   インシデントとインシデント発生後のアクティビティを処理するためのプロセス (教訓や証拠の保持など)

詳細については、次のリファレンスを参照してください。

- [Azure セキュリティ ベンチマーク - ログと脅威検出](/azure/security/benchmarks/security-benchmark-v2-logging-threat-detection)

- [Azure セキュリティ ベンチマーク - インシデント対応](/azure/security/benchmarks/security-benchmark-v2-incident-response)

- [Azure のセキュリティのベスト プラクティス 4 - プロセス: クラウドのインシデント対応プロセスを更新する](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Azure 導入フレームワーク、ログ、およびレポートの決定ガイド](/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Azure のエンタープライズ スケーリング、管理、監視](/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring)

**Azure Security Center の監視**: 適用なし

**責任**: Customer

## <a name="next-steps"></a>次のステップ

- 「[Azure セキュリティ ベンチマーク V2 の概要](/azure/security/benchmarks/overview)」を参照してください。
- [Azure セキュリティ ベースライン](/azure/security/benchmarks/security-baselines-overview)の詳細について学習する
