---
title: 組織で使用されるクラウド プラットフォームのセキュリティを管理する
description: このチュートリアルでは、Microsoft Cloud App Security を使用して、Azure、AWS、および GCP クラウド プラットフォームをセキュリティで保護する方法について説明します。
ms.date: 09/17/2020
ms.topic: tutorial
ms.openlocfilehash: 7711285b895d63e47e770a9079ef50bf8a091808
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96315873"
---
# <a name="tutorial-manage-cloud-platform-security"></a>チュートリアル:クラウド プラットフォームのセキュリティを管理する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

多くの場合、リモート作業では、一般的なビジネス タスクに対してクラウド アプリとクラウド プラットフォームが広く使用されており、クラウド環境をセキュリティで保護し、クラウド セキュリティ製品を導入することが必要となっています。 [共有責任モデル](/azure/security/fundamentals/shared-responsibility)によれば、組織はクラウド プラットフォームの管理とセキュリティ保護に責任を持ちます。これには、ID アクセス管理 (IAM)、仮想マシン (VM) とそのコンピューティング リソース、データとストレージ、ネットワーク リソースが含まれます。

![マルチクラウド環境のセキュリティ保護](media/tutorial-cloud-platform-security.png)

## <a name="how-does-security-posture-management-help"></a>セキュリティ体制管理がどのように役立つか

適切に保護されていない可能性のあるリソースを保護するために、適切なセキュリティ ツールを用意することが重要です。 組織は、クラウド リソースの体制を把握し、各プラットフォームの実際の使用状況を把握するための探索機能を備え、疑わしいアクティビティを監視して構成とコンプライアンス ステータスを評価および確認できるとともに、リアルタイムの保護メカニズムをデプロイできる必要があります。

また、クラウド セキュリティ体制の管理 (CSPM) は、SaaS 構成にも対応するために、IaaS と PaaS のセキュリティ体制を越えて拡張されています。 たとえば、パブリック アクセス レベルの GitHub リポジトリや、Office 365、G Suite、Sales Force などの SaaS アプリにアクセスできる OAuth アプリです。 SaaS CSPM は、Cloud App Security 製品のネイティブ拡張である CSPM の新しい拡張ドメインです。

## <a name="protecting-multiple-clouds-from-a-single-management-portal"></a>1 つの管理ポータルからの複数のクラウドの保護

近年、多くの組織では、さまざまな目的とさまざまなデプロイのスケールや状態に合わせて、複数のクラウド プラットフォームを使用しています。この複雑さにより、マルチクラウド環境を定期的に追跡する機能が必要となっています。  一部のサービスのデプロイ状態は時間の経過と共に変化することがありますが、セキュリティ チームの変更が完全に通知されるとは限りません。 これらの信号を 1 つのポータルで統合することで、管理作業が効率化され、監視を行っている人とクラウド リソースを使用している人の両方が、より効率的に時間とリソースを管理できるようになります。

組織のセキュリティ体制には、組織内のすべてのクラウド プラットフォームが含まれます。この新しい機能は、セキュリティ アーキテクト、中央セキュリティ管理者、またはコンプライアンス アナリストが使用できるように設計されています。 この機能を使用すると、管理者は非準拠リソースを含むサブスクリプションを確認し、リソース所有者による各サブスクリプションの修復を促進することができます。

このチュートリアルでは、Cloud App Security を使用して、Azure、AWS、および GCP クラウド プラットフォームをセキュリティで保護する手順について説明します。

> [!div class="checklist"]
>
> * マルチクラウド リソース、使用状況、およびシャドウ IT を検出する
> * アクティビティとアラートを監視して、ワークロード間の疑わしい動作を検出する
> * クラウド プラットフォームの構成ミスとコンプライアンス ステータスを評価および修復する
> * クラウド リソースの保護とポリシーの適用をリアルタイムで自動化する

## <a name="how-to-secure-your-multi-cloud-environment"></a>マルチクラウド環境をセキュリティで保護する方法

クラウド プラットフォームの重大な構成ミスを回避するには、組織にとって、クラウドの構成状態をマルチクラウドのテナントレベルで可視化し、セキュリティ ベンチマークとコンプライアンスの推奨事項に基づいてセキュリティ体制を強化することが重要です。 組織のマルチクラウド環境をセキュリティで保護するには、次のプロセスを使用します。

### <a name="phase-1-discover-multi-cloud-resources-usage-and-shadow-it"></a>フェーズ 1:マルチクラウド リソース、使用状況、およびシャドウ IT を検出する

**セキュリティ体制を特定する**:まず、Cloud Discovery を実行して組織のクラウド セキュリティ体制を特定し、ネットワークで何が起こっているかを確認して、クラウド プラットフォームでの実際のリソース使用状況を評価します。 これは、Cloud App Security でネットワーク トラフィックを監視および分析するように [Cloud Discovery を設定する](set-up-cloud-discovery.md)ことによって実現できます。 Cloud App Security のシャドウ IT 検出を使用した Web トラフィック ログの分析により、クラウド リソースのシャドウ IT 使用状況の可視性が向上し、Machine Learning 異常検出エンジンまたは定義したカスタム ポリシーを使用して異常なアクティビティが特定されます。

* **検出**:組織のリソース ホスティング クラウド プラットフォーム全体の使用状況を検出します。 たとえば、ストレージ リソースからダウンロードされた実際のデータ量を評価し、データ盗難の試行を示す可能性のある疑わしいリソースの使用を特定します。 同様に、悪意のあるコードをターゲットに挿入することによって環境を侵害しようとしていることを示す可能性のある、疑わしいアップロード アクティビティを特定します。
* **調査**: **[検出されたリソース]** ページを使用すると、Azure、AWS、GCP でホストされているストレージ アカウント、インフラストラクチャ、カスタム アプリなどのリソース間でのデータ アクセスを表示できます。 次のような質問を投げかけてみましょう。特定のリソースへのアクセス時に疑わしい数のトランザクションがありましたか?

    ![検出されたリソースを表示する](media/tutorial-cloud-platform-security-view-discovered-resources.png)

    さらに詳しく調査するには、各リソースにドリルダウンして、発生したトランザクションの種類、それにアクセスしたユーザーを確認し、そのユーザーについてさらに調査します。

    ![検出されたリソースを調査する](media/tutorial-cloud-platform-security-investigate-discovered-resources.png)

### <a name="phase-2-monitor-activities-and-alerts-to-detect-suspicious-behavior-across-workloads"></a>フェーズ 2:アクティビティとアラートを監視して、ワークロード間の疑わしい動作を検出する

IAM (ID およびアクセス管理) ロールの変更や CloudTrail 構成の変更など、侵害を示す可能性のある疑わしいアクティビティを追跡します。 たとえば、定義済みの **パブリックにアクセス可能な AWS S3 バケット** [ポリシー テンプレート](policy-template-reference.md)を使用して、S3 バケット構成の変更を追跡します。

異常検出ツールの適用は、疑わしい変更の監査ログを監視する場合に最適です。これにより、失敗した複数のログイン試行や、あり得ない移動シナリオと組み合わせた削除済みの複数の VM アクティビティを特定することで、考えられる侵害が通知されます。

![アラートを表示する](media/tutorial-cloud-platform-security-view-alerts.png)

真の侵害を特定し、大量の誤検知を処理することによるアラート疲れを減らすために、アラートからわかることを用いてユーザー アクティビティ検出を調整します。 次のポリシー パラメーターを調整することを検討してください。

* [IP アドレス範囲](tutorial-suspicious-activity.md#phase-1-configure-ip-address-ranges)を構成する
* 異常な管理アクティビティ、異常な複数ファイルのダウンロード アクティビティ、ランサムウェア アクティビティ、失敗したクラウド プラットフォームへのサインイン アクティビティなど、[異常検出ポリシー](tutorial-suspicious-activity.md#phase-2-tune-anomaly-detection-policies)を調整する
* 使用状況の監視とアラートの感度を調整することにより、[Cloud Discovery の異常検出ポリシー](tutorial-suspicious-activity.md#phase-3-tune-cloud-discovery-anomaly-detection-policies)を調整する
* パブリックにアクセス可能な AWS S3 バケットを含む、[ルールベースの検出ポリシーとアクティビティ ポリシー](tutorial-suspicious-activity.md#phase-4-tune-rule-based-detection-activity-policies)を調整する
* [アラート](tutorial-suspicious-activity.md#phase-5-configure-alerts)を構成する
* [調査と修復](tutorial-suspicious-activity.md#phase-6-investigate-and-remediate)

### <a name="phase-3-assess-and-remediate-cloud-platform-misconfigurations-and-compliance-status"></a>フェーズ 3:クラウド プラットフォームの構成ミスとコンプライアンス ステータスを評価および修復する

Azure サブスクリプション、AWS アカウント、GCP プロジェクトなどのすべてのパブリック クラウド プラットフォームで、テナントごとのセキュリティ コンプライアンス ステータスを評価します。 評価により、構成のギャップと推奨事項の詳細をリソース所有者に伝え、修復を促進することができます。

各クラウド プラットフォームでは、規制コンプライアンスのベスト プラクティスに基づいて、正しく構成されていないリソースの一覧が示されます。

クラウド アーキテクトまたはコンプライアンス アナリストは、クラウド環境ごとに構成のギャップを評価し、リソース所有者による修復を促進することができます。 たとえば、推奨事項は次の手段によって評価できます。

* サブスクリプション: 運用以外の環境から運用環境を区別する
* 重要度: 重要度の低い推奨事項とは異なる SLA およびプロセスを持つことが多い、重要度の高い推奨事項を識別する

Azure のセキュリティ構成に関する推奨事項については、Azure Security Center のベスト プラクティスに基づいて、Azure テナント全体とそのすべてのサブスクリプションの推奨事項を紹介します。 推奨事項を選択すると、Azure Security Center の推奨事項ページにリダイレクトされます。ここでは、推奨事項に関するさらなる詳細を確認し、これを使用してサブスクリプションの所有者による修復を促進することができます。 いくつかの推奨事項では、問題を修復するための **クイック修正** オプションが用意されています。 Azure のセキュリティに関する推奨事項の詳細については、「[Azure のセキュリティ構成](security-config-azure.md)」を参照してください。

![Azure の推奨事項を表示する](media/tutorial-cloud-platform-security-view-azure-recommendations.png)

AWS のセキュリティ構成に関する推奨事項については、推奨事項を選択して、影響を受けるリソースの詳細にドリルダウンすることができます。 たとえば、AWS CIS 勧告 2.9 'Ensure VPC flow logging in enabled in all VPC' (すべての VPC で VPC フロー ログ記録が有効になっていることを確認します) では、VPC のログが有効になっていないリソースを確認できます。 詳細情報には、VPC 名、リソースがホストされているアカウント、およびリージョンが含まれます。 AWS リンクを選択して関連する検索を表示し、推奨事項に準拠するように AWS の関連する設定を変更することができます。 AWS のセキュリティ構成の詳細については、「[AWS のセキュリティ構成](security-config-aws.md)」を参照してください。

![AWS 推奨事項を表示する](media/tutorial-cloud-platform-security-view-aws-recommendations.png)

GCP のセキュリティ構成に関する推奨事項については、推奨事項を選択すると、問題の修復の影響と取り組みをより深く理解し、評価するのに役立つ詳細な推奨情報および修復手順が表示されます。 その後、[GCP Security Command Center] リンクを選択すると、プラットフォームでの検索を修復できます。 GCP の推奨事項の詳細については、[GCP のセキュリティ構成](security-config-gcp.md)に関するページを参照してください。

![GCP の推奨事項を表示する](media/tutorial-cloud-platform-security-view-gcp-recommendations.png)

### <a name="phase-4-automate-protection-and-policy-enforcement-for-cloud-resources-in-real-time"></a>フェーズ 4:クラウド リソースの保護とポリシーの適用をリアルタイムで自動化する

アクセスとセッション制御のポリシーを適用することで、組織のリソースをデータの漏洩や盗難からリアルタイムで保護します。 詳細については、[リアルタイムでのアプリの保護](tutorial-proxy.md)に関するページを参照してください。

* 管理されていないデバイスまたは危険なデバイスへの[ダウンロードをブロックする](session-policy-aad.md#block-download)ことでデータ盗難を防止し、危険なセッションでのダウンロードから保護します。
* クラウド プラットフォームへの[悪意のあるファイル](session-policy-aad.md#block-malware-on-upload)のアップロードを防止し、さまざまなリスク要因に基づいて特定のユーザーのアクセスをブロックします。

![ポリシー修復アクションを指定する](media/tutorial-cloud-platform-security-remediation.png)

## <a name="see-also"></a>参照

> [!div class="nextstepaction"]
> [Azure 環境を保護する](protect-azure.md)

> [!div class="nextstepaction"]
> [AWS 環境を保護する](protect-aws.md)

> [!div class="nextstepaction"]
> [GCP 環境を保護する](protect-gcp.md)

[!INCLUDE [Open support ticket](includes/support.md)]
