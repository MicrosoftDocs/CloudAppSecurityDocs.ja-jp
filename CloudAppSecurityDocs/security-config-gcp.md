---
title: GCP のセキュリティ構成に関する推奨事項を取得する
description: この記事では、Google Cloud Platform と統合することによって Cloud App Security のセキュリティ構成に関する推奨事項を取得する方法について説明します。
ms.date: 06/28/2020
ms.topic: how-to
ms.openlocfilehash: 15242c8a89aee5a9aa3edd1bf7a881f81734680a
ms.sourcegitcommit: d87372b47ca98e942c2bf94032a6a61902627d69
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96315499"
---
# <a name="security-configuration-for-google-cloud-platform"></a>Google Cloud Platform のセキュリティ構成

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Microsoft Cloud App Security では、Google Cloud Platform (GCP) 環境のセキュリティ構成の評価を得ることができます。 この評価では、[GCP の Center for Internet Security (CIS) ベンチマーク](https://www.cisecurity.org/benchmark/google_cloud_computing_platform/)、バージョン 1.1.0 に基づく基本的なセキュリティに関する推奨事項が提供されます。

この評価では、あらゆる GCP プロジェクトのセキュリティ構成に関する推奨事項が体系的に表示されます。セキュリティ管理者は、セキュリティ構成のギャップを調査したり、リソース所有者別に修復を開始したりできます。

## <a name="prerequisites"></a>[前提条件]

- 組織内のすべての GCP プロジェクトに対して Security Health Analytics を使用して GCP Security Command Center を設定する必要があります。 詳細については、「[Setting up GCP Security Command Center](https://cloud.google.com/security-command-center/docs/quickstart-scc-setup)」(GCP Security Command Center の設定) と [Security Health Analytics の有効化](https://cloud.google.com/security-command-center/docs/how-to-use-security-health-analytics)に関するページを参照してください。
- ご自分の GCP プロジェクトが Cloud App Security に接続されている必要があります。 詳細については、[GCP を Microsoft Cloud App Security に接続する](connect-google-gcp-to-microsoft-cloud-app-security.md)方法に関するページを参照してください。

## <a name="how-to-view-gcp-security-recommendations"></a>GCP のセキュリティに関する推奨事項を表示する方法

1. Cloud App Security で、 **[調査]** 、 **[セキュリティの構成]** の順に参照し、 **[Google Cloud Platform]** タブを選択します。

    > [!NOTE]
    > 変更が有効になるまでに最大 15 分かかる場合があります。

    ![セキュリティの構成メニュー](media/security-configuration-menu.png)

1. 推奨事項は、種類、リソース、サブスクリプションごとにフィルター処理できます。 また、[セキュリティの構成] アイコン ![ASC アイコン](media/asc-icon.png) をクリックして GCP Security Command Center で推奨事項を開いて詳細情報を確認し、推奨事項についてさらに詳しく調べることができます。

    > [!NOTE]
    > 調査をさらに簡単にするために、カスタム クエリを作成して、後で使用できるように保存することができます。 クエリの作成が完了したら、フィルターの右上隅にある **[名前を付けて保存]** ボタンをクリックします。 **[クエリの保存]** ポップアップで、クエリに名前を付けます。

    ![セキュリティの構成](media/security-configuration-gcp.png)

1. 推奨事項を選択すると、説明や詳しい修復ガイドラインなど、推奨事項に関する追加情報が表示されます。

    ![セキュリティの構成に関する推奨事項](media/security-configuration-gcp-details.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
