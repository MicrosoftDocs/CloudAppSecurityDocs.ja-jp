---
title: 脅威保護シナリオの概要
description: このトピックでは、クラウド環境内の脅威から組織を保護するシナリオについて説明します。
ms.date: 12/14/2018
ms.topic: conceptual
ms.openlocfilehash: 86fe03e26d60107d0c8b825fca566f73afe62d56
ms.sourcegitcommit: 72ddcd0f9a83251d588009abf506676612c50267
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2020
ms.locfileid: "97370111"
---
# <a name="protecting-your-organization-from-ransomware"></a>ランサムウェアから組織を保護する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

最近の大規模なランサムウェア攻撃 WannaCry では、150 か国にわたり推定 20 万台のコンピューターが感染し、コンピューターの世界が激しく攻撃されました。 ランサムウェア攻撃はこの数年間で増加しており、2015 年には月平均 25,000 回、2016 年には 56,000 回の攻撃がありました。そのため、ネットワークとクラウドが危険にさらされていないことを積極的に確認することがサイバーセキュリティに必要になってきています。 この記事では、Cloud App Security を使用してクラウドを監視し、脅威を検出して緩和し、ランサムウェアから環境を保護するためのベスト プラクティスを適用する方法について説明します。

## <a name="what-is-ransomware"></a>ランサムウェアとは

ランサムウェアは、攻撃者が、ユーザーに自分のコンピューターにアクセスしたり、自分のファイルを暗号化したりできないようにするファイルを送り付けるサイバー攻撃です。 これらのファイルを人質にして身代金を要求されることがあり、攻撃者にお金を支払うまで、コンピューター、ファイル、または重要な LOB アプリへのアクセスを復元するための暗号化が解除されません。 ランサムウェア攻撃は、すべてのコンピューター、自宅、オフィス、ネットワーク、またはサーバーに影響を与える可能性があります。 実際、大規模な組織には、ネットワーク全体にランサムウェアを解き放つファイルを誤って開いてしまう可能性がある多くのユーザーがいるため、組織は、ランサムウェアを停止してコンピューターまたはファイルへのアクセスを復元するためには、攻撃者にお金を支払わざるを得ないというさらに大きなリスクにさらされています。

>[!NOTE]
> このユース ケースは、Office 365、Google Workspace、Box、Dropbox に該当します。

## <a name="the-threat"></a>脅威

組織内のユーザーがランサムウェア攻撃の標的になります。 ユーザーは知らないうちに感染したメールを開いてランサムウェアを実行してしまう可能性があり、これによりクラウドに同期されたファイルを含むすべてのファイルが感染します。

## <a name="the-solution"></a>解決策

疑わしいアクティビティが検出されたときに最新情報を通知するポリシーを作成することで、クラウド環境で潜在的なランサムウェアを検出し、ランサムウェア ファイルがクラウドに保存されることを防ぐ自動アクションを設定します。

## <a name="out-of-the-box-protection"></a>すぐに使える保護

少なくとも 1 つのクラウド アプリ (Office 365、Google Workspace、Box、Dropbox) を Cloud App Security に[接続](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)します。

1. 既定で、Cloud App Security ではネットワークをスキャンしてベースラインが確立されます。そこでユーザーが通常クラウドで行っていることのパターン、その実行のタイミングと一般的に行っていることが学習されます。

2. Cloud App Security の自動[脅威検出ポリシー](anomaly-detection-policy.md)は、接続したときからバックグラウンドで実行が開始されます。 これらのポリシーの 1 つは、ランサムウェア アクティビティを検索して、高度なランサムウェア攻撃に対する包括的なカバレッジを保証します。 セキュリティ研究の専門知識を活用して、ランサムウェアのアクティビティを反映する行動パターンを識別することにより、Cloud App Security では包括的で堅牢な保護が実現されます。 たとえば、ファイルのアップロードまたはファイルの削除アクティビティの比率が高いことが Cloud App Security によって特定された場合は、悪影響を及ぼす暗号化プロセスを表している可能性があります。 このデータは、接続された API からから受信したログに収集され、その後、学習した動作パターンと脅威インテリジェンス (既知のランサムウェア拡張機能など) と組み合わされます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
