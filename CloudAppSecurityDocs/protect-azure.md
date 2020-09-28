---
title: Cloud App Security は Azure 環境の保護にどのように役立つか
description: この記事では、API コネクタを使用して Azure アプリを Cloud App Security に接続することで使用状況を可視化して制御することの利点について説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: article
ms.date: 09/15/2020
ms.collection: M365-security-compliance
ms.openlocfilehash: 3fde8f4de6eaed15191f773562342195bbe41471
ms.sourcegitcommit: 7d05b81a839286d2afae4cdad2c2d59e7becc1f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90524159"
---
# <a name="how-cloud-app-security-helps-protect-your-azure-environment"></a>Cloud App Security は Azure 環境の保護にどのように役立つか

*適用対象:Microsoft Cloud App Security*

Azure は、組織がそのワークロード全体をクラウド内でホストして管理することを可能にする IaaS プロバイダーです。 クラウド内のインフラストラクチャを活用できる利点があると同時に、組織の最も重要な資産が脅威にさらされる可能性があります。 さらされる資産には、機密性が高い情報を含む可能性があるストレージ インスタンス、最も重要なアプリケーションの一部を操作するコンピューティング リソース、ポート、および組織へのアクセスを可能にする仮想プライベート ネットワークなどがあります。

Azure を Cloud App Security に接続すると、管理およびサインインのアクティビティを監視して、ブルート フォース攻撃の可能性、特権ユーザーのアカウントの不正使用、VM の異常な削除について通知することで、ご利用の資産をセキュリティで保護し、潜在的な脅威を検出することができます。

## <a name="main-threats"></a>主な脅威

- クラウド リソースの不正使用
- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- リソースの構成に誤りがあり、アクセス制御が不十分である

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security は環境の保護にどのように役立つのか

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [共有データの公開を制限し、コラボレーション ポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)
- [セキュリティ構成に関する推奨事項を確認する](security-config-azure.md)

## <a name="control-azure-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して Azure を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それについての通知が届くようにすることができます。

| Type | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[終了させられたユーザーによって実行されるアクティビティ (IdP として AAD が必要)](anomaly-detection-policy.md#activity-performed-by-terminated-user)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[通常とは異なる管理アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なる複数のストレージ削除アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) (プレビュー)<br />[複数の VM 削除アクティビティ](anomaly-detection-policy.md#multiple-delete-vm-activities)<br />[通常とは異なる複数の VM 作成アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) (プレビュー) |

ポリシー作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="security-recommendations"></a>セキュリティに関する推奨事項

Cloud App Security では、Azure プラットフォームのテナントレベルのビューが提供され、テナント内のすべての Azure サブスクリプションのセキュリティに関する推奨事項が一覧表示されます。 [Azure のセキュリティ ベンチマーク](/azure/security/benchmarks/introduction)に照らし、100 以上の Azure リソースに対して Azure のセキュリティに関する既定の推奨事項を使用したり、[カスタムの推奨事項](/azure/security-center/custom-security-policies)を使用したりできます。 既定の推奨事項には、仮想マシン、ID とアクセス、データとストレージ、コンピューティングとアプリ、ネットワーク、コンテナー、アプリ サービスなどの種類のリソースが含まれます。

プラットフォームのセキュリティ体制の現状を査定および評価し、構成の重要な差異を特定するために、セキュリティに関する推奨事項を継続的に確認する必要があります。 次に、Azure プラットフォームの問題を軽減する計画を作成する必要があります。

詳細については、[Azure の推奨事項のガイド](/azure/security-center/recommendations-reference)と [Azure のセキュリティに関する推奨事項](security-config-azure.md)を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

潜在的な脅威を監視することに加えて、次の Azure ガバナンス アクションを適用および自動化することにより、検出された脅威を修復することができます。

| Type | 操作 |
| ---- | ---- |
| ユーザー ガバナンス | - アラートをユーザーに通知する (Azure AD 経由)<br />- ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br />- ユーザーを停止する (Azure AD 経由) |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="protect-azure-in-real-time"></a>Azure をリアルタイムで保護する

[外部ユーザーをセキュリティで保護して共同作業を行う](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)ためのベスト プラクティス、および[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Azure を Microsoft Cloud App Security に接続する方法](connect-azure-to-microsoft-cloud-app-security.md)
