---
title: Cloud App Security は Google Cloud Platform 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して Google Cloud Platform アプリを Cloud App Security に接続することで使用状況を可視化して制御することの利点について説明します。
ms.date: 09/15/2020
ms.topic: article
ms.openlocfilehash: 461d6c0c883c84892a049de7193dd5f28e1a0a99
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96315261"
---
# <a name="how-cloud-app-security-helps-protect-your-google-cloud-platform-gcp-environment"></a>Cloud App Security は Google Cloud Platform (GCP) 環境の保護にどのように役立つか

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Google Cloud Platform は、組織がそのワークロード全体をクラウド内でホストして管理することを可能にする IaaS プロバイダーです。 クラウド内のインフラストラクチャを活用できる利点があると同時に、組織の最も重要な資産が脅威にさらされる可能性があります。 さらされる資産には、機密性が高い情報を含む可能性があるストレージ インスタンス、最も重要なアプリケーションの一部を操作するコンピューティング リソース、ポート、および組織へのアクセスを可能にする仮想プライベート ネットワークなどがあります。

GCP を Cloud App Security に接続すると、管理およびサインインのアクティビティを監視して、ブルート フォース攻撃の可能性、特権ユーザーのアカウントの不正使用、VM の異常な削除について通知することで、ご利用の資産をセキュリティで保護し、潜在的な脅威を検出することができます。

## <a name="main-threats"></a>主な脅威

- クラウド リソースの不正使用
- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- リソースの構成に誤りがあり、アクセス制御が不十分である

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security は環境の保護にどのように役立つのか

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)
- [セキュリティ構成に関する推奨事項を確認する](security-config-gcp.md)

## <a name="control-gcp-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して GCP を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[終了させられたユーザーによって実行されるアクティビティ (IdP として AAD が必要)](anomaly-detection-policy.md#activity-performed-by-terminated-user)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[通常とは異なる管理アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[複数の VM 削除アクティビティ](anomaly-detection-policy.md#multiple-delete-vm-activities)<br />[通常とは異なる複数の VM 作成アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) (プレビュー) |
| アクティビティ ポリシー テンプレート | コンピューティング エンジン リソースに対する変更<br />StackDriver の構成に対する変更<br />ストレージ リソースに対する変更<br />仮想プライベート ネットワークに対する変更<br />危険な IP アドレスからのログオン |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

潜在的な脅威を監視することに加えて、次の GCP ガバナンス アクションを適用および自動化することにより、検出された脅威を修復することができます。

| Type | 操作 |
| ---- | ---- |
| ユーザー ガバナンス | - Google へのパスワードのリセットをユーザーに求める (リンク先 G Suite インスタンスの接続が必要)<br />- ユーザーを停止する (リンク先 G Suite インスタンスの接続が必要)<br />- アラートをユーザーに通知する (Azure AD 経由)<br />- ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br />- ユーザーを停止する (Azure AD 経由) |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="security-recommendations"></a>セキュリティに関する推奨事項

Cloud App Security では、GCP 用の Center for Internet Security (CIS) ベンチマークに基づいて、すべての GCP プロジェクトの GCP プラットフォーム構成コンプライアンスの概要が示されます。

プラットフォームのセキュリティ体制の現状を査定および評価し、構成の重要な差異を特定するために、セキュリティに関する推奨事項を継続的に確認する必要があります。 次に、GCP プラットフォームの問題を軽減する計画を作成する必要があります。

詳細については、[GCP のセキュリティに関する推奨事項](security-config-gcp.md)を参照してください。

## <a name="protect-gcp-in-real-time"></a>GCP をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [GCP を Microsoft Cloud App Security に接続する方法](connect-google-gcp-to-microsoft-cloud-app-security.md)
