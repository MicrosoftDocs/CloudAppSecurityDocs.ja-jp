---
title: Cloud App Security でのユーザー データの匿名化
description: この記事では、Cloud Discovery データ内のユーザー名を匿名化して、ユーザーのプライバシーを保護する方法について説明します。
ms.date: 04/20/2020
ms.topic: how-to
ms.openlocfilehash: bb8befb8c65f766118f6a3221b382c6699b17a0e
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96313527"
---
# <a name="cloud-discovery-data-anonymization"></a>Cloud Discovery データの匿名化

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud Discovery データを匿名化することで、ユーザーのプライバシーを保護することができます。 データ ログが Microsoft Cloud App Security ポータルにアップロードされると、ログはサニタイズされ、すべてのユーザー名情報が暗号化されたユーザー名に置き換えられます。 このように、すべてのクラウド アクティビティの匿名が維持されます。 必要に応じて、(セキュリティ違反や疑わしいユーザー アクティビティが発生した場合などに) 特定のセキュリティ調査を行うために、管理者は実際のユーザー名を解決することができます。 管理者は、特定のユーザーを疑う理由がある場合、既知のユーザー名の暗号化されたユーザー名を調べ、暗号化されたユーザー名を使用して調査を開始することもできます。 ユーザー名の各変換はポータルの **ガバナンス ログ** で監査されます。

重要なポイント:

- 個人情報は保存も、表示もされません。 暗号化された情報のみが保存され、表示されます。
- 個人データは、テナントごとに専用のキーで AES-128 を使用して暗号化されます。
- ユーザー名の解決は、指定の暗号化されたユーザー名を解読することで、ユーザー名ごとに随時行われます。

## <a name="how-data-anonymization-works"></a>データの匿名化のしくみ

1. データの匿名化を適用する方法は次の 3 つです。

    - [新しいスナップショット レポートを作成](create-snapshot-cloud-discovery-reports.md)し、 **[個人情報の匿名化]** を選択して、特定のログ ファイルのデータを匿名化するように設定できます。  
    ![スナップショット データの匿名化](media/anonymize-log.png)

    - 新しいデータ ソースを追加するときに **「Anonymize private information」** (個人情報の匿名化) を選択し、[新しいデータ ソースの自動アップロード](configure-automatic-log-upload-for-continuous-reports.md)に関するページを参照してデータを匿名化するように設定できます。  
    ![ログ データの匿名化](media/anonymize-autolog.png)

    - 次のように、アップロードされたログ ファイルからのスナップショット レポートと、ログ コレクタからの継続的レポートの両方からのデータをすべて匿名化するように、Cloud App Security で既定値を設定できます。

    1. **[設定]**  >  **[Cloud Discovery 設定]** の順に選択します。

    2. 既定でユーザー名が匿名化されるようにするには、 **[匿名化]** タブで、 **[既定で新しいレポートやデータ ソースで個人情報を匿名化します]** を選択します。 **[Anonymize device information by default in 'Win10 Endpoint Users' report]\(既定で 'Win10 エンドポイント ユーザー' レポートでデバイス情報を匿名化する\)** を選択することもできます。
    3. **[Save]** (保存) をクリックします。

    ![匿名化の設定ページ](media/anonymizer1.png)

2. 匿名化を選択すると、Cloud App Security はトラフィック ログを解析し、特定のデータ属性を抽出します。
3. Cloud App Security はユーザー名を暗号化されたユーザー名に置き換えます。
4. 次に、クラウドの使用状況データを分析し、匿名化されたデータに基づいて Cloud Discovery レポートを生成します。

    ![Cloud Discovery ダッシュボードの匿名化](media/anonymize-dashboard.png)

5. 異常な使用量のアラート調査など、特定の調査のために、ポータルで特定のユーザー名を解決し、業務上の正当な理由を示すことができます。

    > [!NOTE]
    > 次の手順は、 **[デバイス]** タブのデバイス名にも使用できます。

    **1 つのユーザー名を解決するには**

    1. 解決するユーザーの行の末尾にある 3 つの点をクリックし、 **[ユーザーの匿名化の解除]** を選択します。

        ![匿名化ユーザー テーブル](media/anonymize-user-table.png)

    1. ポップアップで、ユーザー名を解決する理由を入力し、 **[解決]** をクリックします。 該当する行に、解決済みのユーザー名が表示されます。

        > [!NOTE]
        > このアクションは監査されます。

        ![匿名化の解決ポップアップ](media/anonymize-resolve-dialog.png)

    1 つのユーザー名を解決する別の方法として、次のように既知のユーザー名の暗号化されたユーザー名を検索することもできます。

    1. 「設定」 (歯車アイコン) の **[Cloud Discovery 設定]** を選択します。

    1. **[匿名化]** タブの **[Anonymize and resolve usernames]** \(ユーザー名の匿名化と解決\) で、解決を行う理由を入力します。
    1. **「Enter username to resolve」** (解決するユーザー名を入力してください) で、 **「From anonymized」** (匿名化されたユーザー名を基にする) を選択して匿名化されたユーザー名を入力するか、 **「To anonymized」** (匿名化されたユーザー名の実データを基にする) を選択して、解決する元のユーザー名を入力します。 **[解決]** をクリックします。

        ![匿名化の解決のポップアップ](media/anonymizer.png)

    **複数のユーザー名を解決するには**

    1. 解決するユーザーの近くにあるユーザー アイコンにマウス ポインターを置いたときに表示されるチェックボックスをオンにするか、左上隅にある **[一括選択]** チェックボックスをオンにします。

        ![匿名化の一括解決](media/anonymize-bulk-resolve.png)

    1. **[ユーザーの匿名化解除]** をクリックします。
    1. ポップアップで、ユーザー名を解決する理由を入力し、 **[解決]** をクリックします。 該当する行に、解決済みのユーザー名が表示されます。

        > [!NOTE]
        > このアクションは監査されます。

        ![匿名化の解決ポップアップ](media/anonymize-resolve-dialog.png)

6. アクションはポータルの **ガバナンス ログ** で監査されます。

    ![ガバナンス ログの匿名化アクション](media/anonymize-gov-log.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
