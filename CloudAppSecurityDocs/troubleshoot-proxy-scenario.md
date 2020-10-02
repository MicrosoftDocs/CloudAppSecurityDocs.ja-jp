---
title: アプリの条件付きアクセス制御に関する問題のトラブルシューティング
description: この記事では、考えられるアプリの条件付きアクセス制御の問題の一覧を示し、考えられる解決策を示します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 6e43990b3ee3d3c5f33119643329381001707724
ms.sourcegitcommit: e8c40ab8901744314af19ede50e9017a92111721
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91205544"
---
# <a name="troubleshooting-conditional-access-app-control-issues"></a>アプリの条件付きアクセス制御に関する問題のトラブルシューティング

*適用対象:Microsoft Cloud App Security*

この記事では、考えられるアプリの条件付きアクセス制御の問題の一覧を示し、考えられる解決策を示します。

## <a name="our-system-flagged-a-new-dns-entry-or-generated-a-certificate-for-casms-but-we-dont-use-microsoft-cloud-app-security"></a>*.cas.ms の新しい DNS エントリがフラグ設定されたか、証明書が生成されましたが、Microsoft Cloud App Security を使用していません

これは、お使いの環境を保護する Cloud App Security による通常の動作と結果です。 組織で Cloud App Security を使用していない場合でも、Cloud App Security のアプリの条件付きアクセス制御によって保護されている環境から他のユーザーがサイトまたはサービスにアクセスすると、その URL が書き換えられてアクセスが保護されます。

たとえば、Cloud App Security によって保護された会社である Contoso のユーザーが fabrikam.com にアクセスすると、ユーザーは自動的に fabrikam.com.us.cas.ms にリダイレクトされます。 その結果、Fabrikam のフィッシング チームに fabrikam.com.us.cas.ms の新しい DNS エントリと証明書が表示されます。

この例から、Fabrikam は実際には Cloud App Security を使用していませんが、Contoso が使用しているため、DNS エントリと証明書が作成されることがわかります。

**//TBD[ALEX]: ???解決方法?MS に問い合わせ?例外を追加? ???**

## <a name="i-see-casms-in-my-url-have-i-been-phished"></a>URL に *.cas.ms が表示されます。 フィッシングされているのでしょうか?

まず、フィッシングされているのではありません。 この種類の URL は想定されており、組織によってビジネスに不可欠なデータを保護するために追加のセキュリティ制御が適用されていることを示しています。

次のようなしくみです。

Salesforce、SharePoint Online、AWS などのクラウド アプリにアクセスしようとすると、URL に `*.cas.ms` がサフィックスとして付けられます。 たとえば、XYZ アプリを使用する場合、見慣れた URL が `XYZ.com` から `XYZ.com.us.cas.ms` に変更されるのに気づきます。

URL が置換パターンに完全に一致しない場合 (*.com の *.com.* .cas.ms へのリダイレクトなど)、またはその他の懸念事項がある場合は、IT 部門にお問い合わせください。
