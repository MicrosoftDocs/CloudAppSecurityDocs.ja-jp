---
title: Cloud App Security で発生したアラートを監視する
description: この記事では、すべてのアラートの一覧と説明を示します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 0b7e74adea5ef8f314b1a4c43f3be018a1978468
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88779459"
---
# <a name="monitor-alerts-in-cloud-app-security"></a>Cloud App Security でアラートを監視する

*適用対象:Microsoft Cloud App Security*

アラートは、クラウド環境をより深く理解するためのエントリ ポイントです。 この記事では、すべてのアラートの一覧と説明を示します。

## <a name="monitoring-your-alerts"></a>アラートの監視

すべてのアラートを確認することをお勧めします。 アラートが発生する理由を理解することで、ポリシーを変更するためのツールとして使用することができます。

**アラートを表示するには:** Microsoft Cloud App Security ポータルで、 **[アラート]** をクリックします。

![アラート メニュー](media/alert-menu.png)

- 確認して関心がないと判断したら、アラートを**無視**します。
  - アラートを無視した理由を説明する**コメント**を入力します
  - **[このアラートについてフィードバックをお送りください]** は、アラートを改善するためにセキュリティ リサーチ チームによって確認されます。

- アラートを調査してリスクを軽減する場合は、そのアラートを**解決**します。

  - アラートはアラート テーブルに表示されなくなります。
  - 問題の調査を開始しても、忘れないように残しておきたい場合は、**未読としてマーク**します。
  - 今後のアラートの一致を向上させるために、アラートと一致した**ポリシーを調整**します。
  - アラートを解決すると、コメントを入力し、**Cloud App Security チームにフィードバックを送信する**ことができます。

## <a name="built-in-alerts"></a>組み込みアラート

次の種類のアラートが表示されます。

|アラート名|AlertID|[説明]|
|----|----|----|
|新しい場所|ALERT_GEOLOCATION_NEW_COUNTRY|スキャンが開始されてから新しい場所が検出されました (最大 6 か月)。 このアラートは、組織全体に対して、国や地域ごとに 1 回だけ表示されます。 |
|新しい管理者ユーザー|ALERT_ADMIN_USER|特定のアプリに対して新しい管理者が検出されました。 この管理者は、あるアプリケーションの管理者が、別のアプリケーションの管理者になった人である可能性があります。 このアラートは特定の管理者の種類に関するものであるため、管理者の種類が変更されるたびに表示されます。 ユーザーが管理特権を失ってから、再び得た場合は、このアラートが表示されます。|
|非アクティブなアカウント|ALERT_ZOMBIE_USER|ユーザーがアプリケーションごとに 60 日間非アクティブになっている場合 (たとえば、Box ではアクティブになっていても、G Suite を 60 日間使用していない場合)、そのユーザーは G Suite で非アクティブであると見なされます。 非アクティブなアカウントを検索できるように、これらのユーザーにはタグが追加されます。|
|予期しない管理者の場所|ALERT_NEW_ADMIN_LOCATION|スキャンが開始されてから管理者に対して新しい場所が検出されました (最大 6 か月)。 このアラートは、組織全体のすべての管理者に対して、国や地域ごとに 1 回だけ表示されます。 |
|危険な状態のアカウント|ALERT_COMPROMISED_ACCOUNT|アプリケーションで侵害が発生し、侵害されたアカウントの一覧が発行された場合、Cloud App Security ではその一覧をダウンロードし、ユーザーの一覧と比較します。 ユーザー一覧には、内部ユーザー、外部ユーザー、および個人アカウントが含まれます。 |

## <a name="custom-alerts"></a>カスタム アラート

次の種類のアラートが表示されます。

|アラート名|AlertID|[説明]|
|----|----|----|
|不審なアクティビティのアラート|ALERT_SUSPICIOUS_ACTIVITY|不審なアクティビティには、異常なアクティビティがどの程度疑わしいか (非アクティブなアカウントが関連するかどうか。 新しい場所からのものかどうか) に従ってスコアが付けられますこれらの条件はすべて、次のリスク要因に基づいてリスク スコアを提供するためにまとめられています。 <br />ユーザーは管理者である <br />リモート専用ユーザー<br />匿名プロキシ<br /> セッション全体でログインに失敗した<br />多数のログインの失敗<br />新規 (管理者)<br />ユーザー/テナントの IP/ISP/国/ユーザー エージェント<br /> (管理者) ユーザーのみに使用されている IP/ISP/国/ユーザー エージェント<br />久しぶりの (管理者) ユーザー アクティビティ<br />久しぶりにこの特定の管理アクティビティが実行された<br />この特定の管理アクティビティは一般的なものではない、または、これまで実行されたことがない<br />過去にこの IP のみがログインに失敗している<br />あり得ない移動|
|不審なクラウド使用のアラート|ALERT_DISCOVERY_ANOMALY_DETECTION|Cloud Discovery の異常検出では、通常の動作のパターンが確認され、通常とは異なる方法で使用されているユーザーまたはアプリを探します。 |
|アクティビティ ポリシー違反|ALERT_CABINET_EVENT_MATCH_AUDIT|このアラートでは、ポリシーの一致が検出されたことを知らせます。|
|ファイル ポリシー違反|ALERT_CABINET_EVENT_MATCH_FILE|このアラートでは、ポリシーの一致が検出されたことを知らせます。|
|プロキシ ポリシー違反|ALERT_CABINET_INLINE_EVENT_MATCH|このアラートでは、ポリシーの一致が検出されたことを知らせます。|
|フィールド ポリシー違反|ALERT_CABINET_EVENT_MATCH_OBJECT|このアラートでは、ポリシーの一致が検出されたことを知らせます。|
|新しいサービスが検出されました|ALERT_CABINET_DISCOVERY_NEW_SERVICE|新しいアプリが検出されました。|
|個人アカウントの使用|ALERT_PERSONAL_USER_SAGE|ファイル共有とユーザー名に基づいて、検出エンジンによって個人アカウントが検索されます。 |

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
