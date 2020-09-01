---
title: Microsoft Power Automate を Microsoft Cloud App Security と統合してカスタム アラートを自動化する
description: この記事では、Microsoft Power Automate と Cloud App Security を統合することによって、カスタム アラートの自動化を実現する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.openlocfilehash: c2d208fa3570f32719e247b006c831755ab80173
ms.sourcegitcommit: 870ca47381a36b4bc04e1ccb9b2a522944431fed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88963779"
---
# <a name="integrate-with-microsoft-power-automate-for-custom-alert-automation"></a>カスタム アラートの自動化のために Microsoft Power Automate と統合する

*適用対象:Microsoft Cloud App Security*

Cloud App Security と [Microsoft Power Automate](/flow/getting-started) を統合すると、カスタム アラートの自動化とオーケストレーションのプレイブックが提供されます。 Power Automate で利用できる[コネクタのエコシステム](/connectors/)を使用することにより、Cloud App Security でアラートが生成されたときのプレイブックのトリガーを自動化できます。 たとえば、[ServiceNow コネクタ](/connectors/service-now/)を使用してチケット システムで問題を自動的に作成したり、Cloud App Security でアラートがトリガーされたときにカスタム ガバナンス アクションを実行するための承認メールを自動的に送信したりできます。

## <a name="prerequisites"></a>[前提条件]

- 有効な [Microsoft Power Automate プランが必要](https://flow.microsoft.com/pricing)

## <a name="how-it-works"></a>しくみ

Cloud App Security 自体には、ポリシーを定義するときにユーザーを停止したり、ファイルを非公開にするなどの定義済みのガバナンス オプションがあります。 Cloud App Security コネクタを使用して Power Automate でプレイブックを作成することによって、ポリシーに対してカスタマイズされたガバナンス オプションを有効にするワークフローを作成できます。 Power Automate でプレイブックを作成したら、それを Cloud App Security のポリシーに関連付けて、Power Automate にアラートを送信するだけです。 Microsoft Power Automate では、組織に合わせてカスタマイズされたワークフローを作成するためのコネクタと条件がいくつか提供されています。

Power Automate の [Cloud App Security コネクタ](/connectors/cloudappsecurity/)では、自動化されたトリガーとアクションがサポートされています。 Cloud App Security によってアラートが生成されると、Power Automate が自動的にトリガーされます。 アクションには、Cloud App Security でのアラート状態の変更が含まれます。

## <a name="how-to-create-playbooks-with-power-automate"></a>Power Automate でプレイブックを作成する方法

1. Cloud App Security で [API トークンを作成します](api-tokens.md)。

2. [Power Automate ポータル](https://flow.microsoft.com)に移動し、 **[マイ フロー]** を選択し、 **[新規]** を選択して、ドロップダウンから **[自動 - 一から作成]** を選択します。

    ![Power Automate によって新しいフローが作成される](media/flow-create-new.png)

3. フローの名前を指定し、 **[フローのトリガーを選択してください]** に「**Cloud App Security**」と入力して、 **[アラートが生成される時]** を選択します。

    ![アラートが生成されるときの Power Automate](media/flow-when-alert.png)

4. **[認証の設定]** で、ステップ 1 の API トークンを貼り付けます。

5. Cloud App Security のポリシーによってアラートが生成されたときにトリガーされるワークフローを定義します。 アクション、論理条件、スイッチ ケース条件、またはループを追加して、プレイブックを保存することができます。

    ![Power Automate のワークフロー](media/flow-workflow.png)

6. Cloud App Security ポータルで、 **[ポリシー]** に移動し、アラートを Power Automate に転送するポリシーの行で、3 つのドットをクリックして、 **[設定]** を選択します。
7. **[アラート]** で **[Power Automate にアラートを送信する]** を選択し、ドロップダウン メニューからプレイブックの名前を選択します。

    ![Cloud App Security ポータルで Power Automate を有効にする](media/flow-mcas-config.png)

8. 自分で作成した、またはアクセス権が付与されている Cloud App Security プレイブックを、 **[セキュリティ拡張機能]** 画面で確認できます。

    ![Cloud App Security でプレイブックを表示する](media/flow-extensions.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]