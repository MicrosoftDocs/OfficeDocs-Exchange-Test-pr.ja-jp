---
title: 'Exchange 2013 パフォーマンス カウンター: Exchange 2013 Help'
TOCTitle: Exchange 2013 パフォーマンス カウンター
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63907302
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 パフォーマンス カウンター

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-02-06_

## Exchange 2013 パフォーマンス カウンター

以下のセクションに、Exchange 2013 のパフォーマンスに関する問題をトラブルシューティングするときに利用できるパフォーマンス カウンターの一覧を示します。

## Exchange ドメイン コントローラー接続カウンター

Exchange ドメイン コントローラー接続カウンターで指定できるしきい値とその情報について、次の表で取り上げます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>カウンター</th>
<th>説明</th>
<th>しきい値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchange ADAccess Domain Controllers(*)\LDAP Read Time</p></td>
<td><p>指定されたドメイン コントローラーに LDAP 読み取り要求を送信し、応答を受信するためにかかる時間をミリ秒単位 (ms) で示します。</p></td>
<td><p>平均 50 ミリ秒未満である必要があります。スパイク (最大値) は 100 ミリ秒以下の値である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess Domain Controllers(*)\LDAP Search Time</p></td>
<td><p>LDAP 検索要求を送信し、応答を受信するためにかかる時間 (ミリ秒) を示します。</p></td>
<td><p>平均 50 ミリ秒未満である必要があります。スパイク (最大値) は 100 ミリ秒以下の値である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ADAccess Processes(*)\LDAP Read Time</p></td>
<td><p>指定されたドメイン コントローラーに LDAP 読み取り要求を送信し、応答を受信するためにかかる時間をミリ秒単位で示します。</p></td>
<td><p>平均 50 ミリ秒未満である必要があります。スパイク (最大値) は 100 ミリ秒以下の値である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess Processes(*)\LDAP Search Time</p></td>
<td><p>LDAP 検索要求を送信し、応答を受信するためにかかる時間 (ミリ秒) を示します。</p></td>
<td><p>平均 50 ミリ秒未満である必要があります。スパイク (最大値) は 100 ミリ秒以下の値である必要があります。</p></td>
</tr>
</tbody>
</table>


## プロセッサおよびプロセス カウンター

プロセッサとプロセス カウンターで指定できるしきい値とその情報について、次の表で取り上げます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>カウンター</th>
<th>説明</th>
<th>しきい値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processor(_Total)\% Processor Time</p></td>
<td><p>プロセッサがアプリケーションまたはオペレーティング システム プロセスを実行している時間の割合を示します。これはプロセッサがアイドル状態ではない時間です。</p></td>
<td><p>平均 75% 未満である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>Processor(_Total)\% User Time</p></td>
<td><p>ユーザー モードで経過したプロセッサ時間の割合を示します。ユーザー モードは、アプリケーション、環境サブシステム、および統合サブシステム向けに設計された制限付きの処理モードです。</p></td>
<td><p>平均 75% 未満である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Processor(_Total)\% Privileged Time</p></td>
<td><p>特権モードで経過したプロセッサ時間の割合を示します。特権モードは、オペレーティング システム コンポーネントとハードウェアを操作するドライバー向けに設計された処理モードです。このモードでは、ハードウェアとすべてのメモリへの直接アクセスが可能です。</p></td>
<td><p>平均 75% 未満である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>System\Processor Queue Length (all instances)</p></td>
<td><p>各プロセッサが処理しているスレッドの数を示します。Processor Queue Length は、プロセッサの処理能力が不十分であるために割り当てられた負荷を処理できないことが原因で、プロセッサの競合または高い CPU 使用率が生じていないかどうかを判断するのに使用できます。また、Processor Queue Length は、Processor Ready Queue で遅延が生じ、実行対象としてスケジュールされるのを待っているスレッド数を示します。一覧表示される値は、測定が行われた時点での最新の観測値です。</p></td>
<td><p>プロセッサごとに 5 を超えない必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Process(*)\% Processor Time</p></td>
<td><p>CPU を消費している特定のプロセスを識別するために使用できます。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## メモリ カウンター

メモリ カウンターで指定できるしきい値とその情報について、次の表で取り上げます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>Memory\Available Mbytes</p></td>
<td><p>プロセスに割り当てるかシステムで使用するのに直ちに利用可能な、物理メモリの量を MB 単位で示します。これは、スタンバイ (キャッシュ済み)、空き、ゼロ ページの一覧に割り当てられているメモリの合計と等しくなります。メモリ マネージャーに関する詳細な説明については、MSDN または『Windows Server 2003 リソース キット』の「システム パフォーマンスとトラブルシューティング ガイド」を参照してください。</p></td>
<td><p>RAM 合計の 5% を上回っている必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Memory\% Committed Bytes In Use</p></td>
<td><p>Memory\Committed Bytes の Memory\Commit Limit に対する割合を示します。コミットされたメモリは、ディスクに書き込む必要のあるページング ファイルで領域が予約されている、使用中の物理メモリです。Commit Limit はページング ファイルのサイズにより決定されます。ページング ファイルが拡張されると、Commit Limit も増え、割合は低くなります。このカウンターは、平均値ではなく現在の値のみを割合で表示します。</p></td>
<td><p>この値が 80% を超えると、より多くのメモリを必要とする負荷がシステムで生じている可能性が高いことを示します。</p></td>
</tr>
</tbody>
</table>


## .NET Framework カウンター

.NET Framework カウンターで指定できるしきい値とその情報について、次の表で取り上げます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR Memory(*)\% Time in GC</p></td>
<td><p>ガベージ コレクションが発生した時間を示します。カウンターがしきい値を超えた場合、CPU がクリーンアップされ、負荷に対して効率的に使用されていないことを示します。サーバーにメモリを追加すると、この状況が改善される可能性があります。</p></td>
<td><p>平均で 10% 未満である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>.NET CLR Exceptions(*)\# of Excepts Thrown / sec</p></td>
<td><p>1 秒間にスローされた例外の数を表示します。これには, .NET Framework 例外と, .NET Framework 例外に変換されるアンマネージ例外の両方が含まれます。たとえば、アンマネージ コード内の NULL ポインター参照の例外は、マネージ コード内で .NET Framework System.NullReferenceException として再度スローされる可能性があります。このカウンターには、処理された例外と処理不能な例外の両方が含まれます。</p></td>
<td><p>1 秒あたりの要求 (RPS) の合計の 5% 未満 (Web Server(_Total)\Connection Attempts/sec * .05) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR Memory(*)\# Bytes in all Heaps</p></td>
<td><p>他の 4 つのカウンターの合計を示します。他のカウンターは、Gen 0 Heap Size、Gen 1 Heap Size、Gen 2 Heap Size、および Large Object Heap Size です。このカウンターは、GC ヒープに割り当てられている現在のメモリをバイト単位で示します。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## ネットワーク カウンター

一般的なネットワーク カウンターで指定できるしきい値とその情報について、次の表で取り上げます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>Network Interface(*)\Packets Outbound Errors</p></td>
<td><p>エラーのために送信できなかった送信パケットの数を示します。</p></td>
<td><p>常に 0 である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connection Failures</p></td>
<td><p>現在の状態が ESTABLISHED または CLOSE-WAIT のいずれかである TCP 接続の数を示します。確立できる TCP 接続の数は、非ページ プールのサイズに制約されます。非ページ プールが使い果たされた場合は、新しい接続を確立することはできません。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Connections Reset</p></td>
<td><p>TCP 接続が ESTABLISHED 状態または CLOSE-WAIT 状態のいずれかから CLOSED 状態に直接移行した回数を示します。</p></td>
<td><p>リセット数の増加や、一貫して増加するリセット率は、帯域幅の不足を示している場合があります。</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connections Reset</p></td>
<td><p>TCP 接続が ESTABLISHED 状態または CLOSE-WAIT 状態のいずれかから CLOSED 状態に直接移行した回数を示します。</p></td>
<td><p>リセット数の増加や、一貫して増加するリセット率は、帯域幅の不足を示している場合があります。</p></td>
</tr>
</tbody>
</table>


## Netlogon カウンター

NTLM 認証の問題と MaxConcurrentAPI の問題を監視するための一般的なカウンターで指定できるしきい値とその情報について、次の表で取り上げます。詳しくは、Microsoft サポート技術情報の記事 2688798「[MaxConcurrentApi 設定を使用して NTLM 認証のパフォーマンスをチューニングする方法](https://go.microsoft.com/fwlink/p/?linkid=389728)」をご覧ください。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore Waiters</p></td>
<td><p>セマフォの取得を待機しているスレッド数。</p></td>
<td><p>Microsoft サポート技術情報の記事 2688798「<a href="https://go.microsoft.com/fwlink/p/?linkid=389728">MaxConcurrentApi 設定を使用して NTLM 認証のパフォーマンスをチューニングする方法</a>」をご覧ください。</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore Holders</p></td>
<td><p>セマフォを保持しているスレッド数。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore Acquires</p></td>
<td><p>セキュリティ チャネル接続の存続期間中、または _Total のシステム始動後、セマフォが取得された合計回数。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore Timeouts</p></td>
<td><p>セキュリティ チャネル接続の存続期間中、または _Total のシステム始動後、セマフォの待機中にスレッドがタイムアウトになった合計回数。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Average Semaphore Hold Time</p></td>
<td><p>最後のサンプルでセマフォが保持されていた平均時間 (秒)。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## データベース カウンター

次の表に、アクティブ ログ I/O 遅延要件カウンターとその指定可能なしきい値を示します。しきい値を超えると、クライアントのパフォーマンスが低下します。たとえば、ユーザー側でメッセージ配信に遅延が生じたり、システム パフォーマンスが低下したりする可能性があります。


> [!NOTE]
> Exchange 2013 における通常の格納域の待ち時間のガイダンスは、Exchange 2010 のガイダンスによく似ています。その他のデータベース カウンターは「<A href="https://go.microsoft.com/fwlink/p/?linkid=525622">メールボックス サーバー カウンター</A>」にあります。




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Attached) Average Latency</p></td>
<td><p>データベースの読み取り操作ごとの平均時間 (ミリ秒) を示します。</p></td>
<td><p>平均 20ms 未満でなければなりません。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Writes (Attached) Average Latency</p></td>
<td><p>データベースの書き込み操作ごとに平均時間 (ミリ秒) を示します。</p></td>
<td><p>平均 50ms 未満でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Log Writes Average Latency</p></td>
<td><p>ログ書き込み操作ごとの平均時間 (ミリ秒) を示します。</p></td>
<td><p>平均 10 ms 未満である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Recovery) Average Latency</p></td>
<td><p>パッシブ データベース読み取り操作ごとの平均時間 (ミリ秒) を示します。</p></td>
<td><p>平均 200 ms 未満である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Writes (Recovery) Average Latency</p></td>
<td><p>パッシブ データベース書き込み操作の平均時間 (ミリ秒) を示します。</p></td>
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Recovery) Average Latency カウンターで測定するのと同じインスタンスの読み取りの待ち時間未満である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Attached)/sec</p></td>
<td><p>アタッチされている各データベース インスタンスの 1 秒ごとのデータベース読み取り操作数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Writes (Attached)/sec</p></td>
<td><p>アタッチされている各データベース インスタンスの 1 秒ごとのデータベース書き込み操作数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Log Writes/sec</p></td>
<td><p>各データベース インスタンスの 1 秒ごとのログ書き込み数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Active Manager(_total)\Database Mounted</p></td>
<td><p>サーバー上のアクティブなデータベース コピー数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## ASP.NET

ASP.NET カウンターに指定できるしきい値とその情報を、次の表に取り上げます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Application Restarts</p></td>
<td><p>Web サーバーの有効期間中にアプリケーションが再起動された回数を示します。</p></td>
<td><p>常に 0 である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET\Worker Process Restarts</p></td>
<td><p>コンピューターでワーカー プロセスが再起動された回数を示します。</p></td>
<td><p>常に 0 である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Request Wait Time</p></td>
<td><p>最後の要求がキューで待機している時間 (ミリ秒) を示します。</p></td>
<td><p>常に 0 である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET Applications(*)\Requests In Application Queue</p></td>
<td><p>アプリケーションの要求キューにある要求の数を示します。</p></td>
<td><p>常に 0 である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET Applications(*)\Requests Executing</p></td>
<td><p>現在実行されている要求数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET Applications(*)\Requests/Sec</p></td>
<td><p>1 秒あたりに実行された要求数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## RPC クライアント アクセスのカウンター

RPC クライアント アクセスのカウンターで指定できるしきい値とその情報を、次の表に取り上げます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC Averaged Latency</p></td>
<td><p>過去 1,024 パケットの平均待機時間をミリ秒 (ms) で示します。</p></td>
<td><p>250 ms 未満である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\RPC Requests</p></td>
<td><p>RPC クライアント アクセス サービスが現在処理中のクライアント要求数を示します。</p></td>
<td><p>40 を超えないようにする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Active User Count</p></td>
<td><p>過去 2 分間に何らかの動作が示された一意のユーザー数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Connection Count</p></td>
<td><p>維持されているクライアント接続の合計数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC Operations/sec</p></td>
<td><p>1 秒間に RPC 操作が行われる割合を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\User Count</p></td>
<td><p>サービスに接続しているユーザー数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## HTTP プロキシのカウンター

HTTP プロキシのカウンターについての情報を、次の表に取り上げます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\MailboxServerLocator Average Latency</p></td>
<td><p>MailboxServerLocator Web サービス呼び出しの平均遅延時間 (ミリ秒) を示します。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Average Authentication Latency</p></td>
<td><p>過去 200 サンプルで CAS 要求の認証に費やした平均時間を示します。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Average ClientAccess Server Processing Latency</p></td>
<td><p>過去 200 要求における CAS 処理時間 (プロキシに費やした時間は含みません) の平均遅延時間 (ミリ秒) を示します。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Mailbox Server Proxy Failure Rate</p></td>
<td><p>過去 200 サンプルにおいてこのクライアント アクセス サーバーと MBX サーバー間の接続に関連して障害が発生したパーセンテージを示します。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Outsanding Proxy Requests</p></td>
<td><p>同時実行の未処理プロキシ要求の数を示します。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Proxy Requests/Sec</p></td>
<td><p>1 秒あたりに処理されたプロキシ要求数を示します。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Requests/Sec</p></td>
<td><p>1 秒間に処理される要求の数を示します。</p></td>
</tr>
</tbody>
</table>


## インフォメーション ストア カウンター

インフォメーション ストア カウンターで指定できるしきい値とその情報について、次の表で取り上げます。


> [!NOTE]
> Exchange 2013 における通常の格納域の待ち時間のガイダンスは、Exchange 2010 のガイダンスによく似ています。その他のインフォメーション ストア カウンターは「<A href="https://go.microsoft.com/fwlink/p/?linkid=525622">メールボックス サーバー カウンター</A>」にあります。




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
<td><p>しきい値</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Store(*)\RPC Requests</p></td>
<td><p>インフォメーション ストア プロセス内で現在実行されているすべての RPC 要求を示します。</p></td>
<td><p>常に 70 未満である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Client Type(*)\RPC Average Latency</p></td>
<td><p>サーバー RPC の待機時間 (ミリ秒単位) を特定のクライアント プロトコルの過去 1,024 パケットの平均で示します。</p></td>
<td><p>クライアントごとに平均 50 ミリ秒未満である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Store(*)\RPC Average Latency</p></td>
<td><p>RPC 待機平均時間 (ミリ秒) は、データベースごとの RPC 要求の平均待機時間 (ミリ秒) です。平均は、exrpc32 の読み取り後にすべての RPC に関して計算されます。</p></td>
<td><p>常時 50ms 未満で、スパイク時であっても 100ms 未満でなければなりません。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Store(*)\RPC Operations/sec</p></td>
<td><p>各データベース インスタンスの 1 秒あたりの RPC 操作数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Client Type(*)\RPC Operations/sec</p></td>
<td><p>各クライアントの種類の接続における 1 秒あたりの RPC 操作数を示します。</p></td>
<td><p>該当なし</p></td>
</tr>
</tbody>
</table>


## クライアント アクセス サーバーのカウンター

クライアント接続のカウンターとインターネット インフォメーション サービス (IIS) のカウンターについての情報を、次の表に取り上げます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Requests/sec</p></td>
<td><p>1 秒間に ASP.NET 経由でクライアントから受信される HTTP 要求の数を示します。Exchange ActiveSync の現在の要求頻度を判別します。現在のユーザー負荷を判断するためにのみ使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ActiveSync\Ping Commands Pending</p></td>
<td><p>キューで現在保留中の ping コマンド数を示します。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Sync Commands/sec</p></td>
<td><p>1 秒間に処理される sync コマンドの数を示します。クライアントはこのコマンドを使用してフォルダー内のアイテムを同期します。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Availability Service\Availability Requests (sec)</p></td>
<td><p>1 秒間に処理される要求数を示します。この要求は、空き時間情報のみの場合もあれば、提案を含んでいる場合もあります。1 つの要求には複数のメールボックスが含まれていることがあります。空き時間情報サービス要求が発生する頻度で判断されます。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange OWA\Current Unique Users</p></td>
<td><p>Outlook Web App に現在ログオンしている固有のユーザー数を示します。この値は、一意のアクティブ ユーザー セッションの数を監視するため、ログオフするかセッションがタイムアウトした後にのみ、ユーザーはこのカウンターから削除されます。現在のユーザー負荷で判断されます。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Requests/sec</p></td>
<td><p>1 秒あたりに Outlook Web App が処理した要求数を示します。現在のユーザー負荷で判断されます。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Requests/sec</p></td>
<td><p>1 秒間に処理される自動検出サービス要求の数を示します。現在のユーザー負荷で判断されます。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Requests/sec</p></td>
<td><p>1 秒間に処理される要求の数を示します。現在のユーザー負荷で判断されます。</p></td>
</tr>
<tr class="even">
<td><p>Web Service(_Total)\Current Connections</p></td>
<td><p>Web サービスとの間で現在確立されている接続の数を示します。現在のユーザー負荷で判断されます。</p></td>
</tr>
<tr class="odd">
<td><p>Web Service(Default Web Site)\Current Connections</p></td>
<td><p>既定の Web サイトに対して確立された現在の接続数を示します。これは、フロントエンド CAS サーバー ロールを使用している接続数に相当します。現在のユーザー負荷で判断されます。</p></td>
</tr>
<tr class="even">
<td><p>WebService(_Total)\Connection Attempts/sec</p></td>
<td><p>Web サービスへの接続が試みられている頻度を示します。現在のユーザー負荷で判断されます。</p></td>
</tr>
<tr class="odd">
<td><p>Web Service(_Total)\Other Request Methods/sec</p></td>
<td><p>OPTIONS、GET、HEAD、POST、PUT、DELETE、TRACE、MOVE、COPY、MKCOL、PROPFIND、PROPPATCH、SEARCH、LOCK、または UNLOCK のメソッドを使用せずに HTTP 要求が行われる頻度を示します。現在のユーザー負荷で判断されます。</p></td>
</tr>
</tbody>
</table>


## ワークロード管理のカウンター

Exchange ワークロード管理のカウンターについての情報を、次の表で取り上げます。これらのカウンターは、ワークロード管理がオフピーク時にバックグラウンドでタスクを実行する可能性があるため監視が重要になります。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>カウンター</p></td>
<td><p>説明</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\ActiveTasks</p></td>
<td><p>ワークロード管理がバックグラウンドで現在実行しているアクティブなタスクの数を示します。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange WorkloadManagement Workloads(*)\CompletedTasks</p></td>
<td><p>完了済みのワークロード管理タスクの数を示します。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\QueuedTasks</p></td>
<td><p>現在キューに配置されて処理を待機しているワークロード管理タスクの数を示します。</p></td>
</tr>
</tbody>
</table>

