---
title: Cloud App Security Cloud Discovery API
description: この記事では、Cloud Discovery API の使用方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: cdf70db4edd8b476a1915b9f54459a8d8b1a7bec
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90879773"
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
