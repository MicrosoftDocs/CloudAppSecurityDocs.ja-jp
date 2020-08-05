---
title: Cloud App Security Activities API
description: この記事では、Activities API の使用について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 0f6528074003d43777d21e956961739a19584742
ms.sourcegitcommit: 84eafb4926bf0d4db27bed7df55dc83ca48f9192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87377832"
---
# <a name="activities-api"></a>Activities API

*適用対象:Microsoft Cloud App Security*

Activity API を使用すると、クラウド アプリで実行されたすべてのアクションを把握できます。 この API のデータでは、誰が、いつ、どのアプリにログインしたか、どのファイルが疑わしい場所からダウンロードされているか、などに関する情報を提供できます。

サポートされている要求は次のとおりです。

- [アクティビティの一覧を取得する](api-activities-list.md)
- [アクティビティを取得する](api-activities-fetch.md)
- [アクティビティにフィードバックする](api-activities-feedback.md)

## <a name="filters"></a>フィルタ

フィルターの動作の詳細については、「[フィルター](api-introduction.md#filters)」を参照してください。

次の表では、サポートされているフィルターについて説明します。

| フィルター | Type | 演算子 | [説明] |
| --- | --- | --- | --- |
| サービス | integer | eq、neq | 指定したサービス appID に関連するアクティビティをフィルター処理します。例: 11770 |
| インスタンス | integer | eq、neq | 指定したインスタンスからのアクティビティをフィルター処理します |
| user.orgUnit | string | eq、neq、isset、isnotset | 実行しているユーザーの組織単位でアクティビティをフィルター処理します |
| activity.eventType | string | eq、neq | イベントの種類でアクティビティをフィルター処理します |
| activity.id | string | eq | ID でアクティビティを検索します |
| activity.impersonated | boolean | eq | "true" に設定すると偽装されたイベントのみが返され、"false" に設定すると偽装されていないイベントが返されます |
| activity.type | boolean | eq | "true" に設定すると管理イベントのみが返され、"false" に設定すると通常のイベントが返されます |
| activity.takenAction | string | eq、neq | それらに対して実行されたアクションによってアクティビティをフィルター処理します。 次の値を指定できます。<br /><br />**block**: ［ブロック済み］<br />**proxy**: セッション制御にリダイレクトされた<br />**BypassProxy**: セッション制御をバイパスされた<br />**encrypt**: 暗号化<br />**decrypt**: 暗号化解除された<br />**verified**: 確認された<br />**encryptionFailed**: 暗号化できなかった<br />**protect**: プロテクト<br />**verify**: ステップアップ認証が必要である<br />**null**: アクショなし |
| device.type | string | eq、neq | デバイスの種類でアクティビティをフィルター処理します。 次の値を指定できます。<br /><br />**DESKTOP**: PC<br />**MOBILE**: Mobile<br />**TABLET**: タブレット<br />**OTHER**: その他<br />**null**: 値なし |
| device.tags | string | eq、neq | デバイス タグ ID でアクティビティをフィルター処理します |
| userAgent.userAgent | string | contains、ncontains | ユーザー エージェントに特定の文字列が含まれるかどうかによってアクティビティをフィルター処理します |
| userAgent.tags | string | eq、neq | 指定したユーザー エージェントタグ ID が含まれるアクティビティをフィルター処理します |
| location.country | string | eq、neq、isset、isnotset | 指定した国番号または地域コードから開始されたアクティビティをフィルター処理します |
| location.organizations | string | eq、neq、isset、isnotset、contains | 指定した組織から開始されたアクティビティをフィルター処理します |
| ip.address | string | eq、startswith、doesnotstartwith、isset、isnotset、neq | 指定した IP アドレスから開始されたアクティビティをフィルター処理します |
| fileSelector | file | eq、neq | 指定したファイルまたはフォルダーが含まれるアクティビティをフィルター処理します |
| office365url | string | startswith、eq、endswith | Office 365 の URL でアクティビティをフィルター処理します |
| fileId | string | eq | ID でファイルを検索します |
| ip.category | integer | eq、neq | 指定したサブネット カテゴリでアクティビティをフィルター処理します。 次の値を指定できます。<br /><br />**1**:企業<br />**2**:管理<br />**3**:危険<br />**4**:VPN<br />**5**:クラウド プロバイダー<br />**6**: その他 |
| ip.tags | string | eq、neq | IP タグ ID でアクティビティをフィルター処理します |
| text | string | eq、startswithsingle、text | フリー テキスト検索を実行してアクティビティをフィルター処理します |
| date | timestamp | lte、gte、range、lte_ndays、gte_ndays | 指定した時間範囲内に発生したアクティビティをフィルター処理します |
| ポリシー | string | eq、neq、isset、isnotset | 指定したポリシーに関連するアクティビティをフィルター処理します |
| ソース | string | eq、neq | ソースの種類またはストリーム ID ですべてのアクティビティをフィルター処理します。 例:`[{ "s:stream-id", "t:source-type" }]` 使用可能なソースの種類の値は次のとおりです。<br /><br />**0**:アクセス制御<br />**1**:セッション制御<br />**2**:アプリ コネクター<br />**3**:アプリ コネクター分析<br />**5**:検出<br />**6**: MDATP |
| activity.alertId | string | eq | アラート ID に関連するすべてのアクティビティをフィルター処理します |
| activityObject | string | eq、neq | 指定した ID が含まれるアクティビティをフィルター処理します |
| fileLabels | string | eq、neq | 指定したファイル ラベル (タグ) ID が含まれるファイルをフィルター処理します |
| created || lte、gte、range、gt、lt、eq | 指定した時間範囲内に作成されたアクティビティをフィルター処理します |
| entity | entity pk | eq、neq、isset、isnotset、startswith | アクティビティを実行したエンティティによってアクティビティをフィルター処理します。 例: `[{ "id": "entity-id", "saas": 11161, "inst": 0 }]` |
| user.username | string | eq、neq、isset、isnotset、startswith | アクティビティを実行したユーザーによってアクティビティをフィルター処理します |
| user.tags | string | eq、neq、isset、isnotset、startswith | 実行しているユーザーに属するタグによってアクティビティをフィルター処理します。 グループ ID が必要です |
| user.domain | string | eq、neq、isset、isnotset | 実行しているユーザー ドメインによってアクティビティをフィルター処理します |

[!INCLUDE [Open support ticket](includes/support.md)]
