---
title: "Cloud Discovery のトラブル シューティング | Microsoft Docs"
description: "このトピックでは、Cloud Discovery でよく起こるエラー一覧と、各エラーの推奨される解決策について説明します。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/15/2016
ms.topic: article
ms.prod: 
ms.service: cloud-app-security
ms.technology: 
ms.assetid: 76dfaebb-d477-4bdb-b3d7-04cc3fe6431d
ms.reviewer: reutam
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed4ea71b24767d3602d40894d1cbac7447bcd8a2
ms.openlocfilehash: 2d0b2cebdfa15cccc5888660da498446d620b64f


---

# <a name="troubleshooting-cloud-discovery"></a>クラウド検出のトラブル シューティング
## <a name="log-parsing-errors"></a>ログ解析エラー

ガバナンス ログを使用して Cloud Discovery ログの処理を追跡できます。 このガイドでは、表示される可能性がある各エラーに対する解決方法について説明します。

### <a name="governance-log-errors"></a>ガバナンス ログ エラー
|エラー|説明|解決方法|
|----|----|----|
|サポートされていないファイルの種類|アップロードしたファイルが有効なログ ファイルではありません (画像ファイルなど)。|ファイアウォールまたはプロキシから直接エクスポートされた **text**、**zip**、または **gzip** ファイルをアップロードします。|
|内部エラー。|内部リソース エラーが検出されました|**[再試行]** をクリックして作業を再実行します。|
|ログ形式が予期される形式と一致しません|アップロードしたログの形式が、このデータ ソースで予期されるログの形式と一致しません。|1.ログが破損していないことを確認します。 <br /> 2.ログと、アップロード ページに表示されるサンプル形式とを比較し、照合します。|
|Transactions are more than 90 days old (トランザクションは 90 日より前のものです)|すべてのトランザクションは 90 日よりも前のものなので、無視されます。|最近のイベントが含まれる新しいログをエクスポートし、アップロードし直します。|
|No transactions to cataloged cloud apps (カタログ化されたクラウド アプリに対するトランザクションがありません)|認識されているクラウド アプリに対するトランザクションがログに見つかりません。|ログに送信トラフィック情報が含まれていることを確認します。|
|サポートされていないログの種類|**[データ ソース] = [その他 (サポートされていません)]** の場合、ログは解析されません。 代わりに、Cloud App Security テクニカル チームに送信され、レビューされます。|Cloud App Security テクニカル チームは、データ ソースごとに専用のパーサーを構築しています。 よく使用されているデータ ソースは、[既にサポートされています](set-up-cloud-discovery.md)。 サポートされないデータ ソースの各アップロードはレビューされ、新しいデータ ソース パーサーのパイプラインに追加されます。 新しいパーサーの通知は、Cloud App Security リリース ノートの一部として公開されます。|
## <a name="log-collector-errors"></a>ログ コレクターのエラー

|問題|解決方法|
|----|----|
|FTP でログ コレクターに接続できません|1.SSH の資格情報ではなく、FTP の資格情報を使用していることを確認します。 <br />2.使用している FTP クライアントが SFTP に設定されていないことを確認します。|
|コレクター構成を更新できませんでした|1.最新のアクセス トークンを入力したことを確認します。 <br />2.ファイアウォールで、ログ コレクターがポート 443 で送信トラフィックを開始することが許可されていることを確認します。|
|コレクターに送信されたログがポータルに表示されません|1.ガバナンス ログに失敗した解析タスクがあるかどうかを確認します。  <br />  &nbsp;&nbsp;&nbsp;&nbsp;ある場合は、上記のログ解析エラー一覧を参照してエラーを解決してください。<br /> 2.ない場合は、ポータルでデータ ソースとログ コレクターの構成を確認します。 <br /> &nbsp;&nbsp;&nbsp;&nbsp;a. [データ ソース] ページで、使用しているデータ ソースが正確に構成されていることを確認します。 <br />&nbsp;&nbsp;&nbsp;&nbsp;b. [ログ コレクター] ページで、データ ソースが正しいログ コレクターにリンクされていることを確認します。 <br /> 3.オンプレミス ログ コレクター コンピューターのローカル構成を確認します。  <br />&nbsp;&nbsp;&nbsp;&nbsp;a. SSH でログ コレクターにログインし、collector_config ユーティリティを実行します。<br/>&nbsp;&nbsp;&nbsp;&nbsp;b. 定義したプロトコル (Syslog/TCP、Syslog/UDP、または FTP) を使用してファイアウォールまたはプロキシがログをログ コレクターに送信していること、および正しいポートとディレクトリに送信していることを確認します。<br /> &nbsp;&nbsp;&nbsp;&nbsp;c. コンピューターで netstat を実行し、ファイアウォールまたはプロキシからの接続を受信していることを確認します <br /> 4. ログ コレクターがポート 443 で送信トラフィックを開始することが許可されていることを確認します。|

## <a name="see-also"></a>参照  
[クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)   
[テクニカル サポートが必要な場合は、Cloud App Security のサポート ページをご利用ください。](http://support.microsoft.com/oas/default.aspx?prid=16031)   
[Premier サポートをご利用のお客様は、Premier ポータルから直接 Cloud App Security を選択することもできます。](https://premier.microsoft.com/)  
  
  


<!--HONumber=Oct16_HO4-->

