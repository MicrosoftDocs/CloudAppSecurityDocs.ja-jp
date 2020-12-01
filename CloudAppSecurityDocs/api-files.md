---
title: Cloud App Security Files API
description: この記事では、Files API の使用方法について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: c6aa36fcf011bfe6c33e01435d8807879ba6184c
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96313969"
---
# <a name="files-api"></a>Files API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
>
> - この API はまもなく非推奨になります。 Microsoft Cloud App Security により、ポリシーに違反するファイルを識別して対処するための新しいソリューションが開発されています。
> - この API は、Office 365 Cloud App Security では使用できません。

Files API を使用すると、クラウド アプリに格納されているファイルやフォルダーに関するメタデータ (最終更新日、所有権など) を取得できます。

サポートされている要求は次のとおりです。

- [ファイルの一覧表示](api-files-list.md)
- [ファイルのフェッチ](api-files-fetch.md)

## <a name="filters"></a>フィルタ

フィルターの動作の詳細については、「[フィルター](api-introduction.md#filters)」を参照してください。

次の表では、サポートされているフィルターについて説明します。

| フィルター | Type | 演算子 | [説明] |
| --- | --- | --- | --- |
| サービス | integer | eq、neq | 指定したアプリ appID からファイルをフィルター処理します。次に例を示します。11770 |
| インスタンス | integer | eq、neq | 指定したインスタンスのファイルをフィルター処理します |
| fileType | integer | eq、neq | 指定したファイルの種類のファイルをフィルター処理します。 次の値を指定できます。<br /><br />**0**:その他<br />**1**:マニュアル名の正式名称<br />**2**:スプレッドシート<br />**3**:Presentation<br />**4**:テキスト<br />**5**:画像<br />**6**:フォルダー |
| allowDeleted | boolean | eq | 次の値を指定できます。<br /><br />**true**:削除されたファイルを返します<br />**false** または未設定:削除されていない (ごみ箱の中を含む) ファイルを返します。 これは trashed 演算子によってオーバーライドされます |
| ポリシー | string | cabinetmatchedrulesequals、neq、isset、isnotset | 指定したポリシーに関連するアクティビティをフィルター処理します |
| filename | string | eq | ファイル名でファイルをフィルター処理します |
| modifiedDate | timestamp | lte、gte、range、lte_ndays、gte_ndays | 最終更新日でファイルをフィルター処理します |
| createdDate | timestamp | lte、gte、range | 作成日でファイルをフィルター処理します |
| collaborators.entity | entity pk | eq、neq | 指定したエンティティと共有されているファイルをフィルター処理します。 例: `[{ "id": "entity-id", "saas": 11161, "inst": 0 }]` |
| collaborators.domains | string | eq、neq | 指定したドメインと共有されているファイルをフィルター処理します |
| collaborators.groups | string | eq、neq | 指定したグループと共有されているファイルをフィルター処理します |
| collaborators.withDomain | string | eq、neq、deq | 指定したドメインと共有されているファイルをフィルター処理します |
| owner.entity | entity pk | eq、neq | 指定したエンティティが所有するファイルをフィルター処理します。 例: `[{ "id": "entity-id", "saas": 11161, "inst": 0 }]` |
| owner.orgUnit | string | eq、neq | 指定した組織単位の所有者を持つファイルをフィルター処理します |
| sharing | integer | eq、neq | 指定した共有レベルを持つファイルをフィルター処理します。 次の値を指定できます。<br /><br />**4**:公開 (インターネット)<br />**3**:パブリック<br />**2**:外部<br />**1**:内部<br />**0**:プライベート |
| fileId | string | eq、neq | ファイル ID でファイルをフィルター処理します |
| fileLabels | string | eq、neq、isset、isnotset | 指定したファイル ラベル (タグ) ID が含まれるファイルをフィルター処理します |
| fileScanLabels | string | eq、neq、isset、isnotset | 指定したコンテンツ検査警告 (タグ) ID を含むファイルをフィルター処理します |
| extension | string | eq、neq | 指定したファイル拡張子でファイルをフィルター処理します |
| mimeType | string | eq、neq | 特定の MIME タイプでファイルをフィルター処理します。1 つの文字列である必要があります |
| trashed | boolean | eq | 次の値を指定できます。<br /><br />**true**:ごみ箱の中のファイルのみを返します<br />**false**:ごみ箱に入っていないファイルを返します |
| parentFolder | folder | eq、neq | 指定したフォルダーに含まれるファイルをフィルター処理します |
| folder | boolean | eq | 次の値を指定できます。<br /><br />**true**:フォルダーのみを返します<br >**false**:ファイルのみを返します |
| quarantined | boolean | eq | 次の値を指定できます。<br /><br />**true**:検疫済みのファイルのみを返します<br />**false**:検疫されていないファイルのみを返します |
| snapshotLastModifiedDate | timestamp | lte、gte、range | ファイルをスナップショットの最終変更日でフィルター処理します |

[!INCLUDE [Open support ticket](includes/support.md)]
