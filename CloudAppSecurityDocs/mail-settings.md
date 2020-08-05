---
title: 電子メール通知の基本設定を設定する - Cloud App Security
description: この記事では、Cloud App Security から送信される電子メール通知をカスタマイズする方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 2/4/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 29e6fb15880f9d3c306acbe6e696dd96a73ac241
ms.sourcegitcommit: 021914cf4b16ad3a5543f69958639dc670f09304
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2020
ms.locfileid: "87514515"
---
# <a name="email-notification-preferences"></a>電子メール通知の基本設定

*適用対象:Microsoft Cloud App Security*

この記事では、侵害が検出されたときに Cloud App Security から送信される電子メール通知を、ご自分のユーザー向けにカスタマイズする方法について説明します。

> [!NOTE]
> このカスタマイズは、ご自分のエンド ユーザーに送信される通知にのみ影響し、Cloud App Security の管理者に送信される通知には影響しません。

## <a name="set-email-notification-preferences"></a><a name="mailsettings"></a> 電子メール通知の基本設定を設定する

 Microsoft Cloud App Security では、侵害に関係するエンド ユーザーに送信される電子メール通知をカスタマイズできます。 電子メール通知のパラメーターを設定するには、次の手順に従います。 ご自分のスパム対策サービスで許可する必要がある Microsoft Cloud App Security の電子メール サーバーの IP アドレスについては、「[ネットワークの要件](network-requirements.md)」を参照してください。

1. メニュー バーで設定の歯車をクリックし、 **[設定]** 、 **[メールの設定]** タブを順に選択します。

    ![メールの設定](media/mail-settings-config.png)

2. **[メール送信者の ID]** で次を実行します。既定の電子メール設定を使用する場合は、このセクションの内容を変更する必要はありません。 電子メールの送信者 ID をカスタマイズする場合は、ここの任意の設定を設定して、変更するフィールドをカスタマイズします。 次の項目のいずれか、またはすべて変更することができます。 **[送信元表示名]** 、 **[送信元メール アドレス]** 、 **[返信用メール アドレス]** 。 Microsoft Cloud App Security では、MailChimp&reg; というサードパーティのメール サービスを使用して、このカスタマイズを実現しています。 カスタマイズするには、MailChimp のサービス利用規約とプライバシーに関する声明を確認して同意する必要があります。 それ以外の場合は、Microsoft Cloud App Security では、既定の設定が使用され通知が送信されます。

    > [!NOTE]
    > 表示名と電子メール アドレスには、[rfc822 標準](https://www.rfc-editor.org/rfc/rfc822.txt)に従い、unicode 文字のみを使用できます。

3. **[メールのデザイン]** では、html ファイルを使用し、システムから送信される電子メール メッセージをカスタマイズおよびデザインできます。 使用するテンプレートの html ファイルには、次が含まれている必要があります。

    - テンプレートには、テンプレートのすべての CSS ファイルがインラインで含まれている必要があります。

    - テンプレートには、次の 3 つの編集不可能なプレースホルダーが必要です。

        - **%%logo%%** - [全般設定] ページにアップロードした、あなたの企業のロゴの URL。

        - **%%title%%** - ポリシーにより設定された、電子メールの件名用のプレースホルダー。

        - **%%content%%** - ポリシーにより設定された、エンド ユーザー向けに含めるコンテンツ用のプレースホルダー。

4. **[テンプレートのアップロード...]** をクリックし、作成したファイルを選択します。

5. **[テスト メールを送信]** をクリックし、作成したテンプレートの例をご自分宛に電子メールで送信します。 このメールは、ポータルへのログインに使用したアカウントに送信されます。 テスト メールに表示される次の項目を確認する必要があります。
    - メタデータ フィールド
    - テンプレート
    - メールの件名
    - メール本文のタイトル
    - コンテンツ

## <a name="sample-email-template"></a>サンプルのメール テンプレート

次にメール テンプレートの例を示します。

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
  <html>
       <head>
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
            <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
          </head>
          <body class="end-user">
          <table border="0" cellpadding="20%" cellspacing="0" width="100%" id="background-table">
            <tr>
              <td align="center">
                <!--[if (gte mso 9)|(IE)]>
                <table width="600" align="center" cellpadding="0" cellspacing="0" border="0">
                  <tr>
                    <td>
                <![endif]-->
                <table bgcolor="#ffffff" align="center" border="0" cellpadding="0" cellspacing="0" style="padding-bottom: 40px;" id="container-table">
                  <tr>
                    <td align="right" id="header-table-cell">
                      <img src="%%logo%%" alt="Microsoft Cloud App Security" id="org-logo" />
                    </td>
                  </tr>
                  <tr>
                    <td style="padding-top: 58px;" align="center" valign="top">
                      <table width="100%" cellpadding="12">
                        <tr>
                          <td align="center" class="round-title">
                            %%title%%
                          </td>
                        </tr>
                      </table>
                    </td>
                  </tr>
                  <tr>
                    <td style="padding: 0 40px 79px 40px;" class="content-table-cell" align="left" valign="top">
                        %%content%%
                    </td>
                  </tr>
                  <tr>
                    <td class="last-row"></td>
                  </tr>
                </table>
                <!--[if (gte mso 9)|(IE)]>
                </td>
                </tr>
                </table>
                  <![endif]-->
              </td>
              </tr>
          </table>
            </body>
          </html>
```

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery を設定する](set-up-cloud-discovery.md)

[!INCLUDE [Open support ticket](includes/support.md)]
