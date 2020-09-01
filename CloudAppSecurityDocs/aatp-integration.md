---
title: Azure Advanced Threat Protection と Cloud App Security の統合
description: この記事では、ハイブリッド リスク検出のために Cloud App Security で Azure Advanced Threat Protection の分析情報を利用する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/24/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 33ccea97fd5b41802d7f8b12fe7413c5bd76d8a6
ms.sourcegitcommit: 870ca47381a36b4bc04e1ccb9b2a522944431fed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88963592"
---
# <a name="azure-advanced-threat-protection-integration"></a>Azure Advanced Threat Protection の統合

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security は Azure Advanced Threat Protection (Azure ATP) と統合され、ハイブリッド環境 (クラウド アプリとオンプレミスの両方) でユーザー エンティティの行動分析 (UEBA) を提供します。詳細については、「[チュートリアル: 危険性の高いユーザーを調査する](tutorial-ueba.md)」を参照してください。 Azure ATP によって提供される機械学習と行動分析の詳細については、「[Azure ATP の概要](/azure-advanced-threat-protection/what-is-atp)」を参照してください。

## <a name="prerequisites"></a>[前提条件]

ハイブリッド環境全体で完全なユーザー調査を実行するためには、次が必要です。

- ご自身の Active Directory インスタンスに接続されている Azure ATP の有効なライセンス
- Azure ATP と Cloud App Security の統合を有効にするには、Azure Active Directory グローバル管理者である必要があります。

> [!NOTE]
>
> - Microsoft Cloud App Security のサブスクリプションがない場合でも、Cloud App Security を使用して Azure ATP の分析情報を取得できます。
> - Azure ATP 管理者は、Cloud App Security にアクセスするための新しいアクセス許可が必要になる場合があります。 Cloud App Security に対するアクセス許可を割り当てる方法については、「[管理者アクセスの管理](manage-admins.md)」を参照してください。

## <a name="enable-azure-atp"></a>Azure ATP の有効化

Cloud App Security と Azure ATP の統合を有効にするには:

1. Cloud App Security で、設定の歯車アイコンから **[設定]** を選択します。

    ![[設定] メニュー](media/azip-system-settings.png)

1. **[Threat Protection]\(脅威の防止\)** で、 **[Azure ATP]** を選択します。

    ![Azure Advanced Threat Protection の有効化](media/aatp-integration.png)

1. **[Enable Azure ATP data integration]\(Azure ATP データ統合の有効化\)** を選択してから **[保存]** をクリックします。

> [!NOTE]
> 統合が有効になるまで、最大 12 時間かかることがあります。

Azure ATP 統合を有効にすると、組織内のすべてのユーザーのオンプレミス アクティビティを確認できるようになります。 クラウド環境とオンプレミス環境をまたいで、アラートと疑わしいアクティビティを組み合わせたユーザーの高度な分析情報も得られるようになります。 さらに、Azure ATP のポリシーが Cloud App Security のポリシー ページに表示されるようになります。 Azure ATP ポリシーの一覧については、[セキュリティ アラート](/azure-advanced-threat-protection/suspicious-activity-guide)に関するページを参照してください。

**Azure ATP 構成**リンクを使用して、Cloud App Security に関連する Azure ATP 設定を構成する必要もあります。 これらの設定の詳細については、次の情報を参照してください。

- [Azure ATP センサーの構成](/azure-advanced-threat-protection/install-atp-step5)
- [ディレクトリ サービス アカウントの構成](/azure-advanced-threat-protection/install-atp-step2)
- [VPN 用の RADIUS アカウンティングを構成する](/azure-advanced-threat-protection/install-atp-step6-vpn)
- [Azure ATP ヘルス センターへのアクセス](/azure-advanced-threat-protection/atp-health-center)

## <a name="disable-azure-atp"></a>Azure ATP の無効化

Cloud App Security と Azure ATP の統合を無効にするには:

1. Cloud App Security で、設定の歯車アイコンから **[設定]** を選択します。

1. **[Threat Protection]\(脅威の防止\)** で、 **[Azure ATP]** を選択します。

1. **[Enable Azure ATP data integration]\(Azure ATP データ統合の有効化\)** を選択解除してから **[保存]** をクリックします。

> [!NOTE]
> 統合が無効になっている場合、既存の Azure ATP データは Cloud App Security のデータ保持ポリシーに従って保持されますが、ID セキュリティ体制評価のセクションは削除されます。

## <a name="known-issues"></a>既知の問題

### <a name="missing-siem-alert-updates"></a>SIEM アラートの更新が発生しない

この問題は、複数回トリガーされるアラートに影響します。 アラートの最初のインスタンスは SIEM に送信されますが、同じアラートの後続のトリガーは送信されません。

#### <a name="resolution"></a>解決策

既知の解決策はありません。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]