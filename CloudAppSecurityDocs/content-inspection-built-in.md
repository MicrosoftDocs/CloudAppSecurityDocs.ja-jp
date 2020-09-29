---
title: Cloud App Security で組み込みの DLP コンテンツの検査が実行される方法
description: この記事では、Microsoft Cloud App Security によりクラウド内のデータに対して組み込みの DLP コンテンツ検査が実行されるときのプロセスについて説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 57cb12ae47b153dfd637bd568a2e6e447d264cf5
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881240"
---
# <a name="built-in-content-inspection"></a>組み込みのコンテンツ検査

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、Microsoft Cloud App Security によりクラウド内のデータに対して組み込みの DLP コンテンツ検査が実行されるときのプロセスについて説明します。

Cloud App Security のコンテンツ検査は次のように機能します。

1. まず、Cloud App Security により、新規であるか変更されたと検出されたドライブおよびイベントの準リアルタイム (NRT) スキャンが実行されます。
2. そのスキャンが完了した後、Cloud App Security により、すべてのドライブ内のすべての関連ファイルの継続的なスキャンが実行されます。

NRT スキャンのファイルと継続的スキャンのファイルはどちらも、検査のためにキューに追加されます。 スキャン キューのファイルの順序は、ファイルに対するアクティビティごとに、またドライブのスキャン時に設定されます。 ファイルがスキャンされるのは、サポートされている MIME タイプであることをファイルのメタデータが示している場合だけです。 このスキャンは、データ スキャンに関連するファイル (ドキュメント、画像、プレゼンテーション、スプレッドシート、テキスト、zip/アーカイブ ファイル) が対象となります。

ファイルがスキャンされた後、次のアクションが発生します。

1. メタデータに関連し、コンテンツ自体には関連しないすべてのカスタム ポリシーが Cloud App Security によって適用されます。 たとえば、ファイルが 20 MB より大きいときに警告するポリシーや、docx ファイルを OneDrive に保存したときに警告するポリシーなどです。

2. コンテンツの検査を要求するポリシーがあり、ファイルがコンテンツ検査の条件を満たしている場合、コンテンツは検査のためにキューに入れられます。 キューの長さは、テナントのサイズと、スキャンが必要なファイルの数によって異なります。

3. この時点で、 **[調査]**  >  **[ファイル]** に移動してファイルをクリックすると、コンテンツ検査の状態を表示できます。 ファイル ドロワーが開いてファイルの詳細が表示され、 **[Content Inspection status]\(コンテンツ検査の状態\)** には **[完了]** 、 **[保留中]** 、 **[該当なし]** (ファイルの種類がサポートされていない場合)、失敗メッセージのいずれかが表示されます。 コンテンツのスキャン失敗メッセージについては、「[コンテンツ検査のトラブルシューティング](troubleshooting-content-inspection.md)」を参照してください。

> [!NOTE]
> スキャンの状態にダッシュが表示されている場合は、そのファイルがスキャンの対象としてキューに登録されていないことを意味します。 コンテンツ検査ポリシーの設定の詳細については、「[ファイル ポリシー](data-protection-policies.md)」を参照してください。

組み込みのコンテンツ検査スキャン ポリシーは、次の項目を検索できます。

- メール アドレス
- クレジット カード番号
  - すべてのクレジット カード会社 (Visa、MasterCard、American Express、Diners Club、Discover、JCB、Dankort、UnionPay)
  - 区切り記号 - スペース、ドット、またはダッシュ
  - このスキャンには Luhn 検証も含まれます。
- SWIFT コード
- 国際パスポート番号
- 運転免許証番号
- 日付
- 銀行 ABA ルーティング トランジット ナンバー
- 銀行識別コード
- HIPAA HICN 健康保険請求番号
- HIPAA NPI 米国のプロバイダー ID 番号
- PHI フル ネームと誕生日
- カリフォルニア ID または運転免許証番号
- 運転免許証番号
- 自宅住所
- パスポート カード
- 社会保障番号

## <a name="supported-languages"></a>サポートされる言語

Cloud App Security のコンテンツ検査エンジンは:

- すべての Unicode 文字をサポートします。
- 100 を超えるファイルの種類に対応します。
- 複数の言語、特に、Unicode 文字セットを使用するファイルがサポートされています。 必ず、これらの言語を考慮に入れたポリシーを定義してください。 たとえば、キーワードを探している場合、使用する言語を横断してキーワードを含める必要があります。
- Unicode 以外のエンコードを使用するテキスト ベースのファイルの種類 (中国語 GB2312 など) では、Unicode の中国語キーワードとの比較は期待どおりに機能しません。
- サード パーティのライブラリに依存するファイルの種類の場合、一致する文字列と単語が常に期待どおりに機能するとは限りません。 これは、言語および文字セットの Java 文字列を返すサード パーティのライブラリにコンテンツの検査が依存しているファイル (バイナリのファイルの種類など) で最も一般的です。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
