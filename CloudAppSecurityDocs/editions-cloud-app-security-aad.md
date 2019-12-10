---
title: Cloud App Security と Azure AD の検出機能の相違点
description: この記事では、Microsoft Cloud App Security と Azure AD の検出機能の相違点について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/29/2019
ms.topic: overview
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 825a8532588cc479bcc37e5373bff23ccc841d8d
ms.sourcegitcommit: 6eff466c7a6817b14a60d8c3b2c201c7ae4c2e2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74461040"
---
# <a name="what-are-the-differences-in-discovery-capabilities-for-azure-active-directory-and-microsoft-cloud-app-security"></a>Azure Active Directory と Microsoft Cloud App Security の検出機能の相違点

*適用対象:Microsoft Cloud App Security*

この記事では、Microsoft Cloud App Security と Azure Active Directory (Azure AD) の検出機能の相違点について説明します。

ライセンスについて詳しくは、[Microsoft Cloud App Security のライセンスのデータシート](https://aka.ms/mcaslicensing)をご覧ください。

## <a name="microsoft-cloud-app-security"></a>Microsoft Cloud App Security

Microsoft Cloud App Security は包括的なクロス SaaS ソリューションです。高度な可視化、強力なデータ管理、高性能な脅威防御といった機能をクラウド アプリにもたらします。 Cloud Discovery は、Cloud App Security の機能の 1 つであり、使用中のクラウド アプリを検出することで、シャドウ IT に可視性を確保することができます。

## <a name="enhanced-cloud-app-discovery-in-azure-active-directory"></a>Azure Active Directory で強化された Cloud App Discovery

Azure Active Directory Premium P1 には、[Azure Active Directory Cloud App Discovery](https://aka.ms/caddocsnew) が含まれており、追加費用はかかりません。 この機能は、Microsoft Cloud App Security Cloud Discovery 機能に基づいており、組織内のクラウド アプリの使用状況により詳細な可視性を提供します。 [Microsoft Cloud App Security をアップグレード](https://www.microsoft.com/cloud-platform/cloud-app-security)すると、Microsoft Cloud App Security で提供される Cloud App Security Broker (CASB) の各種機能を受け取ります。

### <a name="feature-comparison"></a>機能の比較

Microsoft Cloud App Security と Azure AD の検出機能の比較を次の表に示します。

|機能|機能|Microsoft Cloud App Security|Azure AD Cloud App Discovery|
|----|----|----|----|
|Cloud Discovery|検出されたアプリ|16,000 を超えるクラウド アプリ|16,000 を超えるクラウド アプリ|
||検出分析の展開|ログの手動アップロードと自動アップロード|ログの手動アップロードと自動アップロード|
||ユーザーのプライバシー保護のためのログの匿名化|はい|はい|
||すべてのクラウド アプリ カタログへのアクセス|はい|はい|
||クラウド アプリのリスク評価|はい|はい|
||アプリ、ユーザー、IP アドレス別のクラウド利用状況分析|はい|はい|
||継続的な分析とレポート|はい|はい|
||検出されたアプリの異常検出|はい||
|情報の保護|データ損失防止 (DLP) サポート|クロス SaaS DLP およびデータ共有制御||
||アプリのアクセス許可とアクセスの取り消し機能|はい||
||ポリシーの設定と適用|はい||
||Azure Information Protection との統合 |はい||
||サード パーティの DLP ソリューションとの統合|はい||
|脅威の検出|異常検出と行動分析|クロス SaaS アプリの場合||
||手動および自動のアラート修復|はい||
||SIEM コネクタ|対応 クロス SaaS アプリのアラートとアクティビティ ログ。||
||Microsoft インテリジェント セキュリティ グラフに統合|はい||
||アクティビティ ポリシー|はい||

## <a name="next-steps"></a>次の手順

基本については、「[Cloud App Security の使用を開始する](getting-started-with-cloud-app-security.md)」をご覧ください。

[!INCLUDE [Open support ticket](includes/support.md)]。
