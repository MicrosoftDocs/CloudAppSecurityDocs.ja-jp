---
title: トラブルシューティング - cas.ms、mcas.ms、または mcas-gov.us とは
description: この記事では、アプリの条件付きアクセス制御によって使用される cas.ms、mcas.ms、または mcas-gov.us の URL サフィックスについて説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/18/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: c62229f209dc1a7862a2f4b4442a663aacce58bc
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90877109"
---
# <a name="troubleshooting---what-is-casms-mcasms-or-mcas-govus"></a>トラブルシューティング - `*.cas.ms`、`*.mcas.ms`、または `*.mcas-gov.us` とは

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、アプリの条件付きアクセス制御によって使用される `cas.ms`、`mcas.ms`、または `mcas-gov.us` の URL サフィックスについて説明します。

## <a name="our-system-flagged-a-new-dns-entry-or-generated-certificate-for-casms-mcasms-or-mcas-govus-but-we-dont-use-cloud-app-security"></a>`*.cas.ms`、`*.mcas.ms`、`*.mcas-gov.us` の新しい DNS エントリがフラグ設定されたか、証明書が生成されましたが、Cloud App Security を使用していません

これは、お使いの環境を保護する Cloud App Security による通常の動作と結果です。 組織で Cloud App Security を使用していない場合でも、これを使用している環境から他のユーザーがサイトまたはサービスにアクセスすると、その URL が書き換えられてアクセスが保護されます。

たとえば、Contoso は Cloud App Security によって提供されるアプリの条件付きアクセス制御を使用して環境を保護しているとします。 Contoso ユーザーが `fabrikam.com` にアクセスすると、ユーザーは自動的に `fabrikam.com.cas.ms` にリダイレクトされます。 その結果、Fabrikam のフィッシング チームに `fabrikam.com.cas.ms` の新しい DNS エントリと証明書が表示されます。

Fabrikam は実際には Cloud App Security を使用していませんが、Contoso が使用しているため、DNS エントリまたは証明書が表示されます。

> [!NOTE]
> また、透明性ログに次のドメインが表示される場合もあります。
>
> - `*.admin-rs-mcas.ms`
> - `*.rs-mcas.ms`
> - `*.admin-rs2-mcas.ms`
> - `*.rs2-mcas.ms`
> - `*.admin-mcas.ms`
> - `*.mcas.ms`
> - `*.admin-mcas-gov.us`

## <a name="heres-why-you-see-casms-mcasms-or-mcas-govus-in-your-url"></a>URL に `*.cas.ms`、`*.mcas.ms`、または `*.mcas-gov.us` が表示される理由

まず、フィッシングされているのではありません。 この種類の URL は想定されており、組織によってビジネスに不可欠なデータを保護するために追加のセキュリティ制御が適用されていることを示しています。

組織はこれを、組織のクラウド環境を保護するためのソリューションである Cloud App Security を使用して行っています。これにより、使用するクラウド アプリに関連するすべての URL と Cookie が置き換えられます。

そのため、Salesforce、SharePoint Online、AWS などのクラウド アプリにアクセスしようとすると、その URL に `.cas.ms`、`.mcas.ms`、または `.mcas-gov.us`がサフィックスとして付けられます。 たとえば、XYZ アプリを使用する場合、URL が `XYZ.com` から `XYZ.com.cas.ms` に変更されるのに気づきます。

URL が置換パターンのいずれかに完全に一致しない場合 (`<app_site>.com` が `<app_site>.com.cas.ms`に置き換わらない場合など)、またはその他の懸念事項がある場合は、IT 部門にお問い合わせください。
