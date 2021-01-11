---
title: API を使用したアクティビティの調査
description: この記事では、ユーザーのアクティビティを Cloud App Security で API を使用して調査する方法について説明します。
ms.date: 12/22/2020
ms.topic: how-to
ms.openlocfilehash: 799e248ed69626b301d9281c43c14053b6ff03cf
ms.sourcegitcommit: 90df07ce9cd64fd9c46fb6563f0249079204e174
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97859065"
---
# <a name="investigate-activities-using-the-api"></a>API を使用したアクティビティの調査

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Activities API を使用すると、接続されたクラウド アプリでユーザーが実行したアクティビティを調査できます。

アクティビティ API モードは、大量のデータ (5,000 を超えるアクティビティ) をスキャンおよび取得できるよう最適化されています。 この API スキャンでは、すべての結果がスキャンされるまで、アクティビティ データが繰り返し照会されます。

> [!NOTE]
> 大量のアクティビティや大規模の展開では、[SIEM エージェント](siem.md)をアクティビティのスキャンに使用することをお勧めします。

## <a name="to-use-the-activity-scan-script"></a>アクティビティ スキャン スクリプトを使用するには

1. お使いのデータに対してクエリを実行します。
1. 1 回のスキャンで列挙できる以上のレコードがある場合、実行する必要のある return コマンドと `nextQueryFilters` を受け取ります。 このコマンドは、クエリによってすべての結果が返されるまで、スキャンするたびに受け取ります。

## <a name="request-body-parameters"></a>要求本文のパラメーター

- "filters":要求のすべての検索フィルターでオブジェクトをフィルターします。詳細については、[アクティビティ フィルター](activity-filters-queries.md)に関するページを参照してください。 お使いの要求がスロットルしないようにするには、最終日のアクティビティを照会するようにしたり、特定のアプリをフィルター処理するようにしたりするなど、お使いのクエリに必ず制限を追加するようにしてください。
- "isScan":ブール型。 スキャン モードを有効にします。
- "sortDirection":並べ替えの方向。可能な値は、“asc” と “desc” です。
- "sortField":アクティビティの並べ替えに使用するフィールド。 指定できる値は次のとおりです。
  - date - アクティビティの発生日 (これが既定です)。
  - created - アクティビティを保存したときのタイムスタンプ。
- "limit":整数。 スキャン モードでは、500 から 5000 (既定値は 500) の間になります。 すべてのデータをスキャンする反復処理の回数を制御します。

## <a name="response-parameters"></a>応答パラメーター

- "data": 返されるデータ。 各回の反復処理のレコード数は "limit"の数までとなります。 プルするレコードが多い場合 (hasNext = true)、すべてのデータが 1 回のみ列挙されるように、最後のいくつかのレコードが削除されます。
- "hasNext":ブール型。 データに対しさらに反復処理が必要かどうかを示します。
- "nextQueryFilters":さらに反復処理が必要な場合は、実行する連続する JSON クエリが含まれます。 次の要求では、これが "filters" パラメーターとして使用されます。

次の Python の例では、Exchange Online の過去 1 日のすべてのアクティビティを取得します。

``` python
import requests
import json
ACTIVITIES_URL = 'https://<your_tenant>.<tenant_region>.contoso.com/api/v1/activities/'

your_token = '<your_token>'
headers = {
'Authorization': 'Token {}'.format(your_token),
}

filters = {
  # optionally, edit to match your filters
  'date': {'gte_ndays': 1},
  'service': {'eq': [20893]}
}
request_data = {
  'filters': filters,
  'isScan': True
}

records = []
has_next = True
while has_next:
    content = json.loads(requests.post(ACTIVITIES_URL, json=request_data, headers=headers).content)
    response_data = content.get('data', [])
    records += response_data
    print('Got {} more records'.format(len(response_data)))
    has_next = content.get('hasNext', False)
    request_data['filters'] = content.get('nextQueryFilters')

print('Got {} records in total'.format(len(records)))
```

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
