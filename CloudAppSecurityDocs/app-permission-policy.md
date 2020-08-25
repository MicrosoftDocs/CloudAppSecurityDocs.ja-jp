---
title: Cloud App Security で OAuth アプリを制御するポリシーを作成する
description: この記事では、Microsoft Cloud App Security でアプリのアクセス許可ポリシーを作成して使用する手順について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/27/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 6d3d281d8ad56e52f717125f62a7feb580b007b9
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781346"
---
# <a name="oauth-app-policies"></a>OAuth アプリ ポリシー

*適用対象:Microsoft Cloud App Security*

環境に接続されている [OAuth アプリの既存の調査](manage-app-permissions.md)に加えて、OAuth アプリが特定の条件を満たしたときに自動通知を受け取るようにアクセス許可ポリシーを設定することができます。 たとえば、高いアクセス許可レベルを必要とし、50 人を超えるユーザーによって承認されたアプリがある場合、自動的にアラートを受け取ることができます。

OAuth アプリ ポリシーを使用すると、各アプリで要求されたアクセス許可と、Office 365、G Suite、Salesforce に対してそれを承認したユーザーを調べることができます。 また、これらのアクセス許可を承認済みまたは禁止済みとしてマークすることもできます。 禁止済みとしてマークすると、承認したユーザーごとに各アプリに対するアクセス許可が取り消されます。

## <a name="create-a-new-oauth-app-policy"></a>新しい OAuth アプリ ポリシーを作成する

新しい OAuth アプリ ポリシーを作成するには、2 つの方法があります。 1 番目の方法は **[調査]** の下にあり、2 番目の方法は **[制御]** の下にあります。

新しい OAuth アプリ ポリシーを作成するには:

1. **[調査]** で、 **[OAuth アプリ]** を選択ます。

1. ニーズに従ってアプリをフィルター処理します。たとえば、**メールボックスの予定表の変更**に対する**アクセス許可**を要求しているすべてのアプリを表示できます。
1. **[検索に基づく新しいポリシー]** ボタンをクリックします。
    ![検索に基づく新しいポリシー](media/app-permissions-filter.png)
1. **[コミュニティの利用状況]** フィルターを使用して、このアプリに対してアクセスを許可することが、一般的か、一般的ではないか、珍しいか、に関する情報を取得できます。 このフィルターは、珍しいアプリで、重要度レベルが高いアクセス許可、または多くのユーザーからのアクセス許可が要求されている場合に役立ちます。
1. アプリを承認したユーザーのグループ メンバーシップに基づいてポリシーを設定できます。 たとえば、管理者は、アクセス許可を承認したユーザーが Administrators グループのメンバーである場合にのみ、一般的ではないアプリが高いアクセス許可を要求した場合にそれらを失効させるポリシーを設定することができます。

または、 **[制御]** をクリックしてから **[ポリシー]** をクリックて、ポリシーを作成することもできます。 その後、 **[ポリシーの作成]** をクリックし、 **[OAuth アプリ ポリシー]** をクリックします。

   ![新しい OAuth アプリ ポリシー](media/app-permissions-policy.png)

## <a name="oauth-app-anomaly-detection-policies"></a>OAuth アプリ異常検出ポリシー

作成できる OAuth アプリポリシーに加えて、次のようなすぐに使用できる異常検出ポリシーがあります。それらでは、OAuth アプリのメタデータがプロファイリングされて、悪意がある可能性のあるものが識別されます。

| ポリシー名 | ポリシーの説明 |
| --- | --- |
| まぎらわしい OAuth アプリ名 | 環境に接続されている OAuth アプリがスキャンされて、まぎらわしい名前のアプリが検出されるとアラートがトリガーされます。 ラテン文字に似た外国語の文字などを使ったまぎらわしい名前は、悪意のあるアプリを、既知の信頼されたアプリとして偽装しようとしていることを示している可能性があります。 |
| OAuth アプリのまぎらわしい発行元名 | 環境に接続されている OAuth アプリがスキャンされて、まぎらわしい発行元名前のアプリが検出されるとアラートがトリガーされます。 ラテン文字に似た外国語の文字などを使ったまぎらわしい発行元の名前は、悪意のあるアプリを、既知の信頼された発行元からのアプリとして偽装しようとしていることを示している可能性があります。 |
| 悪意のある OAuth アプリの同意 | 環境に接続されている OAuth アプリがスキャンされて、悪意を持つ可能性があるアプリが承認されるとアラートがトリガーされます。 悪意のある OAuth アプリは、ユーザーを侵害する試みでフィッシング キャンペーンの一部として使用される可能性があります。 この検出では、Microsoft のセキュリティ研究と脅威インテリジェンスの専門知識が利用されて、悪意のあるアプリが特定されます。 |
| 疑わしい OAuth アプリ ファイルのダウンロード アクティビティ | [異常検出ポリシー](anomaly-detection-policy.md#suspicious-oauth-app-file-download-activities)に関する記事を参照してください |

<!--
| OAuth apps authorized by external users | Scans OAuth apps connected to your environment and triggers an alert when an app was authorized by an external user. |
| OAuth apps with high permissions and rare community use – Google | Scans OAuth apps connected to your environment and triggers an alert for apps with high permissions and rare community use in Google. |
| OAuth apps with high permissions and rare community use – Office | Scans OAuth apps connected to your environment and triggers an alert for apps with high permissions and rare community use in Office. |
| OAuth apps with rare community use - Salesforce | Scans OAuth apps connected to your environment and triggers an alert for apps with rare community use in Salesforce. |
-->

> [!NOTE]
> 異常検出ポリシーは、Azure Active Directory で承認されている OAuth アプリに対してのみ使用できます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [データ保護ポリシー](data-protection-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
