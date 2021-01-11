---
title: Azure を Cloud App Security に接続する
description: この記事では、API コネクタを使用して Azure を Cloud App Security に接続して、使用状況を表示および制御する方法について説明します。
ms.date: 12/27/2020
ms.topic: how-to
ms.openlocfilehash: eb95630ac08763fa6b87a6fab410ec3629010ec8
ms.sourcegitcommit: 40d17309b8729eb914ea91ba5fa7017340231488
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97808914"
---
# <a name="connect-azure-to-microsoft-cloud-app-security"></a>Azure を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、アプリ コネクタ API を使用して Microsoft Cloud App Security を既存の Azure アカウントに接続する方法について説明します。 この接続を使用すると、Azure の使用状況を表示したり制御したりできます。 Cloud App Security での Azure の保護方法の詳細については、[Azure の保護](protect-azure.md)に関する記事を参照してください。

## <a name="how-to-connect-azure-to-cloud-app-security"></a>Azure を Cloud App Security に接続する方法

> [!NOTE]
>
> - Azure を Microsoft Cloud App Security に接続するには、ユーザーが Azure AD のグローバル管理者またはセキュリティ管理者である必要があります。
> - Cloud App Security には、**すべての** サブスクリプションのアクティビティが表示されます。
> - ユーザーが Azure でアクティビティを実行すると、ユーザー アカウント情報が Cloud App Security に設定されます。
> - 現時点では、Cloud App Security では ARM アクティビティのみが監視されます。

1. **[接続されているアプリ]** ページで [+] ボタンをクリックし、 **[Microsoft Azure]** を選択します。

    ![Azure への接続メニュー項目](media/connect-azure-menu.png)

2. Azure のポップアップで、 **[Microsoft Azure に接続]** をクリックします。

    ![Azure の接続](media/connect-azure.png)

> [!NOTE]
> Azure に接続すると、データがプルされます。 その後、データが表示されます。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
