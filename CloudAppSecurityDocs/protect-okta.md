---
title: Cloud App Security は Okta 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して Okta アプリを Cloud App Security に接続することで使用状況を可視化して制御することの利点について説明します。
ms.date: 12/04/2019
ms.topic: article
ms.openlocfilehash: aac67b4c39f95ffea36ac20a4cd0c10abb0054c3
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96315210"
---
# <a name="how-cloud-app-security-helps-protect-your-okta-environment"></a>Cloud App Security は Okta 環境の保護にどのように役立つか

[!INCLUDE [Banner for top of topics](includes/banner.md)]

ID およびアクセス管理ソリューションである Okta では組織の最上位のビジネス クリティカル サービスのキーが保持されます。 ユーザーと顧客の認証および承認のプロセスは、Okta によって管理されます。 悪意のあるアクターまたは人為的なミスによって Okta が悪用されると、最も重要な資産やサービスが潜在的な攻撃にさらされる可能性があります。

Okta を Cloud App Security に接続すると、Okta 管理アクティビティ、マネージド ユーザー、および顧客のサインインに関してより深い分析情報が得られ、異常な動作に関する脅威の検出を行うことができます。

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部関係者の脅威

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security は環境の保護にどのように役立つのか

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-okta-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して Okta を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[ランサムウェアの検出](anomaly-detection-policy.md#ransomware-activity)<br />[通常とは異なる管理アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) |
| アクティビティ ポリシー テンプレート | 危険な IP アドレスからのログオン |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

現在、Okta で利用できるガバナンス コントロールはありません。 このコネクタにガバナンス アクションが必要な場合は、[Cloud App Security チームにフィードバック](support-and-ts.md#feedback)を、必要なアクションの詳細と共に送信することができます。

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-okta-in-real-time"></a>Okta をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Okta を Microsoft Cloud App Security に接続する方法](connect-okta-to-microsoft-cloud-app-security.md)
