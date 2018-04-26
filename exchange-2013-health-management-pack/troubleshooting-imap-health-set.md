---
title: IMAP 正常性セットのトラブルシューティング
TOCTitle: IMAP 正常性セットのトラブルシューティング
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53181826
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IMAP 正常性セットのトラブルシューティング

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

IMAP 正常性セットは、クライアント アクセス サーバー (CAS) 上の IMAP4 プロキシ インフラストラクチャの可用性を監視します。IMAP 正常性セットは、次の正常性セットに密接に関連しています。

[IMAP.Protocol 正常性セットのトラブルシューティング](troubleshooting-imap-protocol-health-set.md)

[IMAP.Proxy 正常性セットのトラブルシューティング](troubleshooting-imap-proxy-health-set.md)

IMAP が正常でないことを示す警告を受け取った場合、それが示すのは、ユーザーが IMAP を使用して自分のメールボックスにアクセスできなくなる可能性がある問題です。

## 説明

IMAP4 サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>認証</p>
<p>メールボックス サーバーの認証</p>
<p>高可用性</p>
<p>ネットワーク</p></td>
<td><p>ImapCTPMonitor (IMAP 正常性セット)</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>IMAP.Proxy</p></td>
<td><p>Active Directory</p>
<p>認証</p></td>
<td><p>ImapProxyTestMonitor (IMAP.Proxy 正常性セット)</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>認証</p>
<p>インフォメーション ストア</p>
<p>高可用性</p></td>
<td><p>IMAP.Protocol (IMAP.Protocol 正常性セット)</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>認証</p></td>
<td><p>IMAP.Protocol (IMAP.Protocol 正常性セット)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (IMAP 正常性セット)</p></td>
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
        
        たとえば、server1.contoso.com に関する IMAP 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **ImapCTPMonitor** だとします。そのモニターに関連するプローブは **ImapCTPProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値が Succeeded ではない場合は、次のセクションで説明する回復手順を参照してください。

## ImapTestDeepMonitor と ImapSelfTestMonitor の回復操作

1.  バックエンド サーバー上の Exchange IMAP4 サービスを再起動します。IMAP4 サービスを停止および開始する方法の詳細については、「[IMAP4 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/bb124022\(v=exchg.150\))」を参照してください。

2.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

3.  問題がまだ存在している場合は、次のコマンドを使用して、メールボックス サーバーでホストされているデータベースをフェールオーバーする必要があります。
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  すべてのデータベースが、問題を報告しているサーバーから移動されたことを確認します。このためには、次のコマンドを実行します。
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    コマンド出力を確認し、サーバー上にアクティブなコピーがなければ、サーバーを再起動します。

5.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

6.  プローブが成功した場合は、次のコマンドを実行して、データベースをフェールオーバーします。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## ImapCTPMonitor の回復操作

このモニター警告は、通常は CA サーバーで発行されます。

1.  バックエンド サーバー上の Exchange IMAP4 サービスを再起動します。IMAP4 サービスの停止および開始の詳細については、「[IMAP4 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/bb124022\(v=exchg.150\))」を参照してください。

2.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

3.  問題がまだ存在している場合は、問題を解決するために、IMAP プロトコルのログを有効にする必要があります。そのためには、以下の手順を実行します。
    
    1.  Windows PowerShell で次のコマンドを実行します。
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  バックエンド サーバー上の Exchange IMAP4 サービスを再起動します。IMAP4 サービスを停止および開始する方法の詳細については、「[IMAP4 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/bb124022\(v=exchg.150\))」を参照してください。
    
    3.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。
    
    4.  次のコマンドを実行して、ログ ファイルの場所を確認します。このためには、次のコマンドを実行します。
        
            Get-ImapSettings -server <CAS server name>
    
    5.  このコマンドにサービスを提供しているメールボックスを特定します。メールボックス サーバーの名前は、エラー メッセージの `_Mbx:` 値の値です。
    
    6.  次のコマンドを実行します。
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **注**   このコマンドの *mailbox1.contoso.com* は、実際のメールボックス サーバー名に置き換えてください。
    
    7.  コマンド出力に一覧表示されたモニターの中に、正常でないと報告されたモニターがある場合は、まず、そのモニターを処置する必要があります。「ImapTestDeepMonitor と ImapSelfTestMonitor の回復操作」セクションに記載されているトラブルシューティング手順を実行してください。

4.  メールボックス サーバーが正常であると報告された場合は、CAS を再起動します。

5.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

6.  プロトコル ログを無効にします。このためには、次の Windows PowerShell コマンドを実行します。
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  IMAP4 サービスを再起動します。

8.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## ImapProxyTestMonitor の回復操作

1.  IMAP4 サービスを再起動します。

2.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

3.  プローブがまだ失敗している場合は、CAS を再起動します。

4.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

5.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## AverageCommandProcessingTimeGt60sMonitor と RequestsQueuedGt500Monitor の回復操作

このモニター警告は、通常は CA サーバーとメールボックス サーバーで発行されます。

1.  バックエンド サーバーまたは CAS 上の Exchange IMAP4 サービスを再起動します。IMAP4 サービスを停止および開始する方法の詳細については、「[IMAP4 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/bb124022\(v=exchg.150\))」を参照してください。

2.  モニターが正常状態に保たれるかどうかを確認するため、10 分間待ちます。10 分後に、次のコマンドを実行します。
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **注**   このコマンドの *server1.contoso.com* は、実際のサーバー名に置き換えてください。

3.  10 分間待ってから、手順 2 に示すコマンドを再度実行し、モニターの状態が正常のままかどうかを確認します。

4.  問題がまだ存在している場合は、サーバーを再起動する必要があります。サーバーが CAS の場合は、サーバーを再起動するだけです。サーバーがメールボックス サーバーの場合は、次の操作を行います。
    
    1.  サーバー上でホストされているデータベースをフェールオーバーします。このためには、次のコマンドを実行します。
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **注**   これ以降のすべてのコード例では、*server1.contoso.com* を実際のサーバー名に置き換えてください。
    
    2.  すべてのデータベースが、問題を報告しているサーバーから移動されたことを確認します。このためには、次のコマンドを実行します。
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        コマンド出力を確認し、サーバー上にアクティブなコピーがなければ、サーバーを再起動します。

5.  サーバーが再起動したら、10 分間待ってから、手順 2 に示すコマンドを再度実行し、モニターの状態が正常なままかどうかを確認します。

6.  モニターが正常なままであり、かつサーバーがメールボックス サーバーの場合は、次のコマンドを実行して、データベースをフェールオーバーします。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[POP3 と IMAP4](https://technet.microsoft.com/ja-jp/library/jj657728\(v=exchg.150\))

[Exchange 2013 で IMAP4 を有効にする](https://technet.microsoft.com/ja-jp/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/ja-jp/library/bb738126\(v=exchg.150\))

