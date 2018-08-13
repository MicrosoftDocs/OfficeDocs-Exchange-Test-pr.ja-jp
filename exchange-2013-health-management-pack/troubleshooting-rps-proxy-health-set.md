---
title: RPS.Proxy 正常性セットのトラブルシューティング
TOCTitle: RPS.Proxy 正常性セットのトラブルシューティング
ms:assetid: a5058323-5d86-438a-ad4a-fa4292310e98
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.rps.proxy(v=EXCHG.150)
ms:contentKeyID: 53181836
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# RPS.Proxy 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

RPS.Proxy 正常性セットは、リモート PowerShell サービスの全体的な状態を監視します。

RPS.Proxy が正常でないことを示す警告を受け取った場合、それが示すのは、リモート PowerShell を使用して Exchange にアクセスできなくなる可能性がある問題です。

## 説明

RPS サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>RPSProxyTestProbe</p></td>
<td><p>RPS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>RPSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## 一般的な問題

このプローブが失敗する場合、その問題には複数の理由が考えられます。より一般的な問題には、次のようなものがあります。

  - 監視対象の CAS サーバーでホストされているアプリケーション プールが適切に動作していない。

  - 監視アカウントの資格情報が正しくない。

  - ドメイン コントローラーが応答していない。

## ユーザー操作

サービスは、警告の発行後に回復できることがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときに最初に実行する必要があるのは、その問題がまだ存在しているかどうかを確認することです。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な発生原因が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェルを開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する RPS.Proxy 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "RPS.Proxy"}
    
    2.  コマンド出力を見て、エラーを報告したモニターを確認します。警告を発行したモニターの **AlertValue** は `Unhealthy` になっています。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。この処理には、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **RPSProxyTestMonitor** だとします。そのモニターに関連するプローブは **RPSProxyTestProbe** です。そのプローブをサーバー server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe RPS.Proxy\RPSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値が Succeeded ではない場合は、次のセクションで説明する回復手順を参照してください。

## RPSProxyTestMonitor の回復操作

正常性セットから警告を受け取ったときは、電子メールに次の情報が含まれています。

  - 警告を送信した CAS サーバーの名前。

  - 完全な例外追跡 (エラー メッセージ、診断データ、および特定の HTTP ヘッダー情報を含む)。完全な例外追跡に記載された情報を使用して、問題をトラブルシューティングできます。

  - 問題の発生日時。

この問題をトラブルシューティングするには、次の手順を実行します。

1.  CAS サーバー上のプロトコル ログを確認します。プロトコル ログは、CAS サーバーの *\<Exchange サーバー インストール ディレクトリ\>*\\Logging\\HttpProxy*\\\<プロトコル\>* フォルダーにあります。

2.  テスト ユーザー アカウントを作成し、そのテスト ユーザー アカウントを使って CAS サーバーにログオンします (例: https:// *\<サーバー名\>*/owa)。

3.  IIS マネージャーを起動し、問題を報告しているサーバーに接続して、MSExchangePowerShellFrontEndAppPool が CAS サーバー上で実行されていることを確認します。

4.  **\[アプリケーション プール\]** をクリックし、Exchange 管理シェルから次のコマンドを実行して、**MSExchangePowerShellFrontEndAppPool** アプリケーション プールをリサイクルします。
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangePowerShellFrontEndAppPool

5.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2.c. を参照)。

6.  問題がまだ存在している場合は、IISReset ユーティリティを使用して、IIS サービスをリサイクルします。

7.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2.c. を参照)。

8.  問題がまだ存在している場合は、サーバーを再起動します。

9.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2.c. を参照)。

10. プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

