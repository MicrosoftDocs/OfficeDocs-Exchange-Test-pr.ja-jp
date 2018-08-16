---
title: MRS 正常性セットのトラブルシューティング
TOCTitle: MRS 正常性セットのトラブルシューティング
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53181831
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MRS 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Mailbox Replication サービス (MRS) 正常性セットは、MRS サービスの全体的な状態を監視します。

## 説明

MRS サービスは、次のプローブとモニターを使用して監視されます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>正常性セット</th>
<th>依存関係</th>
<th>関連するモニター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>インフォメーション ストア</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する MRS 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **MRSServiceCrashingMonitor** だとします。そのモニターに関連するプローブは **MRSServiceCrashingProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値が Succeeded ではない場合は、次のセクションで説明する回復手順を参照してください。

## 一般的な問題

正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。

  - 警告を送信したサーバーの名前

  - 警告の発生日時

  - 使用された認証メカニズムと資格情報

  - 最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)
    
    完全な例外追跡に記載された情報を使用して、問題をトラブルシューティングできます。プローブによって生成された例外には、プローブが失敗した理由を説明する「エラーの理由」が含まれています。

**ロックされたメールボックス**

メールボックスがロックされていると、次のような警告を受信することがあります。

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: Primary (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, Protected Database: exampledb-db089 Exception: MapiExceptionADUnavailable: Unable to prepopulate the cache for user …*

これは、メールボックスがロックされていることを示します。メールボックスをロック解除するには、次のコマンドを実行します。

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]**

注**   このコマンドの \<*mailboxIdentity*\> は、電子メールのメッセージで提示された **MailboxIdentity** に置き換えてください。メールボックスがアーカイブ メールボックスの場合は、**–Archive** フラグも指定する必要があります。メールボックスがプライマリ メールボックスかアーカイブ メールボックスかは、警告の **MailboxGuid** フィールドで確認できます。

**破損した移行ジョブ**

破損した移行ジョブが発生すると、次のような警告を受信することがあります。

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

破損は、移行のメタ データに問題があったときに発生します。破損が発生すると、Microsoft はワトソン博士のレポートを受信します。この問題から回復するには、移行バッチを削除して、再作成する必要があります。そのためには、以下の手順を実行します。

1.  破損したバッチを削除するには、次のコマンドを実行します。
    
        Remove-MigrationBatch -Identity

2.  バッチ ジョブを再作成するには、次のコマンドを実行します。
    
        New-MigrationBatch -Local -Name

詳細については、「[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))」を参照してください。

**MailboxMigration の警告:CriticalError**

メールの移行中に重大なエラーが発生すると、次のような警告を受信することがあります。

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

この問題を解決するには、移行を再試行する必要があります。そのためには、次のコマンドを実行するか、Exchange 管理センター (EAC) の <strong>開始</strong> ボタンを押します。

    Call start-migrationbatch -Identity batchName

この問題が発生すると、調査のためにワトソン博士のメッセージが Microsoft に送信されます。

**Migration Exchange Replication サービスが実行されていません**

このエラー理由が表示された場合は、次のコマンドを実行して、サービスの状態を確認できます。

    Test-MRSHealth <servername> -MonitoringContext:$true

また、次のコマンドを実行して、サービスの起動を試みることもできます。

    Start-Service msexchangemailboxreplication

**MSExchangeMailboxReplication RCP Ping に失敗しました**

このエラー理由が表示された場合は、次のような警告を受信することがあります。

*An issue with MRS was detected at 6/26/2012 6:08:47 AM. Details: MRS RPC Ping check for server \<ServerName\> failed with the following error: The RPC endpoint for the Microsoft Exchange Mailbox Replication service couldn't respond:*

この問題が発生した場合は、次のコマンドを実行して、サービスの状態を確認できます。

    Test-MRSHealth <servername> -MonitoringContext:$true

また、次のコマンドを実行して、サービスの再起動を試みることもできます。

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication サービスが繰り返しクラッシュしています**

MSExchangeMailboxReplication サービスがクラッシュしたり、応答しなくなったりした場合、次のような警告を受信することがあります。

*The MRS process has crashed at least 3 times in last 01:00:00. \<b\>Watson Message:\</b\> Watson report about to be sent for process id: 41432, with parameters: E12, \<ServerName\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

この問題が発生した場合は、次のコマンドを実行して、サービスの状態を確認できます。

    Test-MRSHealth <servername> -MonitoringContext:$true

また、次のコマンドを実行して、サービスの再起動を試みることもできます。

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication が MDB キューをスキャンしていません**

MSExchangeMailboxReplication サービスがキューのスキャンに失敗すると、次のような警告を受信することがあります。

*An issue with MRS was detected at 6/12/2012 6:20:44 PM. Details: MRS queue scan check for server \<servername\> failed with the following error: The Microsoft Exchange Mailbox Replication Service isn't scanning mailbox database queues for jobs. Last scan age: 04:38:02.1959439..*

この問題が発生した場合は、次のコマンドを実行して、サービスの状態を確認できます。

    Test-MRSHealth <servername> -MonitoringContext:$true

また、次のコマンドを実行して、サービスの再起動を試みることもできます。

    Restart-Service msexchangemailboxreplication

**他のトラブルシューティング手順**

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続して、**MSExchangeServicesAppPool** アプリケーション プールが実行されていることを確認します。

2.  IIS マネージャーで <strong>アプリケーション プール</strong> をクリックし、シェルから次のコマンドを実行して、**MSExchangeServicesAppPool** アプリケーション プールをリサイクルします。
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

4.  問題がまだ存在している場合は、IISReset ユーティリティを使用するか、次のコマンドを実行して、IIS サービスをリサイクルします。
    
        Iisreset /noforce

5.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

6.  問題がまだ存在している場合は、サーバーを再起動します。

7.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

8.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、<strong>サポート オプションとリソース</strong> をクリックし、<strong>テクニカル サポートを利用する</strong> に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

