---
title: 'メールボックス データベース コピーを削除する: Exchange 2013 Help'
TOCTitle: メールボックス データベース コピーを削除する
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 48269849
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックス データベース コピーを削除する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-06_

ここでは、メールボックス データベース コピーを削除する手順について説明します。メールボックス データベースの最後のコピーは、これらの手順では削除できません。メールボックス データベース コピーの最後のコピーを削除する手順の詳細については、「[メールボックス データベースを削除する](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)」または「[Remove-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/aa997931\(v=exchg.150\))」を参照してください。

メールボックス データベース コピーに関連する他の管理タスクについては、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間: 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - メールボックス データベース コピーは、正常なデータベース可用性グループ (DAG) からしか削除できません。クォーラムが失われたために DAG の基になるクラスターがダウンした場合など、DAG が正常でない場合、メールボックス データベース コピーを移動できなくなります。

  - データベースの最新のパッシブ コピーを削除する場合、指定したメールボックス データベースの連続レプリケーション循環ログ (CRCL) が無効である必要があります。CRCL が有効である場合、先に無効にする必要があります。メールボックス データベースのコピーが削除した後で、循環ログを有効にできます。レプリケートされていないメールボックス データベースの循環ログを有効にすると、CRCL の代わりに JET 循環ログが使用されます。データベースの最新のパッシブ コピーを削除していない場合は、CRCL を有効のままにできます。

  - データベース コピーを削除した後、データベース コピーを削除するサーバーからすべてのデータベースとトランザクション ログ ファイルを手動で削除する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス データベース コピーを削除する

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  コピーを削除するメールボックス データベースを選択します。

3.  \[詳細\] ウィンドウで、削除するパッシブ コピーを見つけ、<strong>削除</strong> をクリックします。

4.  警告ダイアログ ボックスで <strong>はい</strong> をクリックして、削除することを確認します。

5.  メッセージを確認してから、<strong>OK</strong> をクリックして、削除を確認します。

6.  データベース コピーを削除しているサーバーから、データベースとトランザクション ログ ファイルを手動で削除します。

## シェルを使用してメールボックス データベース コピーを削除する

この例を実行すると、メールボックス サーバー MBX1 からメールボックス データベース DB1 のコピーが削除されます。

    Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False

## 正常な動作を確認する方法

メールボックス データベース コピーが正常に削除されたことを確認するには、次のいずれかを実行します。

  - EAC で <strong>サーバー</strong> \> <strong>データベース</strong> に移動します。適切なデータベースを選択し、\[詳細\] ウィンドウで削除されたパッシブ コピーが表示されないことを確認します。

  - シェルで次のコマンドを実行して、コピーの削除を確認します。
    
        Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
    
    削除されたパッシブ コピーは表示されなくなります。

