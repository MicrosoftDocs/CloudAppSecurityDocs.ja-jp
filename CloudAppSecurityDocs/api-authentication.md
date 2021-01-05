---
title: API トークンの管理
description: この記事では、Cloud App Security 用の API トークンの生成と管理に関する情報について説明します。
ms.date: 03/27/2020
ms.topic: reference
ms.openlocfilehash: cd577565cb67b51dd93c649e69cd00a551736789
ms.sourcegitcommit: 421870fac566642809eff0a545ec1981be1c9165
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2020
ms.locfileid: "97705884"
---
# <a name="managing-api-tokens"></a>API トークンの管理

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud App Security API にアクセスするには、API トークンを作成し、それをソフトウェアで使用して API に接続する必要があります。 このトークンは、Cloud App Security で API 要求を行うときにヘッダーに含まれます。

[API トークン] タブでは、テナントのすべての API トークンを管理できます。

## <a name="generate-a-token"></a>トークンを生成する

1. **[設定]** メニューで、 **[セキュリティ拡張機能]** 、 **[API トークン]** の順に選択します。

2. プラス アイコン、 **[新しいトークンの生成]** の順にクリックし、後でトークンを識別するための名前を指定して、 **[次へ]** をクリックします。

    ![Cloud App Security によって API トークンが生成される](media/api-token-gen.png)

3. トークンの値をコピーし、回復用にどこかに保存しておきます。これを紛失した場合、トークンを再生成する必要があります。 トークンには、それを発行したユーザーの権限が設定されます。 たとえば、セキュリティ閲覧者は、データを変更できるトークンを発行できません。

4. 次の状態によってトークンをフィルター処理できます。アクティブ、非アクティブ、または生成済み。

    - **生成済み:** 使用されたことがないトークン。
    - **アクティブ:** 過去 7 日以内に生成され、使用されたトークン。
    - **非アクティブ:** 使用されたが、過去 7 日間アクティビティが発生していないトークン。

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

[!INCLUDE [Open support ticket](includes/support.md)]

## <a name="check-out-this-video"></a>こちらのビデオをご覧ください。

[Microsoft Cloud App Security - REST API とトークン](https://channel9.msdn.com/Shows/Microsoft-Security/Microsoft-Cloud-App-Security--REST-APIs-and-Tokens)
