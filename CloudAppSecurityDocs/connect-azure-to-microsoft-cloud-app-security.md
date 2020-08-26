---
title: Azure を Cloud App Security に接続する
description: この記事では、API コネクタを使用して Azure を Cloud App Security に接続して、使用状況を表示および制御する方法について説明します。
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
ms.openlocfilehash: 58a8fad9c99fdf71c8ba17089083d02b15cdd8cf
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781108"
---
# <a name="connect-azure-to-microsoft-cloud-app-security"></a>Azure を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、アプリ コネクタ API を使用して Microsoft Cloud App Security を既存の Azure アカウントに接続する方法について説明します。 この接続を使用すると、Azure の使用状況を表示したり制御したりできます。 Cloud App Security での Azure の保護方法の詳細については、[Azure の保護](protect-azure.md)に関する記事を参照してください。

## <a name="how-to-connect-azure-to-cloud-app-security"></a>Azure を Cloud App Security に接続する方法

> [!NOTE]
>
> - Azure を Microsoft Cloud App Security に接続するには、ユーザーが Azure AD のグローバル管理者またはセキュリティ管理者である必要があります。
> - Cloud App Security には、**すべての**サブスクリプションのアクティビティが表示されます。
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
