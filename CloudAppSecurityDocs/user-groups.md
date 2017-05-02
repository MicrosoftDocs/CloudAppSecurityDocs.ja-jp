---
title: "接続されているアプリからユーザー グループをインポートする | Microsoft Docs"
description: "このトピックでは、Cloud App Security にユーザー グループをインポートする方法について説明します。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/19/2017
ms.topic: get-started-article
ms.prod: 
ms.service: cloud-app-security
ms.technology: 
ms.assetid: 87b831ef-5977-4df8-bed3-3ee54a8adbb5
ms.reviewer: reutam
ms.suite: ems
ms.openlocfilehash: a6a4b0e2c79fcb96a307d83a4077492138b73066
ms.sourcegitcommit: 0d4748ea2a71e6ee2b0fa1c0498d9219bfbda29a
translationtype: HT
---
# <a name="import-user-groups-preview"></a>ユーザー グループのインポート (プレビュー)

API コネクタを使用してアプリを接続するとき、Cloud App Security を使用し、たとえば、Office 365 や Azure Active Directory からユーザー グループをインポートできます。
2 種類のユーザー グループがあります。 
- 自動グループ </br>既定で自動グループが Cloud App Security により作成されます。 たとえば、**外部**という名前の自動ユーザー グループがあります。このグループは、組織にとって部外者にあたるすべてのユーザーがすべてのアプリから集められて作られ、ファイルへのアクセスが許可されます。あるいは、テナントのユーザー アクティビティに関与したユーザーのグループです。
 次の自動グループが Cloud App Security に存在します。
  - 外部リンク
  - Dropbox 管理者
  - Office 365 管理者
  - G Suite 管理者
  - Box 管理者
  - すべての Salesforce 標準/カスタム プロファイル (Salesforce システム管理者など)。 完全一覧は[ここ](https://help.salesforce.com/articleView?id=standard_profiles.htm&language=en&type=0)でご覧いただけます。

- インポートされたグループ</br>接続されているアプリからグループをインポートできます。 たとえば、Office 365 (Active Directory) とその他の接続されているアプリからユーザー グループをインポートできます。 組織全体や特定のユーザーを見なくても、特定のグループを見ることで組織内の脅威を探すことができます。 

インポートしたユーザー グループを利用する一般的なシナリオには、HR のユーザーが閲覧するドキュメントの調査、経営グループ内で通常とは異なるイベントが発生していないかのチェック、管理者グループのユーザーが米国外でアクティビティを実行していないかのチェックなどがあります。 ユーザー グループのインポート方法:

1. メニュー バーで設定アイコン ![設定アイコン](./media/settings-icon.png "設定アイコン") をクリックし、**[ユーザー グループ]** を選択します。
2. **[ユーザー グループのインポート]** をクリックします。

  ![ユーザー グループのインポート](./media/user-groups-add.png)

3. ユーザー グループのインポート元にするアプリを選択します。 アプリの一覧は、展開したアプリ コネクタによって変わります。
4. インポートするグループを選択します。 利用できるグループの一覧は、アプリ自体のすべての既存ユーザー グループの一覧になります。 新しいグループを追加する場合、アプリ自体でそれを直接追加する必要があります。その新しいグループがここに表示されたら選択します。
4. グループのサイズによっては、インポートに最大 1 時間かかることがあります。 インポート プロセスがかんりょうしたときにメールで通知するオプションを選択できます。
5. クリックして **インポート**します。 グループをインポートすると、Cloud App Security は Active Directory Connect と同様にグループ メンバーを自動同期します。
7. インポートが完了すると、**[ユーザー グループ]** ページから、特定のグループをクリックし、グループのすべてのメンバーの一覧を表示できます。 また、グループのメンバーをクリックし、特定のアカウントの詳細を表示したり、特定のアカウントで使用されているアプリや、ユーザーのグラフやアクティビティなど、アカウントの概要を表示したりできます。

グループをインポートすると、**[アクティビティ ログ]** で調査したり、ポリシーを作成したりするときのフィルターとしてグループを選択できます。 

> [!NOTE]
> あるユーザー グループのインポート後に実行されたアクティビティにのみ、そのユーザー グループのメンバーにより実行されているというタグが付けられます。

ユーザー グループ フィルターの使用方法については、「[アクティビティ](activity-filters.md)」を参照してください。


    
## <a name="see-also"></a>参照  
[Cloud Discovery のセットアップ](set-up-cloud-discovery.md)   
[テクニカル サポートが必要な場合は、Cloud App Security のサポート ページをご利用ください。](http://support.microsoft.com/oas/default.aspx?prid=16031)   
[Premier サポートをご利用のお客様は、Premier ポータルから直接 Cloud App Security を選択することもできます。](https://premier.microsoft.com/)  
  
  