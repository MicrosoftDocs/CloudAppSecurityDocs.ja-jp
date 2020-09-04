---
title: Microsoft 365 を Cloud App Security に接続する
description: この記事では、API コネクタを使用して Microsoft 365 を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 797ff41831b886354583e3b21e1cf0981f84577e
ms.sourcegitcommit: c174a7ada5c6a14f0fea9870672898c54e5e3b52
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2020
ms.locfileid: "89150209"
---
# <a name="connect-microsoft-365-to-microsoft-cloud-app-security"></a>Microsoft 365 を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、アプリ コネクタ API を使用して Microsoft Cloud App Security を既存の Microsoft 365 アカウントに接続する方法について説明します。 この接続を使用すると、Microsoft 365 の使用状況を表示したり制御したりできます。 Cloud App Security で Microsoft 365 を保護する方法の詳細については、[Microsoft 365 の保護](protect-office-365.md)に関するページを参照してください。
  
Cloud App Security によって、レガシ Office 365 専用プラットフォームと、Microsoft 365 サービスの最新のオファリング (一般に Microsoft 365 の vNext リリース ファミリと呼ばれる) がサポートされています。  Cloud App Security では、レガシ Microsoft Business Productivity Online Standard Suite (BPOS) はサポートされていません。

> [!NOTE]
> 場合により、vNext サービス リリースが、管理レベルで標準の Microsoft 365 オファリングと若干異なることがあります。

Cloud App Security は、次の Microsoft 365 アプリをサポートしています。

- Dynamics 365 CRM
- Exchange (Exchange からのアクティビティがポータルで検出された後にのみ表示され、監査を有効にする必要があります)
- Office
- OneDrive
- Power Automate
- Power BI (Power BI からのアクティビティがポータルで検出された後にのみ表示され、監査を有効にする必要があります)
- SharePoint
- Skype for Business
- Teams (Teams のアクティビティがポータルで検出された後にのみ表示されます)
- Yammer

> [!NOTE]
> Cloud App Security は [Microsoft 365 の監査ログ](/microsoft-365/compliance/detailed-properties-in-the-office-365-audit-log?view=o365-worldwide)と直接統合されて、PowerApps、Forms、Sway、Stream など、**サポートされているすべてのサービス**からすべての監査イベントを受信します。

## <a name="how-to-connect-microsoft-365-to-cloud-app-security"></a>Microsoft 365 を Cloud App Security に接続する方法  

> [!NOTE]
>
>- Microsoft 365 を Cloud App Security に接続するには、少なくとも 1 つの Microsoft 365 ライセンスが割り当てられている必要があります。
>- Cloud App Security で Microsoft 365 のアクティビティの監視を有効にするには、[Office セキュリティ/コンプライアンス センター](https://support.microsoft.com/help/4026501/office-auditing-in-office-365-for-admins)で監査を有効にする必要があります。
>- Microsoft 365 で既定で有効になっている Exchange 管理者監査ログによって、管理者 (または管理者特権が割り当てられているユーザー) が Exchange Online 組織で変更を行ったときに、Microsoft 365 監査ログにイベントが記録されます。 Exchange 管理センターを使用するか、Windows PowerShell でコマンドレットを実行することによって行われた変更は、Exchange 管理者監査ログに記録されます。 Exchange の管理者監査ログの詳細については、[管理者監査ログ](/exchange/security-and-compliance/exchange-auditing-reports/view-administrator-audit-log)に関するページを参照してください。
>- Exchange Online のユーザー アクティビティがログに記録される前に、ユーザーのメールボックスごとに Exchange メールボックスの監査ログをオンにする必要があります。「[Exchange メールボックス アクティビティ](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c)」を参照してください。
>- Office アプリが有効になっている場合は、Microsoft 365 の一部であるグループも、特定の Office アプリから Cloud App Security にインポートされます。たとえば、SharePoint が有効になっている場合、Microsoft 365 グループも SharePoint グループとしてインポートされます。
>- PowerBI のログを取得するには、[PowerBI で監査を有効にする](https://powerbi.microsoft.com/documentation/powerbi-admin-auditing/)必要があります。 監査を有効にすると、Cloud App Security ではログの取得が開始されます (24 - 72 時間の遅延があります)。
>- Dynamics 365 のログを取得するには、[Dynamics 365 で監査を有効にする](/dynamics365/customer-engagement/admin/enable-use-comprehensive-auditing#enable-auditing)必要があります。 監査を有効にすると、Cloud App Security ではログの取得が開始されます (24 - 72 時間の遅延があります)。
>- Active Directory オンプレミス環境のユーザーと自動的に同期するように Azure Active Directory が設定されている場合、オンプレミス環境の設定により Azure AD 設定がオーバーライドされ、 **[ユーザーの停止]** ガバナンス アクションの使用が元に戻されます。
>- Azure AD サインイン アクティビティの場合、Cloud App Security には、対話型のサインイン アクティビティと、ActiveSync などのレガシ プロトコルからのサインイン アクティビティのみが表示されます。 非対話型のサインイン アクティビティは、Azure AD 監査ログで確認できます。
> - [Multi-Geo の展開](/office365/enterprise/office-365-multi-geo)は、OneDrive でのみサポートされています。

1. **[接続されているアプリ]** ページで [+] ボタンをクリックし、 **[Office 365]** を選択します。

    ![O365 への接続メニュー オプション](media/connect-o365.png)

1. Office 365 のポップアップで、 **[Office 365 に接続する]** をクリックします。

    ![O365 への接続ポップアップ](media/office-connect.png)

1. Office 365 コンポーネント ページで、必要なオプションを選択し、 **[接続]** をクリックします。

    > [!NOTE]
    >
    > - 最適な保護を行うには、すべての Office 365 コンポーネントを選択することをお勧めします。
    > - **Office 365 ファイル** コンポーネントには、**Office 365 アクティビティ** コンポーネントと Cloud App Security ファイルの監視 ( **[設定]**  >  **[ファイル]**  >  **[ファイルの監視を有効化]** ) が必要です。

    ![O365 への接続コンポーネント](media/connect-o365-components.png)

1. Microsoft 365 が正常に接続された状態で表示されたら、 **[閉じる]** をクリックします。

> [!NOTE]
> Microsoft 365 に接続すると、Microsoft 365 に接続されている、API をプルしているサードパーティ製アプリケーションも含めて、1 週間前からのデータが表示されます。 接続前に API がプルされていないサードパーティ製アプリの場合は、Microsoft 365 に接続した時点からのイベントが表示されます。これは、Cloud App Security では既定でオフになっているすべての API が有効になるためです。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
