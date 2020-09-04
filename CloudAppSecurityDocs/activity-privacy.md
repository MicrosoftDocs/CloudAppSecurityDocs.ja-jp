---
title: アクティビティのプライバシー
description: この記事では、ユーザー プライバシー ポリシーに準拠するよう、アクティビティ監視を構成する方法に関する情報を提供します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 2d642a834111a1b8cadc3e997bdb63a19426aac1
ms.sourcegitcommit: c174a7ada5c6a14f0fea9870672898c54e5e3b52
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2020
ms.locfileid: "89149909"
---
# <a name="activity-privacy"></a>アクティビティのプライバシー

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security を使用することで、企業では、グループのメンバーシップに基づいて監視するユーザーを細かく決定できます。 アクティビティのプライバシーにより、ユーザーのプライバシーを侵害することなく組織のコンプライアンス規制に従う機能が追加されます。 これは、お客様がユーザーを監視しながら、アクティビティ ログでアクティビティを非表示にすることによってユーザーのプライバシーを維持することで実現されます。 承認された管理者のみがこれらのプライベート アクティビティを表示することを選択できます。各インスタンスはガバナンス ログで監査されます。

## <a name="configure-activity-privacy-user-groups"></a>アクティビティのプライバシーのユーザー グループを構成する

Cloud App Security で監視したいユーザーがいるが、コンプライアンス規制によりその操作を実行できるユーザーを制限する必要がある場合があります。 アクティビティのプライバシーを使用すると、既定でそのアクティビティが非表示になるユーザー グループを定義できます。

ユーザーのプライバシー グループを構成するには、まず Cloud App Security に[ユーザー グループをインポートする](user-groups.md)必要があります。 既定では、次のグループが表示されます。

- **[アプリケーション]** ユーザー グループ - Microsoft 365 および Azure AD アプリケーションによって実行されるアクティビティを表示できる、組み込みのグループです。

- **[外部ユーザー]** グループ - 組織用に構成したいずれかのマネージド ドメインのメンバーではないすべてのユーザー。

1. メニュー バーで設定の歯車アイコンをクリックし、 **[スコープ付きの展開とプライバシー]** を選択します。

    ![設定アイコン](media/settings-icon.png)

1. Cloud App Security によって監視される特定のグループを設定するには、 **[アクティビティのプライバシー]** タブで、プラス記号のアイコンをクリックします。
    ![icon](media/plus-icon.png)

1. **[ユーザー グループの追加]** ダイアログの **[ユーザー グループの選択]** の下で、Cloud App Security でプライベートにするすべてのグループを選択し、 **[追加]** をクリックします。

    ![[ユーザー グループの追加] ダイアログ ボックスを示すスクリーンショット](media/activity-privacy-add-user-groups.png)

    > [!NOTE]
    > ユーザー グループが追加されると、そのグループのユーザーによって実行されるすべてのアクティビティが、それ以降はプライベートになります。 既存のアクティビティは影響を受けません。

## <a name="assign-admins-permission-to-view-private-activities"></a>プライベート アクティビティを表示するアクセス許可を管理者に割り当てる

1. メニュー バーで設定の歯車アイコンをクリックし、 **[管理者のアクセス権管理]** を選択します。

    ![設定アイコン](media/settings-icon.png)

1. 特定の管理者にプライベート アクティビティを表示するアクセス許可を付与するには、 **[アクティビティのプライバシーのアクセス許可]** タブで、プラス記号のアイコンをクリックします。
    ![icon](media/plus-icon.png)

1. **[管理者アクセス許可の追加]** ダイアログで、管理者の UPN またはメール アドレスを入力し、 **[アクセス許可の追加]** をクリックします。

    ![[管理者アクセス許可の追加] ダイアログ ボックスを示すスクリーンショット](media/activity-privacy-add-admin-permission.png)

    > [!NOTE]
    > プライベート アクティビティを表示するアクセス許可は、管理者にのみ割り当てることができます。

## <a name="viewing-private-activities"></a>プライベート アクティビティの表示

管理者は、プライベート アクティビティを表示するための適切なアクセス許可が付与されると、アクティビティ ログでこれらのアクティビティを表示するかどうかを選択できるようになります。

### <a name="to-view-private-activities"></a>プライベート アクティビティを表示するには

1. **[アクティビティ ログ]** ページで、アクティビティ テーブルの右側にある設定アイコンをクリックし、 **[Show private activities]\(プライベート アクティビティの表示\)** を選択します。

    ![アクティビティ ログの設定アイコンを示すスクリーンショット](media/activity-privacy-view-settings-icon.png)

1. **[Show private activities]\(プライベート アクティビティの表示\)** ダイアログで、 **[OK]** をクリックして、この操作が監査対象になることを理解していることを確認します。 確認が完了すると、アクティビティ ログにプライベート アクティビティが表示され、操作がガバナンス ログに記録されます。

[!INCLUDE [Open support ticket](includes/support.md)]
