---
title: Cloud App Security は Dropbox 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して Dropbox アプリを Cloud App Security に接続することで、use.app-security を可視化して制御することの利点について説明します
ms.date: 12/04/2019
ms.topic: article
ms.openlocfilehash: 55d9b2f06a2915e6e5e1438b086e8c5201f0d49e
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96315278"
---
# <a name="how-cloud-app-security-helps-protect-your-dropbox-environment"></a>Cloud App Security は Dropbox 環境の保護にどのように役立つか

[!INCLUDE [Banner for top of topics](includes/banner.md)]

クラウド ファイル ストレージおよびコラボレーション ツールである Dropbox を使用すると、ユーザーは自分のドキュメントを組織全体でおよびパートナーとの間で合理的かつ効率的な方法で共有できます。 Dropbox を使用すると、内部だけでなく外部のコラボレーターにもご利用の機密データが公開されたり、さらに悪いことに、共有リンクを介してそれが公開されたりする可能性があります。 このようなインシデントは、悪意のあるアクターによって、または不注意な従業員によって引き起こされる可能性があります。

Dropbox を Cloud App Security に接続すると、ユーザーのアクティビティに関するより深い分析情報が得られ、機械学習ベースの異常検出を使用した脅威検出、情報保護検出 (外部情報共有の検出など)、修復制御の自動化を行えるようになります。

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- セキュリティ認識の不足
- マルウェア
- ランサムウェア
- アンマネージド Bring Your Own Device (BYOD)

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security は環境の保護にどのように役立つのか

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [クラウドに格納されている規制対象の機密データを検出、分類、ラベル付け、保護する](best-practices.md#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [クラウドに格納されているデータに DLP ポリシーとコンプライアンス ポリシーを適用する](best-practices.md#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [共有データの公開を制限し、コラボレーション ポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-dropbox-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して Dropbox を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[終了させられたユーザーによって実行されるアクティビティ (IdP として AAD が必要)](anomaly-detection-policy.md#activity-performed-by-terminated-user)<br />[マルウェアの検出](anomaly-detection-policy.md#malware-detection)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[ランサムウェアの検出](anomaly-detection-policy.md#ransomware-activity)<br />[異常なファイル削除アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[異常なファイル共有アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なる複数ファイルのダウンロード アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) |
| アクティビティ ポリシー テンプレート | 危険な IP アドレスからのログオン<br />単独のユーザーによる大量ダウンロード<br />ランサムウェアの可能性があるアクティビティ |
| ファイル ポリシー テンプレート | 承認されていないドメインで共有されたファイルの検出<br />個人用メール アドレスで共有されたファイルの検出<br />PII/PCI/PHI を使用したファイルを検出 |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

潜在的な脅威を監視することに加えて、次の Dropbox ガバナンス アクションを適用および自動化することにより、検出された脅威を修復することができます。

| Type | 操作 |
| ---- | ---- |
| データ ガバナンス | - 直接共有リンクを削除する<br />- DLP 違反ダイジェストをファイル所有者に送信する<br />- ファイルをごみ箱に入れる |
| ユーザー ガバナンス | - アラートをユーザーに通知する (Azure AD 経由)<br /> - ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br /> - ユーザーを停止する (Azure AD 経由) |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-dropbox-in-real-time"></a>Dropbox をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Dropbox を Microsoft Cloud App Security に接続する方法](connect-dropbox-to-microsoft-cloud-app-security.md)
