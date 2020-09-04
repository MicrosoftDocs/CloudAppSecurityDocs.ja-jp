---
title: Cloud App Security は Microsoft 365 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して Microsoft 365 アプリを Cloud App Security に接続し、使用状況を可視化して制御することの利点について説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: article
ms.date: 12/04/2019
ms.collection: M365-security-compliance
ms.openlocfilehash: b892d96b2cf7329613b21b6134e33ae6fd62ea29
ms.sourcegitcommit: c174a7ada5c6a14f0fea9870672898c54e5e3b52
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2020
ms.locfileid: "89150062"
---
# <a name="how-cloud-app-security-helps-protect-your-microsoft-365-environment"></a>Cloud App Security は Microsoft 365 環境の保護にどのように役立つか

*適用対象:Microsoft Cloud App Security*

クラウド ファイル ストレージ、コラボレーション、BI、CRM ツールを提供する主要な生産性スイートである Microsoft 365 を使用すると、ユーザーは自分のドキュメントを組織全体でおよびパートナーとの間で合理的かつ効率的な方法で共有できます。 Microsoft 365 を使用すると、内部だけでなく外部のコラボレーターにもご利用の機密データが公開されたり、さらに悪いことに、共有リンクを介してそれが公開されたりする可能性があります。 このようなインシデントは、悪意のあるアクターまたは不注意な従業員によって引き起こされる可能性があります。 また、Microsoft 365 には、生産性の向上に役立つサードパーティ製の大規模なアプリ エコシステムも用意されています。 これらのアプリを使用すると、悪意のあるアプリのリスクまたは過剰なアクセス許可を持つアプリを使用するリスクに組織がさらされる可能性があります。

Microsoft 365 を Cloud App Security に接続すると、ユーザーのアクティビティに関するより深い分析情報が得られ、機械学習ベースの異常検出を使用した脅威検出、情報保護検出 (外部情報共有の検出など)、修復制御の自動化、組織内で有効にされたサードパーティ アプリからの脅威の検出を行えるようになります。

Microsoft 365 コネクタを使用すると、次の製品に対する保護が提供されます。

- Dynamics 365 CRM
- Exchange
- Microsoft 365
- OneDrive
- Power Automate
- Power BI
- SharePoint
- Skype for Business
- Teams
- Yammer

> [!NOTE]
> Cloud App Security は [Microsoft 365 の監査ログ](/microsoft-365/compliance/detailed-properties-in-the-office-365-audit-log?view=o365-worldwide)と直接統合されて、PowerApps、Forms、Sway、Stream など、**サポートされているすべてのサービス**からすべての監査イベントを受信します。

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- セキュリティに対する認識不足
- 悪意のあるサード パーティ製アプリ
- マルウェア
- フィッシング
- ランサムウェア
- アンマネージド Bring Your Own Device (BYOD)

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security で環境を保護する利点

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [クラウドに格納されている規制対象の機密データの検出、分類、ラベル付け、保護を行う](best-practices.md#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [環境にアクセスできる OAuth アプリを検出して管理する](manage-app-permissions.md)
- [クラウドに格納されているデータに DLP ポリシーとコンプライアンス ポリシーを適用する](best-practices.md#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [共有データの公開を制限し、コラボレーション ポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-microsoft-365-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して Microsoft 365 を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それに関する通知を受け取ることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[解雇されたユーザーによって実行されたアクティビティ](anomaly-detection-policy.md#activity-performed-by-terminated-user) (IdP として Azure AD が必要)<br />[マルウェアの検出](anomaly-detection-policy.md#malware-detection)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[ランサムウェアの検出](anomaly-detection-policy.md#ransomware-activity)<br />[疑わしいメール削除アクティビティ (プレビュー)](anomaly-detection-policy.md#suspicious-email-deletion-activity-preview)<br />[受信トレイからの疑わしい転送](anomaly-detection-policy.md#suspicious-inbox-forwarding)[異常なファイル削除アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[異常なファイル共有アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なる複数ファイルのダウンロード アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) |
| アクティビティ ポリシー テンプレート | 危険な IP アドレスからのログオン<br />単独のユーザーによる大量ダウンロード<br />ランサムウェアの可能性があるアクティビティ<br />アクセス レベルの変更 (Teams)<br />追加された外部ユーザー (Teams)<br />大量の削除 (Teams) |
| ファイル ポリシー テンプレート | 承認されていないドメインで共有されたファイルの検出<br />個人用メール アドレスで共有されたファイルの検出<br />PII/PCI/PHI を使用したファイルの検出 |
| OAuth アプリ異常検出ポリシー | [まぎらわしい OAuth アプリ名](app-permission-policy.md#oauth-app-anomaly-detection-policies)<br />[OAuth アプリのまぎらわしい発行元名](app-permission-policy.md#oauth-app-anomaly-detection-policies)<br />[悪意のある OAuth アプリの同意](app-permission-policy.md#oauth-app-anomaly-detection-policies) |

ポリシーの作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

潜在的な脅威を監視することに加えて、次の Microsoft 365 ガバナンス アクションを適用および自動化することにより、検出された脅威を修復することができます。

| Type | 操作 |
| ---- | ---- |
| データ ガバナンス | **OneDrive:**<br /> - 親のフォルダー アクセス許可を継承する<br /> - ファイル/フォルダーをプライベートにする<br /> - ファイル/フォルダーを管理者検疫に配置する<br /> - ファイル/フォルダーをユーザー検疫に配置する<br /> - ファイル/フォルダーをごみ箱に入れる<br /> - 特定のコラボレーターを削除する<br /> - ファイル、フォルダー上の外部コラボレーターを削除する<br /> - Azure Information Protection 分類ラベルを適用する<br /> - Azure Information Protection 分類ラベルを削除する<br /> **SharePoint:**<br /> - 親のフォルダー アクセス許可を継承する<br /> - ファイル/フォルダーをプライベートにする<br /> - ファイル/フォルダーを管理者検疫に配置する<br /> - ファイル/フォルダーをユーザー検疫に配置する<br /> - ファイル/フォルダーをユーザー検疫に配置し、所有者アクセス許可を追加する<br /> - ファイル/フォルダーをごみ箱に入れる<br /> - ファイル、フォルダー上の外部コラボレーターを削除する<br /> - 特定のコラボレーターを削除する<br /> - Azure Information Protection 分類ラベルを適用する<br /> - Azure Information Protection 分類ラベルを削除する |
| ユーザー ガバナンス | - アラートをユーザーに通知する (Azure AD 経由)<br /> - ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br /> - ユーザーを停止する (Azure AD 経由) |
| OAuth アプリのガバナンス | - OAuth アプリのアクセス許可を取り消す |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-microsoft-365-in-real-time"></a>リアルタイムで Microsoft 365 を保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Microsoft 365 を Microsoft Cloud App Security に接続する方法](connect-office-365-to-microsoft-cloud-app-security.md)