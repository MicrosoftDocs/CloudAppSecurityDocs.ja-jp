---
title: お使いの Google Workspace 環境の保護に Cloud App Security がどのように役立つか
description: この記事では、API コネクタを使用してお使いの Google Workspace アプリを Cloud App Security に接続し、使用状況を可視化して制御することの利点について説明します。
ms.date: 12/04/2019
ms.topic: article
ms.openlocfilehash: d8dbdb2ede59c75a8556b5ba1059bd3005c80481
ms.sourcegitcommit: 72ddcd0f9a83251d588009abf506676612c50267
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2020
ms.locfileid: "97370518"
---
# <a name="how-cloud-app-security-helps-protect-your-google-workspace-environment"></a>お使いの Google Workspace 環境の保護に Cloud App Security がどのように役立つか

[!INCLUDE [Banner for top of topics](includes/banner.md)]

クラウド ファイル ストレージおよびコラボレーション ツールである Google Workspace を使用すると、自分の組織全体およびパートナーと、自分のユーザーが合理的かつ効率的にドキュメントを共有できるようになります。 Google Workspace を使用すると、内部だけでなく外部のコラボレーターにもお使いの機密データが公開されたり、さらに悪いことには、共有リンクを介してそれが公開されたりする可能性があります。 このようなインシデントは、悪意のあるアクターによって、または不注意な従業員によって引き起こされる可能性があります。 また、Google Workspace には、生産性の向上に役立つサードパーティ製の大規模なアプリ エコシステムも用意されています。 これらのアプリを使用すると、悪意のあるアプリのリスクまたは過剰なアクセス許可を持つアプリを使用するリスクに組織がさらされる可能性があります。

Google Workspace を Cloud App Security に接続すると、自分のユーザーのアクティビティをより深く洞察できるようになり、機械学習ベースの異常検出を使用した脅威検出、情報保護検出 (外部との情報共有の検出など)、修復制御の自動化、自分の組織で有効になっているサードパーティ アプリからの脅威の検出を行えるようになります。

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- セキュリティ認識の不足
- 悪意のあるサードパーティ製アプリと Google アドオン
- マルウェア
- ランサムウェア
- アンマネージド Bring Your Own Device (BYOD)

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security は環境の保護にどのように役立つのか

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [クラウドに格納されている規制対象の機密データを検出、分類、ラベル付け、保護する](best-practices.md#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [環境にアクセスできる OAuth アプリを検出して管理する](manage-app-permissions.md)
- [クラウドに格納されているデータに DLP ポリシーとコンプライアンス ポリシーを適用する](best-practices.md#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [共有データの公開を制限し、コラボレーション ポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-google-workspace-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して Google Workspace を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[終了させられたユーザーによって実行されるアクティビティ (IdP として AAD が必要)](anomaly-detection-policy.md#activity-performed-by-terminated-user)<br />[マルウェアの検出](anomaly-detection-policy.md#malware-detection)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[ランサムウェアの検出](anomaly-detection-policy.md#ransomware-activity)<br />[通常とは異なる管理アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[異常なファイル削除アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[異常なファイル共有アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なる複数ファイルのダウンロード アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) |
| アクティビティ ポリシー テンプレート | 危険な IP アドレスからのログオン<br />単独のユーザーによる大量ダウンロード<br />ランサムウェアの可能性があるアクティビティ |
| ファイル ポリシー テンプレート | 承認されていないドメインで共有されたファイルの検出<br />個人用メール アドレスで共有されたファイルの検出<br />PII/PCI/PHI を使用したファイルを検出 |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

次の Google Workspace ガバナンス アクションを適用および自動化すると、潜在的な脅威の監視に加え、検出された脅威を修復できるようになります。

| Type | 操作 |
| ---- | ---- |
| データ ガバナンス | - Azure Information Protection 分類ラベルを適用する<br />- ドメインに読み取りアクセス許可を付与する<br />- Google ドライブ内のファイル、フォルダーを非公開にする<br />- ファイル、フォルダーへのパブリック アクセスを削減する<br />- コラボレーターをファイルから削除する<br />- Azure Information Protection 分類ラベルを削除する<br />- ファイル、フォルダー上の外部コラボレーターを削除する<br />- ファイル エディターの共有機能を削除する<br />- ファイル、フォルダーへのパブリック アクセスを削除する<br />- Google へのパスワードのリセットをユーザーに求める<br />- DLP 違反ダイジェストをファイル所有者に送信する<br />- 最後のファイル エディターに DLP 違反を送信する<br />- ファイル所有権を移転する<br />- ファイルをごみ箱に入れる |
| ユーザー ガバナンス | - ユーザーを停止する<br />- アラートをユーザーに通知する (Azure AD 経由)<br />- ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br />- ユーザーを停止する (Azure AD 経由) |
| OAuth アプリのガバナンス | - OAuth アプリのアクセス許可を取り消す |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-google-workspace-in-real-time"></a>Google Workspace をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Google Workspace を Microsoft Cloud App Security に接続する方法](connect-google-workspace-to-microsoft-cloud-app-security.md)
