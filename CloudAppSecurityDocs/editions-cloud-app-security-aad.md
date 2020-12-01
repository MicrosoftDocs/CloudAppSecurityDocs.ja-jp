---
title: Cloud App Security と Azure AD の検出機能の違い
description: この記事では、Cloud App Security と Azure AD の検出機能の違いについて説明します。
ms.date: 8/29/2019
ms.topic: overview
ms.openlocfilehash: 4a5374294407d1b3011f4b7fcd4edca1254e0532
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96311487"
---
# <a name="what-are-the-differences-in-discovery-capabilities-for-azure-active-directory-and-microsoft-cloud-app-security"></a>Azure Active Directory と Microsoft Cloud App Security では、検出機能にどのような違いがありますか。

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、Microsoft Cloud App Security と Azure Active Directory (Azure AD) の検出機能の相違点について説明します。

ライセンスの詳細については、「[Microsoft Cloud App Security ライセンス データシート](https://aka.ms/mcaslicensing)」を参照してください。

## <a name="microsoft-cloud-app-security"></a>Microsoft Cloud App Security

Microsoft Cloud App Security は包括的なクロス SaaS ソリューションです。高度な可視化、強力なデータ管理、高性能な脅威防御といった機能をクラウド アプリにもたらします。 Cloud Discovery は、Cloud App Security の機能の 1 つであり、使用中のクラウド アプリを検出することで、シャドウ IT に可視性を確保することができます。

## <a name="enhanced-cloud-app-discovery-in-azure-active-directory"></a>Azure Active Directory で強化された Cloud App Discovery

Azure Active Directory Premium P1 には、[Azure Active Directory Cloud App Discovery](./set-up-cloud-discovery.md) が含まれており、追加費用はかかりません。 この機能は、Microsoft Cloud App Security Cloud Discovery 機能に基づいており、組織内のクラウド アプリの使用状況により詳細な可視性を提供します。 [Microsoft Cloud App Security をアップグレード](https://www.microsoft.com/cloud-platform/cloud-app-security)すると、Microsoft Cloud App Security で提供される Cloud App Security Broker (CASB) の各種機能を受け取ります。

### <a name="feature-comparison"></a>機能の比較

Microsoft Cloud App Security と Azure AD の検出機能の比較を次の表に示します。

|機能|機能|Microsoft Cloud App Security|Azure AD Cloud App Discovery|
|----|----|----|----|
|Cloud Discovery|検出されたアプリ|16,000 超のクラウド アプリ|16,000 超のクラウド アプリ|
||検出分析のためのデプロイ|手動と自動のログ アップロード|手動と自動のログ アップロード|
||ユーザー プライバシーのログ匿名化|はい|はい|
||完全なクラウド アプリ カタログへのアクセス|はい|はい|
||クラウド アプリのリスク評価|はい|はい|
||アプリ、ユーザー、IP アドレス別のクラウド利用状況分析|はい|はい|
||継続的な分析と報告|はい|はい|
||検出されたアプリの異常検出|はい||
|情報の保護|データ損失防止 (DLP) サポート|クロス SaaS DLP とデータ共有制御||
||アプリのアクセス許可とアクセスを取り消す機能 (OAuth アプリ)|はい||
||ポリシー設定と適用|はい||
||Azure Information Protection との統合 |はい||
||サード パーティ製の DLP ソリューションとの統合|はい||
|脅威検出|異常検出と行動分析|クロス SaaS アプリの場合||
||手動と自動のアラート修復|はい||
||SIEM コネクタ|はい。 クロス SaaS アプリのアラートとアクティビティ ログ。||
||Microsoft インテリジェント セキュリティ グラフへの統合|はい||
||アクティビティ ポリシー|はい||

## <a name="next-steps"></a>次のステップ

基本については、「[Cloud App Security の使用を開始する](getting-started-with-cloud-app-security.md)」をご覧ください。

[!INCLUDE [Open support ticket](includes/support.md)].