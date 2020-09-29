---
title: Cloud App Security は Cisco Webex 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して Cisco Webex アプリを Cloud App Security に接続することで使用状況を可視化して制御することの利点について説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: article
ms.date: 12/04/2019
ms.collection: M365-security-compliance
ms.openlocfilehash: 1c813d804b2f9ef4df1ede9ea85542fdd22f38d9
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880416"
---
# <a name="how-cloud-app-security-helps-protect-your-cisco-webex-environment"></a>Cloud App Security は Cisco Webex 環境の保護にどのように役立つか

[!INCLUDE [Banner for top of topics](includes/banner.md)]

コミュニケーションおよびコラボレーションのプラットフォームである Cisco Webex では、組織全体の円滑なコミュニケーションとコラボレーションを実現することができます。 データと資産のやりとりに Cisco Webex を使用すると、たとえば、外部ユーザーが従業員との会話にも参加している可能性があるチャット ルームなどで、組織の機密情報が外部ユーザーに公開される可能性がありま。

Cisco Webex を Cloud App Security に接続すると、ユーザーのアクティビティに関するより深い分析情報が得られ、情報保護検やガバナンス コントロールの自動化を行えるようになります。

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- セキュリティ認識の不足
- ランサムウェア
- アンマネージド Bring Your Own Device (BYOD)

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security は環境の保護にどのように役立つのか

- [クラウドに格納されているデータに DLP ポリシーとコンプライアンス ポリシーを適用する](best-practices.md#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [共有データの公開を制限し、コラボレーション ポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-cisco-webex-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して Cisco Webex を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [終了させられたユーザーによって実行されるアクティビティ (IdP として AAD が必要)](anomaly-detection-policy.md#activity-performed-by-terminated-user)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[ランサムウェアの検出](anomaly-detection-policy.md#ransomware-activity)<br />[異常なファイル削除アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[異常なファイル共有アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なる複数ファイルのダウンロード アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) |
| ファイル ポリシー テンプレート | 承認されていないドメインで共有されたファイルの検出<br />個人用メール アドレスで共有されたファイルの検出<br />PII/PCI/PHI を使用したファイルを検出 |
| アクティビティ ポリシー テンプレート | 単独のユーザーによる大量ダウンロード<br />ランサムウェアの可能性があるアクティビティ |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

潜在的な脅威を監視することに加えて、次の Cisco Webex ガバナンス アクションを適用および自動化することにより、検出された脅威を修復することができます。

| Type | 操作 |
| ---- | ---- |
| ユーザー ガバナンス | - アラートをユーザーに通知する (Azure AD 経由)<br />- ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br />- ユーザーを停止する (Azure AD 経由) |
| データ ガバナンス | - ファイルをごみ箱に入れる |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-cisco-webex-in-real-time"></a>Cisco Webex をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cisco Webex を Microsoft Cloud App Security に接続する方法](connect-webex-to-microsoft-cloud-app-security.md)
