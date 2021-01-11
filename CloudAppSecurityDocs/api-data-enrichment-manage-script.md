---
title: API を使用して IP アドレス範囲を管理する
description: この記事では、API を使用して Cloud App Security の IP アドレス範囲を管理する方法について説明します。
ms.date: 01/04/2021
ms.topic: how-to
ms.openlocfilehash: 4351649e023128cbb7635c366e3ab5449956c144
ms.sourcegitcommit: 90df07ce9cd64fd9c46fb6563f0249079204e174
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97859068"
---
# <a name="manage-ip-address-ranges-using-the-api"></a>API を使用して IP アドレス範囲を管理する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Data Enrichment API を使用して、IP アドレスの範囲を管理できます。

## <a name="to-use-the-manage-ip-address-ranges-script"></a>IP アドレス範囲管理スクリプトを使用するには

1. 次の必要なフィールドを含む CSV ファイルを作成します: Name、IP_Address_Ranges、Category、Tag(id)、Override_ISP_Name。

1. 次のスクリプト変数の値を更新します: **OPTION_DELETE_ENABLED**、**IP_RANGES_BASE_URL**、**CSV_ABSOLUTE_PATH**、**YOUR_TOKEN**

    > [!IMPORTANT]
    > **OPTION_DELETE_ENABLED** を **True** に設定した場合、テナントでは定義されていて CSV ファイルには存在しない IP アドレス範囲が、スクリプトによってテナントから削除されます。 このオプションを使用する場合は、テナントに必要なすべての IP アドレス範囲が CSV ファイルで定義されていることを確認してください。

1. スクリプトを実行して、新しいレコードを作成し、名前が一致する既存のルールを更新します。

## <a name="request-body-parameters"></a>要求本文のパラメーター

- "filters":要求のすべての検索フィルターでオブジェクトをフィルターします。詳細については、[Data Enrichment のフィルター](api-data-enrichment.md#filters)に関するページを参照してください。 要求が調整されないようにするには、クエリに制限を含めてください。
- "limit":整数。 スキャン モードでは、500 から 5000 (既定値は 500) の間になります。 すべてのデータをスキャンする反復処理の回数を制御します。

## <a name="response-parameters"></a>応答パラメーター

- "data": 返されるデータ。 各回の反復処理のレコード数は "limit"の数までとなります。 プルするレコードが多い場合 (hasNext = true)、すべてのデータが 1 回のみ列挙されるように、最後のいくつかのレコードが削除されます。
- "hasNext":ブール型。 データに対しさらに反復処理が必要かどうかを示します。
- "nextQueryFilters":さらに反復処理が必要な場合は、実行する連続する JSON クエリが含まれます。 次の要求では、これが "filters" パラメーターとして使用されます。

次の Python の例では、CSV ファイルの内容を使用して、Cloud App Security 環境の IP アドレス範囲を管理 (作成、更新、または削除) しています。

```python
import csv
import requests
import json

OPTION_DELETE_ENABLED = False
IP_RANGES_BASE_URL = 'https://<tenant_id>.<tenant_region>.contoso.com/api/v1/subnet/'
IP_RANGES_UPDATE_SUFFIX = 'update_rule/'
IP_RANGES_CREATE_SUFFIX = 'create_rule/'
CSV_ABSOLUTE_PATH = 'rules.csv'
YOUR_TOKEN = '<your_token>'
HEADERS = {
  'Authorization': 'Token {}'.format(YOUR_TOKEN),
}

# Get all records.
def get_records():
  list_request_data = {
    # Optionally, edit to match your filters
    'filters': {},
    "skip": 0,
    "limit": 20
  }
  records = []
  has_next = True
  while has_next:
    content = json.loads(requests.post(IP_RANGES_BASE_URL, json=list_request_data, headers=HEADERS).content)
    response_data = content.get('data', [])
    records += response_data
    has_next = content.get('hasNext', False)
    list_request_data["skip"] += len(response_data)
  return records

# Rule fields are compared to the CSV row.
def rule_matching(record, ip_address_ranges, category, tag, isp_name, ):
  rule_exists_conditions = [sorted([subnet.get('originalString', False) for subnet in record.get('subnets', [])]) !=
                            sorted(ip_address_ranges.split(' ')),
                            str(record.get('category', False)) != category,
                            len(record.get('tags', [])) != len(tag.split(' ')) and
                            (len(record.get('tags', [])) != 0 and len(tag) == 1),
                            bool(record.get('organization', False)) != bool(isp_name) or
                            (record.get('organization', False) is not None and not isp_name)]
  if any(rule_exists_conditions):
    return False
  for tag in record.get('tags', []):
    tag_id = tag.get('id')
    if tag_id and tag_id not in tag.split(' '):
      return False
  return True

def create_update_rule(name, ip_address_ranges, category, tag, isp_name, records, request_data):
  for record in records:
    # Records are compared by name(unique).
    # This can be changed to id (to update the name), it will include adding id to the CSV and changing row shape.
    if record["name"] == name:
      # request_data["_tid"] = record["_tid"]
      if not rule_matching(record, ip_address_ranges, category, tag, isp_name):
        # Update existing rule
        json.loads(
          requests.post(f"{IP_RANGES_BASE_URL}{record['_id']}/{IP_RANGES_UPDATE_SUFFIX}", json=request_data, headers=HEADERS).content)
        return record
      else:
        # The exact same rule exists. no need for change.
        return record
  # Create new rule.
  requests.post(f"{IP_RANGES_BASE_URL}{IP_RANGES_CREATE_SUFFIX}", json=request_data, headers=HEADERS)

# Request data creation.
def create_request_data(name, ip_address_ranges, category, tag, isp_name):
  request_data = {"name": name, "subnets": ip_address_ranges.split(' '), "category": category,
                  "tags": tag.split(' ') if tag else ''}
  if isp_name:
    request_data["overrideOrganization"] = True
    request_data["organization"] = isp_name
  return request_data

def main():
  # CSV fields are: Name,IP_Address_Ranges,Category,Tag(id),Override_ISP_Name
  # Multiple values (eg: multiple subnets) will be space-separated. (eg: value1 value2)
  records = get_records()
  with open(CSV_ABSOLUTE_PATH, newline='\n') as your_file:
    reader = csv.reader(your_file, delimiter=',')
    for row in reader:
      name, ip_address_ranges, category, tag, isp_name = row
      request_data = create_request_data(name, ip_address_ranges, category, tag, isp_name)
      if records:
        # Existing records were retrieved from your tenant
        record = create_update_rule(name, ip_address_ranges, category, tag, isp_name, records, request_data)
        record_id = record['_id']
      else:
        # No existing records were retrieved from your tenant
        record_id = json.loads(requests.post(f"{IP_RANGES_BASE_URL}{IP_RANGES_CREATE_SUFFIX}", json=request_data, headers=HEADERS).content)
      if OPTION_DELETE_ENABLED:
        # Remove CSV file record from tenant records.
        if record_id:
          for record in records:
            if record['_id'] == record_id:
              records.remove(record)
  if OPTION_DELETE_ENABLED:
    # Delete remaining tenant records, i.e. records that aren't in the CSV file.
    for record in records:
      requests.delete(f"{IP_RANGES_BASE_URL}{record['_id']}/", headers=HEADERS)
  
if __name__ == '__main__':
  main()
```

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
