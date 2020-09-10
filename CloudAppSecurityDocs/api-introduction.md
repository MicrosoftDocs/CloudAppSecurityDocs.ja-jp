---
title: Cloud App Security REST API
description: この記事では、HTTPS を使用して Cloud App Security を操作する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 31190fd4df5dc9c3bac19794ff1fd78c4982100d
ms.sourcegitcommit: 5ace3437d49c7bbde2266a6f1565a65a379b9c2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2020
ms.locfileid: "89499494"
---
# <a name="cloud-app-security-rest-api"></a>Cloud App Security REST API

*適用対象:Microsoft Cloud App Security*

この記事では、HTTPS を使用して Cloud App Security を操作する方法について説明します。

Microsoft Cloud App Security API を使用すると、REST API エンドポイントを介して、プログラムで Cloud App Security にアクセスできます。 アプリケーションでは、API を使用して、Cloud App Security のデータとオブジェクトに対する読み取りと更新の操作を実行できます。 たとえば、Cloud App Security API では、ユーザー オブジェクトに対する次の一般的な操作がサポートされています。

- Cloud Discovery にログ ファイルをアップロードする
- ブロック スクリプトを生成する
- アクティビティとアラートの一覧を取得する
- アラートを無視または解決する

## <a name="api-url-structure"></a>API URL 構造

Cloud App Security API を使用するには、最初にテナントから API の URL を取得する必要があります。 API の URL では、次の形式が使用されます: `https://<portal_url>/api/<endpoint>`。

テナントに対する Cloud App Security ポータルの URL を取得するには、次の手順のようにします。

1. Cloud App Security ポータルで、メニュー バーの**疑問符アイコン**をクリックします。 次に、 **[バージョン情報]** を選択します。

    ![[バージョン情報] をクリックする](media/about-menu.png)

1. Cloud App Security のバージョン情報画面で、ポータルの URL を確認できます。

    ![データ センターを表示する](media/api-url.png)

ポータルの URL がわかったら、それに `/api` サフィックスを追加して API の URL を取得します。 たとえば、ポータルの URL が `https://mytenant.us2.contoso.com` である場合、API の URL は `https://mytenant.us2.contoso.com/api` になります。

## <a name="api-tokens"></a>API トークン

Cloud App Security では、サーバーへのすべての API 要求のヘッダーで、API トークンを指定する必要があります。次に例を示します。

```http
Authorization: Token <your_token_key>
```

`<your_token_key>` は個人の API トークンです。

API トークンの詳細については、「[API トークンの管理](api-authentication.md)」を参照してください。

### <a name="example"></a>例

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/example-endpoint"
```

## <a name="what-actions-are-supported"></a>サポートされているアクション

次の表では、サポートされているアクションについて説明します。

|リソース|HTTP 動詞|URI ルート|
|---|---|---|
|検出|GET、POST、PUT|/api/v1/discovery/|
|データ エンリッチメント|POST|/api/subnet/|
|アクティビティ|GET、POST|/api/v1/activities/|
|アラート|GET、POST|/api/v1/alerts/|
|エンティティ|GET、POST|/api/v1/entities/|
|ファイル|GET、POST|/api/v1/files/|

「**リソース**」は、関連エンティティのグループを表します。

## <a name="what-field-types-are-supported"></a>サポートされているフィールドの型

次の表では、サポートされているフィールドの型について説明します。

|フィールド|[説明]|
|---|---|
|string|テキスト文字列|
|boolean|true または false を表すブール値|
|integer|32 ビット符号付き整数|
|timestamp|エポックからのミリ秒数|

## <a name="limits"></a>制限

要求で limit パラメーターを指定することにより、要求を制限することができます。

サポートされている limit パラメーターの指定方法は次のとおりです。

- URL エンコード (`Content-Type: application/x-www-form-urlencoded` ヘッダーで)
- フォーム データ
- JSON 本文 (`Content-Type: multipart/form-data` および適切な境界ヘッダーで)

> [!NOTE]
>
> - 制限を指定しない場合、既定で 100 に設定されます。
> - その API トークンを使用して行われるすべての要求に対する応答は、最大 100 項目に制限されます。
> - すべての API 要求のスロットル制限は、テナントごとに 1 分あたり 30 回の要求です。

## <a name="filters"></a>フィルタ

多数の結果がある場合、フィルターを使用して要求を微調整すると便利です。 このセクションでは、フィルターの構造と、フィルターで使用できる演算子について説明します。

### <a name="structure"></a>構造

一部の API エンドポイントでは、クエリを実行するときにフィルターがサポートされています。 それらに関連するセクションには、使用可能なすべてのフィルター可能なフィールドと、そのリソースに対してサポートされている演算子の一覧が記載されています。

ほとんどのフィルターでは、強力なクエリを提供するために複数の値がサポートされています。 フィルターと演算子を組み合わせるとき、フィルター間の論理演算子としては AND を使用します。

### <a name="example"></a>例

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/example-endpoint" -d '{
  "filters": {
    "some.field": {
      "eq": ["value1", "value2"],
      "isset": true
    },
    "some.field2": {
      "gte": 5
    }
  },
  "skip": 5,
  "limit": 10
}'
```

### <a name="operators"></a>演算子

> [!NOTE]
> すべての演算子がすべてのフィルターと互換性があるわけではありません。

次の表では、サポートされている演算子について説明します。

| 演算子 | 応答の種類 | [説明] |
| --- | --- | --- |
| 次の値を含む | 文字列のリスト | 指定した文字列のいずれかが含まれる関連レコードがすべて返されます |
| deq | 値のリスト | 指定した値のいずれとも等しくない値が含まれるレコードがすべて返されます |
| descendantof | 値のリスト | 指定した値またはその子孫に一致する関連レコードがすべて返されます |
| doesnotstartwith | 文字列のリスト | 指定した文字列のいずれでも始まっていない関連レコードがすべて返されます |
| endswith | 文字列のリスト | 指定した文字列のいずれかで終わっている関連レコードがすべて返されます |
| eq | 値のリスト | 指定した値のいずれかが含まれる関連レコードがすべて返されます |
| gt | 単一の値 | 指定した値より大きい値が含まれるレコードがすべて返されます |
| gte | 単一の値 | 指定した値と等しいか、それより大きい値が含まれるレコードがすべて返されます |
| gte_ndays | 数値 | N 日前より後の日付を持つレコードがすべて返されます |
| isnotset | boolean | "true" に設定すると、指定したフィールドに値が含まれない関連レコードがすべて返されます |
| isset | boolean | "true" に設定すると、指定したフィールドに値が含まる関連レコードがすべて返されます |
| lt | 単一の値 | 指定した値より小さい値が含まれるレコードがすべて返されます |
| lte | 単一の値 | 指定した値と等しいか、それより小さい値が含まれるレコードがすべて返されます |
| lte_ndays | 数値 | N 日前より前の日付を持つレコードがすべて返されます |
| ncontains | 文字列のリスト | 指定したどの文字列も含まれない関連レコードがすべて返されます |
| ndescendantof | 値のリスト | 指定した値またはその子孫に一致しない関連レコードがすべて返されます |
| neq | 値のリスト | 指定したどの値も含まれない関連レコードがすべて返されます |
| range | "開始" フィールドと "終了" フィールドが含まれるオブジェクトのリスト | 指定したいずれかの範囲内のレコードがすべて返されます |
| startswith | 文字列のリスト | 指定した文字列のいずれかで始まっている関連レコードがすべて返されます |
| startswithsingle | string | 指定した文字列で始まっている関連レコードがすべて返されます |
| text | string | すべてのレコードのフルテキスト検索を実行します |

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [API の認証](api-authentication.md)

[!INCLUDE [Open support ticket](includes/support.md)]
