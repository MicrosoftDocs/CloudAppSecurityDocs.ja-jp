---
title: 脅威防止ポリシー - Cloud App Security
description: このトピックでは、Cloud App Security で多数の脅威防止ポリシーを構成する手順の概要について説明します。
author: shsagir
ms.author: shsagir
ms.date: 06/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 92a02c1810c427de10719193bd0b75249c9e6c21
ms.sourcegitcommit: e711727f2f00ee3b54e08337a5040449e352ca46
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2020
ms.locfileid: "93186071"
---
# <a name="threat-protection-policies"></a>脅威保護に関するポリシー

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud App Security を使用すると、リスクの高い使用とクラウドのセキュリティの問題を特定し、異常なユーザー動作を検出して、承認されたクラウド アプリでの脅威を防ぐことができます。 ユーザーと管理者のアクティビティの内容を把握し、疑わしい動作またはリスクがあると考えられる特定のアクティビティが検出されたときに自動的にアラートを出すように、ポリシーを定義します。 Microsoft の脅威インテリジェンスおよびセキュリティ研究に関する膨大なデータを利用して、承認されたアプリに必要なすべてのセキュリティ制御が確実に実施され、それらに対する管理が維持されるようにします。

> [!NOTE]
> Cloud App Security と Azure Advanced Threat Protection (Azure ATP) を統合すると、Azure ATP のポリシーもポリシー ページに表示されます。 Azure ATP ポリシーの一覧については、[セキュリティ アラート](/azure-advanced-threat-protection/suspicious-activity-guide)に関するページを参照してください。

## <a name="detect-and-control-user-activity-from-unfamiliar-locations"></a>不明な場所からのユーザーアクティビティを検出して制御する

組織内の誰もアクセスしたことがない不明な場所からのユーザー アクセスまたはアクティビティの自動検出。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリ、または[セッション制御によるアプリの条件付きアクセス制御](proxy-deployment-aad.md)を使用してオンボードされたアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

この検出は、新しい場所からのアクセスがあったらアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

## <a name="detect-compromised-account-by-impossible-location-impossible-travel"></a>あり得ない場所 (あり得ない移動) によって侵害されたアカウントを検出する

2 つの異なる場所から、2 つの場所の間を移動するのに要する時間より短い間隔で行われた、ユーザー アクセスまたはアクティビティの自動検出。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリ、または[セッション制御によるアプリの条件付きアクセス制御](proxy-deployment-aad.md)を使用してオンボードされたアプリが、少なくとも 1 つ必要です。
### <a name="steps"></a>手順

1. この検出は、あり得ない場所からのアクセスがあったらアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。
2. 省略可能: [異常検出ポリシーをカスタマイズする](anomaly-detection-policy.md#scope-anomaly-detection-policies)ことができます。

    - ユーザーとグループに関する検出スコープをカスタマイズする

    - 考慮するサインインの種類を選択する

    - アラートの感度を設定する

3. 異常検出ポリシーを作成します。

## <a name="detect-suspicious-activity-from-an-on-leave-employee"></a>"休暇中" の従業員からの不審なアクティビティを検出する

無給休暇中で、組織のリソースを利用するはずがないユーザーが、組織のクラウド リソースのいずれかにアクセスしていることを検出します。

### <a name="prerequisites"></a>[前提条件]

- [アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。

- Azure Active Directory で無給休暇中のユーザーに対するセキュリティ グループを作成し、監視対象のすべてのユーザーを追加します。

### <a name="steps"></a>手順

1. [[ユーザー グループ]](user-groups.md) 画面で **[ユーザー グループの作成]** をクリックして、関連する Azure AD グループをインポートします。

2. **[ポリシー]** ページで、新しい **アクティビティ ポリシー** を作成します。

3. フィルター **[ユーザー グループ]** を、無給休暇ユーザー用に Azure AD で作成したユーザー グループの名前と等しい、と設定します。

4. オプション:違反が検出された場合にファイルに対して実行する **ガバナンス** アクションを設定します。 使用できるガバナンス アクションは、サービスによって異なります。 **[ユーザーの停止]** を選択できます。

5. ファイル ポリシーを作成します。

## <a name="detect-and-notify-when-outdated-browser-os-is-used"></a>古いブラウザー OS が使用されたときに検出して通知する

組織に対してコンプライアンスやセキュリティ上のリスクをもたらす可能性がある、期限切れのクライアント バージョンのブラウザーをユーザーが使用していることを検出します。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリ、または[セッション制御によるアプリの条件付きアクセス制御](proxy-deployment-aad.md)を使用してオンボードされたアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **アクティビティ ポリシー** を作成します。

2. フィルター **[ユーザー エージェント タグ]** を、 **[古いブラウザー]** および **[古いオペレーティング システム]** と等しい、と設定します。

3. 違反が検出された場合にファイルに対して実行する **ガバナンス** アクションを設定します。 使用できるガバナンス アクションは、サービスによって異なります。 ユーザーがアラートに対応して必要なコンポーネントを更新できるように、 **[すべてのアプリ]** で **[ユーザーに通知する]** を選択します。

4. アクティビティ ポリシーを作成します。

## <a name="detect-and-alert-when-admin-activity-is-detected-on-risky-ip-addresses"></a>危険な IP アドレスでの管理者アクティビティの検出を検出してアラートを生成する

危険な IP アドレスと見なされる IP アドレスから実行された管理者アクティビティを検出し、詳細な調査が行われるようにシステム管理者に通知するか、管理者のアカウントにガバナンス アクションを設定します。

### <a name="prerequisites"></a>[前提条件]

- [アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。

- 設定の歯車から **[IP アドレス範囲]** を選択し、[+] をクリックして、内部サブネットとそのエグレス パブリック IP アドレスに対する IP アドレス範囲を追加します。 **[カテゴリ]** を **[内部]** に設定します。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **アクティビティ ポリシー** を作成します。

2. **[動作の対象]** を **[1 つのアクティビティ]** に設定します。

3. フィルター **[IP アドレス]** を、 **[カテゴリ]** が **[危険]** と等しい、と設定します

4. フィルター **[管理アクティビティ]** を **[True]** に設定します

5. 違反が検出された場合にファイルに対して実行する **ガバナンス** アクションを設定します。 使用できるガバナンス アクションは、サービスによって異なります。 ユーザーがアラートに対応して必要なコンポーネント **[ユーザーの管理者に CC でメールを送信]** を更新できるように、 **[すべてのアプリ]** で **[ユーザーに通知する]** を選択します。

6. アクティビティ ポリシーを作成します。

## <a name="detect-activities-by-service-account-from-external-ip-addresses"></a>外部 IP アドレスからのサービス アカウントでアクティビティを検出する

内部以外の IP アドレスから開始されたサービス アカウント アクティビティを検出します。 これは、疑わしい動作または侵害されたアカウントを示している可能性があります。

### <a name="prerequisites"></a>[前提条件]

- [アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。
- 設定の歯車から **[IP アドレス範囲]** を選択し、[+] をクリックして、内部サブネットとそのエグレス パブリック IP アドレスに対する IP アドレス範囲を追加します。 **[カテゴリ]** を **[内部]** に設定します。

- 環境でのサービス アカウントに対する名前付け規則を標準化します。たとえば、すべてのアカウント名を "svc" で始まるように設定します。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **アクティビティ ポリシー** を作成します。

2. フィルター **[ユーザー]** を **[名前]** に設定し、 **[次で始まる]** を設定して、名前付け規則 (svc など) を入力します。

3. フィルター **[IP アドレス]** を、 **[カテゴリ]** が **[その他]** および **[企業]** と等しくない、と設定します。

4. 違反が検出された場合にファイルに対して実行する **ガバナンス** アクションを設定します。 使用できるガバナンス アクションは、サービスによって異なります。

5. ポリシーを作成します。

## <a name="detect-mass-download-data-exfiltration"></a>大量のダウンロードを検出する (データ窃盗)

特定のユーザーが短時間に大量のファイルにアクセスしたりダウンロードしたりしたときに検出します。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリ、または[セッション制御によるアプリの条件付きアクセス制御](proxy-deployment-aad.md)を使用してオンボードされたアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **アクティビティ ポリシー** を作成します。

2. フィルター **[IP アドレス]** を、 **[タグ]** が **[Microsoft Azure]** と等しくない、と設定します。 これにより、非対話型のデバイス ベースのアクティビティは除外されます。

3. フィルター **[アクティビティの種類]** を等しいに設定し、関連するすべてのダウンロード アクティビティを選択します。

4. 違反が検出された場合にファイルに対して実行する **ガバナンス** アクションを設定します。 使用できるガバナンス アクションは、サービスによって異なります。
5. ポリシーを作成します。

## <a name="detect-potential-ransomware-activity"></a>ランサムウェアのアクティビティの可能性を検出する

ランサムウェアのアクティビティの可能性を自動的に検出します。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. この検出は、ランサムウェアのリスクの可能性が検出されたらアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

2. 検出の **[スコープ]** を構成し、アラートがトリガーされたときに実行するガバナンス アクションをカスタマイズすることができます。 Cloud App Security によるランサムウェアの識別方法の詳細については、「[ランサムウェアから組織を保護する](use-case-ransomware.md)」を参照してください。

> [!NOTE]
> これは、Office 365、G Suite、Box、Dropbox に適用されます。

## <a name="detect-malware-in-the-cloud"></a>クラウド内のマルウェアを検出する

Cloud App Security の Microsoft 脅威インテリジェンス エンジンとの統合を利用して、クラウド環境内でマルウェアを含むファイルを検出します。

### <a name="prerequisites"></a>[前提条件]

- Office 365 のマルウェア検出の場合は、Office 365 Advanced Threat Protection P1 の有効なライセンスが必要です。
- [アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

- この検出は、マルウェアが含まれる可能性があるファイルがあるときはアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

## <a name="detect-rogue-admin-takeover"></a>悪意のある管理者の引き継ぎを検出する

悪意のある意図を示す可能性がある管理アクティビティの繰り返しを検出します。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. **[ポリシー]** ページで、新しい **アクティビティ ポリシー** を作成します。

2. **[動作の対象]** を **[反復アクティビティ]** に設定し、 **[反復アクティビティの最低回数]** をカスタマイズして、 **[期間]** を組織のポリシーに準拠するように設定します。

3. フィルター **[ユーザー]** を、 **[グループから]** が等しいに設定し、 **[アクターのみ]** として関連するすべての管理者グループを選択します。

4. フィルター **[アクティビティの種類]** を、パスワードの更新、変更、リセットに関連するすべてのアクティビティと等しい、と設定します。

5. 違反が検出された場合にファイルに対して実行する **ガバナンス** アクションを設定します。 使用できるガバナンス アクションは、サービスによって異なります。
6. ポリシーを作成します。

## <a name="detect-suspicious-inbox-manipulation-rules"></a>受信トレイに対する疑わしい操作ルールを検出する

疑わしい受信トレイ ルールがユーザーの受信トレイに設定された場合、ユーザー アカウントが侵害されていること、組織内でスパムやマルウェアを配信するためにメールボックスが使用されていることを示す可能性があります。

### <a name="prerequisites"></a>[前提条件]

- メールに Microsoft Exchange を使用していること。

### <a name="steps"></a>手順

- この検出は、受信トレイに疑わしいルールが設定されたらアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

## <a name="detect-leaked-credentials"></a>漏洩した資格情報を検出する

サイバー犯罪者によって正当なユーザーの有効なパスワードが侵害されると、多くの場合、それらの資格情報が共有されます。 通常、これは、ダーク Web サイトまたは貼り付けサイトに公開するか、ブラック マーケットで資格情報を売買または取引することによって行われます。

Cloud App Security では、Microsoft の脅威インテリジェンスを利用して、このような資格情報が組織内で使用されているものと照合されます。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

この検出は、資格情報漏洩の可能性が検出されたらアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

## <a name="detect-anomalous-file-downloads"></a>異常なファイルのダウンロードを検出する

学習されたベースラインを基準として、ユーザーが 1 つのセッションで複数のファイル ダウンロード アクティビティを実行したことを検出します。 これは、侵害の試行を示している可能性があります。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリ、または[セッション制御によるアプリの条件付きアクセス制御](proxy-deployment-aad.md)を使用してオンボードされたアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. この検出は、異常なダウンロードが発生したらアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

2. 検出のスコープを構成し、アラートがトリガーされたときに実行するアクションをカスタマイズすることができます。

## <a name="detect-anomalous-file-shares-by-a-user"></a>ユーザーによる異常なファイルの共有を検出する

学習されたベースラインを基準として、1 回のセッションでユーザーが複数のファイル共有アクティビティを実行したことを検出します。これは、侵害の試行を示している可能性があります。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリ、または[セッション制御によるアプリの条件付きアクセス制御](proxy-deployment-aad.md)を使用してオンボードされたアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. この検出は、ユーザーが複数のファイル共有を実行するとアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

2. 検出のスコープを構成し、アラートがトリガーされたときに実行するアクションをカスタマイズすることができます。

## <a name="detect-anomalous-activities-from-infrequent-country"></a>頻度の低い国からの異常なアクティビティを検出する

組織内のどのユーザーも最近または一度も訪れていない場所からのアクティビティを検出します。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリ、または[セッション制御によるアプリの条件付きアクセス制御](proxy-deployment-aad.md)を使用してオンボードされたアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. この検出は、頻度の低い国や地域から異常なアクティビティが発生したときにアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

2. 検出のスコープを構成し、アラートがトリガーされたときに実行するアクションをカスタマイズすることができます。

> [!NOTE]
> 異常な場所を検出するには、7 日の初期学習期間が必要です。 学習期間中は、Cloud App Security によって新しい場所に対するアラートは生成されません。

## <a name="detect-activity-performed-by-a-terminated-user"></a>解雇されたユーザーによって実行されたアクティビティを検出する

組織の従業員ではなくなったユーザーが承認されたアプリでアクティビティを実行したことを検出します。 これは、会社のリソースにまだアクセスできる退職した従業員による悪意のあるアクティビティを示している可能性があります。

### <a name="prerequisites"></a>[前提条件]

[アプリ コネクタ](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)を使用して接続されているアプリが、少なくとも 1 つ必要です。

### <a name="steps"></a>手順

1. この検出は、解雇されたユーザーによってアクティビティが実行されたらアラートが生成されるように、何もしなくても自動的に構成されます。 このポリシーを構成するために何らかの操作を行う必要はありません。 詳しくは、[異常検出ポリシー](anomaly-detection-policy.md)に関する記事をご覧ください。

2. 検出のスコープを構成し、アラートがトリガーされたときに実行するアクションをカスタマイズすることができます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]