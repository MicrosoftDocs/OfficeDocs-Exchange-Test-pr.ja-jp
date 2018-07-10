---
title: DataProtection 正常性セットのトラブルシューティング
TOCTitle: DataProtection 正常性セットのトラブルシューティング
ms:assetid: cde3cc34-2076-4e30-8d3c-265b66d00ae8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.dataprotection(v=EXCHG.150)
ms:contentKeyID: 53181838
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DataProtection 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:** 2015-03-09_

DataProtection 正常性セットは、データベース可用性グループ (DAG) 内のデータベースの冗長性を監視します。

DataProtection が正常でないことを示す警告を受け取った場合、それが示すのは、レプリケーションまたはクラスター コンポーネントに影響し、Exchange データベースへのアクセスを妨げる可能性がある問題です。

## 説明

DataProtection 正常性サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>ClusterEndpointProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterEndpointMonitor</p></td>
</tr>
<tr class="even">
<td><p>ClusterGroupProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterGroupMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ClusterNetworkProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterNetworkMonitor</p></td>
</tr>
<tr class="even">
<td><p>ClusterServiceCrashProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterServiceCrashMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServerOneCopyProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServerOneCopyMonitor</p></td>
</tr>
<tr class="even">
<td><p>ServerOneCopyInternalMonitorProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServerOneCopyInternalMonitorMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServiceHealthMSExchangeReplEndpointProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServiceHealthMSExchangeReplEndpointMonitor</p></td>
</tr>
<tr class="even">
<td><p>ServiceHealthMSExchangeReplCrashProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServiceHealthMSExchangeReplCrashMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServerSiteFailureProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServerSiteFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>StorageApparentControllerIssuesProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>StorageApparentControllerIssuesMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseHealthTooManyMountedDatabaseProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>DatabaseHealthTooManyMountedDatabaseMonitor</p></td>
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
        
        たとえば、server1.contoso.com に関する Autodiscover.Protocol 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
        
        コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    2.  モニターの基になるプローブを識別します。ほとんどのプローブは、名前のプレフィックスが同じであることに注意してください。前の例を使用して、"**ClusterNetwork\***" を検索します。
        
            Get-MonitoringItemIdentity -Identity DataProtection -Server server1.contoso.com | ?{$_.Name -like "ClusterNet ItemType  
            work*"}
        
        返される結果は、次のようになります。
        
        
        <table>
        <colgroup>
        <col style="width: 25%" />
        <col style="width: 25%" />
        <col style="width: 25%" />
        <col style="width: 25%" />
        </colgroup>
        <tbody>
        <tr class="odd">
        <td><p><code>ItemType</code></p></td>
        <td><p><code>HealthSetName</code></p></td>
        <td><p><code>Name</code></p></td>
        <td><p><code>TargetResource</code></p></td>
        </tr>
        <tr class="even">
        <td><p><code>Probe</code></p></td>
        <td><p><code>DataProtection</code></p></td>
        <td><p><code>ClusterNetworkProbe</code></p></td>
        <td><p><code>MSExchangeRepl</code></p></td>
        </tr>
        </tbody>
        </table>
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **AutodiscoverSelfTestMonitor** だとします。そのモニターに関連するプローブは **AutodiscoverSelfTestProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値がそれ以外の場合は、次のセクションで説明する回復手順を参照してください。

## トラブルシューティングの手順

正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。

  - 警告を送信したサーバーの名前

  - 警告の発生日時

  - 使用された認証メカニズムと資格情報

  - 最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)
    
    完全な例外追跡に記載された情報を使用して、問題をトラブルシューティングできます。プローブによって生成された例外には、プローブが失敗した理由を説明する「エラーの理由」が含まれています。

高可用性環境で発生するほとんどの問題は、**Test-ReplicationHealth** コマンドレットを実行して、クラスター/ネットワーキング/ActiveManager/サービスのトラブルシューティングを実行できます。それ以外の正常性セット/コンポーネントについては、別の Test-\* コマンドレットがあります。

たとえば、

    Test-ReplicationHealth <ServerName>

返される結果は、次のようになります。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><code>Server</code></p></td>
<td><p><code>Check</code></p></td>
<td><p><code>Result</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>ClusterService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>ReplayService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>ActiveManager</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>TasksRpcListener</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>TcpListener</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>ServerLocatorService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DagMembersUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>ClusterNetwork</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>QuorumGroup</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>FileShareQuorum</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DatabaseRedundancyCheck</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DatabaseAvailabilityCheck</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DBCopySuspended</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DBCopyFailed</code></p></td>
<td><p>確認</p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DBInitializing</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DBDisconnected</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DBLogCopyKeepingUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;サーバー名&gt;</em></p></td>
<td><p><code>DBLogReplayKeepingUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
</tbody>
</table>


すべてのコンポーネントで **\[結果\]** 列に **\[確認\]** が表示されたら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

問題がまだ存在している場合は、サーバーを再起動します。サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

