---
title: Cloud App Security で使用できるファイル データとフィルターについて
description: このリファレンス記事では、Cloud App Security で使用されるファイルおよびファイル フィルターの種類に関する情報を提供します。
ms.date: 02/14/2021
ms.topic: how-to
ms.openlocfilehash: 106b3455811e0616c1594abc5f364241ea547cf3
ms.sourcegitcommit: 97bb78d140be3e87ecfa29b7db67e8863f88a520
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2021
ms.locfileid: "100514860"
---
# <a name="files"></a>ファイル

[!INCLUDE [Banner for top of topics](includes/banner.md)]

データ保護を提供するために、Microsoft Cloud App Security では、接続されているアプリのすべてのファイルを表示することができます。 アプリ コネクタを使用して Microsoft Cloud App Security をアプリに接続した後、すべてのファイル (たとえば、OneDrive や Salesforce に格納されているすべてのファイル) が Microsoft Cloud App Security によってスキャンされます。 その後、各ファイルは変更されるたびに Cloud App Security によって再スキャンされます。内容、メタデータ、または共有アクセス許可の変更を対象にできます。 スキャン時間は、アプリに格納されているファイルの数によって異なります。 また、 **[ファイル]** ページを使用してファイルをフィルター処理し、クラウド アプリに保存されているデータの種類を調査することもできます。

## <a name="file-filter-examples"></a>ファイルのフィルター例

たとえば、 **[ファイル]** ページを使用して、次のように、**社外秘** というラベルの付いた外部共有ファイルをセキュリティで保護します。アプリを Cloud App Security に接続した後、Azure Information Protection と統合します。 その後、 **[ファイル]** ページで、**社外秘** というラベルの付いたファイルをフィルター処理し、 **[コラボレーター]** フィルターでドメインを除外します。 組織外で共有されている機密ファイルがあることがわかった場合は、それらを検出するためのファイル ポリシーを作成できます。 これらのファイルには自動ガバナンス アクション (**外部コラボレーターを削除する** や **ポリシー一致ダイジェストをファイル所有者へ送信** など) を適用し、組織のデータ損失を防ぐことができます。

![社外秘ファイルのフィルター](media/file-filter-confidential.png)

**[ファイル]** ページの使用方法の別の例を以下に示します。 過去 6 か月間に変更されていないファイルを、組織内の誰もが公開または外部共有していないことを確認します。アプリを Cloud App Security に接続し、 **[ファイル]** ページに移動します。 アクセス レベルが **外部** または **パブリック** であるファイルをフィルター処理し、 **[最終更新日時]** の日付を 6 か月前に設定します。 **[検索に基づく新しいポリシー]** をクリックして、これらの古いパブリック ファイルを検出するファイル ポリシーを作成します。 組織のデータ損失を防ぐために、**外部ユーザーの削除** などの自動ガバナンス アクションをそれらに適用します。

![古い外部ファイルのフィルター](media/file-example-stale-external.png)

基本的なフィルターでは、ファイルのフィルター処理を開始するための優れたツールが提供されます。

![基本的なファイル ログ フィルター](media/file-log-filter-basic-1.png)

さらに具体的にファイルを絞り込むために、[詳細] をクリックして、基本的なフィルターを拡張することができます。

![詳細なファイル ログ フィルター](media/file-log-filter-advanced-1.png)

## <a name="file-filters"></a><a name="Filefilters"></a> ファイル フィルター

Cloud App Security では、20 を超えるメタデータ フィルター (アクセス レベルやファイルの種類など) に基づいて任意のファイルの種類を監視できます。

Cloud App Security の組み込み DLP エンジンでは、一般的なファイルの種類からテキストを抽出して内容を検査します。 含まれているファイルの種類には、PDF、Office ファイル、RTF、HTML、コード ファイルなどがあります。

適用できるファイル フィルターの一覧を以下に示します。 ポリシーの作成で強力なツールを提供するために、ほとんどのフィルターでは複数の値と NOT がサポートされます。

> [!NOTE]
> ファイル ポリシー フィルターを使用する場合、 **[が次を含む]** では、コンマ、ピリオド、スペースまたはアンダースコアで区切られた **完全な単語** のみが検索されます。
>
> - 単語間のスペースは OR のように機能します。たとえば、**malware** **virus** を検索すると、名前に malware または virus が含まれるすべてのファイルが検索されるため、malware-virus.exe と virus.exe の両方が検出されます。
> - 文字列を検索する場合は、単語を引用符で囲みます。 これは AND のように機能します。たとえば、 **"malware"** **"virus"** を検索すると、virus_malware_file.exe が検出されますが、malwarevirusfile.exe や malware.exe は検出されません。 しかし、完全に一致する文字列が検索されます。 **"malware virus"** を検索すると、 **"virus"** や **"virus_malware"** は検出されません。
>
> **[が次と等しい]** では、完全な文字列のみが検索されます。たとえば、**malware.exe** を検索すると、malware.exe は検出されますが、malware.exe.txt は検出されません。

- **アクセス レベル** – パブリック、外部、内部、またはプライベートの共有アクセス レベル。  外部ファイルの詳細については、[全般セットアップのポータルの設定](getting-started-with-cloud-app-security.md)に関するページを参照してください

    - **内部** - [全般セットアップ](General-setup.md)で設定した内部ドメイン内のすべてのファイル。
    - **外部** - 設定した内部ドメイン内にない場所に保存されたすべてのファイル。
    - **共有** - プライベートより上の共有レベルのファイル。 次のような共有があります。
        - 内部共有 - 内部ドメイン内で共有されているファイル。
        - 外部共有 - 内部ドメインに一覧表示されていないドメインで共有されているファイル。
        - リンクによる公開 - リンクを使用してすべてのユーザーと共有できるファイル。
        - パブリック - インターネットを検索することで検出できるファイル。

      > [!NOTE]
      > 外部ユーザーによって接続済みのストレージ アプリで共有されるファイルは、Cloud App Security によって次のように処理されます。
      >
      > - **OneDrive:** OneDrive では、外部ユーザーによって OneDrive に配置されたすべてのファイルの所有者として、内部ユーザーを割り当てます。 その後、これらのファイルは組織が所有しているものと見なされるため、Cloud App Security でこれらのファイルがスキャンされ、OneDrive 内の他のすべてのファイルの場合と同様に、ポリシーが適用されます。
      > - **Google Drive:** Google Drive ではこれらは外部ユーザーが所有しているものと見なされ、組織が所有していないファイルとデータに対する法的制約により、Cloud App Security からはこれらのファイルにアクセスできません。
      > - **Box:** Box では外部所有ファイルがプライベート情報と見なされるため、Box のグローバル管理者はファイルの内容を表示することはできません。 このため、Cloud App Security からはこれらのファイルにアクセスできません。
      > - **Dropbox:** Dropbox では外部所有ファイルはプライベート情報と見なされるため、Dropbox のグローバル管理者はファイルの内容を表示することはできません。 このため、Cloud App Security からはこれらのファイルにアクセスできません。

- **アプリ** – これらのアプリ内のファイルのみを検索します。

- **コラボレーター** – 特定のコラボレーター グループを含めるか除外します。

    - **ドメインのすべてのユーザー** – このドメインのすべてのユーザーがファイルにアクセスできる場合。

    - **組織全体** – 組織全体がファイルにアクセスできる場合。

    - **グループ** – 特定のグループがファイルにアクセスできる場合。 グループは、Active Directory やクラウド アプリからインポートすることも、サービスで手動で作成することもできます。

    - **ユーザー** – ファイルにアクセスできる可能性のある特定のユーザー セット。

- **作成日時** - ファイルの作成日時。 フィルターでは、日付の前後と日付の範囲がサポートされます。

- **拡張子** – 特定のファイル拡張子に焦点を当てます。 たとえば、実行可能ファイル (exe) であるすべてのファイルなどです。

- **ファイル ID** – 特定のファイル ID を検索します。ファイル ID は、特定の重要度の高いファイルを、所有者、場所、名前に頼らずに追跡できるようにする高度な機能です。

- **ファイル名** – クラウド アプリで定義されている名前のファイル名またはサブ文字列。たとえば、名前にパスワードが含まれるすべてのファイルなどです。

- **分類ラベル** - 特定のタグが設定されたファイルを検索します。 ラベルは次のいずれかです。
    - **Azure Information Protection タグ** - Azure Information Protection との統合が必要です。
    - **Cloud App Security タグ** - スキャンされるファイルに関するより詳細な分析情報が提供されます。 Cloud App Security DLP でスキャンされるファイルごとに、ファイルが暗号化されているか破損しているために検査がブロックされたかどうかがわかります。 たとえば、アラートを生成するポリシーを設定して、外部で共有されているパスワード保護されたファイルの検疫を行うことができます。
        - **Azure RMS 暗号化** – Azure RMS 暗号化が設定されているために内容が検査されなかったファイル。
        - **パスワードの暗号化** – ユーザーによってパスワード保護されているために内容が検査されなかったファイル。
        - **破損ファイル** – 内容を読み取れなかったために内容が検査されなかったファイル。

- **ファイルの種類** – Cloud App Security では、サービスから受信した MIME の種類 (表を参照) が取得され、ファイルがスキャンされて実際のファイルの種類が判断されます。 このスキャンは、データ スキャンに関連するファイル (ドキュメント、画像、プレゼンテーション、スプレッドシート、テキスト、zip/アーカイブ ファイル) が対象です。 フィルターは、ファイルまたはフォルダーの種類ごとに機能します。 たとえば、... であるすべてのフォルダー、または ... であるすべてのスプレッドシート ファイルなどです。

    | MIME の種類 (MIME type) | ファイルの種類 |
    |--|--|
    | - application/vnd.openxmlformats-officedocument.wordprocessingml.document<br />- application/vnd.ms-word.document.macroEnabled.12<br />- application/msword<br />- application/vnd.oasis.opendocument.text<br />- application/vnd.stardivision.writer<br />- application/vnd.stardivision.writer-global<br />- application/vnd.sun.xml.writer<br />- application/vnd.stardivision.math<br />- application/vnd.stardivision.chart<br />- application/x-starwriter<br />- application/x-stardraw<br />- application/x-starmath<br />- application/x-starchart<br />- application/vnd.google-apps.document<br />- application/vnd.google-apps.kix<br />- application/pdf<br />- application/x-pdf<br />- application/vnd.box.webdoc<br />- application/vnd.box.boxnote<br />- application/vnd.jive.document<br />- text/rtf<br />- application/rtf | マニュアル名の正式名称 |
    | - application/vnd.oasis.opendocument.image<br />- application/vnd.google-apps.photo<br />- **次で始まるもの:** image/ | Image |
    | - application/vnd.openxmlformats-officedocument.presentationml.presentation<br />- application/vnd.ms-powerpoint.template.macroEnabled.12<br />- application/mspowerpoint<br />- application/powerpoint<br />- application/vnd.ms-powerpoint<br />- application/x-mspowerpoint<br />- application/mspowerpoint<br />- application/vnd.ms-powerpoint<br />- application/vnd.oasis.opendocument.presentation<br />- application/vnd.sun.xml.impress<br />- application/vnd.stardivision.impress<br />- application/x-starimpress<br />- application/vnd.google-apps.presentation | プレゼンテーション |
    | - application/vnd.openxmlformats-officedocument.spreadsheetml.sheet<br />- application/vnd.ms-excel.sheet.macroEnabled.12<br />- application/excel<br />- application/vnd.ms-excel<br />- application/x-excel<br />- application/x-msexcel<br />- application/vnd.oasis.opendocument.spreadsheet<br />- application/vnd.sun.xml.calc<br />- application/vnd.stardivision.calc<br />- application/x-starcalc<br />- application/vnd.google-apps.spreadsheet | スプレッドシート |
    | - **次で始まるもの:** text/ | Text |
    | その他すべてのファイルの MIME の種類 | その他 |

    ![policy_種類でのファイル フィルター](media/policy_file-filters-type.png)

- **ごみ箱** – ごみ箱フォルダーのファイルを除外するか含めます。 これらのファイルは引き続き共有され、リスクが生じる可能性があります。

    ![policy_ごみ箱でのファイル フィルター](media/policy_file-filters-trash.png)

- **最終更新日時** – ファイルの変更時刻。 このフィルターでは、日付の前後、日付の範囲、相対的な日時表現がサポートされます。 たとえば、過去 6 か月間に変更されていないすべてのファイルなどです。

- **一致したポリシー** - アクティブな Cloud App Security ポリシーと一致したファイル。

- **MIME の種類** – ファイルの MIME の種類を確認します。自由形式のテキストが受け入れられます。

- **所有者** - 特定のファイル所有者を含めるか除外します。 たとえば、rogue_employee_#100 によって共有されているすべてのファイルを追跡します。

- **所有者 OU** – 特定の組織グループに属するファイル所有者を含めるか除外します。 たとえば、EMEA_marketing によって共有されているファイルを除くすべてのパブリック ファイルなどです。 Google Drive に格納されているファイルにのみ適用されます。

- **親フォルダー** – 親フォルダーに基づいて含めるか除外します。 たとえば、このフォルダー内のファイルを除くすべての公開共有ファイルなどです。

    > [!NOTE]
    > Cloud App Security は、それらのファイルに対していくつか操作が加えられた後でのみ、新しい SharePoint フォルダーと OneDrive フォルダーを検出します。

- **検疫済み** – サービスによって検疫されたファイルです。たとえば、検疫されたすべてのファイルを表示します。

また、 **[適用対象]** フィルターを設定して、特定のファイルに対して実行するようにポリシーを設定することもできます。 **[すべてのファイル]** 、 **[選ばれたフォルダー]** 、または **[選ばれたフォルダーを除くすべてのファイル]** でフィルター処理します。 その後、関連するファイルまたはフォルダーを選択します。

![適用対象フィルター](media/apply-to-filter.png "適用対象フィルター")
<!--
>[!NOTE]
> If at any point you want to clear the filters, you can do so by clicking the clear filters icon ![clear filters icon](media/clear-filters.png).
-->

## <a name="authorizing-files"></a>ファイルの承認

Cloud App Security によって、マルウェアまたは DLP リスクの原因としてファイルが特定された後、ファイルを調査することをお勧めします。 ファイルが安全であると判断した場合は、それらを承認できます。 承認したファイルはマルウェアの検出レポートから削除され、このファイルに対する今後の一致が抑制されます。

### <a name="to-authorize-files"></a>ファイルを承認するには

1. Cloud App Security で、 **[制御]** 、 **[ポリシー]** の順にクリックします。
1. ポリシーの一覧にある、調査をトリガーしたポリシーが表示されている行の **[カウント]** 列で、一致リンクをクリックします。

    > [!TIP]
    > 種類でポリシーの一覧をフィルター処理できます。 次の表には、リスクの種類ごとに、使用するフィルターの種類が示されています。
    >
    > | リスクの種類 | フィルターの種類 |
    > | --- | --- |
    > | DLP | [ファイル ポリシー] |
    > | マルウェア | マルウェアの検出ポリシー |

1. 一致したファイルの一覧で、調査対象のファイルが表示されている行の **[承認]** をクリックします。

## <a name="working-with-the-file-drawer"></a>ファイル ドロワーの操作

ファイル ログでファイル自体をクリックすると、各ファイルの詳細情報を表示できます。 クリックすると **ファイル ドロワー** が開き、ファイルに対して実行できる以下の追加アクションが示されます。

- **URL** - ファイルの場所に移動します。
- **ファイル ID** - ファイル ID と暗号化キーを含む、ファイルについての生データの詳細を示すポップアップが開きます。
- **所有者** - このファイルの所有者のユーザー ページを表示します。
- **一致するポリシー** - ファイルが一致したポリシーの一覧を表示します。
- **分類ラベル** - このファイルで見つかった Azure Information Protection 分類ラベルの一覧を表示します。 その後、このラベルに一致するすべてのファイルでフィルター処理することができます。

ファイル ドロワーのフィールドでは、その他のファイルへのコンテキスト リンクが提供されており、ドリルダウンしてドロワーから直接実行することができます。 たとえば、 **[所有者]** フィールドの横にカーソルを移動すると、[フィルターに追加] アイコン ![フィルターに追加](media/add-to-filter-icon.png) を使用して、現在のページのフィルターに所有者をすぐに追加することができます。 歯車の設定アイコン ![設定アイコン](media/contextual-settings-icon.png) を使用して、設定ページを直接ポップアップで開き、 **[分類ラベル]** など、フィールドのいずれかの構成を変更することもできます。

![ファイル ドロワー](media/file-drawer.png "ファイル ドロワー")

使用できるガバナンス アクションの一覧については、「[ファイル ガバナンス アクション](governance-actions.md#file-governance-actions)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]