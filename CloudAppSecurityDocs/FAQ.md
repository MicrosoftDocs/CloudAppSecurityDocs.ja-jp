---
title: よく寄せられる質問 - Cloud App Security
description: この記事では、Cloud App Security についてよく寄せられる質問とその回答について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: f9e226f117de70c98125708b93ea1badf67aa06d
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90880182"
---
# <a name="frequently-asked-questions"></a>よく寄せられる質問

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、Cloud App Security についてよく寄せられる質問とその回答について説明します。

## <a name="what-kind-of-permissions-do-i-need-to-access-cloud-app-security"></a>Cloud App Security にアクセスするには、どの種類のアクセス許可が必要ですか?

Azure Active Directory のグローバル管理者、コンプライアンス管理者、またはセキュリティ管理者である必要があります。 これらのロールを、Office 365 セキュリティ/コンプライアンス センターで持っているだけでは不十分です。 PowerShell を使用して、ユーザーを Azure Active Directory のグローバル管理者、コンプライアンス管理者、またはセキュリティ管理者に設定できます。 次のコマンドレットを実行します。

```powershell

 $cred = Get-Credential
 Connect-MsolService -credential $cred
 Add-MsolRoleMember -RoleName "Compliance Administrator" -RoleMemberEmailAddress "XX@XX.XX"
```

 または

```powershell
 Add-MsolRoleMember -RoleName "Security Administrator" -RoleMemberEmailAddress “XX@XX.XX”
```

## <a name="next-steps"></a>次のステップ

クラウド アプリの使用の制御に、ポリシーを設定して使用する方法については、「[ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)」を参照してください。

[!INCLUDE [Open support ticket](includes/support.md)]
