---
title: EWS.Protocol 正常性セットのトラブルシューティング
TOCTitle: EWS.Protocol 正常性セットのトラブルシューティング
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53181842
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# EWS.Protocol 正常性セットのトラブルシューティング

 

_**適用先:** Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:** 2015-03-09_

EWS.Protocol 正常性セットは、メールボックス サーバー上の Exchange Web サービス (EWS) 通信プロトコルを監視します。EWS.Protocol 正常性セットは、次の正常性セットに密接に関連しています。

[EWS 正常性セットのトラブルシューティング](troubleshooting-ews-health-set.md)

[EWS.Proxy 正常性セットのトラブルシューティング](troubleshooting-ews-proxy-health-set.md)

EWS.Protocol が正常でないことを示す警告を受け取った場合、ユーザーが Exchange にアクセスできなくなる可能性がある問題を意味しています。

## 説明

EWS.Protocol 正常性セットは、次のプローブで構成されます。

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

EwsSelfTestProbe は、インフォメーション ストアに依存しません。ただし、EwsDeepTestProbe プローブはインフォメーション ストアに依存します。これらのプローブは、両方ともメールボックス サーバーで EWS 操作を実行し、使用する認証方法はクライアント アクセス サーバー (CAS) と同じです。EwsSeftTestProbe は **ConvertId** メソッドを呼び出し、EwsDeepTestProbe は **GetFolder** メソッドを呼び出します。


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
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>インフォメーション ストア</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


プローブとモニターの詳細については、「[サーバーの状態とパフォーマンス](https://technet.microsoft.com/ja-jp/library/jj150551\(v=exchg.150\))」を参照してください。

この正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。

1.  警告が発信されたメールボックス サーバーの名前

2.  最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)

3.  インシデントが発生した時間

## 一般的な問題

このプローブは、次のような一般的な理由で失敗することがあります。

  - 監視対象のメールボックス サーバー上の EWS アプリケーション プールが正しく機能していない。

  - ドメイン コントローラーが応答していないか、ドメイン コントローラーとメールボックス サーバーが通信できない。

  - ユーザーのデータベースがマウントされていないか、特定のメールボックスでインフォメーション ストアが使用できない。

## ユーザー操作

サービスは、警告の発行後に回復することがあります。そのため、正常性セットが異常であることを示す警告を受け取ったときは、まず、その問題がまだ存在しているかどうかを確認します。問題が存在する場合は、次のセクションで説明する適切な回復操作を実行します。

## 問題がまだ存在していることを確認する

1.  警告に記載された正常性セット名とサーバー名を確認します。

2.  メッセージの詳細には、警告の正確な原因に関する情報が示されています。ほとんどの場合、根本原因を特定するためのトラブルシューティング情報としては、メッセージの詳細だけで十分です。メッセージの詳細が不明確な場合は、次の操作を行います。
    
    1.  Exchange 管理シェル を開き、次のコマンドを実行して、警告を発行した正常性セットの詳細を取得します。
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        たとえば、server1.contoso.com に関する EWS.Protocol 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **EWSSelfTestMonitor** だとします。そのモニターに関連するプローブは **EWSSelfTestProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値が Succeeded ではない場合は、次のセクションで説明する回復手順を参照してください。

## EWSSelfTestMonitor と EWSDeepTestMonitor の回復操作

このモニター警告は、通常はメールボックス サーバーに対して発行されます。

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続して、CA サーバーとメールボックス サーバーの両方で MSExchangeServicesAppPool が実行されているかどうかを確認します。

2.  失敗したプローブのメールボックス データベースを探して、そのメールボックス データベースがメールボックス サーバーに対してアクティブであることと、インフォメーション ストアが正常であることを確認します。

3.  <strong>アプリケーション プール</strong> をクリックし、シェルから次のコマンドを実行して、**MSExchangeServicesAppPool** アプリケーション プールをリサイクルします。
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

5.  問題がまだ存在している場合は、IISReset ユーティリティを使用して、IIS サービスを再起動します。

6.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

7.  問題がまだ存在する場合は、メールボックス サーバー上のプロトコル ログ ファイルを確認します。ログは、メールボックス サーバーの *\<Exchange サーバー インストール ディレクトリ\>*\\Logging\\Ews フォルダーにあります。

8.  テスト ユーザー アカウントを作成し、そのテスト ユーザー アカウントを所定のメールボックス サーバーに対してポート 444 で使用してログオンします (https://*\<サーバー名\>*:444/ews/exchange.asmx)。テストが成功した場合は、特定のメールボックス データベースまたは監視メールボックスがあるメールボックス サーバーに問題が影響する可能性があります。そのデータベースでテスト アカウントを使用して、この手順を繰り返します。

9.  EWS.Protocol 正常性セットの警告で、特定のメールボックス サーバーに影響する問題を示しているものがないかどうかを確認します。

10. 問題がまだ存在している場合は、サーバーを再起動します。これを行うには、まず次のコマンドを使用して、サーバー上でホストされているデータベースをフェールオーバーします。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    これ以降のすべてのコード例では、*server1.contoso.com* を実際のサーバー名に置き換えてください。

11. すべてのデータベースが、問題を報告しているサーバーから移動されたことを確認します。このためには、次のコマンドを実行します。
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    コマンド出力を確認し、サーバー上にアクティブなコピーがなければ、サーバーを再起動します。サーバーを再起動します。

12. サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

13. プローブが成功した場合は、次のコマンドを実行して、データベースをフェールオーバーします。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. プローブがまだ失敗する場合は、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、<strong>サポート オプションとリソース</strong> をクリックし、<strong>テクニカル サポートを利用する</strong> に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

