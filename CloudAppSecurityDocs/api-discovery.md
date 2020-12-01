---
title: Cloud App Security Cloud Discovery API
description: この記事では、Cloud Discovery API の使用方法について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: bf02c6a77cfaf165c4ae064c77012228846c44cf
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96314309"
---
# <a name="cloud-discovery-api"></a>Cloud Discovery API

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud Discovery を使用すると、ユーザーから提供されたシステム ログを解析し、クラウド環境内の新規および不明なアプリケーションを検出できます。 会社の検出ログ ファイルのアップロードを自動化するには、Cloud Discovery API を使用します。 ファイルのアップロード プロセスは、連続して呼び出す必要がある 3 つの API 呼び出しで構成されています。

さらに、Cloud App Security を使用すると、既存のオンプレミスのセキュリティ アプライアンスを使用して、承認されていないアプリへのアクセスをブロックできます。 専用のブロック スクリプトを取得し、アプライアンスにインポートするには、ブロック スクリプトの生成呼び出しを使用します。

サポートされている要求は次のとおりです。

- [ファイルのアップロードの開始](api-discovery-initiate.md)
- [ファイルのアップロードの実行](api-discovery-perform.md)
- [ファイルのアップロードの最終処理](api-discovery-finalize.md)
- [ブロック スクリプトの生成](api-discovery-script.md)

[!INCLUDE [Open support ticket](includes/support.md)]
