---
title: 'Exchange 2013 のインストールの確認: Exchange 2013 Help'
TOCTitle: Exchange 2013 のインストールの確認
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 49129908
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 のインストールの確認

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

Microsoft Exchange Server 2013 をインストールした後で、**Get-ExchangeServer** コマンドレットを実行し、セットアップ ログ ファイルを参照してインストールを確認することをお勧めします。セットアップ プロセスが失敗した場合や、インストール中にエラーが発生した場合は、セットアップ ログ ファイルを使用して問題の原因を突き止めることができます。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

## Get-ExchangeServer を実行する

Exchange 2013 が正常にインストールされたことを確認するには、Exchange 管理シェルで **Get-ExchangeServer** コマンドレットを実行します。このコマンドレットを実行すると、指定したサーバーにインストールされているすべての Exchange 2013 サーバーの役割の一覧が表示されます。

構文およびパラメーターの詳細については、「[Get-ExchangeServer](https://technet.microsoft.com/ja-jp/library/bb123873\(v=exchg.150\))」を参照してください。

## セットアップ ログ ファイルを確認する

また、セットアップ処理中に作成されたセットアップ ログを確認して、Exchange 2013 のインストールと構成の詳細を調べることもできます。

インストール中に、Exchange セットアップによって、Service Pack 1 (SP1) を適用した Windows Server 2008 R2 および Windows Server 2012 を実行しているコンピューター上の**\[イベント ビューアー\]** の **\[アプリケーション\]** ログにイベントがログ出力されます。**\[アプリケーション\]** ログを調べて、Exchange セットアップに関連した警告またはエラー メッセージがないことを確認します。これらのログ ファイルには、Exchange 2013 セットアップ中にシステムによって実行された各操作の履歴および発生した可能性があるエラーが含まれます。既定では、ログ出力方法は `Verbose` に設定されます。情報は、インストールされているサーバーの役割ごとに入手可能です。

セットアップ ログ ファイルは、*\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log にあります。*\<system drive\>* 変数は、オペレーティング システムがインストールされているドライブのルート ディレクトリを表します。

セットアップ ログ ファイルは、Exchange 2013 のインストールおよび構成中に実行されるすべてのタスクの進行状況を追跡するものです。ファイルには、インストールの開始前に実行される前提条件とシステムの準備の確認の状態、アプリケーションのインストールの進行状況、およびシステムに対して行われた構成変更に関する情報が含まれます。このログ ファイルを調べて、サーバーの役割が期待どおりにインストールされたことを確認します。

セットアップ ログ ファイルの確認は、エラーを確認することから始めることをお勧めします。エラーが発生したことを示すエントリが見つかった場合は、関連するテキストに目を通してエラーの原因を特定します。

