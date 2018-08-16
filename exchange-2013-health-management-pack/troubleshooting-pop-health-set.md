---
title: POP 正常性セットのトラブルシューティング
TOCTitle: POP 正常性セットのトラブルシューティング
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53181833
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

POP 正常性セットは、Microsoft Exchange POP3 サービスおよび POP3 クライアント接続性の全体的な状態と可用性を監視します。POP 正常性セットは、次の正常性セットに密接に関連しています。

  - [POP.Protocol 正常性セットのトラブルシューティング](troubleshooting-pop-protocol-health-set.md)

  - [POP.Proxy 正常性セットのトラブルシューティング](troubleshooting-pop-proxy-health-set.md)

POP サービスが正常でないことを示す警告を受け取った場合、それが示すのは、ユーザーが Exchange 環境で POP3 を使用して、自分のメールボックスにアクセスできなくなる可能性がある問題です。

## 説明

POP サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>認証</p>
<p>メールボックス サーバーの認証</p>
<p>インフォメーション ストア</p>
<p>高可用性</p>
<p>ネットワーク</p></td>
<td><p>PopCTPMonitor (POP 正常性セット)</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>なし</p></td>
<td><p>PopProxyTestMonitor (POP.Proxy 正常性セット)</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>認証</p>
<p>インフォメーション ストア</p>
<p>高可用性</p></td>
<td><p>PopDeepTestMonitor (POP.Protocol 正常性セット)</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>なし</p></td>
<td><p>PopSelfTestMonitor (POP.Protocol 正常性セット)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (POP 正常性セット)</p></td>
</tr>
</tbody>
</table>


## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する POP 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **PopCTPMonitor** だとします。そのモニターに関連するプローブは **PopCTPProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値が Succeeded ではない場合は、次のセクションで説明する回復手順を参照してください。

## PopTestDeepMonitor と PopSelfTestMonitor の回復操作

このモニター警告は、通常はメールボックス サーバーで発行されます。

1.  POP3 バックエンド サービスを再起動します。詳細については、「[POP3 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/aa997475\(v=exchg.150\))」を参照してください。

2.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

3.  プローブがやはり失敗する場合は、次のコマンドを使用して、メールボックス サーバーでホストされているデータベースをフェールオーバーします。
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  メールボックス サーバーからすべてのデータベースを削除したら、データベースが正しく移動されたことを確認する必要があります。このためには、次のコマンドを実行します。
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  サーバーが、データベースのアクティブなコピーをホストしていないことを確認します。続いて、サーバーを再起動します。

6.  サーバーが正しく再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

7.  プローブが成功した場合は、次のコマンドを実行して、データベースをフェールオーバーします。
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、<strong>サポート オプションとリソース</strong> をクリックし、<strong>テクニカル サポートを利用する</strong> に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## POPCTPMonitor の回復操作

このモニター警告は、通常は CA サーバー (CAS) で発行されます。

1.  CAS ロールを実行しているサーバー上の POP3 サービスを再起動します。詳細については、「[POP3 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/aa997475\(v=exchg.150\))」を参照してください。

2.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

3.  問題がまだ存在している場合は、Windows PowerShell で次のコマンドを実行します。
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  CAS ロールを実行しているサーバー上の POP3 サービスを再起動します。
    
    3.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。
    
    4.  次のコマンドを実行して、ログ ファイルの場所を見つけます。
        
            Get-PopSettings -server <CAS server name>
    
    5.  次のコマンドを実行し、プローブでタイム スタンプを比較して、コマンドにサービスを提供しているメールボックスを確認します。
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  このいずれかのサーバーの状態が正常でないと報告された場合は、「PopTestDeepMonitor と PopSelfTestMonitor の回復操作」セクションの手順を実行します。

4.  メールボックス サーバーが正常であると報告された場合は、CAS を再起動します。

5.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

6.  次のコマンドを実行して、プロトコルのログをオフにします。
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  CAS ロールを実行しているサーバー上の POP3 サービスを再起動します。詳細については、「[POP3 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/aa997475\(v=exchg.150\))」を参照してください。

8.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、<strong>サポート オプションとリソース</strong> をクリックし、<strong>テクニカル サポートを利用する</strong> に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## PopProxyTestMonitor の回復操作

1.  CAS ロールを実行しているサーバー上の POP3 サービスを再起動します。詳細については、「[POP3 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/aa997475\(v=exchg.150\))」を参照してください。

2.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

3.  プローブが引き続き失敗する場合は、CAS を再起動します。

4.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

5.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、<strong>サポート オプションとリソース</strong> をクリックし、<strong>テクニカル サポートを利用する</strong> に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## AverageCommandProcessingTimeGt60sMonitor の回復操作

このモニター警告は、通常は CA サーバーまたはメールボックス サーバーで発行されます。

1.  CA サーバーまたはメールボックス サーバー上の POP3 サービスを再起動します。詳細については、「[POP3 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/aa997475\(v=exchg.150\))」を参照してください。

2.  モニターが正常状態に保たれるかどうかを確認するため、10 分間待ちます。10 分後に、次のコマンドを実行します (この例では、server1.contoso.com を使用しています)。
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  問題がまだ存在している場合は、サーバーを再起動する必要があります。サーバーが CAS の場合は、サーバーを再起動するだけです。サーバーがメールボックス サーバーの場合は、データベースをフェールオーバーし、結果を確認します。そのためには、以下の手順を実行します。
    
    1.  次のコマンドを使用して、サーバー上でホストされているデータベースをフェールオーバーします。
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **注**   これ以降のすべてのコード例では、*server1.contoso.com* を実際のサーバー名に置き換えてください。
    
    2.  すべてのデータベースが、問題を報告しているサーバーから移動されたことを確認します。このためには、次のコマンドを実行します。
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        コマンド出力を確認し、サーバー上にアクティブなコピーがなければ、サーバーを再起動します。

4.  サーバーが再起動したら、10 分間待ってから、手順 2 に示すコマンドを再度実行し、モニターの状態が正常なままかどうかを確認します。

5.  モニターが正常であり、かつこのサーバーがメールボックス サーバーの場合は、次のコマンドを実行して、データベースをメールボックス サーバーにフェールオーバーして戻します。
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、<strong>サポート オプションとリソース</strong> をクリックし、<strong>テクニカル サポートを利用する</strong> に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[POP3 サービスの開始および停止](https://technet.microsoft.com/ja-jp/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/ja-jp/library/bb738143\(v=exchg.150\))

