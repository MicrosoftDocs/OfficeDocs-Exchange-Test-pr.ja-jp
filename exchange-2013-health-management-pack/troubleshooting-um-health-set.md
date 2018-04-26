---
title: UM 正常性セットのトラブルシューティング
TOCTitle: UM 正常性セットのトラブルシューティング
ms:assetid: db947791-63ce-45dd-8634-1dfa5f55e2c2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.scom.um(v=EXCHG.150)
ms:contentKeyID: 53181843
ms.date: 01/28/2016
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 正常性セットのトラブルシューティング

 

_**適用先:**Exchange Server 2013, Project Server 2013_

_**トピックの最終更新日:**2015-03-09_

ユニファイド メッセージング (UM) 正常性セットは、組織内の UM サービスの全体的な状態を監視します。

UM が正常でないことを示す警告を受け取った場合、それが示すのは、ユーザーが組織内の UM サービスを使用できなくなる可能性がある問題です。UM 正常性セットは、次の正常性セットに密接に関連しています。

[UM.CallRouter 正常性セットのトラブルシューティング](troubleshooting-um-callrouter-health-set.md)

[UM.Protocol 正常性セットのトラブルシューティング](troubleshooting-um-protocol-health-set.md)

## 説明

UM サービスは、次のプローブとモニターを使用して監視されます。


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
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Active Directory ドメイン サービス (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Active Directory ドメイン サービス (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
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
        
        たとえば、server1.contoso.com に関する UM.Protocol 正常性セットの詳細を取得するには、次のコマンドを実行します。
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  コマンド出力を確認して、エラーを報告したモニターを特定します。警告を発行したモニターの **AlertValue** の値は `Unhealthy` になります。
    
    3.  正常状態にないモニターに関連するプローブを再実行します。関連するプローブについては、「説明」セクションの表を参照してください。このためには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        たとえば、失敗したモニターが **UMSelfTestMonitor** だとします。そのモニターに関連するプローブは **UMSelfTestProbe** です。そのプローブを server1.contoso.com で実行するには、次のコマンドを実行します。
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  コマンド出力で、プローブの **Result** の値を確認します。値が **Succeeded** であれば、この問題は一時的なエラーであり、もう存在しません。値がそれ以外の場合は、次のセクションで説明する回復手順を参照してください。

## トラブルシューティングの手順

正常性セットから警告を受け取ったときは、電子メール メッセージに次の情報が含まれています。

  - 警告を送信したサーバーの名前

  - 警告の発生日時

  - 使用された認証メカニズムと資格情報

  - 最後のエラーの完全な例外追跡 (診断データおよび特定の HTTP ヘッダー情報を含む)
    
    **注**  完全な例外追跡に記載された情報を使用して、問題をトラブルシューティングできます。プローブによって生成された例外には、プローブが失敗した理由を説明する「エラーの理由」が含まれています。

**UM サービスへの SIP オプションが失敗しました**

UM サービスが無効になっていないかどうかを確認します。UM サービスが開始されていない場合や無効になっている場合は、UM サービスを再起動します。

**過去 1 時間に UM サービスによって拒否された着信呼び出しは {0}% を超えています**

クライアント アクセス サーバー (CAS) 上のイベント ログを参照して、**umipgateway**、**umhuntgroup** などの UM オブジェクトが正しく構成されているかどうかを確認します。

イベント ログに含まれている情報が十分でないときは、UM イベント ログを Expert レベルで有効にしてから、UM 追跡ログ ファイルを確認することが必要な場合もあります。

**過去 1 時間に UM ワーカー プロセスによって拒否された着信呼び出しは {0}% を超えています**

CAS 上のイベント ログを参照して、**umipgateway**、**umhuntgroup** オブジェクトなどの UM オブジェクトが正しく構成されているかどうかを確認します。

イベント ログに含まれている情報が十分でないときは、UM イベント ログを Expert レベルで有効にしてから、UM 追跡ログ ファイルを確認することが必要な場合もあります。

**過去 1 時間に正常に処理されたメッセージは {0}% 未満です**

CAS 上のイベント ログを参照して、**umipgateway**、**umhuntgroup** オブジェクトなどの UM オブジェクトが正しく構成されているかどうかを確認します。

イベント ログに含まれている情報が十分でないときは、UM イベント ログを Expert レベルで有効にしてから、UM 追跡ログ ファイルを確認することが必要な場合もあります。

**Microsoft Exchange ユニファイド メッセージング サービスは、UM パイプラインに空き領域がないため、呼び出しを拒否しました**

CAS 上のイベント ログを参照して、**umipgateway**、**umhuntgroup** オブジェクトなどの UM オブジェクトが正しく構成されているかどうかを確認します。

イベント ログに含まれている情報が十分でないときは、UM イベント ログを Expert レベルで有効にしてから、UM 追跡ログ ファイルを確認することが必要な場合もあります。

**音声ビデオ エッジ サービスは、構成が正しくないか、実行されていません**

1.  メールボックス サーバー上のイベント ログを参照して、Lync サーバーからの呼び出しが失敗している理由を特定します。次に、以下の操作を実行します。
    
      - UM サービスによって選択された Lync プールが機能していることを確認します。
    
      - 特定の Lync サーバーを使用するには、次のコマンドを実行します。
        
            Set-UMServer ExchangeUMServer -SIPAccessService <ServerName>

**UM サーバーは、Communications Server の音声ビデオ エッジ サービスで資格情報を取得できませんでした**

イベント ログを参照して、どの Lync プールが選択されているかを調査し、選択された Lync プールが機能していることを確認します。

**セッションの確立中、Communications Server 音声ビデオ エッジはポートを開けないか、リソースを割り当てることができませんでした**

イベント ログを参照して、どの Lync プールが選択されているかを調査し、選択された Lync プールが機能していることを確認します。

**Microsoft Exchange ユニファイド メッセージング サービスの証明書の有効期限が近づいています**

メールボックス サーバー上の UM サービス証明書を更新します。

**他のトラブルシューティング手順:**

1.  IIS マネージャーを起動し、問題を報告しているサーバーに接続して、**MSExchangeServicesAppPool** アプリケーション プールが実行されているかどうかを確認します。

2.  IIS マネージャーで **\[アプリケーション プール\]** をクリックし、**MSExchangeServicesAppPool** アプリケーション プールをリサイクルします。このためには、Exchange 管理シェル から次のコマンドを実行します。
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

4.  問題がまだ存在している場合は、IISReset ユーティリティを使用するか、次のコマンドを実行して、IIS サービスをリサイクルします。
    
        Iisreset /noforce

5.  関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

6.  問題がまだ存在している場合は、サーバーを再起動します。

7.  サーバーが再起動したら、関連するプローブを再実行します (「問題がまだ存在していることを確認する」セクションの手順 2c を参照)。

8.  プローブがまだ失敗する場合、この問題の解決にサポートが必要なこともあります。この問題を解決するには、Microsoft のサポート担当者にお問い合わせください。Microsoft のサポート担当者に問い合わせるには、「[Exchange Server サポート ページ](http://go.microsoft.com/fwlink/p/?linkid=180809)」にアクセスしてください。ナビゲーション ウィンドウで、**\[サポート オプションとリソース\]** をクリックし、**\[テクニカル サポートを利用する\]** に表示されるいずれかのオプションを使用して、Microsoft のサポート担当者に問い合わせます。組織には Microsoft 製品サポート サービスに直接問い合わせるための特定の手順がある場合があるので、組織のガイドラインを最初に必ず確認してください。

## 詳細情報

[Exchange 2013 の新機能](https://technet.microsoft.com/ja-jp/library/jj150540\(v=exchg.150\))

[Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

