---
title: Microsoft Defender for Identity を Cloud App Security と統合する
description: この記事では、ハイブリッド リスク検出のために Cloud App Security で Microsoft Defender for Identity の分析情報を利用する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/08/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 0c5bb0d20a4e82280841d95352181739be8ea4fa
ms.sourcegitcommit: 66d818441eaae1e07c4bb2ce35bbcb833febf622
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94428110"
---
# <a name="microsoft-defender-for-identity-integration"></a>Microsoft Defender for Identity の統合

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security は Microsoft Defender for Identity と統合され、ハイブリッド環境 (クラウド アプリとオンプレミスの両方) でユーザー エンティティの行動分析 (UEBA) を提供します。詳細については、「[チュートリアル: 危険性の高いユーザーを調査する](tutorial-ueba.md)」を参照してください。 Defender for Identity によって提供される機械学習と行動分析の詳細については、「[Defender for Identity とは](/defender-for-identity/what-is)」を参照してください

## <a name="prerequisites"></a>[前提条件]

ハイブリッド環境全体で完全なユーザー調査を実行するためには、次が必要です。

- ご自身の Active Directory インスタンスに接続されている Microsoft Defender for Identity の有効なライセンス
- Defender for Identity と Cloud App Security の統合を有効にするには、Azure Active Directory グローバル管理者である必要があります

> [!NOTE]
>
> - Microsoft Cloud App Security のサブスクリプションがない場合でも、Cloud App Security を使用して Defender for Identity の分析情報を得ることができます。
> - Defender for Identity 管理者には、Cloud App Security にアクセスするための新しいアクセス許可が必要になる場合があります。 Cloud App Security に対するアクセス許可を割り当てる方法については、「[管理者アクセスの管理](manage-admins.md)」を参照してください。

## <a name="enable-defender-for-identity"></a>Defender for Identity を有効にする

Cloud App Security と Defender for Identity の統合を有効にするには:

1. Cloud App Security で、設定の歯車アイコンから **[設定]** を選択します。

    ![[設定] メニュー](media/azip-system-settings.png)

1. **[脅威の防止]** で、 **[Microsoft Defender for Identity]** を選択します。

    ![Azure Advanced Threat Protection の有効化](media/mdi-integration.png)

1. **[Enable Microsoft Defender for Identity data integration]\(Microsoft Defender for Identity データ統合を有効にする\)** をオンにしてから、 **[保存]** をクリックします。

> [!NOTE]
> 統合が有効になるまで、最大 12 時間かかることがあります。

Defender for Identity 統合を有効にすると、組織内のすべてのユーザーのオンプレミス アクティビティを確認できるようになります。 クラウド環境とオンプレミス環境をまたいで、アラートと疑わしいアクティビティを組み合わせたユーザーの高度な分析情報も得られるようになります。 さらに、Defender for Identity のポリシーが Cloud App Security のポリシー ページに表示されるようになります。 Defender for Identity ポリシーの一覧については、[セキュリティ アラート](/defender-for-identity/suspicious-activity-guide)に関するページを参照してください。 これらのポリシーを編集するには、「[検出からのエンティティの除外](/defender-for-identity/excluding-entities-from-detections)」を参照してください。

**Defender for Identity 構成** リンクを使用して、Cloud App Security に関連する Defender for Identity 設定を構成する必要もあります。 これらの設定の詳細については、次の情報を参照してください。

- [Microsoft Defender for Identity センサーを構成する](/defender-for-identity/install-step5)
- [ディレクトリ サービス アカウントの構成](/defender-for-identity/install-step2)
- [VPN 用の RADIUS アカウンティングを構成する](/defender-for-identity/install-step6-vpn)
- [Microsoft Defender for Identity 正常性センターにアクセスする](/defender-for-identity/health-center)

## <a name="disable-defender-for-identity"></a>Defender for Identity を無効にする

Cloud App Security と Defender for Identity の統合を無効にするには:

1. Cloud App Security で、設定の歯車アイコンから **[設定]** を選択します。

1. **[脅威の防止]** で、 **[Microsoft Defender for Identity]** を選択します。

1. **[Enable Microsoft Defender for Identity data integration]\(Microsoft Defender for Identity データ統合を有効にする\)** をオフにしてから、 **[保存]** をクリックします。

> [!NOTE]
> 統合が無効になっている場合、既存の Defender for Identity データは Cloud App Security のデータ保持ポリシーに従って保持されますが、ID セキュリティ体制評価のセクションは削除されます。

## <a name="known-issues"></a>既知の問題

### <a name="missing-siem-alert-updates"></a>SIEM アラートの更新が発生しない

この問題は、複数回トリガーされるアラートに影響します。 アラートの最初のインスタンスは SIEM に送信されますが、同じアラートの後続のトリガーは送信されません。

#### <a name="resolution"></a>解決策

既知の解決策はありません。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]