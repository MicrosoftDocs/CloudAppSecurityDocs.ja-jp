---
title: クラウド アプリのアカウントの可視化 - Cloud App Security
description: この記事では、接続されているアプリのアカウントを確認する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/20/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 9d59c944fb2467eef98ac13f8d6a3673b2049a8c
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880253"
---
# <a name="accounts"></a>[アカウント]

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security では、接続されているアプリのアカウントを表示できます。 アプリ コネクタを使用して Cloud App Security をアプリに接続すると、接続されたアプリに関連付けられているアカウント情報が Cloud App Security によって読み取られます。 [アカウント] ページでは、これらのアカウント、アクセス許可、所属するグループ、エイリアス、使用しているアプリを調べることができます。 また、接続されているいずれかのアプリ (アクティビティやファイル共有など) で以前は存在しなかった新しいアカウントを Cloud App Security が検出した場合は、そのアカウントがそのアプリのアカウントの一覧に追加されます。 これにより、クラウド アプリとやり取りする外部ユーザーのアクティビティを表示できます。

管理者は、特定のユーザーのメタデータまたはユーザーのアクティビティを検索できます。 **[ユーザーとアカウント]** ページには、接続されたクラウド アプリケーションから取得されたエンティティに関する包括的な詳細情報が表示されます。 また、ユーザーのアクティビティ履歴とユーザーに関連するセキュリティ アラートも提供されます。

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

**[ユーザーとアカウント]** ページでは、特定のアカウントを検索したり、各種のアカウントの詳細を表示したりするために、[フィルター](#users-and-accounts-filters)を使用できます。たとえば、昨年からアクセスされていないすべての外部アカウントをフィルター処理できます。

**[ユーザーとアカウント]** ページでは、次のような問題についてアカウントを簡単に調査できます。

* 特定のサービスで長期間アクティブではないアカウントがあるかどうかを確認します (そのユーザーのそのサービスに対するライセンスを取り消す必要がある場合があります)

* 管理者のアクセス許可を持つユーザーの一覧を表示するためにフィルター処理できます
* 組織のメンバーではなくなったが、まだアクティブなアカウントを持っている可能性があるユーザーを検索できます
* アカウントに対してアプリの中断などの[ガバナンス アクション](#governance-actions)を実行したり、アカウント設定ページに移動したりできます。
* 各ユーザー グループに含まれているアカウントを確認できます  
* 各アカウントによってアクセスされているアプリと、特定のアカウントに対して削除されたアプリを確認できます

    ![アカウント画面](media/accounts-page.png)

## <a name="users-and-accounts-filters"></a>ユーザーとアカウントのフィルター

適用可能なアカウント フィルターの一覧を以下に示します。 ほとんどのフィルターでは NOT をはじめとする複数値がサポートされているため、ポリシー作成時の強力なツールとなります。  
  
<!--- **Account name**: The account name is the primary alias of the user, but other identifiers from other Microsoft accounts (Office 365 and Azure Active Directory) such as proxy addresses, aliases, SID are supported and consolidated beneath the primary alias. -->

* **所属**:[所属] は、 **[内部]**  または **[外部]** のいずれかです。 ユーザーとアカウントを内部として設定するには、 **[設定]** で内部組織の **IP アドレスの範囲**を設定してください。 アカウントに管理者のアクセス許可がある場合は、アカウント テーブルのアイコンに赤いネクタイが追加されます。 ![アカウントの管理者アイコン](media/accounts-admin-icon.png)

* **[アプリ]** :組織内のアカウントで使用されている API で接続されたアプリをフィルター処理できます。
* **ドメイン**: 特定のドメインのユーザーを表示するためにフィルター処理できます。
* **[グループ]** :Cloud App Security のユーザー グループのメンバーをフィルター処理できます (組み込みユーザー グループとインポートされたユーザー グループの両方)。
* **インスタンス**: 特定のアプリ インスタンスのメンバーを表示するためにフィルター処理できます。
* **最終表示日**: **[最終表示日]** フィルターを使用すると、休止状態であり、ユーザーがしばらくの間アクティビティを実行していないアカウントを見つけることができます。
* **組織**:接続されているアプリで定義された特定の組織グループのメンバーを表示するためにフィルター処理できます。
* **管理者のみを表示**:管理者であるアカウントとユーザーを表示するためにフィルター処理します。
* **状態**: ユーザー アカウントの状態 (N/A、ステージング済み、アクティブ、中断、または削除) に基づいてフィルター処理します。 該当なし (N/A) の状態は正常であり、匿名アカウントの場合などに表示されることがあります。
* **種類**:ユーザーまたはアカウントの種類でフィルター処理できます。
* **ユーザー名**:特定のユーザーを表示するためにフィルター処理できます。

## <a name="governance-actions"></a>ガバナンス アクション

**[ユーザーとアカウント]** ページでは、アプリの中断などのガバナンス アクションを実行したり、アカウント設定ページに移動したりできます。 ガバナンス アクションの完全な一覧については、「[ガバナンス ログ](governance-actions.md)」を参照してください。

たとえば、侵害されたユーザーを識別した場合は、 **[Confirm user compromised]** \(ユーザーが侵害されたことを確認\) アクションを適用して、そのユーザーのリスク レベルを「高」に設定し、Azure Active Directory で定義されている関連するポリシー アクションを適用することができます。 アクションは、手動で適用するか、[ガバナンス アクションをサポートする関連ポリシー](governance-actions.md)を使用して適用することができます。

### <a name="to-manually-apply-a-user-or-account-governance-action"></a>ユーザーまたはアカウントのガバナンス アクションを手動で適用するには

**[Confirm user compromised]** \(ユーザーが侵害されたことを確認\) アクションを手動で適用するには、次のいずれかの方法を使用します。

* **[ユーザーとアカウント]** ページの関連するユーザーまたはアカウントが表示されている行で、行の末尾にある 3 つの点を選択し、 **[Confirm user compromised]** \(ユーザーが侵害されたことを確認\) を選択します。

* **[ユーザー]** ページで、 **[ユーザー操作]** を選択して、 **[Confirm user compromised]** \(ユーザーが侵害されたことを確認\) を選択します。

* **ユーザー名**:特定のユーザーを表示するためにフィルター処理できます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
