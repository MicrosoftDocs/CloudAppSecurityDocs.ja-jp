---
title: Cloud App Security で Microsoft データ分類サービスを使用してコンテンツ検査を実行する方法 | Microsoft Docs
description: この記事では、Microsoft データ分類サービスを使用して DLP コンテンツ検査を実行する場合に Microsoft Cloud App Security が従うプロセスについて説明します。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/1/2018
ms.topic: article
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.assetid: bf25d1e6-e5dc-449f-b50e-1cd4a21b6d3d
ms.reviewer: reutam
ms.suite: ems
ms.openlocfilehash: a1a9455681106c066888cf29c83971914e35babb
ms.sourcegitcommit: 9d2a34a2d4145b39d855dd6f596c0fc858b92f9b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37340007"
---
*適用対象: Microsoft Cloud App Security*



# <a name="microsoft-data-classification-services-integration"></a>Microsoft データ分類サービスの統合

Microsoft Cloud App Security を使用すると、Microsoft データ分類サービスをネイティブに利用してクラウド アプリのファイルを分類できます。
Microsoft データ分類サービスには、Office 365、Azure Information Protection、および Microsoft Cloud App Security の間での、統合された情報保護エクスペリエンスが用意されています。また、Microsoft Cloud App Security によって保護されているサード パーティのクラウド アプリにデータ分類を拡張できます。これにより、さらに多くのアプリ間で既存の決定事項を活用できます。

>[!NOTE]
> この機能は現在、米国とヨーロッパ (フランスを除く) でのみ利用できます。

追加構成なしで、Microsoft Cloud App Security のファイルに対するデータ漏えい保護のポリシーを作成するときに、**[Microsoft データ分類サービス]** を使用する **[検査方法]** を自動的に選択できるようになります。

![データ分類サービスの設定](./media/dcs-enable.png)

データ分類サービスを使用するコンテンツ検査を有効にするには、次の操作を行います。

1. [[ファイル ポリシー]](data-protection-policies.md) ページで、**[検査方法]** の下で **[データ分類サービス]** を選択します。
2. ポリシーを適用するタイミングについて、条件が **1 つ以上**満たされた場合、または**すべて**満たされた場合のいずれかを選択します。
3. 機密情報の種類を選択して、コンテンツ検査の種類を選択します。
 ![データ分類サービスの設定](./media/dcs-sensitive-information-type.png)

5. [既定の機密情報の種類](https://support.office.com/article/what-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b)に加えて、Office 365 で作成した[カスタムの機密情報の種類](https://support.office.com/article/create-a-custom-sensitive-information-type-82c382a5-b6db-44fd-995d-b333b3c7fc30)を使用できます (これは正規表現、キーワード、大規模ディクショナリを使用した複雑なパターンをサポートします)。また、それらを再利用して Microsoft Cloud App Security に保護されているファイルへの操作を定義できます。

6. 必要に応じて、一致の最後の 4 文字のマスクを解除できます。 既定では、マスクされた一致がコンテキストの中で示され、一致の前後の 40 文字が含まれます。 このチェック ボックスをオンにした場合、一致自体の最後の 4 文字のマスクが解除されます。

7. また、ポリシーのためにアラートとガバナンス アクションを設定することもできます。 詳細については、[ファイル ポリシー](data-protection-policies.md)と[ガバナンス アクション](governance-actions.md)に関するページをご覧ください。

Microsoft Cloud App Security でポリシーを設定すると、その他の承認されたクラウド アプリすべてに Office 365 DLP 機能の長所を簡単に拡張できます。また、Microsoft Cloud App Security によって提供されるツールセット (たとえば、[Azure Information Protection 分類ラベルを自動的に適用する](azip-integration.md)機能や、共有アクセス許可を制御する機能) をフルに使用して、アプリに保存されているデータを保護できます。



## <a name="see-also"></a>参照  
[ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)   

[Premier サポートをご利用のお客様は、Premier ポータルから直接 Cloud App Security を選択することもできます。](https://premier.microsoft.com/)  
  