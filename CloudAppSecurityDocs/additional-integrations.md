---
title: Cloud App Security への追加の統合
description: この記事では、Cloud App Security にサードパーティ ソリューションを統合する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/28/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 3d7d005940b032cd6e9b9f4bb5f1f3be13ababcb
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880704"
---
# <a name="additional-integrations-with-external-solutions"></a>外部ソリューションとの追加の統合

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security とお客様のその他のセキュリティ投資を統合して、統合された保護エコシステムを活用および強化することができます。 たとえば、外部のモバイル デバイス管理ソリューション、UEBA ソリューション、および外部の脅威インテリジェンス フィードと統合できます。

Cloud App Security の堅牢なプラットフォームは、次のさまざまな外部のセキュリティ ソリューションと統合できます。

- **脅威インテリジェンス (TI) フィード (Bring You Own TI)**  
    Cloud App Security の [IP アドレス範囲 API](api-data-enrichment.md) を使用して、サードパーティの TI ソリューションで識別された新規の危険な IP アドレス範囲を追加できます。 一度定義されると、IP アドレス範囲を使用して、ログとアラートの表示方法と調査方法をタグ付け、分類、およびカスタマイズすることができます。

- **モバイル デバイス管理 (MDM) / Mobile Threat Defense (MTD) ソリューション**  
    Cloud App Security では、セッションをリアルタイムで細かく制御できます。 セッションの評価と保護における重要な要素は、包括的な ID の構築に役立つユーザーが使用するデバイスです。 デバイスの管理状態は、[Azure Active Directory (Azure AD)](/azure/active-directory/conditional-access/overview)、[Microsoft Intune](/intune/mobile-threat-defense) のデバイス管理状態から直接確認するか、またはより一般的には、さまざまなサードパーティの MDM および MTD ソリューションとの統合を可能にするクライアント証明書の分析によって確認できます。

    Cloud App Security は、外部の MDM および MTD ソリューションからの信号を利用し、[デバイスの管理状態](proxy-intro-aad.md#managed-device-identification)に基づいてセッションを制御します。

- **UEBA ソリューション**  
    複数のデータ ソースに依存し、疑わしいユーザー動作と異常なユーザー動作を識別する各 UEBA ソリューションを複数使用して、さまざまなワークロードとシナリオに対応できます。 外部の UEBA ソリューションは、Azure AD Identity Protection を通じ、Microsoft のセキュリティ エコシステムと統合できます。

    一度統合すると、ポリシーを使用して危険なユーザーを識別し、適応型制御を適用し、ユーザーのリスク レベルを "高" に設定することによって危険なユーザーを自動的に修正できます。 一度 "高" に設定されたユーザーには、ユーザーのパスワードのリセット、MFA 認証の要求、マネージド デバイスを使用するようにユーザーに強制する、などの該当するポリシー アクションが適用されます。

    Cloud App Security を使用すると、セキュリティ チームはユーザーを自動的に、または手動で侵害済みと確認して、侵害されたユーザーを迅速に修復できます。

    詳細については、「[Azure AD でリスクに関するフィードバックを使用する方法](/azure/active-directory/identity-protection/howto-identity-protection-risk-feedback#how-does-azure-ad-use-my-risk-feedback)」と「[ガバナンス アクション](accounts.md#governance-actions)」を参照してください。

[!INCLUDE [Open support ticket](includes/support.md)]
