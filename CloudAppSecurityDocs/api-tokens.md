---
title: Cloud App Security での API トークン管理
description: この記事では、Cloud App Security 用の API トークンの生成に関する情報を提供します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 81c44eb4527b19e1f3f42929028791f1ae48715d
ms.sourcegitcommit: b71546236cb97c0a22d0e82742a167f31555b275
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86308243"
---
# <a name="api-tokens"></a>API トークン

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security API を使用すると、REST API エンドポイントを介して、プログラムで Cloud App Security にアクセスできます。 アプリケーションでは、API を使用して、Cloud App Security のデータとオブジェクトに対する読み取りと更新の操作を実行できます。 たとえば、Cloud App Security API では、ユーザー オブジェクトに対する次の一般的な操作がサポートされています。

- Cloud Discovery にログ ファイルをアップロードする
- ブロック スクリプトを生成する
- アクティビティ、アラート、およびポリシー レポートを一覧表示する
- アラートを無視または解決する

Microsoft の API の使用の詳細については、「[Cloud App Security REST API](api-introduction.md)」を参照してください。

API にアクセスするには、API トークンを作成し、それをソフトウェアで使用して Cloud App Security API に接続する必要があります。

[API トークン] タブでは、テナントのすべての API トークンを管理できます。

## <a name="generate-a-token"></a>トークンを生成する

1. **[設定]** メニューで、 **[セキュリティ拡張機能]** 、 **[API トークン]** の順に選択します。

2. プラス アイコン、 **[新しいトークンの生成]** の順にクリックし、後でトークンを識別するための名前を指定して、 **[次へ]** をクリックします。
  ![Cloud App Security によって API トークンが生成される](media/api-token-gen.png)

3. トークンの値をコピーし、回復用にどこかに保存しておきます。これを紛失した場合、トークンを再生成する必要があります。 トークンには、それを発行したユーザーの権限が設定されます。 たとえば、セキュリティ閲覧者は、データを変更できるトークンを発行できません。

4. 次の状態によってトークンをフィルター処理できます。アクティブ、非アクティブ、または作成。

    - [作成] は、使用されたことがないトークンです。
    - [アクティブ] は、過去 7 日以内に生成され、使用されたトークンです。
    - [非アクティブ] は使用されましたが、過去 7 日間アクティビティが発生しませんでした。

5. 新しいトークンを生成すると、Cloud App Security ポータルへのアクセスに使用する新しい URL が提供されます。

    ![Cloud App Security API トークン](media/generate-api-token.png)

    汎用ポータル URL も引き続き機能しますが、トークンと共に提供されるカスタム URL よりかなり遅くなります。 URL を忘れた場合は、いつでもメニューの **?** アイコンに移動し、 **[バージョン情報]** を選択して表示できます。

## <a name="api-token-management"></a>API トークン管理

[API トークン] ページには、生成されたすべての API トークンのテーブルが表示されます。

完全な権限を持つ管理者には、このテナントに対して生成されたすべてのトークンが表示されます。 その他のユーザーには、自分が生成したトークンだけが表示されます。

このテーブルでは、トークンが生成されたときと、最後に使用されたときに関する詳細が提供され、トークンを取り消すことができます。

トークンが取り消されると、テーブルから削除され、それを使用していたソフトウェアは、新しいトークンが提供されるまで API 呼び出しに失敗します。

> [!NOTE]
>
> - SIEM コネクタとログ コレクターでも API トークンが使用されます。 これらのトークンは、ログ コレクターおよび SIEM エージェントのセクションから管理する必要があり、このテーブルには表示されません。
> - プロビジョニング解除されたユーザー API トークンは Cloud App Security に保持されますが、使用することはできません。 これらを使用しようとすると、アクセス許可の拒否の応答が返されます。 ただし、そのようなトークンは、 **[API トークン]** ページで取り消すことが推奨されます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud App Security REST API](api-introduction.md)

> [!div class="nextstepaction"]
> [SIEM 統合問題のトラブルシューティング](troubleshooting-siem.md)

[!INCLUDE [Open support ticket](includes/support.md)]

## <a name="check-out-this-video"></a>こちらのビデオをご覧ください。

[Microsoft Cloud App Security - REST API とトークン](https://channel9.msdn.com/Shows/Microsoft-Security/Microsoft-Cloud-App-Security--REST-APIs-and-Tokens)
