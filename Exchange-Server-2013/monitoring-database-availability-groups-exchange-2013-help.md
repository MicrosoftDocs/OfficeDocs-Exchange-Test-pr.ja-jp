---
title: 'データベース可用性グループの監視: Exchange 2013 Help'
TOCTitle: データベース可用性グループの監視
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 48270263
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データベース可用性グループの監視

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

データベース可用性グループ (DAG) のメールボックス データベース コピーの稼働状態を監視する方法、診断情報を収集する方法、およびディスク領域の低下を監視するしきい値の構成を行う方法については、このトピックで詳細を参照してください。

## Get-MailboxDatabaseCopyStatus コマンドレット

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ja-jp/library/dd298044\(v=exchg.150\)) コマンドレットを使用すると、メールボックス データベース コピーに関する状態の情報を表示できます。このコマンドレットにより、特定のデータベースのすべてのコピーに関する情報、特定のサーバー上のデータベースの特定のコピーに関する情報、またはサーバー上のすべてのデータベース コピーに関する情報を表示することができます。次の表では、メールボックス データベース コピーのコピーの状態で使用可能な値について説明します。

### データベース コピーの状態

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>データベース コピーの状態</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failed</p></td>
<td><p>メールボックス データベース コピーは、中断されていないのでエラー状態にあり、ログ ファイルをコピーまたは再生することができません。データベース コピーが失敗状態で、中断されていない間、システムはコピーの状態にエラーを引き起こした問題が解決されたかどうかを定期的にチェックします。問題が解決したことがシステムによって検出され、他に問題がなければ、コピーの状態は自動的に Healthy に変更されます。</p></td>
</tr>
<tr class="even">
<td><p>Seeding</p></td>
<td><p>メールボックス データベース コピーがシード処理されているか、メールボックス データベース コピーのコンテンツ インデックスがシード処理されています。あるいは、両方がシード処理されています。シード処理が完了すると、コピーの状態は初期化中に変更されます。</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>メールボックス データベースのコピーは、データベース コピーのシード処理のソースとして使用されています。</p></td>
</tr>
<tr class="even">
<td><p>Suspended</p></td>
<td><p>管理者が <strong>Suspend-MailboxDatabaseCopy</strong> コマンドレットを実行して、データベース コピーを手動で中断した結果、メールボックス データベース コピーが中断状態になっています。</p></td>
</tr>
<tr class="odd">
<td><p>Healthy</p></td>
<td><p>メールボックス データベース コピーはログ ファイルを正常にコピーおよび再生しているか、使用可能なすべてのログ ファイルを正常にコピーおよび再生しました。</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>Microsoft Exchange Replication サービスを利用できないか、またはメールボックス データベース コピーをホストするサーバーでサービスが実行されています。</p></td>
</tr>
<tr class="odd">
<td><p>Initializing</p></td>
<td><p>データベース コピーが作成されたとき、Microsoft Exchange Replication サービスの開始中または開始直後、および Suspended、ServiceDown、Failed、Seeding、または SinglePageRestore から別の状態に変移する間は、メールボックス データベース コピーは初期化状態になります。この状態にあるとき、データベースとログ ストリームが一貫した状態にあるかどうかをシステムが確認しています。ほとんどの場合、コピーの状態は約 15 秒間、初期化状態になりますが、いずれにしても、通常はこの状態が 30 秒以上続くことはありません。</p></td>
</tr>
<tr class="even">
<td><p>Resynchronizing</p></td>
<td><p>メールボックス データベース コピーとそのログ ファイルが、データベースのアクティブ コピーと比較され、2 つのコピー間に相違がないかチェックされます。相違が検出され、解決されるまで、コピーの状態はこの状態のままになります。</p></td>
</tr>
<tr class="odd">
<td><p>Mounted</p></td>
<td><p>アクティブ コピーはオンラインで、クライアント接続を受け付けています。メールボックス データベース コピーのアクティブ コピーのみが、Mounted のコピーの状態になることができます。</p></td>
</tr>
<tr class="even">
<td><p>Dismounted</p></td>
<td><p>アクティブ コピーはオフラインで、クライアント接続を受け付けていません。メールボックス データベース コピーのアクティブ コピーのみが、Dismounted のコピーの状態になることができます。</p></td>
</tr>
<tr class="odd">
<td><p>Mounting</p></td>
<td><p>アクティブ コピーがオンラインになりつつありますが、まだクライアント接続を受け付けていません。メールボックス データベース コピーのアクティブ コピーのみが、Mounting のコピーの状態になることができます。</p></td>
</tr>
<tr class="even">
<td><p>Dismounting</p></td>
<td><p>アクティブ コピーはオフラインになりつつあり、クライアント接続を終了しています。メールボックス データベース コピーのアクティブ コピーのみが、Dismounting のコピーの状態になることができます。</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>メールボックス データベース コピーはアクティブ データベース コピーから切断され、切断時には Healthy 状態にありました。この状態は、データベース コピーのソース データベース コピーへの接続状態を表します。ソース コピーとターゲット データベース コピーとの間の DAG ネットワークに障害が発生したときに、この状態が報告されることがあります。</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>メールボックス データベース コピーはアクティブ データベース コピーから切断され、切断時には、再同期中の状態にありました。この状態は、データベース コピーのソース データベース コピーへの接続状態を表します。ソース コピーとターゲット データベース コピーとの間の DAG ネットワークに障害が発生したときに、この状態が報告されることがあります。</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>障害が検出され、障害の解決には管理者の介入が明示的に必要であるため、失敗および中断の状態がシステムによって同時に設定されました。たとえば、アクティブなメールボックス データベースとデータベース コピーとの間に修復不可能な相違がシステムによって検出されたときに、この状態になります。Failed 状態とは異なり、問題が解決されたかどうかがシステムによって定期的にチェックされることがなく、自動的に回復することもありません。代わりに、データベース コピーが正常な状態に戻るには、管理者が介入して障害の原因を解決する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>この状態は、単一ページの復元操作がメールボックス データベース コピーで行われていることを示します。</p></td>
</tr>
</tbody>
</table>


また、**Get-MailboxDatabaseCopyStatus** コマンドレットは、使用中のリプリケーション ネットワークの詳細も返します。これには、データベースのシード操作のソースとして使用されているすべてのデータベースのコピーに加えて、パッシブ データベース コピーに対して返される *IncomingLogCopyingNetwork*、および複数のコピーを持つアクティブ データベースに対して返される *OutgoingConnections* も含まれます。送信接続情報は、ファイル モード レプリケーションのデータベース コピーに提供されます。送信接続情報は、ブロック モード レプリケーションのデータベース コピーには提供されません。

## Get-MailboxDatabaseCopyStatus の例

次の例では、**Get-MailboxDatabaseCopyStatus** コマンドレットを使用します。それぞれの例では、結果を **Format-List** コマンドレットにパイプライン処理して、出力を一覧形式で表示します。

この例では、データベース DB2 のすべてのコピーの状態情報を返します。

    Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List

この例では、メールボックス サーバー MBX2 上のすべてのデータベース コピーの状態を返します。

    Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List

この例では、ローカル メールボックス サーバー上のすべてのデータベース コピーの状態を返します。

    Get-MailboxDatabaseCopyStatus -Local | Format-List

**Get-MailboxDatabaseCopyStatus** コマンドレットの使用方法の詳細については、「[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ja-jp/library/dd298044\(v=exchg.150\))」を参照してください。

## Test-ReplicationHealth コマンドレット

[Test-ReplicationHealth](https://technet.microsoft.com/ja-jp/library/bb691314\(v=exchg.150\)) コマンドレットを使用すると、メールボックス データベース コピーに関する連続レプリケーションの状態の情報を表示できます。このコマンドレットを使用すると、レプリケーションのあらゆる側面と再生の状態を確認して、DAG 内の特定のメールボックス サーバーの完全な概要を提供することができます。

**Test-ReplicationHealth** コマンドレットは、連続レプリケーションと連続レプリケーション パイプライン、アクティブ マネージャー の可用性、および基盤を成すクラスター サービス、クォーラム、およびネットワーク コンポーネントの稼働状態を予防的に監視するように設計されています。DAG 内のどのメールボックス サーバーに対しても、ローカルまたはリモートで実行することができます。**Test-ReplicationHealth** コマンドレットは次の表に示すテストを実行します。

### Test-ReplicationHealth コマンドレット テスト

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>テスト名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>クラスター サービスが実行中で、指定された DAG メンバーに到達できたこと、または DAG メンバーが指定されていない場合はローカル サーバーに到達できたことを確認します。</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>Microsoft Exchange Replication サービスが実行中で、指定された DAG メンバーに到達できたこと、または DAG メンバーが指定されていない場合はローカル サーバーに到達できたことを確認します。</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>指定された DAG メンバー (DAG メンバーが指定されていない場合は、ローカル サーバー) で実行中の アクティブ マネージャー のインスタンスが、有効な役割 (プライマリ、セカンダリ、またはスタンドアロン) になっていることを確認します。</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>タスク リモート プロシージャ コール (RPC) サーバーが実行中で、指定された DAG メンバーに到達できたこと、または DAG メンバーが指定されていない場合はローカル サーバーに到達できたことを確認します。</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>TCP ログ コピー リスナーが実行中で、指定された DAG メンバーに到達できたこと、または DAG メンバーが指定されていない場合はローカル サーバーに到達できたことを確認します。</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>Active Directory および アクティブ マネージャー でルックアップを実行する DAG メンバーおよび クライアント アクセス サーバーで アクティブ マネージャー クライアント/サーバー プロセスを確認し、ユーザーのメールボックス データベースがアクティブである場所を特定します。</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>すべての DAG メンバーが使用可能、実行中、および到達可能であることを確認します。</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>指定された DAG メンバー (または、DAG メンバーが指定されていない場合はローカル サーバー) 上のすべてのクラスター管理ネットワークが利用可能であることを確認します。</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>既定のクラスター グループ (クォーラム グループ) が正常でオンラインの状態にあることを確認します。</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>DAG 用に構成されたミラーリング監視サーバー、監視ディレクトリ、および共有が到達可能であることを確認します。</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>指定された DAG メンバー上で、または DAG メンバーが指定されていない場合はローカル サーバー上で、データベースの正常なコピーが 1 つ以上使用可能であることを確認します。</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>指定された DAG メンバー上で、または DAG メンバーが指定されていない場合はローカル サーバー上で、データベースに十分な可用性があることを確認します。</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>指定された DAG メンバー上、または DAG メンバーが指定されていない場合はローカル サーバー上のメールボックス データベース コピーのいずれかが Suspended 状態になっていないかどうかをチェックします。</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>指定された DAG メンバー上、または DAG メンバーが指定されていない場合はローカル サーバー上のメールボックス データベース コピーのいずれかが Failed 状態になっていないかどうかをチェックします。</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>指定された DAG メンバー上、または DAG メンバーが指定されていない場合はローカル サーバー上のメールボックス データベース コピーのいずれかが Initializing の状態になっていないかどうかをチェックします。</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>指定された DAG メンバー上、または DAG メンバーが指定されていない場合はローカル サーバー上のメールボックス データベース コピーのいずれかが Disconnected の状態になっていないかどうかをチェックします。</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>指定された DAG メンバー (または DAG メンバーが指定されていない場合はローカル サーバー) 上でデータベースのパッシブ コピーによって行われるログのコピーと検査が、アクティブ コピーでのログ生成処理に対応できることを確認します。</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>指定された DAG メンバー (または DAG メンバーが指定されていない場合はローカル サーバー) 上でのデータベースのパッシブ コピーの再生処理が、ログのコピーと検査処理に対応できることを確認します。</p></td>
</tr>
</tbody>
</table>


## Test-ReplicationHealth の例

この例では、**Test-ReplicationHealth** コマンドレットを使用して、メールボックス サーバー MBX1 のレプリケーションの状態をテストします。

    Test-ReplicationHealth -Identity MBX1

## クリムゾン チャネルのイベント ログ

Windows には、2 つのイベント ログ、Windows ログおよびアプリケーションとサービス ログが含まれています。Windows のログ カテゴリには、前のバージョンの Windows で使用可能なイベント ログ、アプリケーション、セキュリティ、およびシステム イベント ログが含まれています。また、このログ カテゴリには 2 つの新しいログ、セットアップ ログと ForwardedEvents ログも含まれています。Windows ログは、従来のアプリケーションのイベントとシステム全体に適用されるイベントを保存するようになっています。

アプリケーションとサービス ログは、イベント ログの新しいカテゴリです。これらのログには、システム全体に影響を及ぼす可能性のあるイベントよりも、1 つのアプリケーションやコンポーネントからのイベントが保存されます。イベント ログのこの新しいカテゴリは、アプリケーションのクリムゾン チャネルといいます。

アプリケーションとサービス ログ カテゴリには、4 つのサブタイプ、管理、操作、分析、およびデバッグ ログがあります。問題をトラブルシューティングするためにイベント ログ レコードを使用する場合は、管理ログ内のイベントが非常に役立ちます。管理ログ内のイベントは、イベントへの対応方法についてのガイダンスを提供します。操作ログ内のイベントも有用ですが、情報が足りない可能性があります。管理ログとデバッグ ログは、わかりやすく記述されていません。分析ログ (既定では非表示にされ、無効化されています) には、問題を追跡するイベントが保存され、通常は大量のイベントが記録されています。デバッグ ログは、開発者がアプリケーションをデバッグするときに使用されます。

Exchange 2013 は、アプリケーションとサービス ログ領域内のクリムゾン チャネルへのイベントを記録します。これらのチャネルを表示するには、次の手順を実行します。

1.  イベント ビューアーを開きます。

2.  コンソール ツリーで、**\[アプリケーションとサービス ログ\]** \> **\[Microsoft\]** \> **\[Exchange\]** の順に移動します。

3.  **\[Exchange\]** の下で、**\[HighAvailability\]** や **\[MailboxDatabaseFailureItems\]** (DAG およびデータベース コピー関連のイベントを確認する場合)、または **\[ActiveMontoring\]** や **\[ManagedAvailability\]** (可用性管理に関連するイベントを確認する場合) などのクリムゾン チャネルを選択します。

HighAvailability チャネルには、Microsoft Exchange Replication サービスの起動とシャットダウンに関連するイベント、および アクティブ マネージャー、サードパーティ製の同期レプリケーション API、タスク RPC サーバー、TCP リスナー、およびボリューム シャドウ コピー サービス (VSS) ライターなど、Microsoft Exchange Replication サービス内で実行されるさまざまなコンポーネントに関連するイベントが含まれます。また、HighAvailability チャネルは、アクティブ マネージャー 役割監視およびデータベース マウント処理やログの切り詰めなどのデータベース処理イベントに関連するイベントを記録し、DAG の基になるクラスターに関連するイベントを記録するために、アクティブ マネージャー によって使用されます。

MailboxDatabaseFailureItems チャネルは、レプリケートされたメールボックス データベースに影響を及ぼす障害に関わるイベントの記録に使用されます。

ActiveMonitoring チャネルには、可用性管理のプローブ、モニター、レスポンダーの定義および結果のイベントが含まれます。

ManagedAvailability チャネルには、回復処理のログと結果、および関連するイベントが含まれます。

## ディスク領域低下の監視

Exchange 2013 可用性管理では、多数のシステム メトリックおよびコンポーネントを毎分監視します。これには、メールボックス サーバーの役割によって使用されるボリュームの空きディスク領域の容量が含まれます。Exchange 2013 Service Pack 1 (SP1) より前では、Exchange はすべてのローカル ボリュームの使用可能な空き領域を監視していました。これには、データベースやログ ファイルが存在しないボリュームも含まれていました。SP1 以降では、Exchange データベースおよびログ ファイルを含むボリュームのみが監視されます。SP1 では、ボリューム領域の低下を監視するための既定しきい値は 200 GB です。Exchange 2013 の累積的な更新プログラム 6 以降では、既定しきい値は 180 GB です。SP1 以降では、カスタマイズする各メールボックス サーバーで、次の DWORD レジストリ値 (MB 単位) を追加することによってしきい値を構成できます。

パス: **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

値: *SpaceMonitorLowSpaceThresholdInMB*

たとえば、しきい値を 100 GB に構成するには、次のレジストリ値を構成します。

**REG\_DWORD 186a0 (100000)**

上記のレジストリ値を構成するか変更した後、Microsoft Exchange DAG 管理サービスを再開して、変更を有効にします。

## CollectOverMetrics.ps1 スクリプト

Exchange 2013 には、Scripts フォルダー内に CollectOverMetrics.ps1 というスクリプトが含まれています。CollectOverMetrics.ps1 は DAG メンバーのイベント ログを読み込み、一定の期間のデータベース操作 (データベースのマウント、移動、フェールオーバーなど) に関する情報を収集します。操作のたびに、このスクリプトは次の情報を記録します。

  - データベースの ID

  - 操作の開始時刻と終了時刻

  - 操作の開始時および終了時にデータベースがマウントされていたサーバー

  - 操作の理由

  - 操作が成功したかどうか。操作が失敗した場合はエラーの詳細

スクリプトはこれらの情報を .csv ファイルに、1 行あたり 1 操作の単位で書き込みます。DAG ごとに異なる .csv ファイルが書き込まれます。

スクリプトの動作と出力をカスタマイズできるパラメーターがサポートされています。たとえば、*Database* や *ReportFilter* パラメーターを使用して、結果の出力を指定したサブセットに制限できます。これらのフィルターに一致する操作のみが、HTML 形式の概要レポートに含まれます。次の表に、使用可能なパラメーターの一覧を示します。

### CollectOverMetrics.ps1 スクリプト パラメーター

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>測定値を収集する DAG の名前を指定します。このパラメーターを省略すると、ローカル サーバーがメンバーになっている DAG が使用されます。ワイルドカード文字を使用して、複数の DAG から情報を収集し、そのレポートを作成することができます。</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>レポートを生成する必要のあるデータベースの一覧を提供します。<code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> または <code>-Database:&quot;DB*&quot;</code> などのワイルドカード文字がサポートされています。</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>レポートの対象期間を指定します。このスクリプトでは、この期間にログに記録されたイベントのみが収集されます。この結果、操作の記録が一部分のみキャプチャされる場合があります (たとえば、期間の始めに操作終了の情報が含まれる場合やその逆の場合があります)。<em>StartTime</em> パラメーターと <em>EndTime</em> パラメーターのいずれも指定されていない場合、スクリプトの既定値は過去 24 時間です。1 つのパラメーターのみが指定された場合、期間は指定した時刻から 24 時間、または指定した時刻までの 24 時間となります。</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>レポートの対象期間を指定します。このスクリプトでは、この期間にログに記録されたイベントのみが収集されます。この結果、操作の記録が一部分のみキャプチャされる場合があります (たとえば、期間の始めに操作終了の情報が含まれる場合やその逆の場合があります)。<em>StartTime</em> と <em>EndTime</em> のいずれも指定されていない場合、スクリプトの既定値は過去 24 時間です。1 つのパラメーターのみが指定された場合、期間は指定した時刻から 24 時間、または指定した時刻までの 24 時間となります。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>イベント処理の結果を保存するためのフォルダーを指定します。このパラメーターを省略すると、Scripts フォルダーが使用されます。このパラメーターを指定すると、スクリプトは生成した .csv ファイルの一覧を取得して参照元データとして使用して、HTML 形式の概要レポートを生成します。このレポートは、-GenerateHtmlReport オプションを指定して生成したレポートと同じものになります。ファイルの生成は、複数の DAG 全体で複数回に分けて実行できます。その期間が重複していてもかまいません。スクリプトはこのすべてのデータを結合します。</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>ログに記録されたすべての情報をスクリプトが収集し、操作の種類ごとにデータを分類し、各グループの統計情報を含む HTML ファイルを生成するよう指定します。レポートには、各グループの操作の総数、失敗した操作の数、および各グループ内での所要時間に関する統計情報が含まれます。また、このレポートには、操作の失敗につながったエラーの種類に関する分析も含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>HTML 生成レポートが生成後に Web ブラウザーで表示されるように指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>このスクリプトが以前に生成した既存の .csv ファイルからデータを読み込むよう指定します。この後、このデータを使用して、<em>GenerateHtmlReport</em> パラメーターによって生成されるレポートと同様の概要レポートが生成されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>スクリプトが収集する必要のある操作の種類を指定します。このパラメーターの有効な値は、<code>Move</code>、<code>Mount</code>、<code>Dismount</code>、および <code>Remount</code> です。<code>Move</code> 値は、コントロールされた移動であれフェールオーバーであれ、データベースがそのアクティブ サーバーを変更する場合を示します。<code>Mount</code> 値、<code>Dismount</code> 値、および <code>Remount</code> 値は、データベースが他のコンピューターに移動せずに、マウントの状態を変更する場合を示します。</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>スクリプトが収集する必要のある管理操作を指定します。このパラメーターの有効な値は、<code>Admin</code> または <code>Automatic</code> です。Automatic 操作は、システムによって自動的に実行された操作 (サーバーがオフラインになったときのフェールオーバーなど) のことです。Admin 操作は、Exchange 管理シェルまたは Exchange 管理センターを使用して管理者が実行した操作のことです。</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>スクリプトが通常は .csv ファイルに書き込む結果を、write-output と同様に、直接出力ストリームに書き込むよう指定します。この情報は他のコマンドにパイプ処理できます。</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>スクリプトが、データベースのマウントにかかった時間の詳細な診断ができるイベントを収集するよう指定します。サーバーのアプリケーション イベント ログのサイズが大きい場合、この段階で時間がかかる可能性があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>スクリプトが各操作に関するデータを含むすべての .csv ファイルを取得し、1 つの .csv ファイルに結合するよう指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>.csv ファイル内に書き込まれるフィールドを使用して、操作にフィルターを適用するよう指定します。このパラメーターでは <code>Where</code> 操作と同じ形式を使用します。各要素は <code>$_</code> に設定され、ブール値が返されます。たとえば、<code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code> を使用すると、レポートから既定のデータベースを除外できます。</p></td>
</tr>
</tbody>
</table>


## CollectOverMetrics.ps1 の例

次の例では、DAG DAG1 内で DB\* (ワイルドカード文字を含む) と一致するすべてのデータベースの測定値を収集します。測定値の収集後、HTML レポートが収集、表示されます。

    CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport

以下の例では、HTML 形式の概要レポートにフィルターをかける方法を示します。1 つ目の例では、*Database* パラメーターが使用されています。このパラメーターで、データベース名の一覧を取得します。概要レポートには、これらのデータベースに関するデータのみが含まれます。その次の 2 つの例では、*ReportFilter* オプションが使用されています。最後の例では、すべての既定のデータベースをフィルター処理します。

    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }

## CollectReplicationMetrics.ps1 スクリプト

Exchange 2013 には、もう 1 つの CollectReplicationMetrics.ps1 という正常性測定スクリプトが含まれています。このスクリプトは、スクリプトの実行中に測定値をリアルタイムで収集するので、アクティブな監視を実現します。CollectReplicationMetrics.ps1 では、データベース レプリケーションに関連するパフォーマンス カウンターからデータを収集します。このスクリプトでは、複数のメールボックス サーバーからカウンター データを収集し、各サーバーのデータを .csv ファイルに書き込み、その後このすべてのデータ (各コピーが失敗した、または中断された時間量、コピー キューまたは再生キューの平均の長さ、コピーがフェールオーバーの条件を満たしていなかった時間量など) を基にさまざまな統計情報をレポートします。

サーバーを個別に指定することも、DAG 全体を指定することもできます。スクリプトを実行して最初にデータを収集し、その後レポートを生成できます。また、データを収集するのみ、または収集済みのデータからレポートを生成するのみの目的で、スクリプトを実行できます。データのサンプリング頻度およびデータを収集する全体の期間を指定できます。

各サーバーから収集されたデータは、**CounterData.\<ServerName\>.\<TimeStamp\>.csv** という名前のファイルに書き込まれます。概要レポートは、**HaReplPerfReport.\<DAGName\>.\<TimeStamp\>.csv**、または **HaReplPerfReport.\<TimeStamp\>.csv** (*DagName* パラメーターなしでスクリプトを実行した場合) という名前のファイルに書き込まれます。

このスクリプトにより、Windows PowerShell のジョブが開始され、各サーバーのデータが収集されます。これらのジョブは、データ収集中の全期間で実行されます。多くのサーバーを指定すると、このプロセスでかなりのメモリ量が消費される可能性があります。また、このプロセスの最終段階で、データが処理され概要レポートが生成される際に、データが大量の場合に非常に時間がかかる可能性があります。収集段階を実行するコンピューターとは異なるコンピューターで、そのデータをコピーして処理する方法を取ることも考えられます。

CollectReplicationMetrics.ps1 スクリプトでは、スクリプトの動作と出力をカスタマイズできるパラメーターがサポートされています。次の表に、使用可能なパラメーターの一覧を示します。

### CollectReplicationMetrics.ps1 スクリプト パラメーター

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>測定値を収集する DAG の名前を指定します。このパラメーターを省略すると、ローカル サーバーがメンバーになっている DAG が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>レポートを生成する必要のあるデータベースの一覧を提供します。<code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> または <code>-DatabaseNames:&quot;DB*&quot;</code> などのワイルドカード文字の使用がサポートされています。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>イベント処理の結果を保存するためのフォルダーを指定します。このパラメーターを省略すると、Scripts フォルダーが使用されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>収集処理が実行される時間量を指定します。通常は 1 ～ 3 時間の値を指定します。各サンプルの間隔が長い場合、または、スケジュールされたタスクによって時間が短い一連のジョブが実行される場合のみ、長い時間を使用することをお勧めします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>データ測定値の収集頻度を指定します。通常は 30 秒、1 分、または 5 分の値を指定します。一般的な環境では、これらの値より短い間隔を指定しても、各サンプル間に大きな差は見られません。</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>統計情報を収集するサーバーの ID を指定します。ワイルドカード文字や GUID などの任意の値を指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>概要レポートを生成する .csv ファイルの一覧を指定します。これらのファイルは、<strong>CounterData.&lt;CounterData&gt;*</strong> という名前のファイルであり、CollectReplicationMetrics.ps1 スクリプトによって生成されたものです。</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>スクリプトが実行される処理段階を指定します。次の値を使用できます。</p>
<ul>
<li><p><code>CollectAndReport</code>   これは既定の値です。この値は、スクリプトがサーバーからのデータの収集とその後の概要レポート生成処理の両方を実行することを示します。</p></li>
<li><p><code>CollectOnly</code>   この値は、スクリプトがデータの収集のみを実行し、レポート生成は実行しないことを示します。</p></li>
<li><p><code>ProcessOnly</code>   この値は、スクリプトが一連の .csv ファイルからデータをインポートし、その後それらを処理して概要レポートを生成することを示します。<em>SummariseFiles</em> パラメーターは、処理するファイルの一覧をスクリプトに提供するために使用します。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>スクリプトでファイルを処理した後、圧縮されたフォルダーに移動する必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>スクリプトがシェル コマンドを読み込むよう指定します。このパラメーターは、スケジュールされたタスク内などの、シェルの外部からスクリプトを実行する必要がある際に便利です。</p></td>
</tr>
</tbody>
</table>


## CollectReplicationMetrics.ps1 の例

次の例では、DAG1 という DAG 内のすべてのサーバーから、1 分間隔でサンプリングして 1 時間分のデータを収集し、その後概要レポートを生成します。さらに、*ReportPath* パラメーターが使用されています。このパラメーターによって、すべてのファイルが現在のディレクトリに保存されます。

    CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath

次の例では、CounterData\* と一致するすべてのファイルからデータを読み込み、その後概要レポートを生成します。

    CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath

