---
title: エンドポイントの修復までガバナンスを拡張する
description: このチュートリアルでは、Microsoft Power Automate ワークフローをトリガーして Microsoft Defender for Endpoint 修復アクションを実行するために、Microsoft Cloud App Security ポリシー アラートを構成するプロセスについて説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: tutorial
ms.date: 04/27/2020
ms.openlocfilehash: 213b041630a1367a4f505643e73482490456682d
ms.sourcegitcommit: 5367d8fdf99d61719a395728f2ef4b014604e3bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2020
ms.locfileid: "94370666"
---
# <a name="tutorial-extend-governance-to-endpoint-remediation"></a>チュートリアル:エンドポイントの修復までガバナンスを拡張する

Cloud App Security には、ユーザーを停止したり、ファイルを非公開にするなどの定義済みのポリシーのガバナンス オプションがあります。 Microsoft Power Automate とのネイティブ統合を使用すると、サービスとしてのソフトウェア (SaaS) コネクタの大規模なエコシステムを使用して、修復などのプロセスを自動化するワークフローを構築できます。

たとえば、危険なマルウェアである可能性の兆候が検出された場合、ワークフローを使用して、ウイルス対策スキャンの実行やエンドポイントの分離などの Microsoft Defender for Endpoint 修復アクションを開始できます。

このチュートリアルでは、ワークフローを使用するポリシー ガバナンス アクションを構成して、ユーザーが疑わしい動作をしているエンドポイントでウイルス対策スキャンを実行する方法について説明します。

> [!div class="checklist"]
>
> * 1:[Cloud App Security の API トークンを生成する](#generate-token)
> * 2:[ウイルス対策スキャンを実行するフローを作成する](#create-flow)
> * 3:[フローを構成する](#configure-flow)
> * 4:[フローを実行するポリシーを設定する](#configure-policy)

> [!NOTE]
> これらのワークフローは、ユーザー アクティビティを含むポリシーにのみ該当します。 たとえば、Discovery や OAuth のポリシーではこれらのワークフローは使用できません。

Power Automate プランがない場合は、[無料試用版アカウントにサインアップ](https://flow.microsoft.com/pricing)します。

## <a name="prerequisites"></a>[前提条件]

* 有効な [Microsoft Power Automate プランが必要](https://flow.microsoft.com/pricing)
* 有効な Microsoft Defender for Endpoint プランが必要
* Power Automate 環境が Azure AD と同期され、Defender for Endpoint の監視対象で、ドメイン参加済みである

## <a name="phase-1-generate-a-cloud-app-security-api-token"></a>フェーズ 1:Cloud App Security の API トークンを生成する<a name="generate-token"></a>

> [!NOTE]
> Cloud App Security コネクタを使用してワークフローを以前に作成している場合は、Power Automate によってトークンが自動的に再利用されるため、この手順を省略できます。

1. Cloud App Security のメニュー バーで設定の歯車 ![設定アイコン](media/settings-icon.png "設定アイコン") をクリックし、 **[セキュリティ拡張機能]** を選択します。

1. **[セキュリティ拡張機能]** ページで [+] ボタンをクリックして新しい API トークンを生成します。
1. **[新しいトークンの生成]** ポップアップに、トークン名 (たとえば "Flow-Token") を入力し、 **[生成]** をクリックします。

    ![名前入力と [生成] ボタンを示すトークンのウィンドウのスクリーンショット。](media/tutorial-flow-token-generate.png)
1. トークンが生成されたら、生成されたトークンの右側にあるコピー アイコンをクリックして、 **[閉じる]** をクリックします。 このトークンは後で必要になります。

    ![トークンとコピーの手順を示すトークン ウィンドウのスクリーンショット。](media/tutorial-flow-token-copy.png)

## <a name="phase-2-create-a-flow-to-run-an-antivirus-scan"></a>フェーズ 2:ウイルス対策スキャンを実行するフローを作成する<a name="create-flow"></a>

> [!NOTE]
> Defender for Endpoint コネクタを使用してフローを以前に作成している場合は、Power Automate によってコネクタが自動的に再利用されるため、 **サインイン** の手順を省略できます。

1. [Power Automate ポータル](https://flow.microsoft.com/)に移動し、 **[テンプレート]** を選択してください。

    ![テンプレートの選択を示す Power Automate のメイン ページのスクリーンショット。](media/tutorial-flow-templates.png)

1. "Cloud App Security" を検索し、 **[Run antivirus scan using Windows Defender upon a Cloud App Security alert]\(Cloud App Security アラート時に Windows Defender を使用してウイルス対策スキャンを実行する\)** を選択します。

    ![検索結果を示す Power Automate のテンプレート ページのスクリーンショット。](media/tutorial-flow-templates-search.png)

1. アプリの一覧で、 **Microsoft Defender for Endpoint コネクタ** が表示されている行で、 **[サインイン]** をクリックします。

    ![サインイン プロセスを示す Power Automate のテンプレート ページのスクリーンショット。](media/tutorial-flow-templates-signin.png)

## <a name="phase-3-configure-the-flow"></a>フェーズ 3:フローを構成する<a name="configure-flow"></a>

> [!NOTE]
> Azure AD コネクタを使用してフローを以前に作成している場合は、Power Automate によってトークンが自動的に再利用されるため、この手順を省略できます。

1. アプリの一覧で、 **[Cloud App Security]** が表示されている行で、 **[作成]** をクリックします。

    ![Cloud App Security の作成ボタンを示す Power Automate のテンプレート ページのスクリーンショット。](media/tutorial-flow-templates-create.png)

1. **Cloud App Security** のポップアップで、接続名 (たとえば "Cloud App Security トークン") を入力し、コピーした API トークンを貼り付けて、 **[作成]** をクリックします。

    ![名前とキーが入力された、[作成] ボタンがある [Cloud App Security] ウィンドウのスクリーンショット。](media/tutorial-flow-templates-create-window.png)

1. アプリの一覧で、 **[Azure AD を使用する HTTP]** が表示されている行で、 **[サインイン]** をクリックします。

1. **[Azure AD を使用する HTTP]** のポップアップで **[基本リソース URL]** と **[Azure AD リソース URI]** の両方のフィールドに「`https://graph.microsoft.com`」を入力し、 **[サインイン]** をクリックして、Azure AD コネクタを使用した HTTP で使用する管理者の資格情報を入力します。

    ![リソースのフィールドと [サインイン] ボタンがある [Azure AD を使用する HTTP] ウィンドウのスクリーンショット。](media/tutorial-flow-templates-azure.png)

1. **[続行]** をクリックします。

    ![完了したアクションと [続行] ボタンを示す、Power Automate のテンプレート ウィンドウのスクリーンショット。](media/tutorial-flow-templates-continue.png)

1. すべてのコネクタが正常に接続されたら、フローのページの **[Apply to each device]\(各デバイスに適用\)** で、必要に応じてコメントとスキャンの種類を変更し、 **[保存]** をクリックします。

    ![スキャンの設定セクションがある Flow ページのスクリーンショット。](media/tutorial-flow-templates-scan.png)

## <a name="phase-4-configure-a-policy-to-run-the-flow"></a>フェーズ 4:フローを実行するポリシーを設定する<a name="configure-policy"></a>

1. Cloud App Security で **[制御]** 、 **[ポリシー]** の順にクリックします。

1. ポリシー一覧の、該当するポリシーが表示されている行の行末の 3 つの点を選択し、 **[ポリシーの編集]** を選択します。

1. **[アラート]** の下の **[Flow にアラートを送信する]** を選択し、次いで **[Run antivirus scan using Windows Defender upon a Cloud App Security alert]** \(Cloud App Security アラート時に Windows Defender を使用してウイルス対策スキャンを実行する\) を選択します。

    ![アラート設定のセクションを示すポリシー ページのスクリーンショット。](media/tutorial-flow-templates-alerts.png)

これで、このポリシーに対して生成されたすべてのアラートで、ウイルス対策スキャンを実行するフローが開始されます。

このチュートリアルの手順を使用すると、Cloud App Security の修復機能を拡張するさまざまなワークフローを使用したアクションを作成できます。これには、その他の Defender for Endpoint アクションも含まれます。 Power Automate に定義済みの Cloud App Security ワークフローの一覧を表示するには、["Cloud App Security" を検索](https://go.microsoft.com/fwlink/?linkid=2102574)してください。

## <a name="see-also"></a>関連項目

> [!div class="nextstepaction"]
> [カスタム アラートの自動化のための Power Automate との統合](flow-integration.md)
