---
title: Cloud App Security Entities API
description: この記事では、Entities API の使用方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 9b6d7c4428b8383a4107a824a6113fcd3362dfa1
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881103"
---
# <a name="entities-api"></a>Entities API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
> この API は、Office 365 Cloud App Security では使用できません。

Entities API を使用すると、組織のクラウド アプリを使用するユーザーとアカウントに関する基本情報を取得し、サービスの使用パターンを把握できます。

サポートされている要求は次のとおりです。

- [エンティティの一覧表示](api-entities-list.md)
- [エンティティのフェッチ](api-entities-fetch.md)
- [エンティティ ツリーのフェッチ](api-entities-fetch-tree.md)

## <a name="filters"></a>フィルタ

フィルターの動作の詳細については、「[フィルター](api-introduction.md#filters)」を参照してください。

次の表では、サポートされているフィルターについて説明します。

| フィルター | Type | 演算子 | [説明] |
| --- | --- | --- | --- |
| type| string | eq、neq | 型でエンティティをフィルター処理します |
| isAdmin | string | eq | 管理者であるエンティティをフィルター処理します |
| entity | entity pk | eq、neq | 特定のエンティティの pk を含むエンティティをフィルター処理します。 ユーザーが選択されている場合は、そのすべてのアカウントも返されます。 例: `[{ "id": "entity-id", "saas": 11161, "inst": 0 }]` |
| userGroups |string | eq、neq | 関連付けられているグループ ID でエンティティをフィルター処理します |
| app | integer | eq、neq | 指定した SaaS ID を持つサービスを使用してエンティティをフィルター処理します。次に例を示します。11770 |
| インスタンス | integer | eq、neq | 指定した SaaS ID のサービスを使用してエンティティをフィルター処理します。次に例を示します。11770、1059065 |
| isExternal | boolean | eq | エンティティの所属。 次の値を指定できます。<br /><br />**true**:外部<br />**false**:内部<br />**null**:値なし |
| domain | string | eq、neq、isset、isnotset | エンティティの関連ドメイン |
| organization | string | eq、neq、isset、isnotset | 指定した組織単位でエンティティをフィルター処理します |
| lastSeen | timestamp | lte、gte、 | 指定した日付の間で最後に見つかったエンティティを範囲フィルター処理します |
| 状態 | string | eq、neq | 状態でエンティティをフィルター処理します。 次の値を指定できます。<br /><br />**0**:該当なし<br />**1**:ステージング中<br />**2**:Active<br />**3**:Suspended<br />**4**:削除済み |
| score | integer | lt、gt、isset、isnotset | エンティティを調査の優先順位スコアでフィルター処理する |

[!INCLUDE [Open support ticket](includes/support.md)]
