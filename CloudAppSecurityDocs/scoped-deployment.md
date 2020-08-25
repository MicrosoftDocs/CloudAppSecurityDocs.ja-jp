---
title: Microsoft Cloud App Security 展開のスコープを指定する
description: この記事では、Cloud App Security 展開のスコープを指定する方法について説明します。特定のユーザーまたはグループを含めたり除外したりできます。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/25/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 0d4d046b406e0849437d02f1abba87948e488473
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88779187"
---
# <a name="scoped-deployment"></a>スコープ付きの展開 <a name="scoped-deployment"></a> 

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security を使うと、展開の範囲を限定できます。 スコープによって、特定のユーザー グループをアプリ監視の対象として選択したり、監視から除外したりできます。

## <a name="include-or-exclude-user-groups"></a>ユーザー グループを含めるか除外する

組織内のすべてのユーザーに対して Microsoft Cloud App Security を使用することを避けたい場合があります。 スコープは、ライセンス制約によって展開を制限する場合に特に便利です。 また、特定の国や地域からのユーザーを監視しないことを要求するコンプライアンス規則のために、制限が必要になることもあります。 たとえば、スコープ付きの展開を使用して、米国に居住する従業員のみを監視します。 または、ドイツに居住するユーザーにアクティビティを表示しないようにすることもできます。

- 展開のスコープを指定するには、まず Microsoft Cloud App Security に[ユーザー グループをインポートする](user-groups.md)必要があります。 既定では、次のグループが表示されます。

  - **[アプリケーション]** ユーザー グループ - Office 365 および Azure AD アプリケーションによって実行されるアクティビティを表示できる、組み込みのグループです。

  - **[外部ユーザー]** グループ - 組織用に構成したいずれかのマネージド ドメインのメンバーではないすべてのユーザー。

- 包含ルールを設定すると、包含されるグループに入らないすべてのグループが自動的に除外されます。 たとえば、米国オフィス グループのすべてのメンバーを含めるルールを設定すると、そのグループの一部でないグループは監視されません。

- 除外されるユーザー グループは、包含されるユーザー グループより優先されます。 つまり、"英国従業員" というユーザー グループを包含して、"マーケティング" を除外した場合、英国のマーケティング メンバーは、**英国従業員**グループのメンバーであっても監視されません。

1. メニュー バーで設定の歯車アイコンをクリックし、 **[スコープ付きの展開]** を選択します。

    ![[設定] アイコン](media/settings-icon.png "設定アイコン")

2. 展開のスコープを指定して特定のグループを包含または除外するためには、まず、Microsoft Cloud App Security に[ユーザー グループをインポートする](user-groups.md)必要があります。

3. Microsoft Cloud App Security で特定のグループを監視するように設定するには、 **[含める]** タブで、プラス記号のアイコンをクリックします。
    ![icon](media/plus-icon.png)

4. **[新しい包含ルールの作成]** ダイアログで、次の手順を行います。

    1. **[ルール名を入力]** で、ルールにわかりやすい名前を付けます。
    2. **[ユーザー グループの選択]** で、Cloud App Security で監視するグループをすべて選択します。
    3. 接続されたすべてのアプリにこのルールを適用するのか、**特定のアプリ**のみに適用するのかを選択します。 **特定のアプリ**を選択した場合、ルールは選択したアプリの監視のみに影響します。 たとえば、 **[UI チーム ユーザー]** グループと **[Box]** を選択した場合、Cloud App Security によって UI チーム ユーザー グループ内のユーザーの Box アクティビティのみが監視され、その他すべてのアプリについては、Cloud Apps Security によってすべてのユーザーのすべてのアクティビティが監視されます。

        ![包含ルール](media/include-rule.png)

5. 特定のグループを監視から除外するように設定するには、 **[含まない]** タブで、プラス記号のアイコンをクリックします。

   ![アイコン](media/plus-icon.png)

6. **[新しい除外ルールの作成]** ダイアログで、次のパラメーターを設定します。

    1. **[ルール名を入力]** で、ルールにわかりやすい名前を付けます。
    **[ユーザー グループの選択]** で、Cloud App Security で監視しないグループをすべて選択します。
    2. 接続されたすべてのアプリにこのルールを適用するのか、**特定のアプリ**のみに適用するのかを選択します。 **特定のアプリ**を選択すると、選択したグループの Cloud App Security による監視が、選択したアプリに対してのみ停止されます。 つまり、 **[UI チーム ユーザー]** グループと **Active Directory** を選択した場合、UI チーム ユーザーによって実行される Active Directory アクティビティを除くすべてのユーザー アクティビティが、Cloud App Security で監視されます。

       ![除外ルール](media/exclude-rule.png)

## <a name="example-results-for-include-and-exclude-rules"></a>包含ルールと除外ルールの結果の例

作成した包含ルールと除外ルールが共に働いて、Microsoft Cloud App Security によって実行される監視全体のスコープが指定されます。 ここでは、作成できる包含ルールと除外ルールの例と、これらのルール実行後に Microsoft Cloud App Security によって何が監視されるかの最終的な結果を示します。

次のルールを作成した場合:

- "ドイツのすべてのユーザー" というユーザー グループを除外する
- Office 365 のアクティビティについてのみ "グローバル営業" というユーザー グループを含める
- Power BI のアクティビティについてのみ "営業マネージャー" というユーザー グループを含める
- Salesforce が Microsoft Cloud App Security に接続されていて、それについてのルールは設定していない

次のユーザー アクティビティが監視されます。

|ユーザー|グループのメンバーシップ|監視されるアクティビティ|
|----|----|----|
|Adriana|ドイツのすべてのユーザー<br />グローバル営業<br />営業マネージャー|なし|
|Alain|グローバル営業|Office 365 とすべてのサブアプリ (Power BI を除く)|
|Cornel|グローバル営業<br />営業マネージャー|Office 365 とすべてのサブアプリ|
|Raymond|営業マネージャー|Power BI のみ|

> [!NOTE]
> 他のアプリは、これらのルールでのグループのスコープによって影響されません
> この例で、Salesforce については、すべてのユーザー グループのすべてのアクティビティが監視されます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery を設定する](set-up-cloud-discovery.md)

[!INCLUDE [Open support ticket](includes/support.md)]  
