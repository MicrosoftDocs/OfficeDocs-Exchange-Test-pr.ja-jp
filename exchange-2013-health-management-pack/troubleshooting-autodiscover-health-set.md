---
title: Autodiscover 正常性セットのトラブルシューティング
TOCTitle: Autodiscover 正常性セットのトラブルシューティング
ms:assetid: bc933621-df73-4d1d-bdef-825b98be8e09
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.autodiscover(v=EXCHG.150)
ms:contentKeyID: 53181837
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autodiscover 正常性セットのトラブルシューティング

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Autodiscover 正常性セットは、クライアントの自動検出サービスの全体的な状態を監視します。

Autodiscover が正常でないことを示す警告を受け取った場合、それが示すのは、ユーザーが自動検出プロセスを使用して自分のメールボックスにアクセスできなくなる可能性がある問題です。

## 説明

自動検出サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>AutodiscoverCtpProbe</p></td>
<td><p>自動検出</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverCtpMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## 一般的な問題

このプローブは、次のような一般的な理由で失敗することがあります。

  - 監視対象のクライアント アクセス サーバー (CAS) でホストされている自動検出アプリケーション プール (MSExchangeAutodiscoverAppPool) が応答していない。または、1 つまたは複数のメールボックス サーバー上でホストされている自動検出アプリケーション プールが応答していない。

  - CAS でネットワークの問題が発生しており、CAS をメールボックス サーバーやドメイン コントローラーに接続できない。

  - 監視アカウントの資格情報が正しくない。

  - ドメイン コントローラーが応答していない。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する Autodiscover 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` です。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **AutodiscoverCtpMonitor** だとします。そのモニターに関連するプローブは **AutodiscoverCtpProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe Autodiscover\AutodiscoverCtpProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値がそれ以外の場合は、次のセクションで説明する回復手順を参照してください。

## AutodiscoverCtpMonitor の回復操作

正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。

  - 警告を送信したサーバーの名前

  - プローブが監視していたメールボックス サーバーの名前

  - 警告の発生日時

  - 使用された認証メカニズムと資格情報

  - 最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)

完全な例外追跡に記載された情報を使用して、問題をトラブルシューティングできます。プローブによって生成された例外には、プローブが失敗した理由を説明する「エラーの理由」が含まれています。たとえば、「エラーの理由」は次のいずれかになることがあります。

  - **X-FEServer**   プローブが実行された CAS を示します

  - **X-CalculatedBETarget**   要求がルーティングされる先のメールボックス サーバーを示します

  - **X-DiagInfo**   要求を受信したメールボックス サーバーを示します

この問題をトラブルシューティングするには、次の手順に従います。

1.  CA サーバーおよびメールボックス サーバー上のプロトコル ログを確認します。CAS のプロトコル ログは、既定では ***\<Exchange サーバー インストール ディレクトリ\>*\\Logging\\HttpProxy\\Autodiscover** フォルダーにあります。メールボックス サーバーのプロトコル ログ ファイルは、既定では ***\<Exchange サーバー インストール ディレクトリ\>*\\Logging\\Autodiscover** フォルダーにあります。

2.  テスト ユーザー アカウントを作成し、そのテスト ユーザー アカウントを使って CAS にログオンします。たとえば、次を使用してログオンします。https://*\<サーバー名\>*/autodiscover/autodiscover.xml
    
    テスト ユーザー アカウント名がパスしたら、監視対象のメールボックスをホストしているメールボックス サーバーに問題が影響する可能性があります。
    
    メールボックス サーバーでテスト アカウントを使用して、上記手順を繰り返します。その試みが失敗する場合は、別の CAS に対してテストを実行し、メールボックス サーバーではなく特定の CAS で問題が発生していることを確認します。

3.  CA およびメールボックス サーバー間のネットワーク接続を確認します。ping.exe を使用して、各サーバーが応答していることを確認します。

4.  Autodiscover.Proxy 正常性セットの警告で、特定のメールボックス サーバーに影響する問題を示しているものがないかどうかを確認します。詳細については、「[Autodiscover.Proxy 正常性セットのトラブルシューティング](troubleshooting-autodiscover-proxy-health-set.md)」を参照してください。

5.  Autodiscover.Protocol 正常性セットの警告で、特定のメールボックス サーバーに影響する問題を示しているものがないかどうかを確認します。詳細については、「[Autodiscover.Protocol 正常性セットのトラブルシューティング](troubleshooting-autodiscover-protocol-health-set.md)」を参照してください。

6.  IIS マネージャーを起動し、問題を報告しているサーバーに接続します。**MSExchangeAutodiscoverAppPool** アプリケーション プールが CA サーバーおよびメールボックス サーバー上で実行されていることを確認します。

7.  IIS マネージャーで **\[アプリケーション プール\]** をクリックし、シェルから次のコマンドを実行して、**MSExchangeAutodiscoverAppPool** アプリケーション プールをリサイクルします。
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

9.  問題がまだ存在している場合は、IISReset ユーティリティを使用するか、次のコマンドを実行して、IIS サービスをリサイクルします。
    
        Iisreset /noforce

10. 関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

11. 問題がまだ存在している場合は、サーバーを再起動します。

12. サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

13. プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

