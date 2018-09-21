---
title: '遅延メールボックス データベース コピーをアクティブにする: Exchange 2013 Help'
TOCTitle: 遅延メールボックス データベース コピーをアクティブにする
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 48269455
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 遅延メールボックス データベース コピーをアクティブにする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-01-28_

遅延メールボックス データベース コピーは、再生ラグ タイムが 0 よりも大きい値で構成されたメールボックス データベース コピーです。遅延メールボックス データベース コピーのアクティブ化および回復は、すべてのログ ファイルを再生してデータベース コピーを現行データベースにする場合に行う簡単な処理です。ログ ファイルを特定の時点まで再生する場合は、ログ ファイルを手動で操作して Eseutil コマンドを実行する必要があるため、複雑な処理になります。

遅延メールボックス データベース コピーに関するその他の情報については、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 遅延メールボックス データベース コピーのアクティブ化にかかる時間は、再生が必要なログ ファイルの数とハードウェアによる再生速度が直接影響します。最低でも、ログ再生速度は、少なくとも、データベースごとに 1 秒あたり 2 ログとなるはずです。



## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:1 分に、時間差コピーの複製、必要なログ ファイルの再生、クライアント アクティビティ用のデータの抽出またはデータベースのマウントにかかった時間を加えた時間

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - アクティブ化しているメールボックス データベース コピーは、再生ラグ タイムを 0 よりも大きい値で構成する必要があります。

  - アクティブ化しているメールボックス データベース コピーには、回復する時点までのすべてのログ ファイルが必要です。回復する時点を決定するときに、データベース トランザクションは複数のログ ファイルにまたがることが可能であることを忘れないでください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して遅延メールボックス データベース コピーを特定時点までアクティブにする


> [!NOTE]
> EAC を使用して、遅延メールボックス データベース コピーを特定時点までアクティブにすることはできません。代わりに、シェルとコマンド ラインを使用して一連の手順を実行します。



1.  この例では、[Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd351074\(v=exchg.150\)) コマンドレットを使用して、アクティブ化されている時間差コピーのレプリケーションを中断します。
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  オプションで (時間差コピーを保存するために)、データベース コピーとそのログ ファイルのコピーを作成します。
    

    > [!NOTE]
    > この時点で、既存のボリュームに対してこの手順を引き続き実行すると、コピーの書き込みパフォーマンスが低下する可能性があります。これが望ましくない場合は、データベースおよびログ ファイルを別のボリュームにコピーして、回復を実行することができます。



3.  この回復の時刻指定要件を満たすためにデータベース内への再生にログ ファイルが必要であるかどうかを確認します (Windows Explorer のように、ログ ファイル日付および時刻に基づいて行われます)。この時点以降に作成されたすべてのログは、回復プロセスが完了するまで別のディレクトリに移動する必要があります。ログは必要ありません。

4.  データベースのチェックポイント (.chk) ファイルを削除します。

5.  この例では、Eseutil を使用して回復操作を実行します。
    
    ```powershell
Eseutil.exe /r eXX /a
```
    

    > [!NOTE]
    > 前の例で、e<EM>XX</EM> はデータベースのログ生成プレフィックスです (E00、E01、E02 など)。

    

    > [!IMPORTANT]
    > この手順には、再生ラグ タイムの長さ、その期間に生成されたログ ファイルの数、回復中のデータベースにハードウェアがそれらのログを再生できる速度など、さまざまな要素によって決まるので、相当時間がかかる場合があります。



6.  ログ再生が完了したら、データベースはクリーン シャットダウン状態になり、回復の目的でコピーおよび使用できるようになります。

7.  回復プロセスが完了した後、この例では、回復プロセスの一部として使用されたデータベースのレプリケーションを再開します。
    
    ```powershell
Resume-MailboxDatabaseCopy DB1\EX3
```

構文およびパラメーターの詳細については、「[Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd351074\(v=exchg.150\))」または「[Resume-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335220\(v=exchg.150\))」を参照してください。

## シェルを使用し、コミットされていないすべてのログ ファイルを再生して、時間差メールボックス データベース コピーをアクティブにする

1.  オプションで (時間差コピーを保存するために)、データベース コピーとそのログ ファイルのコピーを作成します。
    
    1.  この例では、[Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd351074\(v=exchg.150\)) コマンドレットを使用して、アクティブ化されている時間差コピーのレプリケーションを中断します。
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  オプションで (時間差コピーを保存するために)、データベース コピーとそのログ ファイルのコピーを作成します。
        

        > [!NOTE]
        > この時点で、既存のボリュームに対してこの手順を引き続き実行すると、コピーの書き込みパフォーマンスが低下する可能性があります。これが望ましくない場合は、データベースおよびログ ファイルを別のボリュームにコピーして、回復を実行することができます。



2.  この例では、[Move-ActiveMailboxDatabase](https://technet.microsoft.com/ja-jp/library/dd298068\(v=exchg.150\)) コマンドレットと *SkipLagChecks* パラメーターを使用して、遅延メールボックス データベース コピーをアクティブにします。
    
    ```powershell
Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks
```

## シェルで SafetyNet 回復を使用して遅延メールボックス データベース コピーをアクティブにする

1.  必要に応じて (時間差コピーを保持する場合)、データベース コピーおよびそのログ ファイルを含むボリュームについて、ファイル システムに基づく (Exchange 非対応) ボリューム シャドウ コピー サービス (VSS) スナップショットを取得します。
    
    1.  この例では、[Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd351074\(v=exchg.150\)) コマンドレットを使用して、アクティブ化されている時間差コピーのレプリケーションを中断します。
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  オプションで (時間差コピーを保存するために)、データベース コピーとそのログ ファイルのコピーを作成します。
        

        > [!NOTE]
        > この時点で、既存のボリュームに対してこの手順を引き続き実行すると、コピーの書き込みパフォーマンスが低下する可能性があります。これが望ましくない場合は、データベースおよびログ ファイルを別のボリュームにコピーして、回復を実行することができます。



2.  ESEUTIL データベース ヘッダー出力内の "Log Required:" の値を検索することによって時間差データベース コピーに必要なログを決定する
    
    ```powershell
Eseutil /mh <DBPath> | findstr /c:"Log Required"
```
    
    括弧内の 16 進数を書き留めます。最初の数字は必要な最小生成 (LowGeneration と呼ばれる) で、2 つ目の数字は必要な最大生成 (HighGeneration と呼ばれる) です。生成シーケンスが HighGeneration より大きいすべてのログ生成ファイルを別の場所に移して、データベースに再生されないようにします。

3.  データベースのアクティブ コピーをホストしているサーバーで、アクティブ コピーからアクティブになっている時間差コピーのログ ファイルを削除するか、Microsoft Exchange Replication Service を停止します。

4.  データベースの切り替えを実行して、時間差コピーをアクティブにします。この例では、[Move-ActiveMailboxDatabase](https://technet.microsoft.com/ja-jp/library/dd298068\(v=exchg.150\)) コマンドレットといくつかのパラメーターを使用してデータベースをアクティブにします。
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  この時点で、データベースは自動的にマウントし、SafetyNet から見つからないメッセージの再配信を要求します。

## 正常な動作を確認する方法

遅延メールボックス データベース コピーが正常にアクティブになったことを確認するには、次のいずれかの手順を実行します。

  - EAC で <strong>サーバー</strong> \> <strong>データベース</strong> に移動します。適切なデータベースを選択し、\[詳細\] ウィンドウで <strong>詳細の表示</strong> をクリックして、データベース コピーのプロパティを表示します。

  - シェルで次のコマンドを実行して、データベース コピーの状態情報を表示します。
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
```

