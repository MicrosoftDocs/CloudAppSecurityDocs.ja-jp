---
title: レポートの生成 - Microsoft Cloud App Security
description: この記事では、Microsoft Cloud App Security でデータ管理レポートを生成する手順について説明します。
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
ms.openlocfilehash: c08938f5317d5862b480a0498949df6930910e63
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881574"
---
# <a name="generate-data-management-reports"></a>データ管理レポートの生成

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security では、クラウド アプリ内のファイルの概要を提供するレポートを生成することができます。

これらのレポートを生成する手順

1. **[ファイル]** に移動します。
2. 右上隅にある 3 つのドットをクリックし、 **[データ管理レポート]** で以下のいずれかのレポートを選択します。

    ![[データ管理レポート] メニューを示すスクリーンショット](media/reports.png)

## <a name="data-sharing-overview"></a>データ共有の概要

このレポートには、各クラウド アプリに保存されているファイルの数がアクセス許可別に一覧表示されます。 クラウド アプリでは、アクセスが容易でどこからでも利用できるため、ファイルを簡単に共有できるようになりました。 **プライベート ファイル**は、その所有者以外のユーザーと共有されることはありません。 ファイルが共有されている場合、Cloud App Security は 4 種類の状態を区別します。

- **公開共有 (インターネット)** ファイルは、認証を受けなくても検索エンジンの結果などからアクセスできるファイルです。
- **公開共有**ファイルは、認証を受けなくてもリンクを使用してアクセスできるファイルです。
- **外部共有**ファイルは、組織外のユーザーがクラウド アプリの認証を受けてアクセスできるファイルです。
- **内部共有**ファイルは、組織内のすべてまたは一部のユーザーがアクセスできるファイルです。

## <a name="outbound-sharing-by-domain"></a>ドメイン別の送信共有

このレポートでは、従業員が共有している企業ファイルがあるドメインが一覧表示されます。 レポートには、ドメインごとに、そのドメインでファイルを共有しているユーザーが表示されます。 また、共有されているファイルと、コラボレーター ファイルの共有相手も表示されます。 これらのドメインでの共有を管理することをお勧めします。 共有は、関連する各アプリの [アプリ] ページの [ファイル] タブで管理することができます。

## <a name="owners-of-shared-files"></a>共有ファイルの所有者

これには、企業ファイルを外部と共有しているユーザーが一覧表示されます。 外部共有ファイルは、特定の外部のコラボレーターと共有されているファイルです。 公開共有ファイルには、プライベート リンクを使用して、インターネット上で誰でもアクセスできます。 これらのファイルを参照できるのは、明示的にリンクを持っているユーザーのみです。 公開共有ファイル (インターネット) は、検索エンジンの結果を使用してインターネット上で誰でもアクセスすることができます。 過剰な数のファイルを共有しているユーザーが見つかった場合、その理由を調査することをお勧めします。 外部共有の使用状況を詳細に把握するには、[ファイル] タブを使用して調査した後、それらのユーザーに連絡します。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [制御](control.md)

[!INCLUDE [Open support ticket](includes/support.md)]
