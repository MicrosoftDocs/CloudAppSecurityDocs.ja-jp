---
title: アクセスを許可またはブロックするための Cloud App Security アクセス ポリシーを作成する
description: この記事では、Azure AD 経由でリバース プロキシ機能を使用して接続したアプリへのアクセスを許可およびブロックするために、Cloud App Security の "アプリの条件付きアクセス制御" アクセス ポリシーを設定する手順について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/31/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 9fdea4bcf8db70a1f8eed023cb8af81d328b8771
ms.sourcegitcommit: 870ca47381a36b4bc04e1ccb9b2a522944431fed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88963524"
---
# <a name="access-policies"></a>アクセス ポリシー

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security アクセス ポリシーでは、ユーザー、場所、デバイス、アプリを基準に、クラウド アプリへのアクセスをリアルタイムで監視し、制御できます。 クライアント証明書をマネージド デバイスにロールアウトするか、サード パーティの MDM 証明書などの既存の証明書を使用することで、(Hybrid Azure AD Join ではなく、Microsoft Intune によって管理されないデバイスを含めた) 任意のデバイス用のアクセス ポリシーを作成できます。 たとえば、マネージド デバイスにクライアント証明書をデプロイし、その後、証明書のないデバイスからのアクセスをブロックできます。

> [!NOTE]
> [セッション ポリシー](session-policy-aad.md)では、アクセスを完全に許可またはブロックするのではなく、セッションを監視しながらアクセスを許可したり、特定のセッション アクティビティを制限したりできます。

## <a name="prerequisites-to-using-access-policies"></a>アクセス ポリシーを使用するための前提条件

- Azure AD Premium P1 ライセンス、または ID プロバイダー (IdP) ソリューションに必要なライセンス
- 関連するアプリを、[アプリの条件付きアクセス制御と共にデプロイする](proxy-deployment-aad.md)必要があります。
- 次のように、Cloud App Security と連動するように IdP ソリューションを構成します。
  - [Azure AD 条件付きアクセス](/azure/active-directory/active-directory-conditional-access-azure-portal)については、[Azure AD との統合を構成する](proxy-deployment-aad.md#configure-integration-with-azure-ad)方法に関するページを参照してください
  - その他の IdP ソリューションについては、[その他の IdP ソリューションとの統合を構成する](proxy-deployment-aad.md#configure-integration-with-other-idp-solutions)方法に関するページを参照してください。

## <a name="create-a-cloud-app-security-access-policy"></a>Cloud App Security アクセス ポリシーを作成する

新しいアクセス ポリシーを作成するには、次の手順を実行します。

1. ポータルで、 **[Control]\(制御\)** に続けて **[ポリシー]** を選択します。
2. **[ポリシー]** ページで、 **[ポリシーの作成]** をクリックして **[アクセス ポリシー]** を選択します。

3. **[アクセス ポリシー]** ウィンドウで、「*Block access from unmanaged devices*」(アンマネージド デバイスからのアクセスをブロック) のような名前をポリシーに割り当てます。

4. **[Activities matching all of the following]\(以下のすべてに一致するアクティビティ\)** セクションの **[アクティビティ ソース]** で、ポリシーに適用する追加のアクティビティ フィルターを選択します。 フィルターには次のオプションがあります。

    - **[デバイス タグ]** : アンマネージド デバイスを識別するには、このフィルターを使用します。

    - **場所**: 不明な (したがって危険な) 場所を識別するには、このフィルターを使用します。

    - **[IP アドレス]** :IP アドレスでフィルター処理するか、以前に割り当てた IP アドレス タグを使うには、このフィルターを使用します。

    - **[ユーザー エージェント タグ]** : モバイル アプリまたはデスクトップ アプリを識別するためにヒューリスティックを有効にするには、このフィルターを使用します。 このフィルターは、"等しい" または "等しくない" に設定できます。 値は、各クラウド アプリのモバイル アプリとデスクトップ アプリに対してテストする必要があります。

5. **[Actions]\(操作\)** で、次のオプションのいずれかを選択します。

    - **[テスト]** : 設定したポリシー フィルターに従って明示的にアクセスを許可するには、このアクションを設定します。

    - **[ブロック]** :設定したポリシー フィルターに従って明示的にアクセスをブロックするには、このアクションを設定します。

6. **一致するイベントごとにポリシーの重要度に応じたアラートを作成**し、アラート制限を設定して、アラートをメールとテキスト メッセージのどちらにするか、または両方にするかを選択できます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [« 戻る: セッション ポリシーを作成する方法](session-policy-aad.md)

> [!div class="nextstepaction"]
> [次へ: 人気のあるユース ケースを参照する »](use-case-proxy-block-session-aad.md)

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [セッション制御を使用したアンマネージド デバイスでのダウンロードのブロック](use-case-proxy-block-session-aad.md)

> [!div class="nextstepaction"]
> [アクセスおよびセッション制御のトラブルシューティング](troubleshooting-proxy.md)

[!INCLUDE [Open support ticket](includes/support.md)]