---
title: Cloud App Security は Workday 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して Workday アプリを Cloud App Security に接続することで使用状況を可視化して制御することの利点について説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: article
ms.date: 12/04/2019
ms.collection: M365-security-compliance
ms.openlocfilehash: 2ff5f5ffb2dfe58833f556a6aebe1d4b99b8c061
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880367"
---
# <a name="how-cloud-app-security-helps-protect-your-workday-environment"></a>Cloud App Security は Workday 環境の保護にどのように役立つか

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Workday は主要な HCM ソリューションの 1 つであり、従業員の個人データ、契約、ベンダーの詳細など、組織内の最も機密性の高い情報の一部が保持されます。 このデータの漏えいを防ぐには、悪意のある当事者やセキュリティ認識の低い内部関係者が機密情報を持ち出すことがないように、継続的な監視を行う必要があります。

Workday を Cloud App Security に接続すると、ユーザーのアクティビティに関してより深い分析情報が得られ、異常な動作に関する脅威の検出を行うことができます。

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- セキュリティ認識の不足
- アンマネージド Bring Your Own Device (BYOD)

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security で環境を保護する利点

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-workday-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して Workday を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel) |
| アクティビティ ポリシー テンプレート | 危険な IP アドレスからのログオン |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

現在、Workday で利用できるガバナンス コントロールはありません。 このコネクタにガバナンス アクションが必要な場合は、[Cloud App Security チームにフィードバック](support-and-ts.md#feedback)を、必要なアクションの詳細と共に送信することができます。

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-workday-in-real-time"></a>Workday をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Workday を Microsoft Cloud App Security に接続する方法](connect-workday-to-microsoft-cloud-app-security.md)
