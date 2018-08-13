---
title: ECP 正常性セットのトラブルシューティング
TOCTitle: ECP 正常性セットのトラブルシューティング
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53181821
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ECP 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Exchange コントロール パネル (ECP) 正常性セットは、Exchange 管理センター (EAC) および Outlook Web App (OWA) ユーザー設定サービスの全体的な状態を監視します。ECP 正常性セットは、次の正常性セットに密接に関連しています。

[ECP.Proxy 正常性セットのトラブルシューティング](troubleshooting-ecp-proxy-health-set.md)

ECP 正常性セットが正常でないことを示す警告を受け取った場合、それが示すのは、ユーザーが EAC にアクセスできなくなる可能性がある問題です。

## 説明

EAC サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## ユーザー操作

正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。

  - 警告を送信したサーバーの名前

  - 警告の発生日時

  - 認証および資格情報

  - 最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)
    
    **注**   完全な例外の追跡に記載された情報を使用して、問題をトラブルシューティングできます。

サービスは、警告の発行後に回復することがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の手順を実行します。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        たとえば、server1.contoso.com に関する ECP 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        たとえば、失敗したモニターが **EacSelfTestMonitor** だとします。そのモニターに関連するプローブは **EacSelfTestProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値が Succeeded ではない場合は、次のセクションで説明する回復手順を参照してください。

## EacSelfTestMonitor と EacDeepTestMonitor の回復操作

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続します。**\[アプリケーション プール\]** をクリックし、**MSExchangeECPAppPool** という名前の ECP アプリケーション プールをリサイクルします。

2.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

3.  問題がまだ存在している場合は、IISReset ユーティリティを使用して、IIS サービス全体をリサイクルします。

4.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

5.  プローブが失敗した場合は、サーバーを再起動します。

6.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

7.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

[Exchange 2013 の Exchange 管理者センター](https://technet.microsoft.com/ja-jp/library/jj150562\(v=exchg.150\))

