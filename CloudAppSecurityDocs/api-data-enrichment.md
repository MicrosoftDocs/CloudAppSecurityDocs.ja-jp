---
title: Cloud App Security の Data Enrichment API
description: この記事では、Data Enrichment API の使用方法について説明します。
ms.date: 12/13/2020
ms.topic: reference
ms.openlocfilehash: 814f4e038c129576377aea9fe5e7c3e74a4b09d1
ms.sourcegitcommit: 90df07ce9cd64fd9c46fb6563f0249079204e174
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97859015"
---
# <a name="data-enrichment-api"></a>Data Enrichment API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Data Enrichment API を使用すると、物理的なオフィスの IP アドレスなど、識別可能な IP アドレス範囲を作成できます。 IP アドレス範囲を使用すると、ログとアラートの表示と調査の方法をタグ付けして分類し、カスタマイズすることができます。 詳細については、「[IP 範囲とタグの使用](ip-tags.md)」を参照してください。

サポートされている要求は次のとおりです。

- [IP アドレス範囲の一覧表示](api-data-enrichment-list.md)
- [IP アドレス範囲の作成](api-data-enrichment-create.md)
- [IP アドレス範囲の更新](api-data-enrichment-update.md)
- [IP アドレス範囲の削除](api-data-enrichment-delete.md)

## <a name="properties"></a>Properties

応答オブジェクトでは、次のプロパティが定義されています。

| プロパティ | Type | 説明 |
| --- | --- | --- |
| total | INT | レコードの総数 |
| hasNext | [bool] | 追加のレコードがあるかどうかを示します |
| data | list | 既存のレコードの一覧 |
| _id | string | IP 範囲の一意の ID |
| name | string | 範囲の一意の名前 |
| サブネット | list | マスク、IP アドレス (IPv4/IPv6)、元の文字列の配列 |
| location | string | 場所の名前、緯度、経度、国番号、国名が格納されているオブジェクト |
| organization | string | 登録された ISP |
| tags| list | タグ名、ID、説明、名前テンプレート、テナント ID が格納されている、新規または既存のオブジェクトの配列 |
| category | INT | IP 範囲のカテゴリ。 カテゴリを指定すると、対象の IP アドレスからのアクティビティを簡単に識別できます。 次の値を指定できます。<br /><br />**1**:企業<br />**2**:管理<br />**3**:危険<br />**4**:VPN<br />**5**:クラウド プロバイダー<br />**6**: その他 |
| lastModified | long | 最後に変更されたルールのタイムスタンプ |

## <a name="filters"></a>フィルタ

フィルターの動作の詳細については、「[フィルター](api-introduction.md#filters)」を参照してください。

次の表では、サポートされているフィルターについて説明します。

| フィルター | Type | 演算子 | 説明 |
| --- | --- | --- | --- |
| category | integer | eq、neq | IP 範囲をカテゴリでフィルター処理します。 次の値を指定できます。<br /><br />**1**:企業<br />**2**:管理<br />**3**:危険<br />**4**:VPN<br />**5**:クラウド プロバイダー<br />**6**: その他 |
| tags | string | eq、neq | IP 範囲をタグ ID でフィルター処理します |
| builtIn | [bool] | eq | IP 範囲を種類でフィルター処理します。 次の値を指定できます: **true** (組み込み) または **false** (カスタム) |

[!INCLUDE [Open support ticket](includes/support.md)]
