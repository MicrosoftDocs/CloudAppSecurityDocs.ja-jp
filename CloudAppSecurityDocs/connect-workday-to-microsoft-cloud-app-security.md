---
title: Workday を Cloud App Security (プレビュー) に接続する
description: この記事では、お使いの Workday アプリを、使用状況を表示および制御する API コネクタを使用して、Cloud App Security に接続する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/10/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: c849aace75d1d4268a44e02feaecdcd032a53888
ms.sourcegitcommit: 98f1b892294beb74157cb3452aa5d489e78bbef4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94424539"
---
# <a name="connect-workday-to-microsoft-cloud-app-security"></a>Workday を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、アプリ コネクタ API を使用して Microsoft Cloud App Security を既存の Workday アカウントに接続する方法について説明します。 この接続を使用すると、Workday の使用状況を表示したり制御したりできます。 Cloud App Security で Workday を保護する方法の詳細については、[Workday の保護](protect-workday.md)に関するページを参照してください。

## <a name="quick-start"></a>クイック スタート

「クイックスタート」ビデオをご覧ください。前提条件を構成し、Workday の手順を実行する方法を説明しています。 ビデオの手順を完了したら、[Workday コネクタの追加](#add-connector)に進むことができます。

<br />

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4n1ZO]

## <a name="prerequisites"></a>[前提条件]

Cloud App Security への接続に使用する Workday アカウントは、セキュリティ グループ (新規または既存) のメンバーである必要があります。 Workday Integration System User (統合システム ユーザー) の使用をお勧めします。 セキュリティ グループでは、次のドメイン セキュリティ ポリシーに対して次のアクセス許可が選択されている必要があります。

| 機能領域 | ドメイン セキュリティ ポリシー | サブドメイン セキュリティ ポリシー | レポート/タスクの権限 | 統合権限 |
| --- | --- | --- | --- | --- |
| System (システム) | 設定: テナント設定 – 全般 | 設定: テナント設定 – セキュリティ | 表示、変更 | 取得、配置 |
| System (システム) | セキュリティ管理 | | 表示、変更 | 取得、配置 |
| System (システム) | システム監査 | | 表示 | 取得 |
| スタッフ | 従業員データ: スタッフ | 従業員データ: 公務員レポート | 表示 | 取得 |

> [!NOTE]
>
> * セキュリティ グループのアクセス許可の設定に使用するアカウントは、Workday Administrator (管理者) である必要があります。
> * アクセス許可を設定するには、「Domain Security Policies for Functional Area」(機能領域のドメイン セキュリティ ポリシー) を検索してから、各機能領域 ("System"/"Staffing") を検索して、表で示しているアクセス許可を付与します。
> * すべてのアクセス許可を設定したら、「Activate Pending Security Policy Changes」(保留中のセキュリティ ポリシーの変更をアクティブにする) を検索して、変更を承認します。

Workday 統合ユーザー、セキュリティ グループ、アクセス許可の設定の詳細については、[統合または外部エンドポイント アクセスの Workday への付与](https://go.microsoft.com/fwlink/?linkid=2103212)に関するガイド (Workday ドキュメント/コミュニティ資格情報でアクセス可能) の手順 1 ～ 4 を参照してください。

## <a name="how-to-connect-workday-to-cloud-app-security-using-oauth"></a>OAuth を使用して Workday を Cloud App Security に接続する方法

1. 前提条件で説明したセキュリティ グループのメンバーであるアカウントで Workday にサインインします。

1. 「Edit tenant setup – system」(テナント設定の編集 – システム)を検索し、 **[User Activity Logging]\(ユーザー アクティビティ ログ\)** で、 **[Enable User Activity Logging]\(ユーザー アクティビティ ログの有効化\)** を選択します。

    ![ユーザー アクティビティ ログの許可のスクリーンショット](media/connect-workday-enable-logging.png)

1. 「Edit tenant setup – security」(テナント設定の編集 – セキュリティ) を検索し、 **[OAuth 2.0 Settings]\(OAuth 2.0 設定\)** で、 **[OAuth 2.0 Clients Enabled]\(OAuth 2.0 クライアント有効\)** を選択します。

1. 「Register API Client」(API クライアントの登録) を検索し、 **[Register API Client – Task]\(API クライアントの登録 – タスク\)** を選択します。

1. **[Register API Client]\(API クライアントの登録\)** ページで、次の情報を入力してから **[OK]** をクリックします。

    | フィールド名 | 値 |
    | ---- | ---- |
    | クライアント名 | Microsoft Cloud App Security |
    | Client Grant Type (クライアント付与タイプ) | Authorization Code Grant (認証コード付与) |
    | Access Token Type (アクセス トークンの種類) | Bearer |
    | Redirection URI (リダイレクト URI) | `https://portal.cloudappsecurity.com/api/oauth/connect`<br /><br />**注**:US Government GCC High のお客様の場合は、「`https://portal.cloudappsecurity.us/api/oauth/connect`」という値を入力します。 |
    | Non-Expiring Refresh Tokens (有効期限のない更新トークン) | はい |
    | OAuth2 Scopes (OAuth2 スコープ) | **Staffing** (スタッフ) および **System** (システム) |
    | Scope (Functional Areas) (スコープ (機能領域)) | **Staffing** (スタッフ) および **System** (システム) |

    ![API クライアントの登録のスクリーンショット](media/connect-workday-register-api-client.png)

1. 登録したら、次のパラメーターをメモして **[完了]** をクリックします。

    * クライアント ID
    * Client Secret (クライアント シークレット)
    * Workday REST API Endpoint (Workday REST API エンドポイント)
    * Token Endpoint (トークン エンドポイント)
    * Authorization Endpoint (承認エンドポイント)

    ![API クライアントの登録を確認するスクリーンショット](media/connect-workday-register-api-client-confirm.png)

1. <a name="add-connector"></a>Cloud App Security ポータルで、 **[調査]** 、 **[Connected Apps]\(接続されているアプリ\)** の順にクリックします。

1. **[アプリ コネクタ]** ページで、[+] ボタンをクリックして、 **[Workday]** を選択します。

    ![アプリ コネクタの追加のスクリーンショット](media/connect-workday-add-app.png)

1. ポップアップで、インスタンス名を追加してから **[Connect Workday]\(Workday を接続\)** をクリックします。

    ![インスタンス名の追加のスクリーンショット](media/connect-workday-add-app-connect.png)

1. 次のページで、メモしておいた情報を詳細に入力し、 **[Connect in Workday]\(Workday で接続\)** をクリックします。

    ![アプリの詳細の入力のスクリーンショット](media/connect-workday-add-app-connect-details.png)

1. Workday で、Workday アカウントへのアクセスを Cloud App Security に許可するかどうかを確認するポップアップが表示されます。 続行するには、 **[許可]** をクリックします。

    ![アプリへのアクセスの承認のスクリーンショット](media/connect-workday-add-app-allow.png)

1. Cloud App Security ポータルに戻ると、Workday が正常に接続されたというメッセージが表示されます。 **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

> [!NOTE]
> Workday に接続すると、接続前の 7 日間のイベントを受け取ります。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
