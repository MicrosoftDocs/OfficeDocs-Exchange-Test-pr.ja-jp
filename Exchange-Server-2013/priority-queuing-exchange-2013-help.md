---
title: '優先度キュー: Exchange 2013 Help'
TOCTitle: 優先度キュー
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51407544
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 優先度キュー

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

*優先度キュー*は、Microsoft Exchange Server 2013 の機能です。この機能を使用すると、メールボックス サーバー上のトランスポート サービスで、送信者が定義したメッセージ優先度に従ってメッセージが処理されるようになります。

メッセージの優先度は、Microsoft Outlook で送信者がメッセージを作成して送信するときに、送信者によって割り当てられます。Outlook では、メッセージの優先度として次のいずれかの値を送信者が設定できます。

  - 重要度 - 低

  - 重要度 - 標準

  - 重要度 - 高

Outlook または Outlook Web App で作成されるメッセージの既定の優先度は、"標準" です。メッセージの優先度は、メッセージ ヘッダー内の `X-Priority` ヘッダー フィールドに格納されます。

Exchange 2013 組織内で送受信されるメッセージはすべて、ルーティングと配信の前に、メールボックス サーバー上のトランスポート サービスによって分類される必要があります。メールボックス サーバー上のトランスポートサービスのカテゴライザーは、送信キューから 1 つずつメッセージを取得し、そのメッセージを配信キューに格納する前に、受信者の解決、ルーティングの解決、およびメッセージ上のコンテンツ変換を実行します。詳細については、「[メール フロー](mail-flow-exchange-2013-help.md)」を参照してください。

配信キューは、メッセージの宛先に基づいて動的に作成されます。詳細については、「[キュー](queues-exchange-2013-help.md)」を参照してください。

同じ宛先を持つメッセージはすべて、同じ配信キューに格納されます。優先度キューは、配信キューから送信先のメッセージング サーバーへのメッセージ送信に影響を及ぼします。優先度キューが有効になっている場合、高優先度のメッセージは標準優先度のメッセージの前に送信先に送信され、標準優先度のメッセージは低優先度のメッセージの前に送信先に送信されます。メッセージの優先度に基いて優先順位が設定されたメッセージ配信は、ユーザーがメッセージの配信時間に対するサービス レベル契約 (SLA) 要件を定義するのに役立ちます。

## 優先度キューを構成するためのオプション

優先度キューのサポートは、`%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML アプリケーション構成ファイル内のキーによって制御されます。優先度キューを構成する方法については、「[優先度キューを有効化および構成する](enable-and-configure-priority-queuing-exchange-2013-help.md)」を参照してください。

次の表で、それぞれのキーを詳しく説明します。

### EdgeTransport.exe.config ファイル内の優先度キューのキー

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>キー</th>
<th>既定値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>このキーによって、メールボックス サーバー上のトランスポート サービス内の優先度キューを有効または無効にします。このキーの有効な入力値は、<code>true</code> または <code>false</code> です。</p>
<p>このキーが <code>false</code> の場合、優先度キューは無効で、EdgeTransport.exe.config ファイル内に存在する優先度キュー メッセージ制限はすべて無視されます。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>このキーは、高優先度メッセージで許可される最大サイズを指定します。高優先度メッセージがこのキーで指定された値より大きい場合、そのメッセージは高優先度から標準優先度に自動的にダウングレードされます。</p>
<p>このキーの値は、<strong>Set-TransportConfig</strong> コマンドレットの <em>MaxSendMessageSize</em> パラメーターの値より大幅に小さくなければなりません。このパラメーターの既定値は、<code>10 MB</code> です。これら 2 つの値の差は、高優先度メッセージに対して、予測可能な一貫した配信時間を確保するのに役立ちます。</p>
<p>値を入力するときは、値に以下の単位のいずれかを付加した形式で記述します。</p>
<ul>
<li><p>KB (キロバイト)</p></li>
<li><p>MB (メガバイト)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>低</strong> <code>8:00:00</code> (8 時間)</p>
<p><strong>標準</strong> <code>4:00:00</code> （4 時間)</p>
<p><strong>高</strong> <code>00:30:00</code> (30 分)</p></td>
<td><p>これらのキーは、メッセージの優先度に応じて遅延配信状態通知 (DSN) メッセージのタイムアウト間隔を指定します。</p>
<p>メッセージの配信が失敗するたびに、トランスポート サービスは DSN メッセージを生成し、未配信のメッセージの送信者に配信できるようにキューに格納します。この遅延 DSN メッセージは、指定した遅延通知タイムアウト間隔が経過しても、その間に失敗したメッセージを配信できなかった場合にのみ送信されます。この遅延によって、一時的なメッセージ転送障害による不要な遅延 DSN メッセージの送信を防ぐことができます。</p>
<p>値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>低</strong> <code>2.00:00:00</code> (2 日)</p>
<p><strong>標準</strong> <code>2.00:00:00</code> (2 日)</p>
<p><strong>高</strong> <code>8:00:00</code> (8 時間)</p></td>
<td><p>これらのキーは、トランスポート サービスが失敗したメッセージの配信を試みる時間の最大の長さを指定します。有効期限のタイムアウト間隔が経過する前にメッセージを正常に配信できない場合は、元のメッセージまたはメッセージ ヘッダーを含む配信不能レポート (NDR) が送信者に配信されます。</p>
<p>値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>低</strong>   2</p>
<p><strong>標準</strong>   15</p>
<p><strong>高</strong>   3</p></td>
<td><p>これらのキーは、トランスポート サービスを単一のリモート ドメインに対してオープンにできる接続の最大数を指定します。リモート ドメインへの送信接続には、メールボックス サーバー上に存在する配信キューと送信コネクタが使用されます。</p>
<p>これら 3 つのキーの合計は、<strong>Set-TransportService</strong> コマンドレットの <em>MaxPerDomainOutboundConnections</em> パラメーターの値と等しいか、それより小さい値にする必要があります。このパラメーターの既定値は、<code>20</code> です。</p></td>
</tr>
</tbody>
</table>


## 優先度キューがメールボックス サーバー上の他のメッセージ制限に与える影響

トランスポート サービスを通過するメッセージはすべて、メッセージの再試行、再送信、および有効期限のさまざまな制限に従います。詳細については、「[メッセージ サイズの制限](message-size-limits-exchange-2013-help.md)」を参照してください。

**Set-TransportService** コマンドレットで使用可能なメッセージ制限の一部には、対応する優先度キュー メッセージ制限があります。この優先度キュー メッセージ制限は、EdgeTransport.exe.config アプリケーション構成ファイルで使用できます。次の表は、これらの対応するメッセージ制限を示しています。

### EdgeTransport.exe.config ファイル内の優先度キュー メッセージ制限に対応する Set-TransportService コマンドレットのメッセージ制限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ソース</th>
<th>パラメーターまたはキー</th>
<th>既定値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> (4 時間)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code> (4 時間)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code> (2 日)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code> (2 日)</p></td>
</tr>
</tbody>
</table>


優先度キューが無効になっている場合、EdgeTransport.exe.config 構成ファイル内に存在する優先度キュー メッセージ制限はすべて無視されます。**Set-TransportService** コマンドレットのすべてのメッセージ制限が、メールボックス サーバー上のトランスポート サービスを通過するすべてのメッセージに適用されます。

優先度キューが有効になっている場合は、EdgeTransport.exe.config 構成ファイル内の優先度キュー メッセージ制限が、**Set-TransportService** コマンドレットの対応するメッセージ制限より優先されます。**Set-TransportService** コマンドレットの他のメッセージ制限はすべて、メールボックス サーバー上のトランスポート サービスを通過する低優先度、標準優先度、および高優先度のメッセージに引き続き適用されます。

## 優先度キューのユーザー設定

*DowngradeHighPriorityMessagesEnabled* パラメーターを指定した **Set-Mailbox** コマンドレット。既定値は `$false` です。このパラメーターが `$true` に設定されている場合は、メールボックスから送信される高優先度のメッセージがすべて、標準優先度に自動的にダウングレードされます。

