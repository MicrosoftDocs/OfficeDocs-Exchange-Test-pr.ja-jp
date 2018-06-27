---
title: 'Exchange サーバー上のオペレーティング システムのウイルス対策ソフトウェア: Exchange 2013 Help'
TOCTitle: Exchange サーバー上のオペレーティング システムのウイルス対策ソフトウェア
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 48269697
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange サーバー上のオペレーティング システムのウイルス対策ソフトウェア

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-07-22_

ここでは、Microsoft Exchange Server 2013 を実行しているコンピューターに対するファイル レベルのウイルス対策プログラムの影響について説明します。このトピックで説明されている推奨事項を実行すると、Exchange 組織のセキュリティと状態の強化に役立てることができます。

ファイル レベルのスキャン プログラムはよく使用されます。ただし、正しく構成されていないと、これらのプログラムは Exchange 2013 で問題を起こすことがあります。ファイル レベルのスキャン プログラムには 2 種類あります。

  - *メモリ常駐型のファイル レベル スキャン*とは、メモリに常に読み込まれている、ファイル レベルのウイルス対策ソフトウェアの一部を表します。ハード ディスクとコンピューターのメモリで使用されるすべてのファイルをチェックします。

  - *オンデマンドのファイル レベル スキャン*とは、手動で、またはスケジュールに従って、ハード ディスクのファイルをスキャンするように構成できる、ファイル レベルのウイルス対策ソフトウェアの一部を表します。一部のバージョンのウイルス対策ソフトウェアは、すべてのファイルが最新のシグネチャでスキャンされていることを保証するために、ウイルス シグネチャが更新された後で自動的にオンデマンドのスキャンを開始します。

Exchange 2013 でファイル レベルのスキャン プログラムを使用するとき、次のような問題が発生することがあります。

  - ファイル レベルのスキャン プログラムは、ファイルの使用中に、またはスケジュールされた間隔でファイルをスキャンできます。これにより、Exchange 2013 が Exchange ログやデータベース ファイルの使用を試みているときに、スキャン プログラムがそのファイルをロックまたは検疫する可能性があります。この動作は、Exchange 2013 に深刻な障害を引き起こす場合があり、-1018 イベント ログ エラーが発生することもあります。

  - ファイル レベルのスキャン プログラムは、ストーム ワームなどの電子メール ウイルスに対する保護は提供しません。ストーム ワームは、バックドア トロイの木馬プログラムで、電子メール メッセージを介して自身を伝播します。このワームは、感染したコンピューターをボットネットに参加させます。このボットネットでは、感染したコンピューターを使用して、スパムを定期的爆発的に送信します。

## Exchange 2013 でファイル レベルのスキャンを使用する場合の推奨事項

Exchange 2013 サーバーにファイル レベルのスキャン プログラムを展開している場合は、メモリ常駐型とファイル レベルの両方のスキャンに対して、ディレクトリの除外、プロセスの除外、ファイル名拡張子の除外など、適切な除外が設定されていることを確認してください。ここでは、推奨されるディレクトリの除外、プロセスの除外、およびファイル名拡張子の除外について説明します。

**目次**

ディレクトリの除外

プロセスの除外

ファイル名拡張子の除外

## ディレクトリの除外

ファイル レベルのウイルス対策スキャン プログラムを実行する Exchange サーバーごとに、特定のディレクトリを除外する必要があります。ここでは、ファイル レベルのスキャンから除外する必要があるディレクトリについて説明します。

  - **メールボックス サーバー**
    
      - **メールボックス データベース**
        
          - Exchange データベース、チェックポイント ファイル、およびログ ファイル。既定では、これらは %ExchangeInstallPath%Mailbox フォルダーの下のサブフォルダーにあります。メールボックス データベース、トランザクション ログ、およびチェックポイント ファイルの場所を特定するには、次のコマンドを実行します。`Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - データベース コンテンツ インデックス。既定では、これらはデータベース ファイルと同じフォルダーにあります。
        
          - グループ メトリック ファイル。既定では、これらのファイルは %ExchangeInstallPath%GroupMetrics フォルダーにあります。
        
          - メッセージ追跡ログ ファイルや予定表修復ログ ファイルなどの一般的なログ ファイル。既定では、これらのファイルは %ExchangeInstallPath%TransportRoles\\Logs フォルダーと %ExchangeInstallPath%Logging フォルダーの下のサブフォルダーにあります。使用されているログのパスを特定するには、Exchange 管理シェルで次のコマンドを実行します。`Get-MailboxServer <servername> | Format-List *path*`
        
          - オフライン アドレス帳ファイル。既定では、これらは %ExchangeInstallPath%ClientAccess\\OAB フォルダーの下のサブフォルダーにあります。
        
          - %SystemRoot%\\System32\\Inetsrv フォルダーの IIS システム ファイル。
        
          - メールボックス データベースの一時フォルダー: %ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **データベース可用性グループのメンバー**
        
          - **メールボックス データベース**一覧にリストされているすべてのアイテム、および %Windir%\\Cluster に存在しているクラスター クォーラム データベース。
        
          - 監視ディレクトリ ファイル。これらのファイルは、環境内の別のサーバー、通常はメールボックス サーバーと同じコンピューター上にインストールされていないクライアント アクセス サーバーにあります。既定では、監視ディレクトリ ファイルは、%SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\> にあります。
    
      - **Transport サービス**
        
          - メッセージ追跡ログや接続ログなどのログ ファイル。既定では、これらのファイルは %ExchangeInstallPath%TransportRoles\\Logs フォルダーの下のサブフォルダーにあります。使用されているログのパスを特定するには、Exchange 管理シェルで次のコマンドを実行します。`Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - メッセージのピックアップ ディレクトリ フォルダーと再生ディレクトリ フォルダー既定では、これらのフォルダーは %ExchangeInstallPath%TransportRoles フォルダーの下にあります。使用されているパスを特定するには、Exchange 管理シェルで次のコマンドを実行します。`Get-TransportService <servername>| Format-List *dir*path*`
        
          - キュー データベース、チェックポイント、およびログ ファイル。既定では、これらは %ExchangeInstallPath%TransportRoles\\Data\\Queue フォルダーにあります。
        
          - 送信者評価データベース、チェックポイント、およびログ ファイル。既定では、これらは %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation フォルダーにあります。
        
          - 次の変換を実行するために使用される一時フォルダー。
            
              - 既定では、コンテンツ変換は、Exchange サーバーの %TMP% フォルダーで実行されます。
            
              - 既定では、リッチ テキスト形式 (RTF) から MIME/HTML への変換は、%ExchangeInstallPath%\\Working\\OleConverter フォルダーで実行されます。
        
          - コンテンツ スキャン コンポーネントは、マルウェア エージェントとデータ損失防止 (DLP) で使用されます。既定では、これらのファイルは %ExchangeInstallPath%FIP-FS フォルダーにあります。
    
      - **メールボックス トランスポート サービス**
        
          - 接続ログなどのログ ファイル。既定では、これらのファイルは %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox フォルダーの下のサブフォルダーにあります。使用されているログのパスを特定するには、Exchange 管理シェルで次のコマンドを実行します。`Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **ユニファイド メッセージング**
        
          - 異なるロケール (en-EN や es-ES など) の文章校正ファイル。既定では、これらは %ExchangeInstallPath%UnifiedMessaging\\grammars フォルダーの下のサブフォルダーに格納されます。
        
          - 音声プロンプト、案内応答、および情報メッセージ ファイル。既定では、これらは %ExchangeInstallPath%UnifiedMessaging\\Prompts フォルダーの下のサブフォルダーに格納されます。
        
          - %ExchangeInstallPath%UnifiedMessaging\\voicemail フォルダーに一時的に格納されているボイスメール ファイル。
        
          - ユニファイド メッセージングによって生成された一時ファイル。既定では、これらは %ExchangeInstallPath%UnifiedMessaging\\temp フォルダーに格納されます。
    
      - **セットアップ**
        
          - Exchange Server のセットアップ一時ファイル。これらのファイルは、通常、%SystemRoot%\\Temp\\ExchangeSetup に配置されます。
    
      - **Exchange Search サービス**
        
          - セキュリティで保護された環境でファイルの変換を実行するために、Exchange Search サービスと Microsoft Filter Pack によって使用される一時ファイル。これらのファイルは %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\ にあります。

<!-- end list -->

  - **クライアント アクセス サーバー**
    
      - **Web コンポーネント**
        
          - インターネット インフォメーション サービス (IIS) 7.0 を使用しているサーバーの場合、Microsoft Outlook Web App で使用される圧縮フォルダー。既定では、IIS 7.0 の圧縮フォルダーは %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files にあります。
        
          - %SystemRoot%\\System32\\Inetsrv フォルダーの IIS システム ファイル。
        
          - Inetpub\\logs\\logfiles\\w3svc。
        
          - %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET Files 内のサブフォルダー
    
      - **POP3 プロトコルと IMAP4 プロトコルのログ**
        
          - POP3 のフォルダー:%ExchangeInstallPath%Logging\\POP3
        
          - IMAP4 のフォルダー:%ExchangeInstallPath%Logging\\IMAP4
    
      - **フロント エンド トランスポート サービス**
        
          - 接続ログやプロトコル ログなどのログ ファイル。既定では、これらのファイルは %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd フォルダーの下のサブフォルダーにあります。使用されているログのパスを特定するには、Exchange 管理シェルで次のコマンドを実行します。`Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **セットアップ**
        
          - Exchange Server セットアップの一時ファイル。これらのファイルは、通常 %SystemRoot%\\Temp\\ExchangeSetup にあります。

Exchange 2013 でファイル レベルのスキャンを使用する場合の推奨事項

## プロセスの除外

多くのファイル レベルのスキャン プログラムは、現在ではプロセスのスキャンをサポートしています。この機能は、適切でないプロセスがスキャンされた場合に、Microsoft Exchange に悪影響を与えることがあります。このため、以下のプロセスをファイル レベルのスキャン プログラムから除外する必要があります。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロセス</th>
<th>Path</th>
<th>コメント</th>
<th>サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>サブスクライブしたエッジ トランスポート サーバーの Active Directory Lightweight Directory Services (AD LDS)。</p></td>
<td><p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport サービス ワーカー プロセス</p></td>
<td><p>メールボックス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>マルウェア エージェントおよび DLP によって使用されるコンテンツ スキャン コンポーネント。</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Microsoft Exchange Search Host Controller サービス (HostControllerService)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>インターネット インフォメーション サービス (IIS)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Anti-spam Update サービス (MSExchangeAntispamUpdate)</p></td>
<td><p>メールボックス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>コンテンツ フィルター エージェント</p></td>
<td><p>メールボックス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Diagnostics サービス (MSExchangeDiagnostics)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Active Directory トポロジ サービス (MSExchangeADTopology)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Credential サービス (MSExchangeEdgeCredential)</p></td>
<td><p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange EdgeSync サービス (MSExchangeEdgeSync)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 サービス (MSExchangeImap4)</p></td>
<td><p>クライアント アクセス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 バックエンド サービス (MSExchangeIMAP4BE)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange POP3 サービス (MSExchangePop3)</p></td>
<td><p>クライアント アクセス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange POP3 バックエンド サービス (MSExchangePOP3BE)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Service Host サービス (MSExchangeServiceHost)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange RPC クライアント アクセス サービス (MSExchangeRPC)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Search サービス (MSExchangeFastSearch)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Service Host サービス (MSExchangeServiceHost)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Information Store サービス (MSExchangeIS)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Information Store サービス ワーカー プロセス</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービス (MSExchangeUMCR)</p></td>
<td><p>クライアント アクセス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange DAG 管理サービス (MSExchangeDagMgmt)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Mailbox Transport Delivery サービス (MSExchangeDelivery)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Frontend Transport サービス (MSExchangeFrontEndTransport)</p></td>
<td><p>クライアント アクセス サーバー</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Health Manager サービス (MSExchangeHM)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Health Manager サービス ワーカー プロセス</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange メールボックス アシスタント サービス (MSExchangeMailboxAssistants)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange メールボックス レプリケーション サービス (MSExchangeMailboxReplication)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Migration Workflow サービス (MSExchangeMigrationWorkflow)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange レプリケーション サービス (MSExchangeRepl)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Mailbox Transport Submission サービス (MSExchangeSubmission)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport サービス (MSExchangeTransport)</p></td>
<td><p>メールボックス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport Log Search サービス (MSExchangeTransportLogSearch)</p></td>
<td><p>メールボックス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 調整サービス (MSExchangeThrottling)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Microsoft Exchange Search サービス (MSExchangeFastSearch)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>外部受信者用にリッチ テキスト形式 (RTF) のメッセージを MIME/HTML に変換します。</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Microsoft Exchange Search サービス (MSExchangeFastSearch)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Exchange 管理シェル</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p>
<p>エッジ トランスポート サーバー</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>マルウェア エージェントおよび DLP によって使用されるコンテンツ スキャン コンポーネント。</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>マルウェア エージェントおよび DLP によって使用されるコンテンツ スキャン コンポーネント。</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>Outlook Web App での WebReady ドキュメント表示。</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange ユニファイド メッセージング サービス (MSExchangeUM)</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange ユニファイド メッセージング サービス ワーカー プロセス</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>マルウェア エージェントおよび DLP によって使用されるコンテンツ スキャン コンポーネント。</p></td>
<td><p>メールボックス サーバー</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>インターネット インフォメーション サービス (IIS)</p></td>
<td><p>メールボックス サーバー</p>
<p>クライアント アクセス サーバー</p></td>
</tr>
</tbody>
</table>


Exchange 2013 でファイル レベルのスキャンを使用する場合の推奨事項

## ファイル名拡張子の除外

特定のディレクトリとプロセスの除外に加えて、ディレクトリの除外が失敗する、またはファイルが既定の場所から移動される場合、次に示すような Exchange 固有のファイル名拡張子を除外する必要があります。

  - アプリケーション関連の拡張子:
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - データベース関連の拡張子:
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - オフライン アドレス帳関連の拡張子
    
      - .lzx

<!-- end list -->

  - コンテンツ インデックス関連の拡張子:
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - ユニファイド メッセージング関連の拡張子:
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - グループ メトリック関連の拡張子:
    
      - .dsc
    
      - .txt

Exchange 2013 でファイル レベルのスキャンを使用する場合の推奨事項

