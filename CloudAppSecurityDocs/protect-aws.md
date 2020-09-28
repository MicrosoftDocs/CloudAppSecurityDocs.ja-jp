---
title: Cloud App Security でアマゾン ウェブ サービス環境を保護する利点
description: この記事では、API コネクタを使用して AWS アプリを Cloud App Security に接続することで使用状況を可視化して制御することの利点について説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: article
ms.date: 09/15/2020
ms.collection: M365-security-compliance
ms.openlocfilehash: 24f4598958361d2ea705f08bc0fb3d5fa8a19324
ms.sourcegitcommit: 7d05b81a839286d2afae4cdad2c2d59e7becc1f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90524142"
---
# <a name="how-cloud-app-security-helps-protect-your-amazon-web-services-aws-environment"></a>Cloud App Security でアマゾン ウェブ サービス (AWS) 環境を保護する利点

*適用対象:Microsoft Cloud App Security*

アマゾン ウェブ サービスは、組織がそのワークロード全体をクラウド内でホストして管理することを可能にする IaaS プロバイダーです。 クラウド内のインフラストラクチャを活用できる利点があると同時に、組織の最も重要な資産が脅威にさらされる可能性があります。 さらされる資産には、機密性が高い情報を含む可能性があるストレージ インスタンス、ご利用の最も重要なアプリケーションの一部を操作するコンピューティング リソース、ポート、および組織へのアクセスを可能にする仮想プライベート ネットワークなどがあります。

AWS を Cloud App Security に接続すると、管理およびサインインのアクティビティを監視して、ブルート フォース攻撃の可能性、特権ユーザーのアカウントの不正使用、VM の異常な削除、公開されたストレージ バケットについて通知することで、ご利用の資産をセキュリティで保護し、潜在的な脅威を検出することができます。

## <a name="main-threats"></a>主な脅威

- クラウド リソースの不正使用
- 侵害されたアカウントと内部関係者の脅威
- データ漏えい
- リソースの構成に誤りがあり、アクセス制御が不十分である

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security で環境を保護する利点

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者を検出する](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [共有データの公開を制限し、コラボレーション ポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [セキュリティの構成に関する最新の推奨事項を常に把握する](security-config-aws.md)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)
- [セキュリティ構成に関する推奨事項を確認する](security-config-aws.md)

## <a name="control-aws-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーおよびポリシー テンプレートを使用して AWS を制御する

次に示す組み込みポリシー テンプレートを使用すれば、潜在的な脅威を検出して、それに関する通知を受け取ることができます。

| Type | 名前 |
| ---- | ---- |
| アクティビティ ポリシー テンプレート | 管理コンソールへのサインインの失敗<br />CloudTrail 構成の変更<br />EC2 インスタンス構成の変更<br />IAM ポリシーの変更<br />危険な IP アドレスからのログオン<br />ネットワーク アクセス制御リスト (ACL) の変更<br />ネットワーク ゲートウェイの変更<br />S3 構成の変更<br />セキュリティ グループ構成の変更<br />仮想プライベート ネットワークの変更 |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[終了させられたユーザーによって実行されるアクティビティ (IdP として AAD が必要)](anomaly-detection-policy.md#activity-performed-by-terminated-user)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[通常とは異なる管理アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なる複数のストレージ削除アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) (プレビュー)<br />[複数の VM 削除アクティビティ](anomaly-detection-policy.md#multiple-delete-vm-activities)<br />[通常とは異なる複数の VM 作成アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) (プレビュー)<br />[クラウド リソースの通常とは異なるリージョン](anomaly-detection-policy.md#unusual-activities-by-user) (プレビュー) |
| ファイル ポリシー テンプレート | S3 バケットがパブリックにアクセス可能 |

ポリシーの作成の詳細については、「[ポリシーの作成](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンス コントロールを自動化する

潜在的な脅威を監視することに加えて、次の AWS ガバナンス アクションを適用および自動化することにより、検出された脅威を修復することができます。

| Type | 操作 |
| ---- | ---- |
| ユーザー ガバナンス | - アラートをユーザーに通知する (Azure AD 経由)<br />- ユーザーにもう一度サインインするよう要求する (Azure AD 経由)<br />- ユーザーを停止する (Azure AD 経由) |
| データ ガバナンス | - S3 バケットをプライベートにする<br />- S3 バケットのコラボレーターを削除する |

アプリからの脅威の修復の詳細については、「[接続されているアプリを管理する](governance-actions.md)」を参照してください。

## <a name="security-recommendations"></a>セキュリティに関する推奨事項

Cloud App Security では、AWS 用の Center for Internet Security (CIS) ベンチマークに基づいて、すべての AWS アカウントの AWS プラットフォーム構成コンプライアンスの概要が示されます。

プラットフォームのセキュリティ体制の現状を査定および評価し、構成の重要な差異を特定するために、セキュリティに関する推奨事項を継続的に確認する必要があります。 次に、AWS プラットフォームの問題を軽減する計画を作成する必要があります。

詳細については、[AWS のセキュリティに関する推奨事項](security-config-aws.md)を参照してください。

## <a name="protect-aws-in-real-time"></a>AWS をリアルタイムで保護する

[アンマネージド デバイスまたは危険なデバイスへの機密データのダウンロードをブロックして保護する](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)ためのベスト プラクティスを確認してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [AWS を Microsoft Cloud App Security に接続する方法](connect-aws-to-microsoft-cloud-app-security.md)
