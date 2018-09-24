---
title: 'データベースの移植性を使用して、メールボックス データベースを移動する: Exchange 2013 Help'
TOCTitle: データベースの移植性を使用して、メールボックス データベースを移動する
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51407561
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# データベースの移植性を使用して、メールボックス データベースを移動する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-16_

データベースの移植性を使用して、同じ組織内の Exchange 2013 メールボックス サーバー間で Microsoft Exchange Server 2013 メールボックス データベースを移動できます。これによって一部の障害シナリオ全体の回復時間を減らすことができます。詳細については、「[データベースの移植性](database-portability-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分に、データを復元し、データベース ファイルを移動し、Active Directory のレプリケーションが完了するまでの時間を合わせた時間。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス回復」。

  - EAC を使用して、データベースの移植性を使用し回復したデータベースまたはダイヤル トーン データベースにユーザー メールボックスを移動することはできません。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して、データベースの移植性を使用し回復したデータベースまたはダイヤル トーン データベースにユーザー メールボックスを移動する

1.  移動するデータベースがクリーン シャットダウン状態であることを確認します。データベースがクリーン シャットダウン状態でない場合は、ソフト リカバリを実行します。
    

    > [!NOTE]
    > ソフト リカバリを実行すると、コミットされていないすべてのログ ファイルがデータベースにコミットされます。必要なログ ファイルがすべて揃っていない場合、ソフト リカバリ処理を実行できません。手順 2. に進んでください。

    
    コミットされていないすべてのログ ファイルをデータベースにコミットするには、コマンド プロンプトから次のコマンドを実行します。
    
    ```powershell
    ESEUTIL /R <Enn>
    ```
    

    > [!NOTE]
    > &lt;E<EM>nn</EM>&gt; には、ログ ファイルの再生先のデータベースのログ ファイル プレフィックスを指定します。&lt;E<EM>nn</EM>&gt; で指定するログ ファイル プレフィックスは、Eseutil /r の必須パラメーターです。



2.  次の構文を使用して、サーバー上にデータベースを作成します。
    
    ```powershell
        New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>
    ```

3.  次の構文を使用して、*This database can be over written by restore* 属性を設定します。
    
    ```powershell
    Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true
    ```

4.  元のデータベース ファイル (.edb ファイル、ログ ファイル、Exchange Search カタログ) を、上で新しいデータベースを作成した時に指定したデータベース フォルダーに移動します。

5.  次の構文を使用して、データベースをマウントします。
    
    ```powershell
    Mount-Database <DatabaseName>
    ```

6.  データベースがマウントされたら、[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットを使用して、ユーザー アカウントが新しいメールボックス サーバーのメールボックスを参照するようにユーザー アカウントの設定を変更します。古いデータベースから新しいデータベースにすべてのユーザーを移動するには、次の構文を使用します。
    
    ```powershell
    Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>
    ```

7.  以下の構文を使用して、キュー内に残っているすべてのメッセージの配信をトリガーします。
    
    ```powershell
    Get-Queue <QueueName> | Retry-Queue -Resubmit $true
    ```

Active Directory のレプリケーションが完了したら、すべてのユーザーが新しい Exchange サーバーのメールボックスにアクセスできます。大半のクライアントは、自動検出によってリダイレクトされます。Microsoft Office Outlook Web App ユーザーも自動的にリダイレクトされます。

## 正常な動作を確認する方法

メールボックスが正常に移動されたことを確認するには、次の手順を実行します。

  - Outlook Web App を使用してメールボックスを開きます。

  - Microsoft Outlook を使用してメールボックスを開きます。

