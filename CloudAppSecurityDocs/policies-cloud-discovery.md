---
title: Cloud Discovery ポリシー - Cloud App Security
description: この記事では、Cloud App Security で多数の Cloud Discovery ポリシーを構成する手順の概要について説明します。
author: shsagir
ms.author: shsagir
ms.date: 06/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 028df24a9efbd88337727032df3941e8b086f6e1
ms.sourcegitcommit: e711727f2f00ee3b54e08337a5040449e352ca46
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2020
ms.locfileid: "93186091"
---
# <a name="cloud-discovery-policies"></a>Cloud Discovery ポリシー

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、Cloud Discovery を使用して組織全体のシャドウ IT を可視化するために、Cloud App Security の使用を開始する方法の概要について説明します。

Cloud App Security を使用すると、組織の環境内で使用されているクラウド アプリを検出して分析することができます。 Cloud Discovery ダッシュボードでは、環境内で実行されているすべてのクラウド アプリが表示され、機能別およびエンタープライズ対応別に分類されます。 エンドポイント デバイスにエージェントをインストールする必要なしに、アプリごとに、関連付けられているユーザー、IP アドレス、デバイス、トランザクションを検出し、リスク評価が実行されます。

## <a name="detect-new-high-volume-or-wide-app-use"></a>大量または広範な新しいアプリの使用を検出する <a name= "detect-volume"></a>

組織でのユーザー数またはトラフィック量に関して、多く使用されている新しいアプリを検出します。

### <a name="prerequisites"></a>[前提条件]

「[継続的なレポートのために自動ログ アップロードを構成する](configure-automatic-log-upload-for-continuous-reports.md)」で説明されているように、継続的な Cloud Discovery レポート用に自動ログ アップロードを構成します。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **アプリ検出ポリシー** を作成します

2. **[ポリシー テンプレート]** フィールドで、 **[ボリュームの大きい新しいアプリ]** または **[新しい人気の高いアプリ]** を選択して、テンプレートを適用します。

3. 組織の要件を満たすようにポリシー フィルターをカスタマイズします。

4. アラートがトリガーされたときに実行するアクションを構成します。

> [!NOTE]
> 過去 90 日以内に検出されなかった新しいアプリごとに、アラートが生成されます。

## <a name="detect-new-risky-or-non-compliant-app-use"></a>新しいアプリの使用で危険なものまたは非準拠のものを検出する

クラウド アプリにおいて可能性のある組織の公開で、セキュリティ標準を満たしていないものを検出します。

### <a name="prerequisites"></a>[前提条件]

「[継続的なレポートのために自動ログ アップロードを構成する](configure-automatic-log-upload-for-continuous-reports.md)」で説明されているように、継続的な Cloud Discovery レポート用に自動ログ アップロードを構成します。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **アプリ検出ポリシー** を作成します。

2. **[ポリシー テンプレート]** フィールドで、 **[新しい危険なアプリ]** テンプレートを選択して、テンプレートを適用します。

3. **[次のすべてに一致するアプリ]** で、 [[リスク スコア]](risk-score.md) スライダーと [コンプライアンス リスク要因] を設定して、アラートをトリガーするリスクのレベルをカスタマイズし、組織のセキュリティ要件に合わせて他のポリシー フィルターを設定します。

    1. オプション:さらに意味のある検出を行うには、アラートがトリガーされるトラフィックの量をカスタマイズします。

    2. **[以下のすべてが同じ日に起こった場合にポリシーの一致をトリガーする]** チェック ボックスをオンにします。

    3. **[毎日のトラフィック]** として 2000 GB (またはその他) より大きい値を選択します。

4. アラートがトリガーされたときに実行するガバナンス アクションを構成します。 **[ガバナンス]** で、 **[アプリに "承認されていない" のタグを付ける]** を選択します。<br />ポリシーが一致すると、アプリへのアクセスが自動的にブロックされます。

5. オプション:[Cloud App Security ネイティブ統合](set-up-cloud-discovery.md)とセキュリティで保護された Web ゲートウェイを利用して、アプリのアクセスをブロックします。

## <a name="detect-use-of-unsanctioned-business-apps"></a>未承認のビジネス アプリの使用を検出する

承認されたビジネス対応アプリの代わりとして、従業員が承認されていないアプリの使用を続けている場合に、それを検出できます。

### <a name="prerequisites"></a>[前提条件]

- 「[継続的なレポートのために自動ログ アップロードを構成する](configure-automatic-log-upload-for-continuous-reports.md)」で説明されているように、継続的な Cloud Discovery レポート用に自動ログ アップロードを構成します。

### <a name="steps"></a>手順

1. クラウド アプリ カタログで、ビジネス対応アプリを検索し、[カスタム アプリ タグ](discovered-app-queries.md#creating-and-managing-custom-app-tags)でそれをマークします。

2. 「[新しい大量または大規模なアプリの使用を検出する](#detect-volume)」の手順に従います。

3. **[アプリ タグ]** フィルターを追加し、ビジネス対応アプリ用に作成したアプリ タグを選択します。

4. アラートがトリガーされたときに実行するガバナンス アクションを構成します。 [ガバナンス] で、 **[アプリに "承認されていない" のタグを付ける]** を選択します。<br />ポリシーが一致すると、アプリへのアクセスが自動的にブロックされます。

5. オプション:[Cloud App Security ネイティブ統合](set-up-cloud-discovery.md)とセキュリティで保護された Web ゲートウェイを利用して、アプリのアクセスをブロックします。

## <a name="detect-unusual-usage-patterns-on-your-network"></a>ネットワークでの通常な使用パターンを検出する

組織のネットワーク内のユーザーまたは IP アドレスから送信された、クラウド アプリでの異常なトラフィック使用パターン (アップロードまたはダウンロード) を検出します。

### <a name="prerequisites"></a>[前提条件]

「[継続的なレポートのために自動ログ アップロードを構成する](configure-automatic-log-upload-for-continuous-reports.md)」で説明されているように、継続的な Cloud Discovery レポート用に自動ログ アップロードを構成します。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **Cloud Discovery 異常検出ポリシー** を作成します。

2. **[ポリシー テンプレート]** フィールドで、 **[検出されたユーザーでの異常な動作]** または **[検出された IP アドレスの異常なビヘイビアー]** を選択します。

3. 組織の要件を満たすようにフィルターをカスタマイズします。

4. 危険なアプリが関係する異常が存在する場合にのみアラートを受け取る場合は、 **[リスク スコア]** フィルターを使用して、アプリが危険と見なされる範囲を設定します。

5. スライダーを使用して **[異常を検出する秘密度を選択]** を設定します。

> [!NOTE]
> 継続的なログ アップロードを確立した後、異常検出エンジンによって、組織で予想される動作に対するベースラインが確立されるまで、数日かかります (学習期間)。 ベースラインが確立された後、ユーザーまたは IP アドレスによって実行される、クラウド アプリ全体で予想されるトラフィックの動作からの差異に基づいて、アラートを受け取り始めます。

## <a name="detect-data-exfiltration-to-unsanctioned-storage-apps"></a>承認されていないストレージ アプリへのデータ抜き取りを検出する

ユーザーによる承認されていないクラウド ストレージ アプリへのデータ抜き取りの可能性を検出します。

### <a name="prerequisites"></a>[前提条件]

「[継続的なレポートのために自動ログ アップロードを構成する](configure-automatic-log-upload-for-continuous-reports.md)」で説明されているように、継続的な Cloud Discovery レポート用に自動ログ アップロードを構成します。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、組み込みポリシー **[承認されていないアプリへのデータ抜き取り]** を編集します。

2. **[アプリ カテゴリ]** フィルターを **[クラウド ストレージ]** に設定します。

3. **[一致するイベントごとにポリシー重要度に応じたアラートを作成する]** チェック ボックスをオンにします。

4. アラートがトリガーされたときに実行するアクションを構成します。

## <a name="detect-risky-oauth-apps"></a>危険な OAuth アプリを検出する

G Suite、Office 365、Salesforce などのアプリ内にインストールされている [OAuth アプリ](investigate-risky-oauth.md)の情報を取得して制御します。 高いアクセス許可を要求し、コミュニティをあまり使用しない OAuth アプリは、危険であると見なされる場合があります。

### <a name="prerequisites"></a>[前提条件]

G Suite、Office 365、または Salesforce アプリは、[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続する必要があります。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **OAuth アプリ ポリシー** を作成します。

2. **[アプリ]** フィルターを選択し、ポリシーでカバーするアプリ (G Suite、Office 365、または Salesforce) を設定します。

3. **[アクセス許可レベル]** フィルターを **[高]** に設定します (G Suite と Office 365 で使用可能)。

4. **[コミュニティの利用状況]** フィルターを **[まれ]** に設定します。

5. アラートがトリガーされたときに実行するアクションを構成します。 たとえば、Office 365 の場合は、ポリシーによって検出された OAuth アプリに対して **[アプリの取り消し]** をオンにします。

> [!NOTE]
> G Suite、Office 365、Salesforce アプリ ストアでサポートされています。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
