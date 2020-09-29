---
title: Cloud App Security で接続されたアプリからユーザー グループをインポートする
description: この記事では、接続されているアプリから Cloud App Security にユーザー グループをインポートする手順について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/17/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: ed844bd996cbf6b9b5a4119999f95ae6209c6207
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90878392"
---
# <a name="importing-user-groups-from-connected-apps"></a>接続されているアプリからユーザー グループをインポートする

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security により、API コネクタを使用してアプリを接続するときに、Office 365 や Azure Active Directory などのユーザー グループをインポートすることができます。 ユーザー グループには、次の 2 種類があります。

- 自動グループ  
自動グループは、既定で Microsoft Cloud App Security によって作成されます。 たとえば、**外部**という名前の自動ユーザー グループがあり、組織の外部にいてファイルへのアクセス権があるか、またはあなたのテナント内でユーザー アクティビティを行っていたすべてのユーザーをすべてのアプリからまとめているとします。 Cloud App Security には、次の自動グループが存在します。

  - 外部
  - Dropbox 管理者
  - Office 365 管理者
  - G Suite 管理者
  - Box 管理者
  - すべての Salesforce 標準およびカスタム プロファイル (例: Salesforce システム管理者)。 完全なリストは、[こちら](https://help.salesforce.com/articleView?id=standard_profiles.htm&language=en&type=0)をご覧ください。

- インポートされたグループ  
接続されているアプリから任意のグループをインポートできます。 たとえば、Office 365 (Active Directory) およびその他の接続されているアプリからユーザー グループをインポートできます。 これらのグループにより、組織全体や特定のユーザーを調べるのではなく、特定のグループを調べることで、組織内の脅威を探すことができます。

  インポートされたユーザー グループを使用する一般的なシナリオは次のとおりです。

  - 人事担当者が見ているドキュメントを調査する
  - 役員グループで異常なことが起こっていないかどうかを確認する
  - 管理者グループのだれかが米国外でアクティビティを行ったかどうかを確認する

## <a name="how-to-import-user-groups"></a>ユーザー グループをインポートする方法

1. メニュー バーで、設定アイコン ![設定アイコン](media/settings-icon.png "設定アイコン")、 **[ユーザー グループ]** の順にクリックします。
1. **[ユーザー グループのインポート]** をクリックします。

    ![ユーザー グループのインポート](media/user-groups-add.png)

1. ユーザー グループをインポートするアプリを選択します。 アプリのリストは、展開したアプリ コネクタによって異なります。
1. インポートするグループを選択します。 使用可能なグループのリストは、アプリ自体の既存のすべてのユーザー グループのリストになります。 新しいグループを追加する場合は、アプリ自体で直接追加する必要があります。 次に、このリストにグループが表示されたら、それを選択します。
1. グループのサイズによっては、インポートに最大で 1 時間かかることがあります。 インポート処理が完了したら、メールで通知するオプションを選択できます。
1. **[インポート]** をクリックします。 グループをインポートすると、Active Directory Connect と同様に、Cloud App Security によってグループ メンバーが自動的に同期されます。
1. インポートが完了したら、 **[ユーザー グループ]** ページで特定のグループをクリックすると、グループのすべてのメンバーのリストを表示できます。 グループの任意のメンバーをクリックすると、特定のアカウントの詳細にドリルダウンできます。 彼らが使用しているアプリと、ユーザーとそのアクティビティのグラフを含むアカウントの概要を表示できます。

グループをインポートすると、**アクティビティ ログ**を調べたりポリシーを作成したりするときに、それらのグループをフィルターとして選択できます。

> [!NOTE]
>
> - インポートされたユーザー グループがフィルターで使用できるようになるまでに、短時間の遅延が発生することがあります。
> - ユーザー グループのインポート後に実行されたアクティビティだけが、ユーザー グループのメンバーによって実行されたとものとしてタグ付けされます。
> - 最初の同期後は、1 時間ごとにグループが更新されます。

ユーザー グループ フィルターの使用方法の詳細については、「[アクティビティ](activity-filters.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery を設定する](set-up-cloud-discovery.md)

[!INCLUDE [Open support ticket](includes/support.md)]
