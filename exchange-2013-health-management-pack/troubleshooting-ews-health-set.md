---
title: EWS 正常性セットのトラブルシューティング
TOCTitle: EWS 正常性セットのトラブルシューティング
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53181848
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# EWS 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Exchange Web サービス (EWS) 正常性セットは、EWS サービスの全体的な状態を監視します。EWS 正常性セットは、次の正常性セットに密接に関連しています。

[EWS.Protocol 正常性セットのトラブルシューティング](troubleshooting-ews-protocol-health-set.md)

[EWS.Proxy 正常性セットのトラブルシューティング](troubleshooting-ews-proxy-health-set.md)

EWS が正常でないことを示す警告を受け取った場合、ユーザーが Exchange サーバーと通信できなくなる可能性がある問題を示しています。

## 説明

EWS は、次のプローブとモニターを使用して監視されます。


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>インフォメーション ストア</p>
<p>Active Directory ドメイン サービス (AD DS)</p></td>
<td><p>EwsCtpMonitor (EWS 正常性セット)</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory ドメイン サービス (AD DS)</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>インフォメーション ストア</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


このプローブは、監視アカウントを使用して、クライアント アクセス サーバー (CAS) からメールボックス サーバーへの完全な EWS ログオンを実行します。このプローブは、EWS の **GetFolder** メソッドを呼び出します。プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

## 一般的な問題

このプローブは、次のような一般的な理由で失敗することがあります。

  - プローブで使用される認証メカニズムと CAS 仮想ディレクトリで使用される認証メカニズムが一致しない。

  - 監視中の CAS の EWS アプリケーション プールが応答していない。

  - CAS がメールボックス サーバーに接続するときに、ネットワークの問題が発生している。

  - CAS がドメイン コントローラーに接続するときに、通信の問題が発生している。

  - ドメイン コントローラーが応答していない。

  - 1 つまたは複数のメールボックス サーバーにある EWS アプリケーション プールが応答していない。

  - ユーザーのデータベースがマウントされていないか、特定のメールボックスでインフォメーション ストアが使用できない。

  - 1 つまたは複数のメールボックス サーバー上のインフォメーション ストア サービスで問題が発生している。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。
    
    この正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。
    
    1.  警告が作成された CAS の名前
    
    2.  ターゲット リソースとしてプローブが監視していたメールボックス サーバーの名前
    
    3.  最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)
    
    4.  インシデントが発生した時間
    
    5.  使用された認証メカニズムと資格情報
    
    例外の追跡情報には、プローブが失敗している原因について最も重要な情報が記載されています。エスカレーション メッセージには、次の HTTP ヘッダーも含まれます。
    
    1.  **X-FEServer**   プローブが実行された CAS を示します
    
    2.  **X-TargetBEServer**   要求のルーティング先である MBX サーバーを示します
    
    3.  **X-DiagInfo**   要求を受信した MBX サーバーを示します

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する EWS 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、EWS 正常性セットで、失敗したモニターが **EWSCtpMonitor** だとします。そのモニターに関連するプローブは **EWSCtpProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値がそれ以外の場合は、次のセクションで説明する回復手順を参照してください。

## EwsCtpMonitor の回復操作

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続して、CA サーバーとメールボックス サーバーの両方で **MSExchangeServicesAppPool** アプリケーション プールが実行されているかどうかを確認します。

2.  失敗したプローブのメールボックス データベースを特定します。そのメールボックス データベースがメールボックス サーバーに対してアクティブであることと、インフォメーション ストアが正常であることを確認します。

3.  <strong>アプリケーション プール</strong> をクリックし、シェルから次のコマンドを実行して、**MSExchangeServicesAppPool** アプリケーション プールをリサイクルします。
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

5.  問題がまだ存在している場合は、IISReset ユーティリティを使用して、IIS サービス全体をリサイクルします。

6.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

7.  問題がまだ存在する場合は、CA サーバーとメールボックス サーバー上のプロトコル ログ ファイルを確認します。CAS のプロトコル ログは、*\<Exchange サーバー インストール ディレクトリ\>\\Logging\\HttpProxy\\Ews* フォルダーにあります。メールボックス サーバーでは、ログは *\<Exchange サーバー インストール ディレクトリ\>\\Logging\\Ews* フォルダーにあります。

8.  テスト ユーザー アカウントを作成し、そのテスト ユーザー アカウントを特定の CAS に対して実行して、ログオンします。たとえば、https:// \<サーバー名\>/ews/exchange.asmx を使用してログオンします。それでも問題が解決しない場合は、別の CAS を試して、問題が関連しているのがその CAS であり、メールボックス サーバーではないかどうかを確認します。テスト ユーザー名がパスしたら、特定のメールボックス データベースまたは監視するメールボックスがあるメールボックス サーバーに、問題が影響する可能性があります。メールボックス データベース内に存在するテスト アカウントを使用して、この手順を繰り返します。

9.  CA サーバーとメールボックス サーバー間のネットワーク接続を確認します。

10. EWS.Proxy 正常性セットの警告で、特定の CAS に影響する問題を示しているものがないかどうかを確認します。

11. EWS.Protocol 正常性セットの警告で、特定のメールボックス サーバーに影響する問題を示しているものがないかどうかを確認します。

12. 問題がまだ存在している場合は、サーバーを再起動します。サーバーを再起動するには、まず、サーバー上でホストされているデータベースをフェールオーバーします。このためには、次のコマンドを実行します。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **注**   これ以降のすべてのコード例では、*server1.contoso.com* を実際のサーバー名に置き換えてください。

13. すべてのデータベースが、問題を報告しているサーバーから移動されたことを確認します。このためには、次のコマンドを実行します。
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    コマンド出力を確認し、サーバー上にアクティブなコピーがなければ、サーバーを再起動します。

14. サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

15. プローブが成功した場合は、次のコマンドを実行して、データベースをフェールオーバーしてメールボックス サーバーに戻します。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. プローブがまだ失敗する場合は、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、<strong>サポート オプションとリソース</strong> をクリックし、<strong>テクニカル サポートを利用する</strong> に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

