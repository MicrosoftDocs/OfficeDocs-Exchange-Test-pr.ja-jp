---
title: 'メールボックス データベース コピー用にメールボックス データベース パスを移動する: Exchange 2013 Help'
TOCTitle: メールボックス データベース コピー用にメールボックス データベース パスを移動する
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 48269333
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックス データベース コピー用にメールボックス データベース パスを移動する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-05-07_

メールボックス データベースを作成した後、EAC またはシェルを使用して、そのデータベースを別のボリューム、フォルダー、場所、またはパスに移動できます。レプリケートされないメールボックス データベースのデータベース パスを移動する方法の詳細な手順については、「[Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)」を参照してください。

移動対象のメールボックス データベースが 1 つ以上のメールボックス データベース コピーにレプリケートされる場合は、このトピックの手順に従ってメールボックス データベース パスを移動する必要があります。メールボックス データベースのすべてのコピーは、コピーをホストしている各サーバーの同じパスに置かれている必要があります。たとえば、データベース DB1 がサーバー EX1 の C:\\mountpoints\\DB1 に置かれている場合、サーバー EX2、EX3 などの DB1 のコピーも C:\\mountpoints\\DB1 に置かれている必要があります。

メールボックス データベース コピーに関連する他の管理タスクについては、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:2 分 + データの移動にかかる時間。ただしこの時間は、データベースのサイズ、転送速度、利用できる帯域幅、ネットワークの待機時間、ストレージの書き込み速度などさまざまな要因によって異なります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - 移動操作を実行するには、対象のデータベースを一時的にマウント解除し、どのユーザーからもアクセスできないようにする必要があります。既にマウント解除されている場合には、操作が完了しても再マウントされません。

  - 移動操作を実行するには、データベースのレプリケーションをすべてのコピーに対して無効にする必要があります。レプリケーションを中断するだけでは不十分です。[Remove-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335119\(v=exchg.150\)) コマンドレットを使用してデータベース コピーを削除することで、レプリケーションを無効にする必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用してレプリケートされたメールボックス データベースを新しいパスに移動する


> [!NOTE]
> EAC を使用して、レプリケートされたメールボックス データベースを新しいパスに移動することはできません。



1.  移動するメールボックス データベースのすべてのコピーの再生ラグ設定または切り詰めラグ設定に注意してください。この情報を取得するには、次の例のように [Get-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb124924\(v=exchg.150\)) コマンドレットを使用します。
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  データベースに対して循環ログが有効になっている場合、処理の前に無効にする必要があります。メールボックス データベースの循環ログを無効にするには、次の例のように [Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\)) コマンドレットを使用します。
    
    ```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $false
```

3.  移動するデータベースのすべてのメールボックス データベース コピーを削除します。詳細な手順については、「[メールボックス データベース コピーを削除する](remove-a-mailbox-database-copy-exchange-2013-help.md)」を参照してください。すべてのコピーを削除した後、別の場所に移動することでそのデータベース コピーを削除する各サーバーのデータベース ファイルやトランザクション ログ ファイルを保持します。これらのファイルは保持されるため、再度追加した後でも、データベース コピーを再シードする必要はありません。

4.  メールボックス データベース パスを新しい場所に移動します。詳細な手順については、「[Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)」を参照してください。
    

    > [!IMPORTANT]
    > 移動操作中には、移動するデータベースをマウント解除する必要があります。移動が完了するまで、この処理によって、移動中のデータベースのメールボックスを使用しているすべてのユーザーに対して、サービスが中断し停止します。移動操作が完了したら、データベースが自動的にマウントされます。



5.  移動されたメールボックス データベースのパッシブ コピーが以前含まれていた各メールボックス サーバーに、必要なフォルダー構造を作成します。たとえば、データベースを C:\\mountpoints\\DB1 に移動した場合、メールボックス データベース コピーをホストする各メールボックス サーバー上にこれと同じパスを作成する必要があります。

6.  フォルダー構造を作成した後、メールボックス データベースのパッシブ コピーとそのログ ストリームを新しい場所に移動します。これらは、手順 3. で残され、その手順後に保持されたファイルです。手順 3. で削除された各データベース コピーについて、この処理を繰り返します。

7.  手順 3. で削除されたすべてのデータベース コピーを追加します。詳細な手順については、「[メールボックス データベース コピーを追加する](add-a-mailbox-database-copy-exchange-2013-help.md)」を参照してください。

8.  移動するメールボックス データベースのコピーを含む各サーバーで、次のコマンドを実行して、コンテンツ インデックス サービスを停止し、再開します。
    
        Net stop MSExchangeFastSearch
        Net start MSExchangeFastSearch

9.  必要に応じて、次の例のように、[Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\)) コマンドレットを使用して循環ログを有効にします。
    
    ```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $true
```

10. 次の例のように、[Set-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd298104\(v=exchg.150\)) コマンドレットを使用して、再生ラグ タイムと切り詰めラグ タイム用に以前に設定された値を再構成します。
    
    ```powershell
Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00
```

11. 各コピーを追加する場合、次のコピーを追加する前に、コピーの稼働状態を確認することをお勧めします。次の方法で、稼動状態を確認できます。
    
    1.  データベースまたはデータベース コピーに関連するエラー イベントまたは警告イベントのイベント ログを調べる。
    
    2.  [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ja-jp/library/dd298044\(v=exchg.150\)) コマンドレットを使用して、データベース コピーの連続レプリケーションの稼動状態を確認する。
    
    3.  [Test-ReplicationHealth](https://technet.microsoft.com/ja-jp/library/bb691314\(v=exchg.150\)) コマンドレットを使用して、データベース可用性グループと連続レプリケーションの稼動状態を確認する。

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ja-jp/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/ja-jp/library/bb691314\(v=exchg.150\))

## 正常な動作を確認する方法

メールボックス データベースのコピーのパスが正しく移動できたことを確認するには、以下の手順を実行します。

  - EAC で <strong>サーバー</strong> \> <strong>データベース</strong> に移動します。コピーされたデータベースを選択します。詳細ペインに、データベースのコピーの状況とそのコンテンツ インデックスが、現在のコピー キューの長さと共に表示されます。正常な状態であることを確認します。

  - シェルで次のコマンドを実行して、メールボックス データベースのコピーが作成され、かつ正常な状態にあることを確認します。
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
```
    
    ステータスとコンテンツ インデックス ステータスの両方が正常である必要があります。

