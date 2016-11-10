---
title: "制御 | Microsoft Docs"
description: "この記事では、組織のクラウド アプリの使用を制御するため Cloud App Security で実施できるガバナンス アクションについて説明します。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/15/2016
ms.topic: article
ms.prod: 
ms.service: cloud-app-security
ms.technology: 
ms.assetid: bc11bbfe-ec6c-458c-8302-8112c383199d
ms.reviewer: reutam
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed4ea71b24767d3602d40894d1cbac7447bcd8a2
ms.openlocfilehash: 9dc74c35f32c9a3dff251d6e0ac6b35a3591f4b9


---

# <a name="control"></a>Control
ガバナンス アクションは、クラウド環境全体のユーザーのファイルに適用できます。 クラウドについて十分に調査して理解したら、ガバナンス アクションを使用して組織を保護することができます。  
  
## <a name="applying-governance-actions"></a>ガバナンス アクションの適用  
ガバナンス アクションは、ポリシー内、アラート内、[**ファイル**] ログから適用できます。  
  
[**設定**] (歯車アイコン) ![設定アイコン](./media/settings-icon.png "settings icon") をクリックし、[**ガバナンス ログ**] をクリックすると、以前に適用されたすべてのガバナンス アクションの状態をいつでも表示して確認することができます。  
  
ガバナンス アクションが失敗した場合は、再試行アイコン ![再試行アイコン](./media/retry-icon.png "retry icon") をクリックして再度適用できます。  
  
ポリシー、違反、アプリの種類に応じて、さまざまなガバナンス アクションを使用できます。  
  
## <a name="moving-from-detection-to-automatic-remediation"></a>検出から自動修復への移行  
ポリシー フィルターを定義してカスタマイズすると、ポリシー違反が発生するたびに実行される自動ガバナンス アクションを選択できます。  
修復アクションではクラウド プロバイダーの API を利用するため、アプリごとにアクションが異なる場合があります。  
  
> [!NOTE]  
>  ガバナンス アクションを設定する場合には十分に注意してください。ファイルへのアクセス許可が失われ、元に戻せなくなる可能性があります。  
> 検索フィールドを使用して、ポリシーを実行する対象ファイルのみが表示されるようにフィルター条件をフィルタリングすることをお勧めします。 フィルター条件を絞り込むほど、適切な結果が得られます。  
>   
>  [フィルター] セクションの [**結果の編集とプレビュー**] ボタンを使用すると結果を確認できます。  
  
![ファイル ポリシーの編集とプレビュー結果](./media/file-policy-edit-and-preview-results.png "file policy edit and preview results")  
  
## <a name="migration"></a>移行  
Cloud App Security では、組織内のどのユーザーがどのアプリを使用しているかを把握できると共に、新しいアプリの導入を監視するツールを提供することで、移行のロールアウトをサポートします。 また、組織内でどのような種類のアプリを提供する必要があるかを理解できるように、すべてのユーザーが既に使用しているアプリを表示するツールが提供されます。  
  
### <a name="how-to-migrate-your-users-to-a-new-app"></a>新しいアプリにユーザーを移行する方法  
たとえば、最近になって Office 365 を購入し、組織内のすべてのユーザーに他のクラウド ストレージ アプリの使用を停止して、代わりに OneDrive を使用してほしいと考えているとします。 この場合、以下の操作を実行できます。  
  
-   **Cloud Discovery ダッシュボード**に移動して、[**カテゴリ**] から [**クラウド ストレージ**] によってアプリをフィルタリングします。 [**ユーザー**] または [**IP アドレス**] 別に結果を並べ替え、最も多く使用されているアプリを確認します。  
  
-   他のアプリを使用しているユーザーを確認することができます。  
  
     また、それらのアプリにドリルダウンして、以下の手順で、そのアプリを使用しているユーザーに対して OneDrive に移行するように通知することもできます。  
  
    1.  **Cloud Discovery ダッシュボード**で [Dropbox] をクリックし、[**IP アドレス**] または [**ユーザー**] タブをクリックします。  
  
    2.  矢印 ![矢印アイコン](./media/arrow-icon.png "arrow icon") をクリックして、[**エクスポート**] を選択します。  
  
### <a name="find-more-secure-alternatives"></a>安全な代替アプリの検索  
Cloud App Security サービス カタログを使用すると、ユーザーが使用している危険なアプリの代わりに、組織に最適な代替アプリを検索できます。  
  
たとえば、生産性ツールの購入を検討しているものの、ユーザーがそのツールを活用するかどうか確信できないとします。  
  
-   **Cloud Discovery ダッシュボード**に移動します。  
  
-   [**カテゴリ**] から [**生産性**] によってアプリをフィルタリングします。  
  
-   使用中の各アプリについて、[**スコア**] をチェックして、アプリが安全であるかどうかを確認し、安全でない場合はその理由を確認します。  
  
-   組織全体のエンタープライズ ライセンスを購入しようと考えている場合は、決定を下す前に、[**ユーザー**] 列もチェックして、現在最も多くのユーザーが使用しているアプリ、そのアプリの信頼性、そのアプリに備わっているセキュリティ機能を確認することをお勧めします。  
  
## <a name="see-also"></a>参照  
[ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)   
[テクニカル サポートが必要な場合は、Cloud App Security のサポート ページをご利用ください。](http://support.microsoft.com/oas/default.aspx?prid=16031)   
[Premier サポートをご利用のお客様は、Premier ポータルから直接 Cloud App Security を選択することもできます。](https://premier.microsoft.com/)  
  
  


<!--HONumber=Oct16_HO4-->

