---
title: '回復用データベースを使用してデータを復元する: Exchange 2013 Help'
TOCTitle: 回復用データベースを使用してデータを復元する
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 48270110
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 回復用データベースを使用してデータを復元する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-10-01_

回復用データベース (RDB) は特別な種類のメールボックス データベースで、回復操作の一部として、復元されたメールボックス データベースをマウントし、そこからデータを抽出できます。RDB を使用すると、ユーザーが現在のデータにアクセスできる状態のまま、データベースのバックアップやコピーからデータを回復できます。

RDB を作成した後で、バックアップ アプリケーションを使用するか、データベースとそのログ ファイルを RDB フォルダー構造にコピーすることで、メールボックス データベースを RDB に復元できます。次に、[New-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829875\(v=exchg.150\)) コマンドレットを使用して回復したデータベースからデータを抽出できます。抽出後に、データをフォルダーにエクスポートしたり、既存のメールボックスに結合したりできます。

RDB に関連する追加の管理タスクについては、「[回復用データベース](recovery-databases-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:1 分 + データベースをクリーン シャットダウン状態にし、データを抽出するためにかかる時間。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 [受信者のアクセス許可](recipients-permissions-exchange-2013-help.md) の「メールボックス回復」。

  - 一部のバックアップ アプリケーションでは、Exchange データを回復用データベースに直接復元することができます。Windows サーバーのバックアップでは、回復用データベースに復元できるのはファイル レベルのバックアップのみです。アプリケーション レベルのバックアップの回復用データベースへの復元には使用できません。

  - 回復したデータを含むデータベースとログ ファイルは、RDB フォルダー構造に復元またはコピーする必要があります。

  - データベースがクリーン シャットダウン状態である必要があります。RDB はすべてのデータベースの代替の復元場所であるため、すべての復元済みデータベースはダーティ シャットダウンの状態です。**Eseutil /R** を使用して、復元済みデータベースをクリーン シャットダウンの状態にする必要があります。

## シェルを使用して、回復用データベースを使用したデータを回復するには

1.  回復用データベースに使用する場所に、復元済みデータベースとそのログ ファイルをコピーするか、データベースとそのログ ファイルを復元します。

2.  Eseutil を使用して、そのデータベースをクリーン シャットダウンの状態にします。次の例で、EXX はデータベースのログ生成プレフィックスです (E00、E01、E02 など)。
    
        Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
    
    次の例は、ログ生成プレフィックスが E01、回復用データベースおよびログ ファイルのパスが E:\\Databases\\RDB1 です。
    
        Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1

3.  回復用データベースを作成します。回復用データベースに一意の名前を付けます。ただし、EdbFilePath パラメーターにはデータベース ファイルの名前とパスを使用し、LogFolderPath パラメーターには復元済みログ ファイルの場所を使用します。
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    
    次の例では、E:\\Databases\\RDB1 にある DB1.edb とそのログ ファイルの復元に使用される回復用データベースの作成方法を示します。
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"

4.  Microsoft Exchange Information Store サービスを再開します。
    
        Restart-Service MSExchangeIS

5.  回復用データベースをマウントします。
    
        Mount-database <RDBName>

6.  マウントされたデータベースに、復元するメールボックスが含まれていることを確認します。
    
        Get-MailboxStatistics -Database <RDBName> | ft -auto

7.  New-MailboxRestoreRequest コマンドレットを使用して、メールボックスまたはアイテムを回復用データベースから運用中のメールボックスに復元します。
    
    次の例では、メールボックス データベース DB1 にある MailboxGUID が 1d20855f-fd54-4681-98e6-e249f7326ddd の復元元メールボックスを、エイリアスが Morris の復元先メールボックスに復元します。
    
        New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    
    次の例では、メールボックス データベース DB1 の表示名が Morris Cornejo である復元元メールボックスの内容を Morris@contoso.com のアーカイブ メールボックスに復元します。
    
        New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive

8.  [Get-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829907\(v=exchg.150\)) を使用してメールボックス復元要求の状態を定期的に確認します。
    
    復元の状態が \[完了\] になったら、[Remove-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829910\(v=exchg.150\)) を使用して復元要求を削除します。たとえば、次のようにです。
    
        Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

## 正常な動作を確認する方法

メールボックスが正常に復元されたことを確認するには、Outlook または Outlook Web App を使用してターゲット メールボックスを開き、復元されたデータが存在することを確認します。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


