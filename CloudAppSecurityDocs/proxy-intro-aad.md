---
title: Microsoft Cloud App Security のアプリの条件付きアクセス制御を使用して保護する
description: この記事では、Cloud App Security のアプリの条件付きアクセス制御のリバース プロキシの機能について説明します。
ms.date: 10/14/2020
ms.topic: conceptual
ms.openlocfilehash: 18caaec466ec7d79102661705037870f70a7b15f
ms.sourcegitcommit: 72ddcd0f9a83251d588009abf506676612c50267
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2020
ms.locfileid: "97370011"
---
# <a name="protect-apps-with-microsoft-cloud-app-security-conditional-access-app-control"></a>Microsoft Cloud App Security のアプリの条件付きアクセス制御を使用してアプリを保護する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

今日の職場では、多くの場合、クラウド環境で起きていることを、それが起きた後で知るのでは十分ではありません。 従業員が意図的または不注意にデータと組織を危険にさらす前に、侵害とリークをリアルタイムで停止する必要があります。 組織内のユーザーがクラウド アプリで利用できるサービスとツールを最大限に活用し、自分のデバイスを持ち込んで使用できるようにすることが重要です。 同時に、データの漏洩やデータの盗難から、リアルタイムで組織を保護するためのツールが必要です。 Microsoft Cloud App Security では、任意の ID プロバイダー (IdP) と統合することにより、これらの機能がアクセス制御およびセッション制御と共に提供されます。 Azure Active Directory (Azure AD) を IdP として使用している場合、これらの制御は、Azure AD の [条件付きアクセス ツール](/azure/active-directory/conditional-access/overview)を基に構築されたよりシンプルで調整されたデプロイ用に、統合および合理化されています。

> [!NOTE]
>
> - 有効な Cloud App Security ライセンスに加えて、Cloud App Security のアプリの条件付きアクセス制御を使用するには、[Azure Active Directory P1 ライセンス](https://azure.microsoft.com/pricing/details/active-directory/)、または IdP ソリューションに必要なライセンスと、Cloud App Security ライセンスも必要です。

## <a name="how-it-works"></a>しくみ

アプリの条件付きアクセス制御は、リバース プロキシ アーキテクチャが使用されていて、IdP と統合されます。 Azure AD の条件付きアクセスと統合するときは、わずか数回のクリックでアプリの条件付きアクセス制御と連携するようにアプリを構成できます。これにより、条件付きアクセスの条件に基づいて、組織のアプリに対してアクセス制御とセッション制御を簡単かつ選択的に適用できます。 条件では、条件付きアクセス ポリシーを "*誰に*" (ユーザーまたはユーザーのグループ)、"*何に*" (クラウド アプリ)、"*どこに*" (場所とネットワーク) 適用するかを定義します。 条件を決定した後は、アクセス制御とセッション制御を適用することにより、アプリの条件付きアクセス制御でデータを保護できる Cloud App Security にユーザーをルーティングできます。

アプリの条件付きアクセス制御を使用すると、ユーザーは、アクセスとセッションのポリシーに基づいて、アプリのアクセスとセッションをリアルタイムで監視および制御することができます。 アクセス ポリシーとセッション ポリシーは、フィルターをさらに調整し、ユーザーに対して実行されるアクションを設定するため、 Cloud App Security ポータル内で使用されます。 アクセス ポリシーとセッション ポリシーを使用すると、次のことができます。

- **データ窃盗を防ぐ**:たとえばアンマネージド デバイスなどで、機密性の高いドキュメントのダウンロード、切り取り、コピー、および印刷をブロックできます。

- **ダウンロードを保護する**: 機密性の高いドキュメントのダウンロードをブロックするのではなく、ドキュメントにラベルを付け、Azure Information Protection で保護されるように要求することができます。 このアクションにより、危険を及ぼす可能性のあるセッションにおいて確実にドキュメントが保護され、ユーザー アクセスが制限されます。

- **ラベルのないファイルのアップロードを禁止する**: 機密性の高いファイルがアップロード、配布、および他のユーザーに使用される前に、ファイルに適切なラベルと保護が設定されるようにすることが重要です。 機密性の高い内容が含まれるラベルのないファイルが、その内容をユーザーが分類するまで、アップロードされないようにすることができます。

- **マルウェアの可能性をブロックする**: 悪意のある可能性のあるファイルのアップロードをブロックすることで、環境をマルウェアから保護することができます。 アップロードまたはダウンロードされるファイルを、Microsoft 脅威インテリジェンスに対してスキャンし、すぐにブロックすることができます。

- **ユーザー セッションのコンプライアンスを監視する**: リスクの高いユーザーをアプリへのサインイン時に監視し、そのアクションをセッション内からログに記録します。 ユーザーの動作を調査して分析し、将来どこで、どのような条件においてセッション ポリシーを適用する必要があるかを理解することができます。

- **[アクセスのブロック]** : 複数のリスク要因に応じて、特定のアプリとユーザーのアクセスを細かくブロックできます。 たとえば、デバイス管理の形式としてクライアント証明書を使用している場合に、ブロックできます。

- **カスタム アクティビティをブロックする**: Microsoft Teams や Slack といったアプリで機密性の高いコンテンツを含むメッセージを送信する場合のように、アプリによってはリスクを伴う固有のシナリオがあります。 このようなシナリオでは、メッセージで機密性の高いコンテンツをスキャンし、リアルタイムでブロックできます。

### <a name="how-session-control-works"></a>セッション制御のしくみ

アプリの条件付きアクセス制御でセッション ポリシーを作成すると、アプリに直接ではなく、リバース プロキシ経由でユーザーをリダイレクトすることで、ユーザー セッションを制御できます。 その後、ユーザーの要求と応答は、アプリと直接ではなく、Cloud App Security を通して行われます。

セッションがプロキシによって保護されていると、関連するすべての URL と Cookie が Cloud App Security によって置き換えられます。 たとえば、ドメインが `myapp.com` で終わるリンクが含まれるページがアプリから返される場合、次のように、リンクのドメインには `*.mcas.ms` のようなサフィックスが付けられます。

|アプリの URL|置き換えられた URL|
|---|---|
|`myapp.com`|`myapp.com.mcas.ms`|

この方法では、デバイスに何もインストールする必要がなく、アンマネージド デバイスやパートナー ユーザーからのセッションを監視または制御する場合に最適です。

> [!NOTE]
>
> - Microsoft のテクノロジでは、クラス最高の特許取得のヒューリスティックを使用して、対象アプリでユーザーが実行するアクティビティが識別および制御されます。 ヒューリスティックは、セキュリティを最適化し、使いやすさとのバランスを取るように設計されています。 まれに、サーバー側でアクティビティをブロックすることによってアプリが使用不可能になる場合、これらのアクティビティはクライアント側でのみ保護され、悪意のある内部関係者による悪用の影響を受ける可能性があります。
> - Cloud App Security では、世界中の Azure データ センターが活用され、位置情報によって最適化されたパフォーマンスが提供されます。 つまり、トラフィック パターンとその場所によっては、ユーザーのセッションが特定のリージョンの外部でホストされる可能性があります。 ただし、お客様のプライバシーを保護するために、これらのデータ センターにセッション データが保存されることはありません。
> - プロキシ サーバーには、保存データは格納されません。 コンテンツをキャッシュする場合は [RFC 7234 (HTTP キャッシュ)](https://tools.ietf.org/html/rfc7234) に記載されている要件に従い、パブリック コンテンツのみをキャッシュします。

## <a name="managed-device-identification"></a>マネージド デバイスの識別

アプリの条件付きアクセス制御を使用すると、デバイスがマネージドかどうかが考慮されるポリシーを作成できます。 デバイスの状態を識別するには、次のことを確認するようにアクセス ポリシーとセッション ポリシーを構成できます。

- Microsoft Intune 準拠デバイス [Azure AD でのみ利用可能]
- Hybrid Azure AD 参加済みデバイス [Azure AD でのみ利用可能]
- 信頼されたチェーンにおけるクライアント証明書の存在

### <a name="intune-compliant-and-hybrid-azure-ad-joined-devices"></a>Intune 準拠デバイスと Hybrid Azure AD 参加済みデバイス

Azure AD の条件付きアクセスでは、Intune 準拠デバイスと Hybrid Azure AD 参加済みデバイスの情報を、Cloud App Security に直接渡すことができます。 そこから、デバイスの状態をフィルターとして使用するアクセス ポリシーまたはセッション ポリシーを開発できます。 詳細については、[Azure Active Directory のデバイス管理の概要](/azure/active-directory/device-management-introduction)に関するページを参照してください。

> [!NOTE]
> 一部のブラウザーでは、拡張機能のインストールなどの追加の構成が必要になる場合があります。 詳細については、[条件付きアクセスでのブラウザーのサポート](/azure/active-directory/conditional-access/concept-conditional-access-conditions)に関するページを参照してください。

### <a name="client-certificate-authenticated-devices"></a>クライアント証明書で認証されたデバイス

デバイス識別メカニズムを使用すると、クライアント証明書を使用して関連するデバイスに認証を要求できます。 組織に既に展開されている既存のクライアント証明書を使用するか、マネージド デバイスに新しいクライアント証明書を展開することができます。 クライアント証明書がコンピューター ストアではなく、ユーザー ストアにインストールされていることを確認します。 その後、それらの証明書の存在を使用して、アクセス ポリシーとセッション ポリシーを設定します。

SSL クライアント証明書は、信頼チェーンによって検証されます。 PEM 証明書形式で書式設定された X.509 ルート証明機関 (CA) または中間証明機関をアップロードできます。 これらの証明書には、CA の公開キーが含まれている必要があります。これは、セッション中に提示されたクライアント証明書の署名に使用されます。

証明書がアップロードされ、関連するポリシーが構成された後は、該当するセッションがアプリの条件付きアクセス制御を通過すると、Cloud App Security エンドポイントによって、ブラウザーに SSL クライアント証明書を提示するよう要求されます。 ブラウザーは、秘密キーと共にインストールされている SSL クライアント証明書を提供します。 この証明書と秘密キーの組み合わせは、PKCS #12 ファイル形式 (通常は .p12 または .pfx) を使用して行われます。

クライアント証明書のチェックが実行されるとき、Cloud App Security によって次の条件が確認されます。

1. 選択されたクライアント証明書が有効で、正しいルート CA または中間 CA の下にある。
1. 証明書が取り消されていない (CRL が有効になっている場合)。

> [!NOTE]
>
> ほとんどの主要なブラウザーでは、クライアント証明書のチェックがサポートされています。 ただし、モバイル アプリとデスクトップ アプリでは、多くの場合、このチェックをサポートしていない可能性がある組み込みブラウザーが利用されているため、これらのアプリの認証に影響があります。

クライアント証明書によりデバイス管理を利用するようにポリシーを構成するには:

1. Cloud App Security のメニュー バーで設定の歯車 ![設定アイコン](media/settings-icon.png "設定アイコン") をクリックし、 **[設定]** を選択します。

1. **[デバイスの識別]** タブを選択します。
1. 必要な数のルート証明書または中間証明書をアップロードします。

    > [!TIP]
    > どのように動作するかをテストするには、次のようにサンプルのルート CA とクライアント証明書を使用することができます。
    >
    > 1. サンプルの[ルート CA](https://github.com/microsoft/Microsoft-Cloud-App-Security/blob/master/Doc%20Assets/Proxy/Samples/SampleRootCA.crt.pem) と[クライアント証明書](https://github.com/microsoft/Microsoft-Cloud-App-Security/blob/master/Doc%20Assets/Proxy/Samples/SampleClientCert.pfx)をダウンロードします。
    > 1. ルート CA を Cloud App Security にアップロードします。
    > 1. 関連するデバイスにクライアント証明書 (パスワード = Microsoft) をインストールします。

証明書がアップロードされたら、**デバイス タグ** と **有効なクライアント証明書** に基づいて、アクセス ポリシーとセッション ポリシーを作成できます。

## <a name="supported-apps-and-clients"></a>サポートされているアプリとクライアント

セッション制御とアクセスの制御は、SAML 2.0 認証プロトコルを使用して、任意の対話型シングル サインオンに適用できます。また、Azure AD を使用している場合は、Open ID Connect 認証プロトコルも使用できます。 さらに、アプリが Azure AD で構成されている場合は、[Azure AD アプリ プロキシ](/azure/active-directory/manage-apps/application-proxy)で構成されてオンプレミスでホストされているアプリに、これらの制御を適用することもできます。 また、アクセス制御は、ネイティブのモバイルおよびデスクトップ クライアント アプリに適用することもできます。

Cloud App Security では、クラウド アプリ カタログで利用可能な情報を使用してアプリが識別されます。 組織やユーザーによっては、プラグインを追加することでアプリをカスタマイズしている場合があります。 ただし、これらのプラグインでセッション制御が正しく機能するためには、関連付けられているカスタム ドメインを、カタログ内の各アプリに追加する必要があります。

> [!NOTE]
> 他のネイティブ クライアント アプリのサインイン フローの中で、Authenticator アプリは、非対話型のサインイン フローが使用されており、アクセス制御では使用できません。

### <a name="access-controls"></a>アクセス制御

クラウド アプリでセッション内アクティビティを制御するためにセッション制御を使用している多くの組織では、アクセス制御を適用して、ネイティブ モバイル アプリとデスクトップ クライアント アプリの同じセットをブロックすることで、アプリに包括的なセキュリティが提供されます。

アクセス ポリシーを使用してネイティブ モバイル アプリとデスクトップ クライアント アプリへのアクセスをブロックするには、 **[クライアント アプリ]** フィルターを **[モバイルとデスクトップ]** に設定します。 一部のネイティブ クライアント アプリは個別に認識できますが、アプリのスイートの一部である他のアプリは、最上位レベルのアプリとしてのみ識別できます。 たとえば、SharePoint Online などのアプリは、Office 365 アプリに適用されるアクセス ポリシーを作成することによってのみ認識できます。

> [!NOTE]
> **[クライアント アプリ]** フィルターが **[モバイルとデスクトップ]** に明示的に設定されていない場合、結果のアクセス ポリシーはブラウザー セッションにのみ適用されます。 このようになる理由は、誤ってユーザー セッションがプロキシされないようにするためです。これは、このフィルターを使用したときの副産物です。 ほとんどの主要なブラウザーではクライアント証明書のチェックがサポートされていますが、一部のモバイル アプリおよびデスクトップ アプリでは、このチェックがサポートされていない組み込みのブラウザーが使用されています。 したがって、このフィルターを使用すると、これらのアプリの認証に影響を与える可能性があります。

### <a name="session-controls"></a>セッション制御

セッション制御は、任意のオペレーティング システム上の任意の主要プラットフォーム上の任意のブラウザーで動作するように構築されていますが、サポートされているのは [Microsoft Edge](https://www.microsoft.com/edge) (最新)、Google Chrome (最新)、Mozilla Firefox (最新)、または Apple Safari (最新) です。 モバイル アプリとデスクトップ アプリへのアクセスをブロックまたは許可することもできます。

> [!NOTE]
>
> - Cloud App Security では、クラス最高レベルの暗号化の提供に、トランスポート層セキュリティ (TLS) プロトコル 1.2 以降を使用しています。 TLS 1.2 以降をサポートしていないネイティブ クライアント アプリとブラウザーは、セッション制御が構成されていると、アクセスできなくなります。 ただし、TLS 1.1 以下を使用している SaaS アプリは、Cloud App Security を使用して構成されている場合、TLS 1.2 以降を使用しているようにブラウザーに表示されます。
> - セッション コントロールを portal.office.com に適用するには、Microsoft 365 管理センターをオンボードする必要があります。 アプリのオンボードの詳細については、「[任意のアプリに対するアプリの条件付きアクセス制御のオンボードと展開](proxy-deployment-any-app.md)」を参照してください。

<a name="featured-apps"></a>[前に説明した認証プロトコル](#supported-apps-and-clients)を使用して構成されている Web アプリは、アクセス制御とセッション制御で動作するようにオンボードできます。 さらに、次のアプリには、アクセスとセッションの両方の制御が既にオンボードされています。

- AWS
- Azure DevOps (Visual Studio Team Services)
- Azure portal
- ボックス
- Concur
- CornerStone on Demand
- DocuSign
- ドロップボックス
- Dynamics 365 CRM (プレビュー)
- Egnyte
- Exchange Online
- GitHub
- Google Workspace
- HighQ
- JIRA/Confluence
- OneDrive for Business
- LinkedIn Learning
- Power BI
- Salesforce
- ServiceNow
- SharePoint Online
- Slack
- Tableau
- Microsoft Teams (プレビュー)
- Workday
- Workiva
- Workplace by Facebook
- Yammer (プレビュー)

### <a name="office-365-cloud-app-security-featured-apps"></a><a name="O365-apps"></a>Office 365 Cloud App Security のおすすめアプリ

以下の一覧は、[Office 365 Cloud App Security](editions-cloud-app-security-o365.md) でサポートされているおすすめアプリです。

- Exchange Online
- OneDrive for Business
- Power BI
- SharePoint Online
- Microsoft Teams (プレビュー)
- Yammer (プレビュー)

特定のアプリのサポートに関心がある場合は、[アプリに関する詳細情報をお送りください](mailto:casfeedback@microsoft.com)。 そのオンボードについて興味のあるユース ケースを必ずお知らせください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [おすすめアプリに対してアプリの条件付きアクセス制御を展開する](proxy-deployment-aad.md)

> [!div class="nextstepaction"]
> [アプリの条件付きアクセス制御がすべてのアプリに展開](proxy-deployment-any-app.md)

> [!div class="nextstepaction"]
> [アクセスおよびセッション制御のトラブルシューティング](troubleshooting-proxy.md)

[!INCLUDE [Open support ticket](includes/support.md)]