---
title: コンテンツ検査エラーのトラブルシューティング - Cloud App Security | Microsoft Docs
description: この記事では、コンテンツ検査の状態とその意味の一覧を示します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/25/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 3831d576d3ead9164924557a8b097b78f39808cf
ms.sourcegitcommit: 7b6124e5ecb3fa8fc1176d89e06b052f2a53a310
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83854213"
---
# <a name="troubleshooting-content-inspection"></a>コンテンツ検査のトラブルシューティング

*適用対象:Microsoft Cloud App Security*

この記事では、コンテンツ検査の状態とその意味の一覧を示します。

## <a name="content-inspection-status"></a>コンテンツ検査の状態

この表には、各コンテンツ検査の状態とその説明が示されています。

|コンテンツ検査の状態|[説明]|
|---|---|
|Completed|コンテンツ検査が正常に完了しました。|
|適用できません|このファイルは、コンテンツ検査の適用対象ではありませんでした。 この状態は、このファイルのコンテンツ検査を必要とするポリシーがないか、ファイルの種類がサポートされていないために表示されることがあります。|
|Pending|現在、ファイルはコンテンツ検査キューに入れられています。|
|失敗:ダウンロード エラー|Microsoft Cloud App Security が、検査対象のファイルをダウンロードできませんでした。|
|失敗:ファイルが暗号化されています|ファイルを暗号化解除できませんでした。|
|失敗:ファイルが壊れています|ファイルが破損しているため、検査できませんでした。|
|失敗:内部エラー。|ファイルの検査時に、不明な問題が発生しました。|
|失敗:外部 DLP エラー|外部 DLP で問題が発生したため、Cloud App Security でコンテンツの検査に失敗しました。|
|失敗:ファイル サイズが上限を超過しています|ファイルのサイズが最大値の 50 MB を超えています。|
|失敗:ファイルが長すぎるため、部分的にスキャンされました|ファイルの文字数が最大値の 100 万文字を超えています。 スキャンされたコンテンツの一部については、関連するポリシーの一致が適用されています。|
|失敗:ファイル アクセスの拒否|ファイルはクラウドの外部にあり、Cloud App Security がアクセスできませんでした。|
|失敗:ファイルは削除されました|ファイルはクラウドに存在しなくなったため、検査できませんでした。|
|失敗:サポートされていないファイルの種類|このファイルの種類に対しては、Cloud App Security でコンテンツ検査を実行できません。 この状態は、ファイルの種類がサポートされていないか、ファイルが実際に予期されたファイルの種類の形式ではないために表示されることがあります。|

> [!NOTE]
> スキャンの状態にダッシュが表示されている場合は、そのファイルがスキャンの対象としてキューに登録されていないことを意味します。 コンテンツ検査ポリシーの設定の詳細については、「[ファイル ポリシー](data-protection-policies.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
