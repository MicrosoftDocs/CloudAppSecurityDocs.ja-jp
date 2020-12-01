---
title: サポートされていないログ用の Cloud App Security カスタム ログ パーサー
description: この記事では、カスタム ログ パーサーを使用して、Cloud App Security に対してサポートされていないデバイスのログをアップロードする方法について説明します。
ms.date: 12/10/2018
ms.topic: how-to
ms.openlocfilehash: a70e7930dcbf1d5932c02beeb03d006f6229c705
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96312023"
---
# <a name="use-a-custom-log-parser"></a>カスタム ログ パーサーを使用する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Cloud App Security では、Cloud Discovery に使用できるように、ログの形式を一致させて処理するためのカスタム パーサーを構成できます。 通常、ファイアウォールまたはデバイスが Cloud App Security によって明示的にサポートされていない場合に、カスタム パーサーを使用します。 CSV パーサーまたはカスタム キー値パーサーを使用できます。

カスタム パーサーを使用すると、このプロセスに従って、サポートされていないファイアウォールからのログを使用できます。

カスタム パーサーを構成するには:

1. Cloud App Security ポータルで **[探索]** をクリックし、 **[新しいスナップショット レポートの作成]** をクリックします。

    ![新しいスナップショット レポートを作成する](media/create-new-snapshot-report.png)

2. **[レポート名]** と **[説明]** を入力します。

3. **[データ ソース]** で、 **[カスタム ログ形式...]** を選択します。

    ![新しいスナップショット レポート](media/custom-log-upload.png)

4. 組織のユーザーがインターネット アクセスに使用するファイアウォールとプロキシからログを収集します。 組織内のすべてのユーザー アクティビティを示す、トラフィック ピーク時のログを収集するようにしてください。

5. 処理するログをテキスト エディターで開きます。 形式を確認し、ログでの列名が **[カスタム ログ形式]** 画面のフィールドに対応していることを確認します。

    ![カスタム ログ パーサーのフィールドの確認](media/log-data.png)

6. 次に、データに基づいてフィールドに入力し、データ内の列と Cloud App Security での特定のフィールドとの関連付けを示します。 適切に関連付けるためには、ログ ファイル内の列名を変更することが必要になる場合があります。

    > [!NOTE]
    > フィールドは大文字と小文字が区別されます。 Cloud App Security とログ ファイルで列の名前が同じように入力されていることを確認します。 また、選択した日付形式が同じであることを確認します。

    ![カスタム ログ パーサーのフィールドの入力](media/custom-log-parser.png)

7. **[Save]** (保存) をクリックします。 構成したカスタム ログ形式は、既定のカスタム パーサーとして保存されます。 **[編集]** をクリックして、いつでもそれを編集できます。

8. **[Choose the traffic logs]\(トラフィック ログの選択\)** で、変更したログファイルを選択してアップロードします。 一度に最大 20 個のファイルをアップロードできます。 圧縮された ZIP 形式のファイルもサポートされます。

9. **[作成]** をクリックします。

10. アップロードが完了すると、ログが正常にアップロードされたことを通知するステータス メッセージが画面右上隅に表示されます。

11. ログ ファイルのアップロード後、ファイルの解析および分析には多少時間がかかります。
    ログ ファイルの処理が完了すると、終了したことを通知する電子メールを受信します。

12. 通知バナーが、**Cloud Discovery ダッシュボード** の上部にあるステータス バーに表示されます。 バナーにより、ログ ファイルの最新の処理状態が通知されます。
    ![処理中のログ ファイル メニュー バー](media/processing-log-file-menu-bar.png)

13. ログが正常にアップロードされると、ログ ファイルの処理が正常に完了したことを知らせる通知が表示されます。 この時点で、ステータス バーのリンクをクリックするか、設定の歯車アイコンに移動して [ **[Cloud Discovery settings]\(Cloud Discovery の設定\)** ] を選択することで、レポートを表示できます。

    ![Discovery の [設定] タブ](media/discovery-settings-tab.png)
14. **[スナップショット レポートの管理]** を選択し、スナップショット レポートを選択します。

    ![スナップショット レポートの管理](media/snapshot-report-managment.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery のスナップショット レポートを作成する](create-snapshot-cloud-discovery-reports.md)

> [!div class="nextstepaction"]
> [継続的なレポートのために自動ログ アップロードを構成する](configure-automatic-log-upload-for-continuous-reports.md)

> [!div class="nextstepaction"]
> [Cloud Discovery データでの作業](working-with-cloud-discovery-data.md)

[!INCLUDE [Open support ticket](includes/support.md)]
