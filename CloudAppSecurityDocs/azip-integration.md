---
title: Azure Information Protection を Cloud App Security と統合する
description: この記事では、Cloud App Security で Azure Information Protection タグを活用して、組織のクラウド アプリの使用状況をさらに制御する方法について説明します。
ms.date: 12/27/2020
ms.topic: how-to
ms.openlocfilehash: 2b5d3399479850d04caba7f6e7f0411c4429b4a6
ms.sourcegitcommit: 243baad1adeb32d157c7f6165c08df2136b28db0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/27/2020
ms.locfileid: "97792775"
---
# <a name="azure-information-protection-integration"></a>Azure Information Protection の統合

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security を使用すると、Azure Information Protection 分類ラベル (保護あり、または保護なし) をファイル ポリシーのガバナンス アクションとして、自動的にファイルに適用することができます。 また、Cloud App Security ポータル内で、適用された分類ラベルをフィルタリングしてファイルを調査することもできます。 分類を使用すると、クラウドでの機密データの可視性と制御が大幅に向上します。 Azure Information Protection と Cloud App Security の統合は、1 つのチェック ボックスをオンにするだけで簡単に行うことができます。

> [!NOTE]
> この記事は、Office 365 の統合秘密度ラベルにも関連します (既に [Office 365 セキュリティ/コンプライアンス センターのために分類ラベルを移行](/azure/information-protection/configure-policy-migrate-labels)している場合)。 既存の分類ラベルを移行せずに、Office 365 セキュリティ/コンプライアンス センターで新しいラベルの作成を開始した場合、Cloud App Security では Azure Information Protection ポータルで構成された既存のラベルしか使用されません。

Azure Information Protection を Cloud App Security に統合することによって、次のように、両方のサービスのすべての機能を使用でき、クラウドでファイルをセキュリティ保護できます。

- 特定のポリシーと一致するファイルに、ガバナンス アクションとして分類ラベルを適用する機能
- 分類されたすべてのファイルを 1 か所で表示する機能
- 分類レベルに従って調査を行い、クラウド アプリケーションを介したの機密データの公開を定量化する機能
- 分類されたファイルが適切に処理されるようにポリシーを作成する機能

## <a name="prerequisites"></a>前提条件

> [!NOTE]
> この機能を有効にするには、Cloud App Security のライセンスと Azure Information Protection Premium P1 のライセンスの両方が必要です。 両方のライセンスの準備が整うとすぐに、Cloud App Security によって Azure Information Protection サービスからの組織のラベルの同期が行われます。

- Azure Information Protection の統合を進めるには、[Office 365 のアプリ コネクター](connect-office-365-to-microsoft-cloud-app-security.md)を有効にする必要があります。

Cloud App Security でラベルを使用するには、ラベルをポリシーの一部として公開する必要があります。 Azure Information Protection を使用している場合は、Azure Information Protection ポータルでラベルを公開する必要があります。 統合ラベルに移行した場合は、Office 365 セキュリティ/コンプライアンス センターからラベルを公開する必要があります。

現在、Cloud App Security は、次のファイルの種類について Azure Information Protection 分類ラベルの適用をサポートしています。

- Word: docm、docx、dotm、dotx
- Excel: xlam、xlsm、xlsx、xltx
- PowerPoint: potm、potx、ppsx、ppsm、pptm、pptx
- PDF
  > [!NOTE]
  > PDF の場合は、統合ラベルを使用する必要があります。

この機能は現在、Box、Google Workspace、SharePoint Online、OneDrive for Business に格納されているファイルで使用できます。 今後のバージョンでは、サポートされるクラウド アプリが増える予定です。

## <a name="how-it-works"></a>しくみ

おそらく、[Azure Information Protection](/azure/information-protection/what-is-information-protection) のファイル分類ラベルについてはよく理解しているでしょう。 Azure Information Protection の分類タグが Cloud App Security に表示されます。 Cloud App Security を Azure Information Protection と統合するとすぐに、Cloud App Security は次のようにファイルをスキャンします。

1. Cloud App Security が、テナントで使用されているすべての分類ラベルの一覧を取得します。 この処理は、一覧を最新の状態に保つために 1 時間おきに実行されます。

2. Cloud App Security は、次のようにファイルをスキャンして分類ラベルを探します。

    - 自動スキャンを有効にすると、新規または変更されたすべてのファイルがスキャン キューに追加され、既存のすべてのファイルとリポジトリがスキャンされます。
    - 分類ラベルを検索するようにファイル ポリシーを設定すると、これらのファイルが分類ラベルのスキャン キューに追加されます。

3. 前述のように、これらのスキャンが対象とするのは、テナントで使用されている分類ラベルを確認するために Cloud App Security が行った最初のスキャンで検出された分類ラベルです。 外部ラベル (テナント外部のユーザーによって設定された分類ラベル) が、分類ラベルの一覧に追加されます。 これらをスキャンしない場合は、 **[Only scan files for Azure Information Protection classification labels from this tenant]\(このテナントの Azure Information Protection 分類ラベルについてのみファイルをスキャンする\)** チェックボックスをオンにします。

4. Cloud App Security で Azure Information Protection を有効にすると、接続されているクラウド アプリに追加されたすべての新しいファイルで分類ラベルがスキャンされます。

5. Cloud App Security 内に新しいポリシーを作成して、分類ラベルを自動的に適用できます。

> [!NOTE]
>
> - Cloud App Security の外部で保護ありとしてラベル付けされたファイルは、Cloud App Security では変更できません。 ただし、[保護されたファイルのコンテンツ検査](content-inspection.md#content-inspection-for-protected-files)のアクセス許可を付与することで、これらのファイルをスキャンできます。
> - 反対に、ファイル が Cloud App Security によってラベル付けされて SharePoint または OneDrive にアップロードされ、サービス プリンシパル名からアカウントを使用してラベルで暗号化が適用されると、ファイルを Web 上の Office で開くことはできません。 シナリオの例としては、Cloud App Security や、メールで Teams に送信されるファイルなどがあります。

## <a name="how-to-integrate-azure-information-protection-with-cloud-app-security"></a>Azure Information Protection を Cloud App Security と統合する方法

### <a name="enable-azure-information-protection"></a>Azure Information Protection を有効にする

Azure Information Protection と Cloud App Security を統合するために行うのは、1 つのチェックボックスをクリックするだけです。 自動スキャンを有効にすると、ポリシーを作成しなくても、Office 365 ファイルで Azure Information Protection 分類ラベルを検索できるようになります。 有効にした後で、Azure Information Protection 分類ラベルのラベルが付いたファイルがクラウド環境内にある場合、Cloud App Security に表示されます。

Cloud App Security で、コンテンツ検査を有効にして分類ラベルについてファイルをスキャンできるようにするには、次のようにします。

1. Cloud App Security の設定の歯車アイコンで、 **[システム]** 見出しの下にある **[設定]** ページを選択します。

    ![[設定] メニュー](media/azip-system-settings.png)
1. **[Azure Information Protection]** で、 **[Azure Information Protection 分類ラベルの新しいファイルの自動スキャン]** を選択します。

    ![Azure Information Protection を有効にする](media/enable-azip.png)

Azure Information Protection を有効にすると、分類ラベルが付いているファイルを表示し、Cloud App Security でラベルによってフィルタリングできます。 Cloud App Security がクラウド アプリに接続されたら、Azure Information Protection 統合機能を使用して、Cloud App Security ポータルで Azure Information Protection 分類ラベル (保護あり、または保護なし) を適用することができます。これは、ファイルに直接追加するか、ガバナンス アクションとして分類ラベルを自動的に適用するファイル ポリシーを構成することで行います。

> [!NOTE]
> 自動スキャンでは、既存のファイルは変更されない限りスキャンされません。 既存のファイルで Azure Information Protection 分類ラベルについてスキャンするには、コンテンツ検査を含む **ファイル ポリシー** が少なくとも 1 つ必要です。 ない場合は、新しい **ファイル ポリシー** を作成し、 **[検査方法]** の下で事前設定されたすべてのフィルターを削除し、 **[組み込み DLP]** を選択します。 **[コンテンツ検査]** フィールドで、 **[事前設定した式と一致するファイルを含める]** を選択し、事前定義された値を選択して、ポリシーを保存します。 これにより、Azure Information Protection 分類ラベルを自動的に検出するコンテンツ検査が有効になります。

#### <a name="set-internal-and-external-tags"></a>内部タグと外部タグを設定する

既定では、Cloud App Security は、組織内で定義された分類ラベルだけでなく、他の組織で定義された外部ラベルもスキャンします。

組織の外部で設定された分類ラベルを無視するには、Cloud App Security ポータルで、 **[設定]** の **[Azure Information Protection]** に移動します。 **[Only scan files for Azure Information Protection classification labels and content inspection warnings from this tenant]\(Azure Information Protection 分類ラベルとこのテナントのコンテンツ検査警告についてのみファイルをスキャンする\)** を選択します。

![ラベルを無視](media/azip-ignore.png)

### <a name="apply-labels-directly-to-files"></a>ファイルにラベルを直接適用する

1. **[ファイル]** ページの **[調査]** で、保護するファイルを選択します。 ファイルの行の末尾にある 3 つの点をクリックし、 **[分類ラベルの適用]** を選択します。

    ![アプリを保護](media/protect-app.png)

    >[!NOTE]
    > Cloud App Security は、50 MB までのファイルに Azure Information Protection を適用できます。

2. ファイルに適用する組織の分類ラベルの 1 つを選択するように求められます。その後、 **[適用]** をクリックします。

    ![保護分類ラベル](media/protect-template.png)

3. 分類ラベルを選択して [適用] をクリックすると、Cloud App Security によって分類ラベルが元のファイルに適用されます。

4. **[分類ラベルの削除]** オプションを選択すると、分類ラベルを削除することもできます。

> [!NOTE]
> ラベルを削除できるのは、保護が含まれておらず、Cloud App Security 内から適用された場合のみです。Information Protection で直接適用されたラベルはできません。

Cloud App Security と Azure Information Protection の連携の詳細については、「[Azure Information Protection 分類ラベルを自動的に適用する](use-case-information-protection.md)」を参照してください。

### <a name="automatically-label-files"></a>ファイルに自動的にラベルを付ける

分類ラベルをファイルに自動的に適用するには、ファイル ポリシーを作成し、ガバナンス アクションとしての **[分類ラベルの適用]** を設定します。

ファイル ポリシーを作成するには、次の手順に従います。

1. ファイル ポリシーを作成します。
2. 検出するファイルの種類を含めてポリシーを設定します。 たとえば、 **[アクセス レベル]** が **[内部]** と等しくなく、 **[所有者 OU]** が財務チームと等しいすべてのファイルを選択します。
3. 関連するアプリのガバナンス アクションで、 **[分類ラベルの適用]** をクリックしてから、ラベルの種類を選択します。

    ![ラベルを適用](media/aip-gov-action.png)

> [!NOTE]
>
> - ファイル ポリシーを介して、Azure Information Protection のラベルを自動的に適用する機能は強力です。 お客様が多数のファイルに誤ってラベルを適用することを防ぐための安全策として、アプリごと、テナントごとに 1 日に実行できる **ラベルの適用** 操作は 100 回に制限されています。 1 日の上限に達すると、ラベルの適用操作は一時的に停止し、翌日 (UTC 12 時 00分 を過ぎてから) に自動的に再開します。 テナントの上限を引き上げるには、サポート チケットを開きます。
> - ポリシーを無効にすると、そのポリシーのすべての保留中ラベル付けタスクが一時停止されます。

### <a name="control-file-exposure"></a>ファイルの公開を制御する

- たとえば、次に示すのは、Azure Information Protection 分類ラベルでラベル付けしたドキュメントです。

    ![Azure Information Protection サンプル画面](media/azip-screen.png)

- **[ファイル]** ページで、Azure Information Protection の分類ラベルでフィルタリングすると、このドキュメントを Cloud App Security で表示できます。

    ![Cloud App Security と Azure Information Protection の比較](media/cas-compared-azip.png)

- これらのファイルとその分類ラベルの詳細は、ファイル ドロワーで確認できます。 **[ファイル]** ページで関連するファイルをクリックするだけで、分類ラベルがあるかどうかを確認できます。

    ![ファイル ドロワー](media/azip-file-drawer.png)

- 次に、Cloud App Security でファイル ポリシーを作成して、不適切に共有されているファイルを制御したり、ラベルが付いている最近変更されたファイルを見つけたりできます。

- 分類ラベルを特定のファイルに自動的に適用するポリシーを作成できます。
- また、ファイル分類に関連するアクティビティについてアラートをトリガーすることもできます。

> [!Note]
> Azure Information Protection ラベルがファイルで無効になると、無効になったラベルは Cloud App Security でも無効であると表示されます。 削除されたラベルは表示されません。

**サンプル ポリシー - Box で外部共有されている機密データ:**

1. ファイル ポリシーを作成します。
2. ポリシーの名前、重要度、およびカテゴリを設定します。
3. Box で外部共有されているすべての機密データを検索するには、次のフィルターを追加します。

    ![機密性ポリシー](media/azip-confidentiality-policy.png)

**サンプル ポリシー - SharePoint の Finance フォルダー以外で最近変更された制限付きデータ:**

1. ファイル ポリシーを作成します。
2. ポリシーの名前、重要度、およびカテゴリを設定します。
3. フォルダー選択オプションで Finance フォルダーを除外し、最近変更されたすべての制限付きファイルを検索するために、次のフィルターを追加します。

    ![制限付きデータ ポリシー](media/azip-restricted-data-policy.png)

また、アラートやユーザー通知を設定したり、これらのポリシーに対して直ちにアクションを実行したりすることもできます。
ガバナンス アクションの詳細については[こちら](governance-actions.md)を参照してください。

[Azure Information Protection](/information-protection/understand-explore/what-is-information-protection) の詳細を確認し、Azure Information Protection の[クイック スタート チュートリアル](/information-protection/get-started/infoprotect-quick-start-tutorial)もご覧ください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

## <a name="related-videos"></a>関連ビデオ

> [!div class="nextstepaction"]
> [Cloud App Security と Azure Information Protection の統合](https://channel9.msdn.com/Shows/Microsoft-Security/MCAS--AIP-Integrations)

[!INCLUDE [Open support ticket](includes/support.md)]
