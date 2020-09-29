---
title: Azure Information Protection 分類ラベルの自動適用
description: このチュートリアルでは、Microsoft Cloud App Security で Azure Information Protection 分類ラベルを自動的に適用する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/5/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 33078d72d6bbcb5430f207a029c3352d776958ba
ms.sourcegitcommit: 575f2b2efa9ca4477d7e60271d21e225ef2c38ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90881121"
---
# <a name="tutorial-automatically-apply-azure-information-protection-classification-labels"></a>チュートリアル:Azure Information Protection 分類ラベルの自動適用

[!INCLUDE [Banner for top of topics](includes/banner.md)]

理想の世界では、社員が全員、情報保護の重要性を理解し、会社の方針から外れることなく仕事をします。 しかしながら、現実の世界では、経理を担当する社員が間違ったアクセス許可で会社の Box リポジトリにドキュメントをアップロードすることがあります。 1 週間後、会社の機密情報が競合他社に漏れたことが判明します。 Microsoft Cloud App Security は、この種の災難を発生前に止める目的で役立ちます。 この機能は Box、SharePoint、OneDrive for Business で利用できます。 Azure Information Protection ラベルの適用は、利用できるさまざまな[ガバナンス アクション](governance-actions.md)の 1 つです。

このチュートリアルは、違反の発生時に警告されるよう、クラウド ストレージに保存されているドキュメントに設定されているパブリック アクセス許可を特定する目的で役立ちます。 また、Azure Information Protection **機密**分類ラベルを自動適用し、ファイルを暗号化できます。

> [!div class="checklist"]
>
> * データ保護を設定する
> * ポリシーを検証する

## <a name="enhanced-data-level-encryption-protection"></a>データレベル暗号保護の強化

Cloud App Security と Azure Information Protection を統合することで、ファイルが自動的に暗号化され、保護レベルが上がります。 Azure Information Protection でファイルを暗号化すると、Office 365 など、Azure Information Protection をサポートするアプリケーションでは、ファイルを開く方法が理解され、分類ラベルに設定されているアクセス許可が守られます。 特定の保護規則を適用するには、ラベルを使用してください。 たとえば、開くことはできるが、共有、印刷、転送、編集はできないようにファイルを設定できます。

この強力な保護レベルがファイルと共に転送されます。 ファイルを送信し、コピーし、オンライン ストレージ アプリに保存する場合もファイルは保護されます。 社員の誰かがファイルの入った USB ドライブをなくしても、そのファイルには鍵がかかったままです。 誰かがそのファイルを開こうとすると、ファイルの持ち主に警告が届きます。 Cloud App Security では、保護を自動的に適用できます。 たとえば、クレジット カード番号が含まれるファイルや財務部がアップロードし、外部で共有されるファイルをすべて分類ラベルで自動的に保護するように設定します。

## <a name="the-threat"></a>脅威

組織に属するあるユーザーが顧客の機密情報ファイルを Box に保存し、組織内の全員と共有するようにそれを設定します。 直属のチームだけでなく、サポート スタッフ全員がその Box アカウントにアクセスできることをそのユーザーは知りません。 このアクセスには、ベンダー、パートナー、オフィスにときどき立ち寄る訪問者が含まれます。 組織の Box アカウントにアクセスできるあらゆる人がその情報にアクセスできるようになったわけです。 このようなアクセスは組織にとって危険であるだけでなく、多くの国や地域で個人情報規則に違反する可能性があり、法的な問題を引き起こすことがあります。

## <a name="the-solution"></a>解決策

Cloud App Security と Azure Information Protection を使用して分類と保護の情報を組み込み、永続的な保護がデータについて回るようにします。それにより、保管場所や共有相手に関係なく、データは常に保護されます。 この保護により、同僚、顧客、パートナーと安全にデータを共有できます。 データにアクセスできる人とその人がデータに対して行える操作を定義します。 たとえば、ファイルを閲覧し、編集する許可をユーザーに与えるが、印刷する許可と転送する許可は与えません。 また、共同作成者や共有機能を削除するなど、Cloud App Security でサポートされているその他の[ガバナンス アクション](governance-actions.md)をファイルに追加できます。

## <a name="prerequisites"></a>[前提条件]

* テナントの [Cloud App Security と Azure Information Protection を有効にします](azip-integration.md)。
* Cloud App Security に [Box を接続します](connect-box-to-microsoft-cloud-app-security.md)。

## <a name="set-up-data-protection"></a>データ保護を設定する

Box アカウントに補完されているファイルでクレジット カード番号を探すポリシーを設定しましょう。 ファイルが見つかったとき、Azure Information Protection ラベルを自動的に適用し、あらゆるファイルで発生することをそのラベルで制御します。

1. Box に保存されている機密データを暗号化するポリシーを設定することで Box に保存するデータの保護を開始します。

    1. **[コントロール]** タブで [ **[ポリシー]** ](control-cloud-apps-with-policies.md) をクリックします。

    2. **[ポリシーの作成]** をクリックし、 **[ファイル ポリシー]** を選択します。

    3. *Box data protection* というポリシーを呼び出します。

    4. **[このポリシーの対象となるファイルのためのフィルターを作成]** の下で所有財産と機密データを対象にします。
        * たとえば、 **[親フォルダー]** 、[次の値と等しい]、Box の **[顧客データ]** を選択し、 **[所有者]** 、[次の値と等しい]、[財務チーム] を選択します。

    5. そのフォルダーの中で、クレジット カード情報が含まれるファイルを探します。 **[コンテンツ検査方法]** の下で **[組み込み DLP]** を選択し、 **[事前設定した式に一致するファイルを含める]** を選択し、 **[すべての国: 財務: クレジット カード番号]** を選択します。

    6. **[ガバナンス]** の下で **[Box]** セクションを開き、 **[分類ラベルの適用]** を選択します。 適用するラベルを選択します。

    7. [Cloud App Security と Azure Information Protection が統合されているため](azip-integration.md)、データ保護に使用する分類ラベルを既存の一覧から選択できます。

    8. **[作成]** をクリックします。

   ![分類ラベルをポリシーに追加する](media/aip-auto-policy.png)

2. 一致を調査する

    1. **[ポリシー]** ページでポリシー名をクリックし、 **[ポリシー レポート]** に移動します。 ポリシーに対してトリガーされた一致を確認します。

    2. 特定の一致をクリックしてファイル ドロワーを開くことで一致を調査できます。 ドロワーでは、このファイルが一致したその他のポリシーを確認できます。

## <a name="validate-your-policy"></a>ポリシーを検証する

1. アラートをシミュレートするには、Box アカウントに進み、 **[顧客データ]** フォルダーに含まれるファイルにアクセスします。
2. ポリシー レポートに移動します。 ファイル ポリシーの一致がすぐに表示されるはずです。
3. 一致をクリックすると、保護されたファイルを表示できます。 一致自体は機密データを保護する目的でマスキングされます。

>[!NOTE]
>
> *- Cloud App Security は、現時点で Box、GSuite、SharePoint、OneDrive for Business での Azure Information Protection ラベルの自動適用をサポートしています。
> *- Cloud App Security を使用してドキュメントがラベル付けされると、視覚的なマーキングはすぐには適用されず、ドキュメントが Office アプリで開かれ、最初に保存されたときに適用されます。 詳細については、「[Azure Information Protection 用の視覚的なマーキングのラベルを構成する方法](/information-protection/deploy-use/configure-policy-markings#when-visual-markings-are-applied)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]