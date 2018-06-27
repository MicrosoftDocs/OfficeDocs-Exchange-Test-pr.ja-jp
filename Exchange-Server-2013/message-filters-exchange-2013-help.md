---
title: 'メッセージ フィルター: Exchange 2013 Help'
TOCTitle: メッセージ フィルター
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 49896357
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メッセージ フィルター

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

フィルター処理により、キュー内のメッセージの異なるビューが生成されます。フィルター条件を指定すると、メッセージをすばやく見つけて、操作を行うことができます。電子メール メッセージが複数の受信者に送信される場合、そのメッセージは複数のキューに存在する可能性があります。メッセージのプロパティによってフィルター処理を行う場合は、すべてのキューにあるメッセージを見つけることができます。以下のシナリオは、メッセージのフィルター処理を使用してメール フローを管理する方法の例です。

  - インターネットから電子メールを受信するメールボックス サーバーまたはエッジ トランスポート サーバーの送信キューには、配信のためにキューに置かれた大量のメッセージが含まれています。これらのメッセージの多くが、同じ件名になっています。このため、組織にスパムが送信されている可能性があります。件名の条件に一致するメッセージをすべて表示するためのフィルターを作成することができます。それらのメッセージがスパムであると判断した場合は、そのメッセージをすべて選択し、NDR を送信せずに配信キューから削除できます。

  - ユーザーから、メール フローに時間がかかっているという報告を受けました。キューを調べると、ランダムな件名を持つ多数のメッセージが単一のドメインから送信されていることがわかりました。キューに置かれているそのドメインからのメッセージをすべて表示するためのフィルターを作成することができます。それらのメッセージがスパムであると判断した場合は、そのメッセージをすべて選択し、NDR を送信せずに配信キューから削除できます。

## フィルターとなるメッセージのプロパティ

メッセージのプロパティを使用してフィルターを作成し、指定した条件に一致するメッセージを見つけることができます。キュー ビューアーで、またはメッセージ管理コマンドレットで *Filter* パラメーターを使用してフィルターを作成できます。メッセージ管理コマンドレットは、キュー ビューアーよりも多くのフィルター処理可能なプロパティをサポートしています。次の表は、フィルター処理できるメッセージのプロパティと、それらのプロパティに関連付けられた値の一覧です。

### メッセージをフィルター処理する場合に使用するメッセージのプロパティ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>キュー ビューアーのメッセージのプロパティ</th>
<th>シェルのメッセージのプロパティ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>受信日</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>メッセージがキューに置かれた日時。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>このプロパティは、メッセージの配信が延期された理由を識別します。メッセージの配信が延期されなかった場合、このプロパティの値は <code>None</code> です。配信が延期されたメッセージは、受信者の解決中に発生した一時的なエラーのために送信キューに返されます。延期されたメッセージの詳細については、「<a href="recipient-resolution-exchange-2013-help.md">受信者の解決</a>」を参照してください。値は次のいずれかです。</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>有効期限</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>このプロパティには、メッセージが配信できない場合に、そのメッセージの有効期限が切れてキューから削除される日時が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>送信元アドレス</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>このプロパティには、受信者の SMTP アドレスが含まれています。</p></td>
</tr>
<tr class="odd">
<td><p>該当なし</p></td>
<td><p><code>Identity</code></p></td>
<td><p>このプロパティは、<em>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</em> という形式のメッセージの ID です。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「メッセージの ID」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>インターネット メッセージ ID</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>このプロパティには、メッセージ ヘッダー内にある <code>Message-ID:</code> ヘッダー フィールドの値が含まれています。この値は、GUID および送信側 SMTP サーバーの FQDN を含む 電子メール アドレスとして表されます。たとえば、</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>[最新のエラー]</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>このプロパティには、メッセージに対して記録された最新のエラーを示すテキストが含まれています。たとえば、<code>A matching connector cannot be found to route the external recipient</code> などです。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>このプロパティには、メッセージがサーバーの送信キューに最初に入ってから、メッセージがキューに置かれるまでに経過した時間が含まれています。この値では、構文 <em>hh:mm:ss.ff</em> を使用します。ここで <em>hh</em> は時間、<em>mm</em> は分、<em>ss</em> は秒、<em>ff</em> は 1 秒の端数です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>メッセージの送信元の名前</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>このプロパティには、キューにメッセージを送信したトランスポート コンポーネントの名前を示すテキスト文字列が含まれています。たとえば、受信コネクタ経由でメッセージが来た場合、値は <code>SMTP:</code><em>&lt;ConnectorName&gt;</em> になります。メッセージが配信状態通知 (DSN) の場合、値は <code>DSN</code> です。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>Priority</code></p></td>
<td><p>このプロパティには、Outlook または Outlook Web App でユーザーによって割り当てられるメッセージの優先度が含まれています。指定できる値は、<code>Low</code>、<code>Normal</code>、および <code>High</code> です。詳細については、「<a href="priority-queuing-exchange-2013-help.md">優先度キュー</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>キュー ID</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>このプロパティは、メッセージを保持するキューの ID です。キュー の ID には、構文 <em>&lt;Server&gt;\&lt;Queue&gt;</em> を使用します。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「キューの ID」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>該当なし</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>このプロパティは、送信先へのメッセージの配信が自動または手動で試行された回数を識別します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>SCL (Spam Confidence Level) プロパティの値は、メッセージの SCL を指定します。有効な SCL の値は、0 ～ 9 の範囲の整数です。SCL プロパティの値が空の場合、メッセージはコンテンツ フィルター エージェントによって処理されなかったことを示します。</p>
<p>このプロパティには、メッセージの SCL (Spam Confidence Level) が含まれています。有効な SCL の値は、0 ～ 9 の範囲の整数と -1 です。詳細については、「<a href="spam-confidence-level-threshold-exchange-2013-help.md">Spam Confidence Level のしきい値</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>サイズ (KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>このプロパティには、メッセージのサイズが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>送信元 IP</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>このプロパティには、キュー内にメッセージを保持している Exchange サーバーにメッセージを送信したサーバーの IP アドレスが含まれています。アドレスは、リモート SMTP サーバーの IP アドレスか、またはローカル Exchange サーバーの IP アドレスの可能性があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>状態</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>このプロパティには、現在のメッセージの状態が表示されます。メッセージの状態は、以下のいずれかの値になります。</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「メッセージのプロパティ」セクションを参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>件名</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>このプロパティには、メッセージ ヘッダーの <code>Subject:</code> ヘッダー フィールドに表示されるメッセージの件名が表示されます。</p></td>
</tr>
</tbody>
</table>

