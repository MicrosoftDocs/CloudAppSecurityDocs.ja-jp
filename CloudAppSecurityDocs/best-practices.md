---
title: 組織を保護するためのベスト プラクティス - Cloud App Security
description: この記事では、組織を保護するための一連のベスト プラクティスについて説明します。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: quickstart
ms.date: 10/24/2019
ms.collection: M365-security-compliance
ms.openlocfilehash: e26d98c00a520f710774ccd86a1406f4c8392530
ms.sourcegitcommit: 29a8e66c665f51d831516924ae4d9d8047b39276
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88781312"
---
# <a name="cloud-app-security-best-practices"></a>Cloud App Security のベスト プラクティス

*適用対象:Microsoft Cloud App Security*

この記事では、Microsoft Cloud App Security を使用して組織を保護するためのベスト プラクティスについて説明します。 これらのベスト プラクティスは、Cloud App Security に関する Microsoft の経験と、お客様の経験から得られたものです。

この記事で説明するベスト プラクティスは次のとおりです。

> [!div class="checklist"]
> * [クラウド アプリの検出と評価](#discover-and-assess-cloud-apps)
> * [クラウド ガバナンス ポリシーを適用する](#apply-cloud-governance-policies)
> * [共有データの公開を制限し、コラボレーション ポリシーを適用する](#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
> * [クラウドに格納されている規制対象の機密データを検出、分類、ラベル付け、保護する](#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
> * [クラウドに格納されているデータに DLP ポリシーとコンプライアンス ポリシーを適用する](#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
> * [管理されていないデバイスまたは危険なデバイスへの機密データのダウンロードをブロックおよび保護する](#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)
> * [リアルタイム セッション制御を適用することにより、外部ユーザーとの共同作業をセキュリティで保護する](#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)
> * [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者、ランサムウェアを検出する](#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
> * [フォレンジック調査のためにアクティビティの監査証跡を使用する](#use-the-audit-trail-of-activities-for-forensic-investigations)
> * [IaaS サービスとカスタム アプリをセキュリティで保護する](#secure-iaas-services-and-custom-apps)

## <a name="discover-and-assess-cloud-apps"></a>クラウド アプリの検出と評価

Cloud App Security と Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) を統合すると、企業ネットワークやセキュリティで保護された Web ゲートウェイを越えて Cloud Discovery を使用できるようになります。 ユーザーとコンピューターの情報を組み合わせることで、Microsoft Defender ATP ポータルで、危険なユーザーまたはコンピューターの特定、使用しているアプリの確認、詳細調査を行うことができます。

**ベスト プラクティス**:Microsoft Defender ATP を使用して Shadow IT Discovery を有効にする  
**詳細**:Cloud Discovery を使用して、Microsoft Defender ATP により収集されたトラフィック ログを分析し、特定したアプリをクラウド アプリ カタログに照らして評価して、コンプライアンスとセキュリティの情報を取得します。 Cloud Discovery を構成することにより、クラウドの使用状況、シャドウ IT、および承認されていないアプリのユーザー使用の継続的な監視を可視化できます。  
**参照項目**:

* [Cloud App Security と Microsoft Defender ATP の統合](wdatp-integration.md)
* [Cloud Discovery を設定する](set-up-cloud-discovery.md)
* [ネットワーク内のシャドウ IT の検出と管理](tutorial-shadow-it.md)

---

**ベスト プラクティス**:アプリ検出ポリシーを構成して、危険、非対応、人気上昇中のアプリを事前に特定する  
**詳細**:アプリ検出ポリシーを使用すると、組織内で検出された重要なアプリケーションを簡単に追跡できるため、これらのアプリケーションを効率的に管理できます。 リスク、非対応、人気上昇中、または高ボリュームとして特定された新しいアプリを検出したときにアラートを受け取るポリシーを作成します。  
**参照項目**:

* [Cloud Discovery ポリシー](cloud-discovery-policies.md)
* [Cloud Discovery 異常検出ポリシー](cloud-discovery-anomaly-detection-policy.md)
* [行動分析と異常検出を瞬時に取得する](anomaly-detection-policy.md)

---

**ベスト プラクティス**:ユーザーによって承認された OAuth アプリを管理する  
**詳細**:多くのユーザーが自分のアカウント情報にアクセスするための OAuth アクセス許可を不用意にサードパーティ製アプリに付与し、そうすることで、他のクラウド アプリの自分のデータへのアクセス権も間違って付与してしまいます。 通常、IT 部門にはこれらのアプリを可視化する機能がないため、アプリによるセキュリティ リスクと生産性の利点を比較するのは困難です。

Cloud App Security には、ユーザーが付与したアプリのアクセス許可を調査および監視する機能が用意されています。 この情報を使用して、疑わしい可能性のあるアプリを特定でき、危険であると判断した場合にアクセスを禁止することができます。  
**参照項目**:

* [OAuth アプリの管理](manage-app-permissions.md)
* [OAuth アプリ ポリシー](app-permission-policy.md)

---
---
---
---

## <a name="apply-cloud-governance-policies"></a>クラウド ガバナンス ポリシーを適用する

**ベスト プラクティス**:アプリにタグを付け、ブロック スクリプトをエクスポートする  
**詳細**:組織内で検出されたアプリの一覧を確認してから、不要なアプリが使用されないように環境をセキュリティで保護することができます。 組織によって承認されているアプリには**承認された**タグを、承認されていないアプリには**承認されていない**タグを適用することができます。 検出フィルターを使用して承認されていないアプリを監視したり、オンプレミスのセキュリティ アプライアンスを使用して承認されていないアプリをブロックするスクリプトをエクスポートしたりできます。 タグとエクスポート スクリプトを使用することで、安全なアプリへのアクセスのみを許可して、アプリを整理し、環境を保護することができます。  
**参照項目**:

* [検出されたアプリの管理](governance-discovery.md)

---
---
---
---

## <a name="limit-exposure-of-shared-data-and-enforce-collaboration-policies"></a>共有データの公開を制限し、コラボレーション ポリシーを適用する

**ベスト プラクティス**:Office 365 の接続  
**詳細**:Office 365 を Cloud App Security に接続すると、ユーザーのアクティビティやアクセスしているファイルを瞬時に表示でき、Office 365、SharePoint、OneDrive、Teams、Power BI、Exchange、Dynamics のガバナンス アクションが提供されます。  
**参照項目**:

* [アプリの接続](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)
* [Office 365 を Microsoft Cloud App Security に接続する](connect-office-365-to-microsoft-cloud-app-security.md)

---

**ベスト プラクティス**:サードパーティ製アプリを接続する  
**詳細**:サードパーティ製アプリを Cloud App Security に接続することにより、ユーザーのアクティビティ、脅威検出、ガバナンス機能に関する洞察が向上します。 サポートされているサードパーティ製アプリの API:[アマゾン ウェブ サービス (AWS)](connect-aws-to-microsoft-cloud-app-security.md)、[Box](connect-box-to-microsoft-cloud-app-security.md)、[Dropbox](connect-dropbox-to-microsoft-cloud-app-security.md)、[G Suite](connect-google-apps-to-microsoft-cloud-app-security.md)、[Okta](connect-okta-to-microsoft-cloud-app-security.md)、[Salesforce](connect-salesforce-to-microsoft-cloud-app-security.md)、[ServiceNow](connect-servicenow-to-microsoft-cloud-app-security.md)、[WebEx](connect-webex-to-microsoft-cloud-app-security.md)、および [Workday](connect-workday-to-microsoft-cloud-app-security.md)。  
**参照項目**:

* [アプリの接続](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)

---

**ベスト プラクティス**:組織のデータ露出を確認する  
**詳細**:ファイル露出レポートを使用すると、ユーザーがクラウド アプリでファイルを共有している方法を可視化できます。 次のレポートが使用可能であり、Microsoft Power BI などのツールで詳細な分析を行うためにエクスポートできます。

* **データ共有の概要**:各クラウド アプリに格納されているファイルをアクセス許可別に一覧表示します
* **ドメイン別の送信共有**:従業員が共有している会社のファイルがあるドメインを一覧表示します
* **共有ファイルの所有者**:会社のファイルを外部と共有しているユーザーを一覧表示します  
**参照項目**:

* [データ管理レポートを生成する](built-in-reports.md)

---

**ベスト プラクティス**:個人アカウントとの共有を削除するポリシーを作成する  
**詳細**:Office 365 を Cloud App Security に接続すると、ユーザーのアクティビティやアクセスしているファイルを瞬時に表示でき、Office 365、SharePoint、OneDrive、Teams、Power BI、Exchange、Dynamics のガバナンス アクションが提供されます。  
**参照項目**:

* [接続されているアプリを管理する](governance-actions.md)

---
---
---
---

## <a name="discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud"></a>クラウドに格納されている規制対象の機密データを検出、分類、ラベル付け、保護する

**ベスト プラクティス**:Azure Information Protection と統合する  
**詳細**:Azure Information Protection と統合すると、分類ラベルを自動的に適用し、必要に応じて暗号化保護を追加することができます。 統合を有効にすると、ラベルをガバナンス アクションとして適用する、ファイルを分類別に表示する、ファイルを分類レベル別に調査する、分類されたファイルが適切に処理されるような詳細なポリシーを作成することができます。 統合を有効にしない場合は、クラウド内のファイルを自動的にスキャン、ラベル付け、暗号化する機能を利用できません。  
**参照項目**:

* [Azure Information Protection の統合](azip-integration.md)
* [チュートリアル:Azure Information Protection 分類ラベルの自動適用](use-case-information-protection.md)

---

**ベスト プラクティス**:データ露出ポリシーを作成する  
**詳細**:ファイル ポリシーを使用して、情報共有を検出し、クラウド アプリの機密情報をスキャンします。 データ露出が検出されたときにアラートを生成するために、次のファイルのポリシーを作成します。

* 外部で共有され、機密データが含まれるファイル
* 外部で共有され、**機密**としてラベル付けされているファイル
* 承認されていないドメインで共有されているファイル
* SaaS アプリの機密ファイルの保護

**参照項目**:

* [コンテンツ検査](content-inspection.md)
* [ファイル ポリシー](data-protection-policies.md)
* [情報保護に関するポリシー](policies-information-protection.md)

---

**ベスト プラクティス**: **[ファイル]** ページでレポートを確認する  
**詳細**:さまざまな SaaS アプリをアプリ コネクタを使用して接続すると、Cloud App Security により、これらのアプリによって格納されているファイルがスキャンされます。 さらに、ファイルは変更されるたびに、再度スキャンされます。 **[ファイル]** ページを使用して、クラウド アプリに格納されているデータの種類を把握し、調査することができます。 調査に役立つように、ドメイン、グループ、ユーザー、作成日、拡張子、ファイル名と種類、ファイル ID、分類ラベルなどでフィルター処理できます。 これらのフィルターを使用すると、ファイルを調査してデータが危険にさらされていないことを確認する方法を制御できます。 データがどのように使用されているかについてよく把握したら、これらのファイル内の機密コンテンツをスキャンするポリシーを作成できます。  
**参照項目**:

* [アプリの接続](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md)
* [ファイル フィルター](file-filters.md)
* [コンテンツ検査](content-inspection.md)

---
---
---
---

## <a name="enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud"></a>クラウドに格納されているデータに DLP ポリシーとコンプライアンス ポリシーを適用する

**ベスト プラクティス**:機密データが外部ユーザーと共有されないように保護する  
**詳細**:ユーザーが**機密**分類ラベルを持つファイルを組織外部の人と共有しようとしたときに検出するファイル ポリシーを作成し、外部ユーザーを削除するようにガバナンス アクションを構成します。 このポリシーを使用すると、機密データが組織の外に出ることがなくなり、外部ユーザーがアクセスできないことを確実にすることができます。  
**参照項目**:

* [接続されているアプリを管理する](governance-actions.md)

---
---
---
---

## <a name="block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices"></a>管理されていないデバイスまたは危険なデバイスへの機密データのダウンロードをブロックおよび保護する

**ベスト プラクティス**:危険度の高いデバイスへのアクセスを管理および制御する  
**詳細**:アプリの条件付きアクセス制御を使用して、SaaS アプリのコントロールを設定します。 危険度が高く、信頼度が低いセッションを監視するセッション ポリシーを作成できます。 同様に、管理されていないデバイスまたは危険なデバイスから機密データにアクセスしようとするユーザーによるダウンロードをブロックして保護するセッション ポリシーを作成できます。 危険度が高いセッションを監視するセッション ポリシーを作成しないと、Web クライアントでのダウンロードをブロックして保護する機能に加えて、Microsoft とサードパーティ製のアプリの両方で信頼度が低いセッションを監視する機能も失われます。  
**参照項目**:

* [Microsoft Cloud App Security のアプリの条件付きアクセス制御を使用してアプリを保護する](proxy-intro-aad.md)
* [セッション ポリシー](session-policy-aad.md)

---
---
---
---

## <a name="secure-collaboration-with-external-users-by-enforcing-real-time-session-controls"></a>リアルタイム セッション制御を適用することにより、外部ユーザーとの共同作業をセキュリティで保護する

**ベスト プラクティス**:アプリの条件付きアクセス制御を使用して外部ユーザーとのセッションを監視する  
**詳細**:環境内の共同作業をセキュリティで保護するために、内部ユーザーと外部ユーザーの間のセッションを監視するセッション ポリシーを作成できます。 これにより、ユーザー間のセッションを監視できる (セッションのアクティビティが監視されていることを通知できる) だけでなく、特定のアクティビティを制限することもできます。 アクティビティを監視するセッション ポリシーを作成するときに、監視するアプリとユーザーを選択できます。  
**参照項目**:

* [Microsoft Cloud App Security のアプリの条件付きアクセス制御を使用してアプリを保護する](proxy-intro-aad.md)
* [セッション ポリシー](session-policy-aad.md)

---
---
---
---

## <a name="detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware"></a>クラウドの脅威、侵害されたアカウント、悪意のある内部関係者、ランサムウェアを検出する

**ベスト プラクティス**:異常ポリシーの調整、IP 範囲の設定、アラートに関するフィードバック送信を行う  
**詳細**:異常検出ポリシーにより、すぐに使用できるユーザー/エンティティ行動分析 (UEBA) と機械学習 (ML) が提供されるため、クラウド環境全体で高度な脅威検出をすぐに実行できます。

異常検出ポリシーは、環境内のユーザーが実行した異常なアクティビティがあるときにトリガーされます。 Cloud App Security により、ユーザーのアクティビティが継続的に監視され、UEBA と ML を使用してユーザーの "*通常*" の行動が学習、把握されます。 ポリシー設定は、組織の要件に合わせて調整できます。たとえば、ポリシーの感度を設定したり、ポリシーのスコープを特定のグループに限定したりすることができます。

* **異常検出ポリシーを調整してスコープを限定する**:たとえば、あり得ない移動アラート内の偽陽性の数を減らすには、ポリシーの感度スライダーを低に設定します。 組織内に頻繁に出張するユーザーがいる場合は、ユーザー グループに追加し、このポリシーのスコープ内で、そのグループを選択することができます。

* **IP 範囲を設定する**:IP アドレス範囲を設定すると、Cloud App Security で既知の IP アドレスを識別することができます。 IP アドレス範囲を構成して、ログとアラートの表示と調査の方法をタグ付け、分類、カスタマイズすることができます。 IP アドレス範囲を追加することで、偽陽性を減らし、アラートの精度を向上させることができます。 IP アドレスを追加しないことを選択すると、調査対象になる可能性がある偽陽性とアラートの数が増えることがあります。

* **アラートに関するフィードバックを送信する**

    アラートを無視または解決する場合は、アラートを無視した理由や解決方法についてフィードバックを送信してください。 この情報は、Cloud App Security によるアラートを改善し、偽陽性を減らすのに役立ちます。

**参照項目**:

* [行動分析と異常検出を瞬時に取得する](anomaly-detection-policy.md)
* [IP 範囲とタグの使用](ip-tags.md)
* [Cloud App Security でアラートを監視する](monitor-alerts.md)

---

**ベスト プラクティス**:予期しない場所または国からのアクティビティを検出する  
**詳細**:予期しない場所または国や地域からユーザーがサインインしたときに通知するアクティビティ ポリシーを作成します。 これらの通知を使用して、発生前に脅威を検出して修復できるように、環境内で侵害される可能性のあるセッションを警告できます。  
**参照項目**:

* [脅威保護に関するポリシー](policies-threat-protection.md)

---

**ベスト プラクティス**:OAuth アプリ ポリシーを作成する  
**詳細**:OAuth アプリが特定の条件を満たしたときに通知する OAuth アプリ ポリシーを作成します。 たとえば、高いアクセス許可レベルを必要とする特定のアプリにアクセスするユーザーが 100 人を超えたときに通知を受け取るように選択できます。  
**参照項目**:

* [OAuth アプリ ポリシー](app-permission-policy.md)

---
---
---
---

## <a name="use-the-audit-trail-of-activities-for-forensic-investigations"></a>フォレンジック調査のためにアクティビティの監査証跡を使用する

**ベスト プラクティス**:アラートの調査時にアクティビティの監査証跡を使用する  
**詳細**:アラートは、ユーザー、管理者、またはサインイン アクティビティがポリシーに準拠していないときにトリガーされます。 アラートを調査して、環境に脅威の可能性があるかどうかを把握することが重要です。

アラートを調査するには、 **[アラート]** ページでアラートを選択し、そのアラートに関連するアクティビティの監査証跡を確認します。 監査証跡を使用すると、同じ種類、同じユーザー、同じ IP アドレスと場所のアクティビティを表示して、アラートの全体像を把握できます。 アラートにより、さらなる調査が必要となる場合は、組織内のこれらのアラートを解決する計画を作成します。

アラートを無視するときは、アラートがなぜ重要でないのか、または偽陽性であるかを調査し、把握することが重要です。 このようなアクティビティが大量にある場合は、アラートをトリガーするポリシーの確認と調整も検討します。  
**参照項目**:

* [アクティビティ](activity-filters.md)

---
---
---
---

## <a name="secure-iaas-services-and-custom-apps"></a>IaaS サービスとカスタム アプリをセキュリティで保護する

**ベスト プラクティス**:Azure、AWS、GCP に接続する  
**詳細**:これらの各クラウド プラットフォームを Cloud App Security に接続すると、脅威検出機能を向上させることができます。 これらのサービスの管理およびサインイン アクティビティを監視することで、ブルート フォース攻撃の可能性、特権ユーザーのアカウントの不正使用などの脅威を環境内で検出し、通知を受けることができます。 たとえば、VM の異常な削除や、これらのアプリでの偽装アクティビティなどのリスクを特定できます。  
**参照項目**:

* [Azure を Microsoft Cloud App Security に接続する](connect-azure-to-microsoft-cloud-app-security.md)
* [AWS を Microsoft Cloud App Security に接続する](connect-aws-to-microsoft-cloud-app-security.md)
* [GCP を Microsoft Cloud App Security に接続する (プレビュー)](connect-google-gcp-to-microsoft-cloud-app-security.md)

---

**ベスト プラクティス**:Azure、AWS、GCP のセキュリティ構成の評価を確認する  
**詳細**:Azure Security Center と統合すると、Azure 環境のセキュリティ構成の評価が得られます。 この評価により、不足している構成とセキュリティ制御に関する推奨事項が提供されます。 これらの推奨事項を確認すると、環境内の異常や潜在的な脆弱性を特定し、Azure セキュリティ ポータルで、関連する場所に直接移動して解決することができます。

クラウドのセキュリティを向上させる方法について、AWS および GCP により、セキュリティ構成の推奨事項を可視化する機能が提供されています。

これらの推奨事項を使用して、Azure サブスクリプション、AWS アカウント、GCP プロジェクトなど、組織全体のコンプライアンスの状態とセキュリティの状態を監視します。  
**参照項目**:

* [Azure のセキュリティ構成](security-config.md)
* [AWS のセキュリティ構成](security-config-aws.md)
* [GCP のセキュリティ構成](security-config-gcp.md)

---

**ベスト プラクティス**:カスタム アプリをオンボードする  
**詳細**:基幹業務アプリのアクティビティの可視化を向上させるには、カスタム アプリを Cloud App Security にオンボードできます。 カスタム アプリを構成すると、だれが使用しているのか、どの IP アドレスから使用されているのか、どのくらいのトラフィック量がアプリで送受信されているかについての情報が表示されます。

また、カスタム アプリをアプリの条件付きアクセス制御アプリとしてオンボードして、信頼度の低いセッションを監視することもできます。  
**参照項目**:

* [Cloud Discovery にカスタム アプリを追加する](cloud-discovery-custom-apps.md)
* [任意のアプリに対するアプリの条件付きアクセス制御のオンボードと展開](proxy-deployment-any-app.md)
