---
title: Azure Active Directory Identity Protection を Cloud App Security と統合する
description: この記事では、ハイブリッド リスク検出のために Cloud App Security で Identity Protection のアラートを利用する方法について説明します。
ms.date: 12/27/2020
ms.topic: how-to
ms.openlocfilehash: f71e73dfd3ca8be7d6ed5e03847ac6e11e290818
ms.sourcegitcommit: 4900168878f42e9fa79873df4b7c2d81991b5b27
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97857956"
---
# <a name="azure-active-directory-identity-protection-integration"></a>Azure Active Directory Identity Protection の統合

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security は Azure Active Directory Identity Protection (Identity Protection) と統合され、ハイブリッド環境全体でユーザー エンティティ行動分析 (UEBA) を提供します。 Identity Protection によって提供される機械学習と行動分析の詳細については、「[Identity Protection とは](/azure/active-directory/identity-protection/overview-identity-protection)」を参照してください。

## <a name="prerequisites"></a>[前提条件]

- Identity Protection と Cloud App Security の統合を可能にする Cloud App Security 管理者アカウント。

## <a name="enable-identity-protection"></a>Identity Protection を有効にする

> [!NOTE]
> Identity Protection 機能は既定で有効になっています。 ただし、機能が無効になっている場合、次の手順で有効化できます。

Cloud App Security と Identity Protection の統合を有効にするには:

1. Cloud App Security で、設定の歯車アイコンから **[設定]** を選択します。

    ![[設定] メニュー](media/azip-system-settings.png)

1. **[Threat Protection]\(脅威の防止\)** で、 **[Azure AD Identity Protection]** を選択します。

    ![Azure Advanced Threat Protection の有効化](media/aadip-integration.png)

1. **[Enable Azure AD Identity Protection alert integration]\(Azure AD Identity Protection のアラート統合を有効にする\)** を選択してから **[保存]** をクリックします。

Identity Protection 統合を有効にすると、組織内のすべてのユーザーに対するアラートを確認できるようになります。

## <a name="disable-identity-protection"></a>Identity Protection を無効にする

Cloud App Security と Identity Protection の統合を無効にするには:

1. Cloud App Security で、設定の歯車アイコンから **[設定]** を選択します。

1. **[Threat Protection]\(脅威の防止\)** で、 **[Azure AD Identity Protection]** を選択します。

1. **[Enable Azure AD Identity Protection alert integration]\(Azure AD Identity Protection のアラート統合を有効にする\)** を選択解除してから **[保存]** をクリックします。

> [!NOTE]
>
> - 統合が無効になっている場合、既存の Identity Protection アラートは Cloud App Security のデータ保持ポリシーに従って保持されます。
> - Cloud App Security で使用されるのは Azure AD からの対話型ログインのみであるため、一部のアラートで関連するアクティビティが表示されない場合があります。 そのようなアクティビティは、Azure AD ポータルで調査できます。

## <a name="configure-identity-protection-policies"></a>Identity Protection のポリシーを構成する

Identity Protection のポリシーは、重大度スライダーを使用して、組織のニーズに合わせて微調整できます。 感度スライダーを使用すると、どのアラートが取り込まれるかを制御できます。 このようにして、カバレッジのニーズと (SNR) ターゲットに応じて検出を調整できます。

次のポリシーを利用できます。

|ポリシー|[説明]|既定の状態|既定の重要度|
|---|---|---|---|
|漏えいした資格情報|漏えいした資格情報 (ユーザーの有効な資格情報が漏えいしている) のアラートを表示する|Enabled|低 - すべてのアラートを受信する|
|危険なサインイン|複数の危険なサインイン (ユーザーが実行したのではないサインイン) の検出を集計する|Enabled|高 - 重大度が高いアラートのみを受信する|

> [!NOTE]
> Cloud App Security によって、Identity Protection のアラートに関するメール通知が送信されることはありません。 ただし、Identity Protection ポータルでそれらのメール通知を構成できます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
