---
title: ActiveSync 正常性セットのトラブルシューティング
TOCTitle: ActiveSync 正常性セットのトラブルシューティング
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53181832
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ActiveSync 正常性セットのトラブルシューティング

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Exchange ActiveSync 正常性セットは、組織内のモバイル クライアントの ActiveSync サービスの全体的な状態を監視します。ActiveSync 正常性セットは、次の正常性セットに密接に関連しています。

[ActiveSync.Protocol 正常性セットのトラブルシューティング](troubleshooting-activesync-protocol-health-set.md)

[ActiveSync.Proxy 正常性セットのトラブルシューティング](troubleshooting-activesync-proxy-health-set.md)

ActiveSync 正常性セットが正常でないことを示す警告を受け取った場合、それが示すのは、ユーザーが ActiveSync を使用して自分のメールボックスにアクセスできなくなる可能性がある問題です。

## 説明

ActiveSync サービスは、次のプローブとモニターを使用して監視されます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>プローブ</th>
<th>正常性セット</th>
<th>依存関係</th>
<th>関連するモニター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>認証</p>
<p>メールボックス サーバーの認証</p>
<p>インフォメーション ストア</p>
<p>高可用性</p>
<p>ネットワーク</p></td>
<td><p>ActiveSyncCTPMonitor (ActiveSync 正常性セット)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor (ActiveSync.Proxy 正常性セット)</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>認証</p>
<p>インフォメーション ストア</p>
<p>高可用性</p></td>
<td><p>ActiveSyncDeepTestMonitor (ActiveSync 正常性セット)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>認証</p></td>
<td><p>ActiveSyncSelfTestMonitor (ActiveSync.Protocol 正常性セット)</p>
<p>RequestsQueuedGt500Monitor (ActiveSync 正常性セット)</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、ActiveSync 正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題の確認

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する ActiveSync 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は **Unhealthy** になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **ActiveSyncCTPMonitor** だとします。そのモニターに関連するプローブは **ActiveSyncCTPProbe** です。このプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの Result セクションを確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値が Succeeded ではない場合は、次のセクションで説明する回復手順を参照してください。

## ActiveSyncDeepTestMonitor と ActiveSyncSelfTestMonitor の回復操作

このモニター警告は、通常はメールボックス サーバーで発行されます。回復操作を実行するには、次の手順に従います。

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続します。**\[アプリケーション プール\]** をクリックし、**MSExchangeSyncAppPool** という名前の ActiveSync アプリケーション プールをリサイクルします。

2.  関連するプローブを再実行します (「問題の確認」セクションの手順 2c を参照)。

3.  問題がまだ存在している場合は、IISReset ユーティリティを使用して、IIS サービス全体をリサイクルします。

4.  関連するプローブを再実行します (「問題の確認」セクションの手順 2c を参照)。

5.  問題がまだ存在している場合は、サーバーを再起動します。これを行うには、まず次のコマンドを使用して、サーバー上でホストされているデータベースをフェールオーバーします。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    これ以降のすべてのコード例では、*server1.contoso.com* を実際のサーバー名に置き換えてください。

6.  次に、すべてのデータベースが、問題を報告しているサーバーから移動されたことを確認します。このためには、次のコマンドを実行します。
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  手順 6 のコマンド出力を確認し、サーバー上にアクティブなコピーがなければ、サーバーを再起動します。アクティブなコピーが出力に表示されている場合は、手順 5 および 6 を再度実行します。

8.  サーバーが再起動したら、関連するプローブを再実行します (「問題の確認」セクションの手順 2c を参照)。

9.  プローブが成功した場合は、次のコマンドを実行して、データベースをフェールオーバーします。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. プローブがやはり失敗する場合は、さらなるサポートがこの問題の解決に必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## ActiveSyncCTPMonitor の回復操作

このモニター警告は、通常は CA サーバー (CAS) で発行されます。

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続します。**\[アプリケーション プール\]** をクリックし、**MSExchangeSyncAppPool** という名前の ActiveSync アプリケーション プールをリサイクルします。

2.  関連するプローブを再実行します (「問題の確認」セクションの手順 2c を参照)。

3.  問題がまだ存在している場合は、IISReset ユーティリティを使用して、IIS サービス全体をリサイクルします。

4.  関連するプローブを再実行します (「問題の確認」セクションの手順 2c を参照)。

5.  依然として問題が存在する場合は、該当するメールボックス サーバーの正常性状態を確認する必要があります。メールボックス サーバーの名前は、エラー メッセージに記述された `_Mbx:` 値です。
    
    1.  該当するメールボックス サーバーに対して次のコマンドを実行します。たとえば、mailbox1.contoso.com という名前のメールボックス サーバーに対して次のコマンドを実行します。
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  コマンド出力に一覧表示されたモニターの中に、正常でないと報告されたモニターがある場合は、まず、そのモニターを処置する必要があります。これを行うには、「ActiveSyncDeepTestMonitor と ActiveSyncSelfTestMonitor の回復操作」セクションに記載されているトラブルシューティング手順を実行してください。

6.  メールボックス サーバー上のすべてのモニターが正常な場合は、CAS を再起動します。

7.  サーバーが再起動したら、関連するプローブを再実行します (「問題の確認」セクションの手順 2c を参照)。

8.  プローブの失敗が続く場合、さらなるサポートがこの問題の解決に必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## RequestsQueuedGt500Monitor の回復操作

このモニター警告は、通常は CA サーバーで発行されます。

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続します。**\[アプリケーション プール\]** をクリックし、**MSExchangeSyncAppPool** という名前の ActiveSync アプリケーション プールをリサイクルします。

2.  モニターが正常状態に保たれるかどうかを確認するため、10 分間待ちます。10 分後に、該当するサーバーに対して、次のコマンドを実行します。たとえば、次のコマンドを server1.contoso.com に対して実行します。
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  問題がまだ存在している場合は、IISReset ユーティリティを使用して、IIS サービス全体をリサイクルします。

4.  10 分間待ってから、手順 2 に示すコマンドを再度実行し、モニターの状態が正常のままかどうかを確認します。

5.  依然として問題が存在する場合は、サーバーを再起動します。サーバーが CAS の場合は、サーバーを再起動するだけです。サーバーがメールボックス サーバーの場合は、次の操作を行います。
    
    1.  サーバー上でホストされているデータベースをフェールオーバーします。このためには、次のコマンドを実行します。
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **注**   これ以降のすべてのコード例では、*server1.contoso.com* を実際のサーバー名に置き換えてください。
    
    2.  すべてのデータベースが、問題を報告しているサーバーから移動されたことを確認します。このためには、次のコマンドを実行します。
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        コマンド出力を確認し、サーバー上にアクティブなコピーがなければ、サーバーを再起動します。

6.  サーバーが再起動したら、10 分間待ってから、手順 2 に示すコマンドを再度実行し、モニターの状態が正常なままかどうかを確認します。

7.  モニターが正常なままであり、かつサーバーがメールボックス サーバーの場合は、次のコマンドを実行して、データベースをフェールオーバーします。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  プローブの失敗が続く場合、さらなるサポートがこの問題の解決に必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange ActiveSync](https://technet.microsoft.com/ja-jp/library/aa998357\(v=exchg.150\))

[モバイル デバイス](https://technet.microsoft.com/ja-jp/library/bb232129\(v=exchg.150\))

[Exchange ActiveSync 仮想ディレクトリの管理タスク](https://technet.microsoft.com/ja-jp/library/bb125170\(v=exchg.150\))

