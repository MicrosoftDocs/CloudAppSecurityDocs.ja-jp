---
title: アマゾン ウェブ サービスを Cloud App Security に接続する
description: この記事では、API コネクタを使用して AWS アプリを Cloud App Security に接続して、使用状況を表示および制御する方法について説明します。
ms.date: 06/24/2020
ms.topic: how-to
ms.openlocfilehash: c1d53e417fa8158ef30c688811f66bcb7ed87ee7
ms.sourcegitcommit: 16a65ab2c8ca778d0b3cfa97b847af4c812363b2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2021
ms.locfileid: "97855797"
---
# <a name="connect-aws-to-microsoft-cloud-app-security"></a>AWS を Microsoft Cloud App Security に接続する

[!INCLUDE [Banner for top of topics](includes/banner.md)]

この記事では、コネクタ API を使用して既存のアマゾン ウェブ サービス (AWS) アカウントを Microsoft Cloud App Security に接続する手順について説明します。 Cloud App Security で AWS を保護する方法の詳細については、[AWS の保護](protect-aws.md)に関するページを参照してください。

Cloud App Security 接続には、次の AWS の一方または両方を接続できます。

- **セキュリティ監査**: この接続を使用すると、AWS アプリの使用状況を表示したり制御したりできます。
- **セキュリティ構成**: この接続では、AWS の Center for Internet Security (CIS) ベンチマークに基づいたセキュリティに関する基本的な推奨事項が提供されます。

接続のいずれか一方または両方を追加できるため、この記事では、各接続の手順を個別の手順として説明します。 接続のいずれか一方を既に追加している場合は、必要に応じて既存の構成を編集してください。

## <a name="how-to-connect-aws-security-auditing-to-cloud-app-security"></a>AWS のセキュリティ監査を Cloud App Security に接続する方法

次の手順に従って、AWS 監査を構成し、Cloud App Security に接続します。

### <a name="step-1-configure-amazon-web-services-auditing"></a>手順 1:アマゾン ウェブ サービス監査を構成する

1. [アマゾン ウェブ サービス コンソール](https://console.aws.amazon.com/)の **[Security, Identity & Compliance]\(セキュリティ、ID、コンプライアンス\)** で、 **[IAM]** をクリックします。

    ![AWS の ID とアクセス](media/aws-identity-and-access.png "AWS の ID とアクセス")

1. **[ユーザー]** をクリックし、 **[ユーザーの追加]** をクリックします。

    ![AWS ユーザー](media/aws-users.png "AWS ユーザー")

1. **[詳細]** の手順で、Cloud App Security の新しいユーザー名を指定します。 **[アクセスの種類]** で、 **[プログラムによるアクセス]** を選択していることを確認し、 **[Next: Permissions]\(次へ: アクセス許可\)** をクリックします。<a name="set-permissions"></a>

    ![AWS でユーザーを作成する](media/aws-create-user.png "AWS でユーザーを作成する")

1. **[JSON]** タブをクリックします。

    ![AWS の [JSON] タブ](media/aws-json.png "AWS の [JSON] タブ")

1. 指定された領域に次のスクリプトを貼り付けます。

    ```json
    {
      "Version" : "2012-10-17",
      "Statement" : [{
          "Action" : [
            "cloudtrail:DescribeTrails",
            "cloudtrail:LookupEvents",
            "cloudtrail:GetTrailStatus",
            "cloudwatch:Describe*",
            "cloudwatch:Get*",
            "cloudwatch:List*",
            "iam:List*",
            "iam:Get*",
            "s3:ListAllMyBuckets",
            "s3:PutBucketAcl",
            "s3:GetBucketAcl",
            "s3:GetBucketLocation"
          ],
          "Effect" : "Allow",
          "Resource" : "*"
        }
      ]
     }
    ```

     ![AWS コード](media/aws-code.png "AWS コード")

1. **[Review policy]\(ポリシーの確認\)** をクリックします。

1. **[名前]** を入力し、 **[ポリシーの作成]** をクリックします。

    ![AWS ポリシーの名前を指定する](media/aws-create-policy.png "AWS ポリシーの名前を指定する")

1. **[ユーザーの追加]** 画面に戻り、必要に応じて一覧を更新し、作成したユーザーを選択して、 **[Next: Review]\(次へ: 確認\)** をクリックします。

    ![AWS で既存のポリシーをアタッチする](media/aws-attach-policy.png "AWS で既存のポリシーをアタッチする")

1. すべての詳細が正しい場合は、 **[ユーザーの作成]** をクリックします。

    ![AWS でのユーザーのアクセス許可](media/aws-user-permissions.png "AWS でユーザーのアクセス許可を確認する")

1. 成功メッセージが表示されたら、 **[.csv をダウンロード]** をクリックして、新しいユーザーの資格情報のコピーを保存します。これは、後で必要になります。

    ![AWS で .csv をダウンロードする](media/aws-download-csv.png "AWS で .csv をダウンロードする")

1. AWS コンソールで **[サービス]** をクリックし、 **[管理ツール]** で **[CloudTrail]** をクリックします。

    ![AWS CloudTrail](media/aws-cloudtrail.png "AWS CloudTrail")

    以前に CloudTrail を使用したことがなければ、 **[Get Started]\(開始\)** をクリックして、名前を入力し、適切な S3 バケットを選択し、 **[有効にする]** をクリックして設定します。 対象範囲がすべて含まれるようにするために、 **[Apply to all regions]\(すべてのリージョンに適用する\)** を **[はい]** に設定します。

    ![AWS で CloudTrail を有効にする](media/aws-turnon-cloudtrail.png "AWS で CloudTrail を有効にする")

    **[Trails]** の一覧に新しい CloudTrail 名が表示されます。

    ![AWS の CloudTrail の一覧](media/aws-cloudtrail-list.png "AWS の CloudTrail の一覧")

    > [!NOTE]
    > AWS に接続すると、接続前の 7 日間のイベントを受け取ります。 CloudTrail を有効にしたばかりであれば、CloudTrail を有効にした時点からのイベントを受け取ります。

### <a name="step-2-connect-amazon-web-services-auditing-to-cloud-app-security"></a>手順 2:アマゾン ウェブ サービス監査を Cloud App Security に接続する

1. Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. **[アプリ コネクタ]** ページで、次のいずれかの手順を行って、AWS コネクタの資格情報を入力します。

    **新しいコネクタの場合**

    1. プラス記号 **[+]** をクリックして、 **[アマゾン ウェブ サービス]** をクリックします。

        ![AWS 監査の接続](media/connect-aws.png "AWS の接続")

    1. ポップアップでコネクタの名前を指定し、 **[アマゾン ウェブ サービスに接続]** をクリックします。

        ![AWS 監査コネクタ名](media/connect-aws-name.png)

    1. [アマゾン ウェブ サービスに接続] ページで、 **[Security auditing]\(セキュリティ監査\)** を選択し、.csv ファイルの **アクセス キー** と **秘密鍵** を関連フィールドに貼り付けて、 **[接続]** をクリックします。

        ![新しいコネクタ用に AWS アプリのセキュリティ監査を接続する](media/aws-connect-app-audit.png "AWS アプリのセキュリティ監査を接続する")

    **既存のコネクタの場合**

    1. コネクタの一覧で、AWS コネクタが表示されている行の **[Connect security auditing]\(セキュリティ監査を接続\)** をクリックします。

        ![セキュリティ監査の編集リンクを示す [接続アプリ] ページのスクリーンショット](media/aws-connect-app-edit-audit.png)

    1. [アマゾン ウェブ サービスに接続] ページで、.csv ファイルの **アクセス キー** と **秘密鍵** を関連フィールドに貼り付けて、 **[接続]** をクリックします。

        ![既存のコネクタ用に AWS アプリのセキュリティ監査を接続する](media/aws-connect-app-edit-audit-creds.png "AWS アプリのセキュリティ監査を接続する")

1. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 完了すると、成功または失敗の通知が表示されます。 成功の通知を受信したら、 **[完了]** をクリックします。

## <a name="how-to-connect-aws-security-configuration-to-cloud-app-security"></a>AWS のセキュリティ構成を Cloud App Security に接続する方法

AWS のセキュリティ構成を接続すると、AWS の Center for Internet Security (CIS) ベンチマークに基づいたセキュリティに関する基本的な推奨事項の分析情報が提供されます。

AWS のセキュリティ構成を Cloud App Security に接続するには、次の手順に従います。

> [!div class="checklist"]
>
> - [AWS Security Hub を設定する](#set-up-aws-security-hub)
> - [AWS のセキュリティ構成を Cloud App Security に接続する](#connect-aws-security-configuration-to-cloud-app-security)

### <a name="set-up-aws-security-hub"></a>AWS Security Hub を設定する

複数のリージョンのセキュリティに関する推奨事項を表示するには、関連するリージョンごとに次の手順を繰り返します。

> [!NOTE]
> マスター アカウントを使用している場合は、これらの手順を繰り返して、関連するすべてのリージョンで、マスター アカウントと、接続されたすべてのメンバー アカウントを構成します。

1. [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-console.html) を有効にします。
1. [AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html) を有効にします。
1. Security Hub にデータが流れていることを確認します。

    > [!NOTE]
    > Security Hub を初めて有効にする場合は、データが使用可能になるまで数時間かかることがあります。

### <a name="connect-aws-security-configuration-to-cloud-app-security"></a>AWS のセキュリティ構成を Cloud App Security に接続する

AWS のセキュリティ構成を接続する前に、セキュリティおよびコンプライアンスに関する基本的な推奨事項を収集するように、[ご使用の AWS 環境が設定されている](#set-up-aws-security-hub)ことを確認してください。

> [!NOTE]
> [AWS マスター アカウント](https://aws.amazon.com/security-hub/faqs/)を使用している場合は、次の手順を行ってマスター アカウントを接続します。 マスター アカウントを接続すると、すべてのリージョンのすべてのメンバー アカウントに関する推奨事項を受け取ることができます。

### <a name="step-1-configure-amazon-web-services-security-configuration"></a>手順 1:アマゾン ウェブ サービスのセキュリティ構成を構成する

1. "*AWS のセキュリティ監査を接続する方法*" の手順に従って、[アクセス許可](#set-permissions)のページに移動します。

1. アクセス許可のページで、 **[Attach existing policies directly]\(既存のポリシーを直接アタッチする\)** をクリックして、**AWSSecurityHubReadOnlyAccess** ポリシーと **SecurityAudit** ポリシーを適用し、 **[Next: Tags]\(次へ: タグ\)** をクリックします。

    ![AWS で既存のポリシーをアタッチする](media/aws-attach-policy.png "AWS で既存のポリシーをアタッチする")

1. オプション:タグをユーザーに追加します。

    ![AWS でタグをユーザーに追加する](media/aws-add-tags.png)

    > [!NOTE]
    > タグをユーザーに追加しても接続には影響しません。

1. **[Next: Review]\(次へ: 確認\)** をクリックします。

1. すべての詳細が正しい場合は、 **[ユーザーの作成]** をクリックします。

    ![AWS でのユーザーのアクセス許可](media/aws-user-permissions.png "AWS でユーザーのアクセス許可を確認する")

1. 成功メッセージが表示されたら、 **[.csv をダウンロード]** をクリックして、**アクセス キー ID** と **秘密アクセス キー** のコピーを保存します。これは、後で必要になります。

    ![AWS で .csv をダウンロードする](media/aws-download-csv.png "AWS で .csv をダウンロードする")

### <a name="step-2-connect-amazon-web-services-security-configuration-to-cloud-app-security"></a>手順 2:アマゾン ウェブ サービスのセキュリティ構成を Cloud App Security に接続する

1. Cloud App Security で、 **[調査]** をクリックし、 **[接続アプリ]** を選択します。

1. **[Security configuration apps]\(セキュリティ構成アプリ\)** タブで、[+] ボタンをクリックして、 **[アマゾン ウェブ サービス]** を選択します。

    ![AWS のセキュリティ構成を接続する](media/connect-aws-security-configuration.png)

1. **[インスタンス名]** ページで、インスタンスの種類を選択して、 **[次へ]** をクリックします。

    - 既存のコネクタの場合は、関連するインスタンスを選択します。

        ![AWS インスタンスの選択](media/connect-aws-existing-instance.png)

    - 新しいコネクタの場合は、インスタンスの名前を指定します。

        ![AWS のセキュリティ構成のコネクタ名](media/aws-connect-name.png)

1. **[アカウントの詳細]** ページで、.csv ファイルの **アクセス キー** と **秘密鍵** を対応するフィールドに貼り付けて、 **[次へ]** をクリックします。

    ![AWS アカウントの接続の詳細](media/aws-connect-account-details.png)

1. **[完了]** ページで、接続が成功したことを確認し、 **[完了]** をクリックします。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
