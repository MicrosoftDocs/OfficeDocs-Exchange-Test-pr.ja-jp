---
title: 'メールボックス データベース コピーを中断または再開する: Exchange 2013 Help'
TOCTitle: メールボックス データベース コピーを中断または再開する
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 48269822
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックス データベース コピーを中断または再開する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-02_

さまざまな理由で、データベース コピーを中断または再開する必要があることがあります。たとえば、データベース コピーを含むディスクの保守や、障害復旧を目的とした個々のデータベース コピーのアクティブ化の中断などです。

メールボックス データベース コピーに関連する他の管理タスクについては、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間: 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス データベース コピーを中断する

1.  EAC で、**\[サーバー\]** \> **\[データベース\]** に移動します。

2.  コピーを中断するデータベースを選択します。

3.  \[詳細\] ウィンドウの **\[データベース コピー\]** で、中断するデータベース コピーの下の **\[中断\]** をクリックします。

4.  **\[コメント\]** フィールドに、中断の理由を示す最大 512 文字のコメント (省略可能) を追加します。

5.  自動アクティブ化によるデータベース コピーを中断するには、**\[このコピーは手動操作によってのみアクティブにできます\]** チェック ボックスをオンにします。

6.  **\[保存\]** をクリックしてデータベース コピーを中断します。

## EAC を使用してメールボックス データベース コピーを再開する

1.  EAC で、**\[サーバー\]** \> **\[データベース\]** に移動します。

2.  コピーを再開するデータベースを選択します。

3.  \[詳細\] ウィンドウの **\[データベース コピー\]** で、再開するデータベース コピーの下の **\[再開\]** をクリックします。

4.  **\[はい\]** をクリックしてデータベース コピーを再開します。

## シェルを使用してメールボックス データベース コピーを中断する

この例では、サーバー MBX1 上でホストされているデータベース DB1 のコピーの連続レプリケーションを中断します。オプションのコメントも指定されています。

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False

この例では、サーバー MBX2 上でホストされているデータベース DB2 のコピーのアクティブ化を中断します。

    Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False

## シェルを使用してメールボックス データベース コピーを再開する

この例では、サーバー MBX1 上にあるデータベース DB1 のコピーを再開します。

    Resume-MailboxDatabaseCopy -Identity DB1\MBX1

この例では、レプリケーション専用のサーバー MBX2 上にあるデータベース DB2 のコピーを再開します。

    Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly

## 正常な動作を確認する方法

メールボックス データベース コピーが正常に中断または再開されたことを確認するには、次のいずれかを実行します。

  - EAC で **\[サーバー\]** \> **\[データベース\]** に移動します。適切なデータベースを選択し、\[詳細\] ウィンドウで **\[詳細の表示\]** をクリックして、データベース コピーのプロパティを表示します。

  - シェルで次のコマンドを実行して、データベース コピーの状態情報を表示します。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

