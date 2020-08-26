---
title: Microsoft データ分類サービスを使用した Cloud App Security のコンテンツ検査
description: この記事では、Microsoft データ分類サービスを使用して DLP のコンテンツ検査を実行するときに Cloud App Security が従うプロセスについて説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/24/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 18e4aa471a5223234b961e62742f69b2f93d03ae
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88780326"
---
# <a name="microsoft-data-classification-services-integration"></a>Microsoft データ分類サービスの統合

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security では、Microsoft データ分類サービスをネイティブに使用して、クラウド アプリ内のファイルを分類できます。 Microsoft データ分類サービスでは、Office 365、Azure Information Protection、Microsoft Cloud App Security に対して統一された情報保護エクスペリエンスが提供されます。 分類サービスを使用すると、Microsoft Cloud App Security によって保護されているサードパーティのクラウド アプリまでデータ分類作業を拡張し、さらに多くのアプリに対して既に行った決定を利用できます。

>[!NOTE]
> この機能は現在、米国、ヨーロッパ、オーストラリア、インド、カナダ、日本、および APAC で利用できます。

## <a name="enable-content-inspection-with-data-classification-services"></a>データ分類サービスによるコンテンツ検査を有効にする

**Microsoft データ分類サービス**を使用するように **[検査方法]** を設定するオプションがあり、追加の構成は必要ありません。 このオプションは、Microsoft Cloud App Security でファイルのデータ リーク防止ポリシーを作成する場合に便利です。

1. [ファイル ポリシー](data-protection-policies.md)のページの **[検査方法]** で、 **[データ分類サービス]** を選択します。 また、[セッション ポリシー](session-policy-aad.md)のページの **[検査方法]** で、 **[ファイル ダウンロードの制御 (検査を含む)]** を設定することもできます。

    ![データ分類サービスの設定](media/dcs-enable.png)
2. 条件の**いずれか**または**すべて**のどちらが満たされたときに、ポリシーを適用するかを選択します。
3. **[検査の種類を選択]** で、 **[機密性の高い情報の種類]** を選択します。

    ![データ分類サービスの検査の種類の選択](media/dcs-sensitive-information-type.png)

4. [既定の機密性の高い情報の種類](https://support.office.com/article/what-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b)を使用して、Microsoft Cloud App Security によって保護されているファイルに対する処理を定義できます。 また、[Office 365 のカスタム機密情報の種類](https://support.office.com/article/create-a-custom-sensitive-information-type-82c382a5-b6db-44fd-995d-b333b3c7fc30)を再利用することもできます。
    > [!NOTE]
    > [指紋](/microsoft-365/compliance/document-fingerprinting?view=o365-worldwide)、[完全データ一致](/microsoft-365/compliance/create-custom-sensitive-information-types-with-exact-data-match-based-classification)、[トレーニング可能な分類器](/microsoft-365/compliance/classifier-getting-started-with)などの高度な分類の種類を使用するようにポリシーを構成することができます。

5. 必要に応じて、一致の最後の 4 文字をマスク解除できます。 既定では、一致はマスクされてコンテキストで示され、一致の前後の 40 文字が含まれます。 このチェック ボックスをオンにすると、一致自体の最後の 4 文字がマスク解除されます。

6. ファイル ポリシーを利用すると、ポリシーに対してアラートとガバナンス アクションを設定することもできます。 詳細については、[ファイル ポリシー](data-protection-policies.md)と[ガバナンス アクション](governance-actions.md)に関するページを参照してください。 セッション ポリシーを利用すると、ファイルが DCS の種類に一致する場合に、アクションをリアルタイムで監視および制御することもできます。 詳しくは、[セッション ポリシー](session-policy-aad.md)に関するページを参照してください。

これらのポリシーを設定すると、強力な Office 365 DLP の機能を他のすべての承認されたクラウド アプリにまで簡単に拡張し、それらに格納されているデータを、[Azure Information Protection の分類ラベルを自動的に適用する](azip-integration.md)機能や、共有のアクセス許可を制御する機能など、Microsoft Cloud App Security によって提供される完全なツールセットを使用して保護することができます

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
