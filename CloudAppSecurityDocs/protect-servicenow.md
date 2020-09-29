---
title: Cloud App Security は ServiceNow 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して ServiceNow アプリを Cloud App Security に接続することで使用状況を可視化して制御することの利点について説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: article
ms.date: 12/04/2019
ms.collection: M365-security-compliance
ms.openlocfilehash: 7a8838ed08b6ffdc3949234204a957f2a28a0eeb
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880426"
---
# <a name="how-cloud-app-security-helps-protect-your-servicenow-environment"></a>Cloud App Security は ServiceNow 環境の保護にどのように役立つか

[!INCLUDE [Banner for top of topics](includes/banner.md)]

主要な CRM クラウド プロバイダーである ServiceNow では、顧客、内部プロセス、インシデント、および組織内のレポートに関する大量の機密情報が組み込まれます。 ビジネスに不可欠なアプリである ServiceNow は、組織内のユーザーのほか、組織外のユーザー (パートナーや請負業者など) によっても、さまざまな目的でアクセスされ使用されます。 多くの場合、ServiceNow にアクセスするユーザーの大部分はセキュリティに対する意識が低く、機密情報を誤って共有することによってそれを危険にさらしてしまう可能性があります。 他の例では、悪意のあるアクターが最も機密性の高い顧客関連資産にアクセスできる可能性があります。

ServiceNow を Cloud App Security に接続すると、ユーザーのアクティビティに関するより深い分析情報が得られ、機械学習ベースの異常検出を使用した脅威検出、機密の顧客情報が ServiceNow クラウドにアップロードされたタイミングの特定などの情報保護検出を行えるようになります。

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- セキュリティ認識の不足
- ランサムウェア
- アンマネージド Bring Your Own Device (BYOD)

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security で環境を保護する利点

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [クラウドに格納されている規制対象の機密データを検出、分類、ラベル付け、保護する](best-practices.md#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [クラウドに格納されているデータに DLP ポリシーとコンプライアンス ポリシーを適用する](best-practices.md#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [共有データの公開を制限し、コラボレーション ポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-servicenow-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して ServiceNow を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[終了させられたユーザーによって実行されるアクティビティ (IdP として AAD が必要)](anomaly-detection-policy.md#activity-performed-by-terminated-user)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[ランサムウェアの検出](anomaly-detection-policy.md#ransomware-activity)<br />[通常とは異なる複数ファイルのダウンロード アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) |
| アクティビティ ポリシー テンプレート | 危険な IP アドレスからのログオン<br />単独のユーザーによる大量ダウンロード<br />ランサムウェアの可能性があるアクティビティ |
| ファイル ポリシー テンプレート | 承認されていないドメインで共有されたファイルの検出<br />個人用メール アドレスで共有されたファイルの検出<br />PII/PCI/PHI を使用したファイルを検出 |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

潜在的な脅威を監視することに加えて、次の ServiceNow ガバナンス アクションを適用および自動化することにより、検出された脅威を修復することができます。

| Type | 操作 |
| ---- | ---- |
| ユーザー ガバナンス | - アラートをユーザーに通知する (Azure AD 経由)<br />- ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br />- ユーザーを停止する (Azure AD 経由) |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-servicenow-in-real-time"></a>ServiceNow をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ServiceNow を Microsoft Cloud App Security に接続する方法](connect-servicenow-to-microsoft-cloud-app-security.md)
