---
title: 'Information Rights Management のログ出力を有効または無効にする: Exchange 2013 Help'
TOCTitle: Information Rights Management のログ出力を有効または無効にする
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 49896292
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Information Rights Management のログ出力を有効または無効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-12_

Exchange Server 2013 では、Information Rights Management (IRM) ログを利用して IRM の操作の監視およびトラブルシューティングを行うことができます。 既定では、IRM のログ出力は有効になっています。

IRM ログでは、次の共通パラメーター セットを使用します。

  - *IrmLogEnabled*   IRM のログ出力を有効または無効にする。 既定値は次のとおりです。 `$true`.

  - *IrmLogMaxAge*   IRM ログ ファイルの最大保存期間を指定します。 指定した期間より古いファイルは削除されます。 既定値は次のとおりです。 30 日

  - *IrmLogMaxDirectorySize*   IRM ログが含まれるディレクトリの最大サイズを指定します。 ディレクトリが最大ファイル サイズに到達すると、最も古いログ ファイルから削除されます。 既定値は次のとおりです。250 MB

  - *IrmLogMaxFileSize*   各 IRM ログ ファイルの最大サイズを指定します。 ログ ファイルが指定したサイズに達すると、新しいログ ファイルが作成されます。 既定値は次のとおりです。 10 MB

  - *IrmLogPath*   IRM ログ ディレクトリの場所を指定します。 既定値は次のとおりです。`%ExchangeInstallPath%Logging\IRMLogs`.

IRM に関連する追加の管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 ～ 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「IRM ログ出力の構成」。

  - Exchange 管理センター (EAC) を使用して、サーバーでの IRM ログ出力を有効または無効にすることはできません。 シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して、サーバーで IRM ログ出力を有効にする

この例では、メールボックス サーバーで IRM ログを有効にしています。

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $true

構文およびパラメーターの詳細については、「[Set-TransportService](https://technet.microsoft.com/ja-jp/library/jj215682\(v=exchg.150\))」を参照してください。

## シェルを使用して、サーバーで IRM ログ出力を無効にする

この例では、メールボックス サーバーで IRM ログを無効にしています。

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $false

構文およびパラメーターの詳細については、「[Set-TransportService](https://technet.microsoft.com/ja-jp/library/jj215682\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

サーバーで IRM ログが正しく有効または無効にされたことを確認するには、[Get-TransportService](https://technet.microsoft.com/ja-jp/library/jj215746\(v=exchg.150\)) コマンドレットを実行して IRM の設定を取得します。

この例では、EXCH01 サーバー上のすべての IRM ログのプロパティを取得します。

    Get-TransportService -Identity EXCH01 | Format-List IRMLog*

