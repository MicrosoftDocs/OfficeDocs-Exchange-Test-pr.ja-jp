---
title: 'Exchange 管理シェルを使用してキューを管理する: Exchange 2013 Help'
TOCTitle: Exchange 管理シェルを使用してキューを管理する
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51407531
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 管理シェルを使用してキューを管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

旧バージョンの Exchange と同様に、Microsoft Exchange Server 2013 では Exchange 管理シェルを使用して、キューとキュー内のメッセージに関する情報を表示し、キューとメッセージに対する管理アクションを実行できます。Exchange 2013 では、キューはメールボックス サーバーとエッジ トランスポート サーバー上に存在します。このトピックでは、これらのサーバーを*トランスポート サーバー*と呼びます。

シェルを使用して、トランスポート サーバー上のキューとキュー内のメッセージを表示および管理する場合、管理するキューまたはメッセージを特定する方法を把握しておくことが重要です。一般に、トランスポート サーバーには配信されるキューとメッセージが大量に含まれています。キューとメッセージの管理コマンドレットで使用できるフィルター処理パラメーターにより、表示または管理するキューあるいはメッセージを特定します。

なお、キューとキュー内メッセージの管理には、Exchange ツールボックスのキュー ビューアーも使用できます。ただし、キューとメッセージの表示コマンドレットは、フィルター処理が可能なプロパティとフィルター オプションをキュー ビューアーよりも多くサポートしています。キュー ビューアーの使用の詳細については、「[キュー ビューアー](queue-viewer-exchange-2013-help.md)」を参照してください。

**目次**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## キュー フィルター処理パラメーター

次の表に、キュー管理コマンドレットで使用可能なフィルター処理パラメーターを示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンドレット</th>
<th>フィルター処理パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p><em>Identity</em> パラメーターは、<em>Filter</em> パラメーターと同じコマンドで使用することはできません。<em>Include</em> および <em>Exclude</em> パラメーターは、<em>Filter</em> パラメーターと同じコマンドで使用できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p><em>Identity</em> パラメーターまたは <em>Filter</em> パラメーターのいずれかを使用する必要がありますが、同じコマンドで両方を使用することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p><em>Server</em>、<em>Dag</em>、<em>Site</em>、または <em>Forest</em> パラメーターを使用する必要がありますが、いずれかを同時に同じコマンドで使用することはできません。<em>Filter</em> パラメーターは他すべてのフィルター処理パラメーターと共に使用できます。</p></td>
</tr>
</tbody>
</table>


なお、*Server* パラメーターはすべてのキュー管理コマンドレットで使用できます。**Get-QueueDigest** コマンドレットでは、*Server* パラメーターはスコープ パラメーターとして、キューに関する概要情報を表示するサーバーを指定します。その他すべてのキュー管理コマンドレットでは、*Server* パラメーターを使用して特定のサーバーに接続し、そのサーバー上でキュー管理コマンドを実行します。*Server* パラメーターは *Filter* パラメーターと共に、またはこのパラメーターなしで使用できますが、*Server* パラメーターを *Identity* パラメーターと共に使用することはできません。トランスポート サーバーのホスト名または FQDN と共に *Server* パラメーターを使用します。

ページのトップへ

## キュー ID

キュー管理コマンドレットの *Identity* パラメーターは、特定のキューを識別します。*Identity* パラメーターを使用すると、すでに一意のキューを指定したことになるため、他のキューのフィルター処理パラメーターはどれも使用できなくなります。*Identity* パラメーターは基本構文の *\<サーバー\>*\\*\<キュー\>* を使用します。

*\<サーバー\>* プレースホルダーは、たとえば、`mailbox01` または `mailbox01.contoso.com` などの、Exchange サーバーのホスト名または FQDN です。*\<サーバー\>* 修飾子を省略すると、ローカル サーバーが暗黙的に使用されます。

\<*キュー*\> プレースホルダーには、次のいずれかの値を指定します。

  - **永続キュー名**   永続キューには、メールボックス サーバーまたはエッジ トランスポート サーバー上に一貫した一意の名前があります。永続的なキューの名前は次のとおりです。
    
      - **送信**   このキューには、カテゴライザーによる処理を待っているメッセージが含まれます。
    
      - **到達不能**   このキューにはルーティングできないメッセージが含まれます。そこにメッセージが置かれるまで、このキューは存在しません。
    
      - **有害**   このキューには、Exchange サーバーにとって有害であると判断されたメッセージが含まれます。そこにメッセージが置かれるまで、このキューは存在しません。

  - **配信キュー名**   配信キューの名前は、そのキューの **NextHopDomain** プロパティの値です。たとえば、キューの名前には送信コネクタのアドレス スペース、Active Directory サイトの名前、または DAG の名前を指定できます。詳細については、「[キュー](queues-exchange-2013-help.md)」の「NextHopSolutionKey」セクションを参照してください。

  - **キュー整数**   配信キューとシャドウ キューには、キュー データベースで一意の整数値が割り当てられます。ただし、**Get-Queue** コマンドレットを実行して、**Identity** プロパティまたは **QueueIdentity** プロパティでキューの整数値を検索する必要があります。

  - **シャドウ キュー名**   シャドウ キューは、構文 `Shadow\`*\<QueueInteger\>* を使用します。

次の表に、キュー管理コマンドレットの *Identity* パラメーターと共に使用できる構文をまとめています。すべての値で、*\<サーバー\>* は、サーバーのホスト名または FQDN です。

### キュー ID の形式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Identity パラメーターの値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> または<code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>指定したサーバーまたはローカル サーバー上の永続的なキュー。</p>
<p><em>&lt;PersistentQueueName&gt;</em> は、<code>Submission</code>、<code>Unreachable</code>、または <code>Poison</code> です。</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> または<code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>指定したサーバーまたはローカル サーバー上の配信キュー。</p>
<p><em>&lt;NextHopDomain&gt;</em> は、キュー内のメッセージのルーティング先または配信グループです。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションを参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> または<code>&lt;QueueInteger&gt;</code></p></td>
<td><p>指定したサーバーまたはローカル サーバー上の配信キュー。</p>
<p><em>&lt;QueueInteger&gt;</em> は、<strong>Get-Queue</strong> コマンドレットの <strong>Identity</strong> プロパティに表示されるキューの一意の整数値です。</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> または<code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>指定したサーバーまたはローカル サーバー上のシャドウ キュー。</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> または<code>*</code></p></td>
<td><p>指定したサーバーまたはローカル サーバー上のすべてのキュー。これらの値は、<strong>Get-Queue</strong> コマンドレットでのみ使用できる点に注意してください。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## キュー フィルター パラメーター

*Filter* パラメーターは、すべてのキュー管理コマンドレットで使用でき、キューのプロパティに基づいて表示または管理するキューを指定することが可能です。*Filter* パラメーターは、比較演算子を使用した式を作成し、キューの操作をフィルター条件に合うキューに限定します。論理演算子 `-and` を使用すると、結果が満たす必要がある複数の条件を指定できます。

*Filter* パラメーターと共に使用できるキュー プロパティの一覧については、「[キュー](queues-exchange-2013-help.md)」を参照してください。

*Filter* パラメーターと共に使用できる比較演算子の一覧は、「Comparison operators to use when filtering queues or messages」を参照してください。

*Filter* パラメーターを使用してキューを表示および管理する手順の例については、「[キューを管理する](manage-queues-exchange-2013-help.md)」を参照してください。

ページのトップへ

## Include および Exclude パラメーター

Exchange 2013 には、`Get-Queue` コマンドレットで使用できる *Include* および *Exclude* パラメーターがあります。これらのパラメーターを個別に、同時に、または *Filter* パラメーターと共に使用することで、ローカル サーバーまたは指定したトランスポート サーバー上のキューの結果を微調整できます。たとえば、以下のように調整できます。

  - 空のキューを結果から除外します。

  - 外部の宛先へのキューを結果から除外します。

  - **DeliveryType** の特定の値があるキューを結果に含めます。

*Include* パラメーターと *Exclude* パラメーターは次のキュー プロパティを使用してキューをフィルター処理します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
<th>シェルのコード例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>この値は、<strong>DeliveryType</strong> プロパティに基づいてキューを含めるか、または除外します。複数の値をコンマで区切って指定できます。<strong>DeliveryType</strong> の有効な値については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションで説明します。</p></td>
<td><p>この例では、ローカル サーバー上のすべての配信キューを返します。このとき、スマート ホスト ルーティング用に構成されたローカル サーバー上の送信コネクタが次ホップになります。</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>この値は空のキューを含めるか、除外します。空のキューは、<strong>MessageCount</strong> プロパティの値が <code>0</code> になります。</p></td>
<td><p>この例では、メッセージを含むローカル サーバー上のすべてのキューを返します</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>この値は、<strong>NextHopCategory</strong> プロパティの値が <code>External</code> のキューを含めるか、除外します。</p>
<p>外部キューは、常に、<strong>DeliveryType</strong> の値が次のいずれかになります。</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションを参照してください。</p></td>
<td><p>この例では、ローカル サーバー上のすべての内部キューを返します。</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>この値は、<strong>NextHopCategory</strong> プロパティの値が <code>Internal</code> のキューを含めるか、除外します。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションを参照してください。</p></td>
<td><p>この例では、ローカル サーバー上のすべての内部キューを返します。</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


なお、*Include* パラメーターと *Exclude* パラメーターの機能は、*Filter* パラメーターを使用して複製できます。たとえば、コマンド `Get-Queue -Exclude Empty` は `Get-Queue -Filter {MessageCount -gt 0}` と同じ結果を取得します。ただし、*Include* パラメーターと *Exclude* パラメーターの構文は、よりシンプルで覚えやすくなっています。

ページのトップへ

## Get-QueueDigest

Exchange 2013 には、**Get-QueueDigest** という新しいキュー コマンドレットが追加されました。このコマンドレットでは、単一のコマンドにより、Exchange 組織内の一部またはすべてのキューの情報を表示できます。具体的には、**Get-QueueDigest** コマンドレットは、サーバー、DAG、Active Directory サイト、または Active Directory フォレスト全体の場所に基づいて、キューに関する情報を表示できます。境界ネットワーク内のサブスクライブ済みエッジ トランスポート サーバー上のキューは、結果に含まれないことに注意してください。また、**Get-QueueDigest** はエッジ トランスポート サーバーでは使用できますが、その場合、結果は エッジ トランスポート サーバー上のキューに制限されます。


> [!NOTE]
> 既定では、<STRONG>Get-QueueDigest</STRONG> コマンドレットは、10 以上のメッセージを含む配信キューを表示します。この結果は 1 ～ 2 分間前のものです。これらの既定値の変更方法の説明については、「<A href="configure-get-queuedigest-exchange-2013-help.md">Configure Get-QueueDigest</A>」を参照してください。



次の表に、**Get-QueueDigest** コマンドレットで使用できるフィルターと並べ替えのパラメーターを示します。


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
<td><p><em>Dag</em>、<em>Server</em>、または <em>Site</em></p></td>
<td><p>これらのパラメーターは相互に排他的で、コマンドレットのスコープを設定します。これらのパラメーターの 1 つ、または <em>Forest</em> スイッチを指定する必要があります。一般にサーバー、DAG、または Active Directory サイトの名前を使用しますが、そのサーバー、DAG、またはサイトを一意で特定する値には任意のものを使用できます。複数のサーバー、DAG、またはサイトをコンマで区切って指定できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p><em>Dag</em>、<em>Server</em>、または <em>Site</em> パラメーターを使用しない場合は、このスイッチが必要です。このスイッチを使用する場合は値を指定しません。このスイッチを使用すると、Active Directory フォレスト内のすべての Exchange 2013 メールボックス サーバーからキューを取得します。<em>Forest</em> スイッチを使用して、リモート Active Directory フォレスト内のキューを表示することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>このパラメーターに指定できる値は <code>None</code>、<code>Normal</code>、および <code>Verbose</code> です。既定値は <code>Normal</code> です。<code>None</code> 値を使用する場合、結果の <strong>[詳細]</strong> 列からキューの名前が省略されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>このパラメーターでは、キューのプロパティに基づいてキューをフィルター処理できます。「<a href="queue-filters-exchange-2013-help.md">キューのフィルター</a>」で説明したフィルター処理可能なキュー プロパティは、すべて使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>このパラメーターは、キューの結果をグループ化します。次のプロパティのいずれかによって結果をグループ化することができます。</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>Status</p></li>
<li><p>ServerName</p></li>
</ul>
<p>既定では、<code>NextHopDomain</code> によって結果がグループ化されます。これらのキュー プロパティの詳細については、「<a href="queue-filters-exchange-2013-help.md">キューのフィルター</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>このパラメーターは、キューの結果を指定した値に制限します。キューはキュー内のメッセージ番号に基づいて降順に並べ替えられ、<em>GroupBy</em> パラメーターによって指定された値でグループ化されます。既定値は 1000 です。これは、既定では、コマンドが <strong>NextHopDomain</strong> によってグループ化された上位 1,000 個のキューを表示し、最大数のメッセージを含むキューから最小数のメッセージを含むキューの順に並べ替えることを意味します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>このパラメーターには、操作がタイムアウトになるまでの秒数を指定します。既定値は <code>00:00:10</code>、つまり 10 秒間です。</p></td>
</tr>
</tbody>
</table>


この例では、Mailbox01、Mailbox02、および Mailbox03 という Exchange 2013 メールボックス サーバー上の空ではない外部キューをすべて返します。

```powershell
Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty
```

ページのトップへ

## メッセージ フィルター処理パラメーター

次の表に、メッセージ管理コマンドレットで使用可能なフィルター処理パラメーターを示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンドレット</th>
<th>フィルター処理パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>すべてのフィルター パラメーターは相互に排他的で、同じコマンド内で同時に使用できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p><em>Identity</em> パラメーターまたは <em>Filter</em> パラメーターのいずれかを使用する必要がありますが、同じコマンドで両方を使用することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p><em>Identity</em> パラメーターは必須です。</p></td>
</tr>
</tbody>
</table>


*Server* パラメーターは、**Export-Message** コマンドレットを除いたすべてのメッセージ管理コマンドレットで使用できます。*Server* パラメーターを使用して特定のサーバーに接続し、そのサーバー上でメッセージ管理コマンドを実行します。*Server* パラメーターは *Filter* パラメーターと共に、またはこのパラメーターなしで使用できますが、*Server* パラメーターを *Identity* パラメーターと共に使用することはできません。トランスポート サーバーのホスト名または FQDN と共に *Server* パラメーターを使用します。

ページのトップへ

## メッセージ ID

メッセージ管理コマンドレットの *Identity* パラメーターは、1 つ以上のキューの特定のメッセージを識別します。*Identity* パラメーターを使用すると、すでに一意のメッセージを指定したことになるため、他のメッセージ フィルター処理パラメーターはどれも使用できなくなります。*Identity* パラメーターは基本構文の *\<サーバー\>*\\*\<キュー\>*\\*\<メッセージ整数\>* を使用します。

*\<サーバー\>* プレースホルダーは、たとえば、`mailbox01` または `mailbox01.contoso.com` などの、Exchange サーバーのホスト名または FQDN です。*\<サーバー\>* 修飾子を省略すると、ローカル サーバーが暗黙的に使用されます。

\<*キュー*\> プレースホルダーには、このトピックの「キュー ID」で説明するキュー ID を使用できます。たとえば、キュー データベースでは永続キュー名、**NextHopDomain** 値、またはキューの一意の整数値を使用できます。

*\<メッセージ整数\>* プレースホルダーは、メッセージが最初にサーバー上のキュー データベースに置かれたときにメッセージに割り当てられた一意の整数値を表します。メッセージが複数のキューを必要とする複数の受信者に送信される場合、キュー データベース内のすべてのキューにあるメッセージのコピーは、すべて同じ整数値を持つことになります。ただし、**Get-Message** コマンドレットを実行して、**Identity** プロパティまたは **MessageIdentity** プロパティでメッセージの整数値を検索する必要があります。

次の表に、メッセージ管理コマンドレットの *Identity* パラメーターと共に使用できる構文をまとめています。すべての値で、*\<サーバー\>* は、サーバーのホスト名または FQDN です。

### メッセージ ID の形式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Identity パラメーターの値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> または<code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>指定したサーバーまたはローカル サーバー上の特定のキュー内のメッセージ。</p>
<p><em>&lt;メッセージ整数&gt;</em> は、<strong>Get-Message</strong> コマンドレットの <strong>Identity</strong> プロパティに表示されるメッセージの一意の整数値です。</p>
<p><em>&lt;キュー&gt;</em> は、次のいずれかの値を表します。</p>
<ul>
<li><p><strong>永続キュー名</strong>   値 <code>Submission</code>、<code>Unreachable</code>、または <code>Poison</code>。</p></li>
<li><p><strong>配信キュー名</strong>   そのキューの <strong>NextHopDomain</strong> プロパティの値で、事実上キューの名前です。この値には、ルーティング先または配信グループを指定できます。詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」の「NextHopSolutionKey」セクションを参照してください。</p></li>
<li><p><strong>キュー整数</strong> <strong>Get-Message</strong> または <strong>Get-Queue</strong> コマンドレットの <strong>Identity</strong> プロパティに表示される配信キューまたはシャドウ キューの一意の整数値。</p></li>
<li><p><strong>シャドウ キュー ID</strong>   シャドウ キュー ID は、構文 <code>Shadow\&lt;QueueInteger&gt;</code> を使用します。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code>、<code>*\&lt;MessageInteger&gt;</code>、または <code>&lt;MessageInteger&gt;</code> です。</p></td>
<td><p>指定したサーバーまたはローカル サーバー上のキュー データベース内にあるすべてのキューのすべてのメッセージ コピー。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージ フィルター パラメーター

**Get-Message**、**Remove-Message**、**Resume-Message**、および **Suspend-Message** コマンドレットで *Filter* パラメーターを使用して、表示または管理するメッセージを、そのメッセージのプロパティに基づいて指定できます。*Filter* パラメーターは、比較演算子を使用した式を作成し、メッセージの操作をフィルター条件に合うメッセージに限定します。論理演算子 `-and` を使用すると、結果が満たす必要がある複数の条件を指定できます。

*Filter* パラメーターと共に使用できるメッセージ プロパティの一覧については、「[キュー](queues-exchange-2013-help.md)」を参照してください。

*Filter* パラメーターと共に使用できる比較演算子の一覧は、「Comparison operators to use when filtering queues or messages」を参照してください。

*Filter* パラメーターを使用してメッセージを表示および管理する手順の例については、「[キューを管理する](manage-queues-exchange-2013-help.md)」を参照してください。

ページのトップへ

## キュー パラメーター

*Queue* パラメーターは、**Get-Message** コマンドレットでのみ使用します。このパラメーターを使用すると、ワイルドカード文字 (\*) を使用して、特定のキュー内のすべてのメッセージ、または複数のキューからすべてのメッセージを取得できます。*Queue* パラメーターを使用する場合は、このトピックの「キュー ID」セクションで説明するように、*\<サーバー\>*\\*\<キュー\>* というキュー ID 形式を使用します。

ページのトップへ

## キューまたはメッセージのフィルター処理に使用する比較演算子

*Filter* パラメーターを使用してキューまたはメッセージ フィルター式を作成するには、一致させるプロパティ値に対する比較演算子を含める必要があります。次の表に、フィルター式で使用できる比較演算子と、各演算子の機能を示します。すべての演算子は、比較する値の大文字小文字を区別しません。

### 比較演算子

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>演算子</th>
<th>機能</th>
<th>シェルのコード例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>この演算子は、結果が式で指定されているプロパティ値に正確に一致する必要があることを指定するために使用されます。</p></td>
<td><p>状態が &quot;再試行&quot; になっているすべてのキューの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>状態が &quot;再試行&quot; であるすべてのメッセージの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>この演算子は、結果が式で指定されているプロパティ値に一致してはならないことを指定するために使用されます。</p></td>
<td><p>状態が &quot;アクティブ&quot; 以外のすべてのキューの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>状態が &quot;アクティブ&quot; 以外のすべてのメッセージの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>この演算子は、値が整数または日付/時間で表されるプロパティで使用されます。このフィルターの結果には、指定したプロパティの値が、式で提供された値より大きいキューまたはメッセージのみが含まれます。</p></td>
<td><p>現在 1,000 を超えるメッセージが存在しているキューの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>現在の再試行回数が 3 よりも大きいメッセージの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>この演算子は、値が整数または日付/時間で表されるプロパティで使用されます。このフィルターの結果には、指定したプロパティの値が、式で提供された値より大きいか、等しいキューまたはメッセージのみが含まれます。</p></td>
<td><p>現在 1,000 以上のメッセージが存在しているキューの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>現在の再試行回数が 3 以上のメッセージの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>この演算子は、値が整数または日付/時間で表されるプロパティで使用されます。このフィルターの結果には、指定したプロパティの値が、式で提供された値より小さいキューまたはメッセージのみが含まれます。</p></td>
<td><p>現在存在しているメッセージが 1,000 より少ないキューの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>SCL が 6 よりも小さいメッセージの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>この演算子は、値が整数または日付/時間で表されるプロパティで使用されます。このフィルターの結果には、指定したプロパティの値が、式で提供された値より小さいか、等しいキューまたはメッセージのみが含まれます。</p></td>
<td><p>現在 1,000 以下のメッセージが存在しているキューの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>SCL が 6 以下のメッセージの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>この演算子は、値が文字列で表されるプロパティで使用されます。このフィルターの結果には、指定したプロパティの値に、式で提供されたテキスト文字列が含まれているキューまたはメッセージのみが含まれます。ワイルドカード文字 (*) は、文字列フィールドに適用される <strong>-like</strong> 式に使用することはできますが、列挙の種類のフィールドに使用することはできません。</p></td>
<td><p>Contoso.com で終わる SMTP ドメインが送信先に指定されている配信キューの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>テキスト &quot;payday loan&quot; を件名に含むメッセージの一覧を表示するには、次の式を使用します。</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


**-and** 比較演算子を使用して、複数の式を評価するフィルターを指定できます。キューまたはメッセージが結果に含まれるには、フィルターのすべての条件を満たす必要があります。

この例では、Contoso.com で終わる SMTP ドメイン名を送信先に持つキューと、現在 500 を超えるメッセージが存在するキューの一覧が表示されます。

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

この例では、5 よりも大きい SCL を持つ contoso.com ドメインの電子メール アドレスから送信されたメッセージの一覧が表示されます。

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

ページのトップへ

## 高度なページ パラメーター

現在のメール フローによっては、キューおよびメッセージに対するクエリがオブジェクトの大きなセットを返すことがあります。高度なページ パラメーターを使用すると、クエリ結果の取得および表示方法を制御することができます。

シェルを使用してキューおよびキュー内のメッセージを表示する場合、クエリは一度に 1 ページの情報を取得します。高度なページ パラメーターは、結果セットのサイズを制御し、結果の並べ替えにも使用することができます。高度なページ パラメーターはすべて省略可能であり、**Get-Queue** コマンドレットと **Get-Message** コマンドレットで使用できるどのパラメーター セットとも組み合わせることができます。高度なページ パラメーターを指定しない場合、クエリは ID を昇順に並べて結果を返します。

既定では、並べ替えの順序が指定されている場合、メッセージ ID プロパティが常に含まれ、昇順で並べ替えられます。これは順序に関する既定の関係です。並べ替えの順序に含めることができる他のプロパティは一意ではないため、メッセージ ID プロパティが含まれます。並べ替えの順序にメッセージ ID プロパティを明示的に含めることで、結果でメッセージ ID が降順で並べ替えられるように指定することができます。

*BookmarkIndex* パラメーターと *BookmarkObject* パラメーターを使用すると、並べ替えられた結果セット内の位置をマークすることができます。結果の次のページが取得されるときにブックマーク オブジェクトが既に存在しなくなっていた場合は、順序に関する既定の関係により、結果セットはブックマークに最も近いオブジェクトから開始されます。最も近いオブジェクトは、指定されている並べ替えの順序によって異なります。

次の表で、高度なページ パラメーターの説明を示します。

### 高度なページ パラメーター

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
<td><p><em>BookmarkIndex</em></p></td>
<td><p>このパラメーターは、結果の表示が開始される結果セット内の位置を指定します。このパラメーターの値は、全結果セットに対する 1 から始まるインデックスです。値が 0 以下の場合は、結果の最初の完全なページが返されます。値が <code>Int.MaxValue</code> に設定されている場合は、結果の最後の完全なページが返されます。</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>このパラメーターは、結果の表示が開始される結果セット内のオブジェクトを指定します。ブックマーク オブジェクトを指定すると、オブジェクトは検索の開始場所として使用されます。<em>SearchForward</em> パラメーターの値に従って、そのオブジェクトの前または後の行が取得されます。<em>BookmarkObject</em> パラメーターと、<em>BookmarkIndex</em> パラメーターを 1 つのクエリで組み合わせることはできません。</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>このパラメーターは、結果セットにブックマーク オブジェクトを含めるかどうかを指定します。既定では、この値は <code>$true</code> に設定され、ブックマーク オブジェクトが含まれます。限られた結果サイズのクエリを実行し、その結果セットの最後のアイテムを次のクエリ用のブックマークとして設定する場合があります。この場合、<em>IncludeBookmark</em> を <code>$false</code> に設定して、オブジェクトがいずれの結果セットにも含まれないようにすることができます。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>このパラメーターは、1 ページに表示する結果の数を指定します。値を指定しない場合は、既定の結果サイズである 1,000 オブジェクトが使用されます。Exchange は、結果セットを 250,000 に制限します。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>このパラメーターは、隠しパラメーターです。結果の合計数および現在のページの最初のオブジェクトのインデックスに関する情報を返します。既定値は <code>$false</code> です。</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>このパラメーターは、結果セット内を順方向に検索するか逆方向に検索するかを指定します。このパラメーターは、結果セットが返される順序には影響しません。ブックマーク インデックスまたはオブジェクトを基準にして検索の方向を決定します。ブックマーク インデックスまたはオブジェクトが指定されていない場合、<em>SearchForward</em> パラメーターによって、検索が結果セット内の最初のオブジェクトから始まるか最後のオブジェクトから始まるかが決まります。</p>
<p>このパラメーターの既定値は <code>$true</code> です。このパラメーターが <code>$true</code> に設定され、ブックマークが指定されている場合、クエリはそのブックマークから順方向に検索を行います。この構成を使用していて、ブックマークの先に結果が存在しない場合、クエリは結果の最後のページ全体を返します。</p>
<p><em>SearchForward</em> パラメーターが <code>$false</code> に設定され、ブックマークが指定されている場合、クエリはそのブックマークから逆方向に検索を行います。この構成を使用していて、ブックマークより先の結果が 1 ページに満たない場合、クエリは結果の最初のページ全体を返します。</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>このパラメーターは、結果セットの並べ替えの順序を制御するために使用されるメッセージ プロパティの配列を指定します。並べ替えの順序のプロパティは、優先順位の高い順に指定します。各プロパティはコンマで区切り、昇順で並べ替える場合はプラス記号 (+)、降順で並べ替える場合はマイナス (-) 記号を付加します。</p>
<p>このパラメーターを使用して明示的な並べ替えの順序が指定されていない場合は、クエリに一致するレコードが表示され、個別のオブジェクトの種類の Identity フィールドによって並べ替えられます。並べ替えの順序が明示的に指定されていない場合、結果は常に ID によって昇順で並べ替えられます。</p></td>
</tr>
</tbody>
</table>


次のコード例は、クエリで高度なページ パラメーターを使用する方法を示しています。この例では、コマンドは、指定されたサーバーに接続し、500 オブジェクトを含む結果セットを取得します。結果は並べ替えられた順序で表示されます。まず送信者アドレスによって昇順で並べ替えられてから、メッセージ サイズによって降順で並べ替えられます。

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

次に続くページを表示する場合は、結果セットで取得される最後のオブジェクトに対してブックマークを設定し、追加のクエリを実行します。この手順を実行するには、シェルのスクリプト機能を使用する必要があります。

次の例は、スクリプトを使用して、結果の最初のページを取得し、ブックマーク オブジェクトを設定し、結果セットからブックマーク オブジェクトを除外し、指定されたサーバー上で次の 500 オブジェクトを取得しています。

1.  シェルを開き、次のコマンドを入力して結果の最初のページを取得します。
    
    ```powershell
    $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size
    ```

2.  ブックマーク オブジェクトを設定するには、次のコマンドを入力して、最初のページの最後の要素を変数に保存します。
    
    ```powershell
    $temp=$results[$results.length-1]
    ```

3.  指定されたサーバー上で次の 500 オブジェクトを取得し、ブックマーク オブジェクトを除外するには、次のコマンドを入力します。
    
    ```powershell
    Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size
    ```

ページのトップへ

