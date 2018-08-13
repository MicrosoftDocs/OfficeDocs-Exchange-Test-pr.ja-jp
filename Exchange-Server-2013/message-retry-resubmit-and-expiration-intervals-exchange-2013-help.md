---
title: 'メッセージの再試行、再送信、および有効期限の間隔: Exchange 2013 Help'
TOCTitle: メッセージの再試行、再送信、および有効期限の間隔
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51407495
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージの再試行、再送信、および有効期限の間隔

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Microsoft Exchange Server 2013 の場合、正常に配信できないメッセージには、メッセージの配信元や配信先に基づき、再試行、再送信、有効期限の設定など、さまざまな処理が行われます。*再試行*は、配信先との接続を改めて試すことです。*再送信*は、カテゴライザーが再処理するように、送信するメッセージを送信キューに戻す操作です。指定した期間にすべての配信試行が失敗すると、メッセージは*期限切れ*になります。メッセージが期限切れになると、送信者は配信エラーの通知を受け取ります。その後、メッセージはキューから削除されます。

再試行、再送信、および期限切れの 3 つの状況すべてにおいて、メッセージに対し自動的な動作が実行される前に、手動で介入することができます。

これらの間隔を構成する方法については、「[メッセージの再試行、再送信、および有効期限の間隔を構成する](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)」を参照してください。

## メッセージの再試行の構成オプション

トランスポート サーバーが次のホップに接続できないと、キューの状態は "再試行" となります。接続試行は、キューの有効期限が切れるか、接続が確立されるまで繰り返し行われます。

## メッセージの自動再試行の構成オプション

次の表は、メッセージの再試行の間隔に使用できる構成オプションを説明したものです。

### メッセージの再試行の間隔に使用できる構成オプション

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名またはキー名</th>
<th>既定値</th>
<th>構成する場所</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>このキーには、トランスポート サーバーが送信先サーバーに接続できない場合に、直ちに試行する接続試行の回数を指定します。そのような接続エラーは通常、極めて短時間のネットワークの停止が原因で起こります。</p>
<p>このキーの有効な入力値は、0 ～ 15 の整数です。</p>
<p>一般に、ネットワークの信頼性が低く、接続の切断が意図せず何度も発生する状態が続いているのではない限り、このキーを変更する必要はありません。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> または 1 分</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>このキーでは、<em>QueueGlitchRetryCount</em> キーで指定された接続試行の間隔を制御します。</p>
<p>一般に、ネットワークの信頼性が低く、接続の切断が意図せず何度も発生する状態が続いているのではない限り、このパラメーターを変更する必要はありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p>Exchange 管理センター (EAC) の <strong>Set-TransportService</strong> コマンドレットまたはサーバーのプロパティ</p></td>
<td><p>このパラメーターには、<em>QueueGlitchRetryCount</em> キーと <em>QueueGlitchRetryInterval</em> キーで制御される接続試行が失敗した後で試行する、接続試行の回数を指定します。<em>QueueGlitchRetryCount</em> キーと <em>QueueGlitchRetryInterval</em> キーをすべて使用した接続エラーは、サーバーの再起動またはキャッシュされた DNS 参照の失敗が原因で起こることがあります。</p>
<p>このパラメーターの有効な入力値は、0 ～ 15 の整数です。このパラメーターを 0 に設定すると、次の接続試行は <em>OutboundConnectionFailureRetryInterval</em> パラメーターによって制御されます。</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>メールボックス サーバー上のトランスポート サービス:<code>00:05:00</code> または 5 分</p></li>
<li><p>エッジ トランスポート サーバー:<code>00:01:00</code> または 10 分</p></li>
</ul></td>
<td><p>EAC の <strong>Set-TransportService</strong> コマンドレットまたはサーバーのプロパティ</p></td>
<td><p>このパラメーターでは、<em>TransientFailureRetryCount</em> パラメーターに指定された接続試行の間隔を制御します。</p>
<p>値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>メールボックス サーバー上のトランスポート サービス:<code>00:10:00</code> または 10 分</p></li>
<li><p>エッジ トランスポート サーバー:<code>00:30:00</code> または 30 分</p></li>
</ul></td>
<td><p>EAC の <strong>Set-TransportService</strong> コマンドレットまたはサーバーのプロパティ</p></td>
<td><p>このパラメーターには、前に失敗した送信接続の再試行の間隔を指定します。以前に失敗した接続試行は、<em>TransientFailureRetryCount</em> パラメーターと <em>TransientFailureRetryInterval</em> パラメーターによって制御されます。</p>
<p>値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> または 15 分</p></td>
<td><p><strong>Set-TransportService</strong> コマンドレット</p></td>
<td><p>このパラメーターには、&quot;再試行&quot; の状態を持つ個々のメッセージに対する再試行の間隔を指定します。マイクロソフト カスタマー サービスおよびサポートからの指示がない限り、この既定値を変更しないことをお勧めします。</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> または 5 分</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>このキーでは、正常に到達できない接続先メールボックス データベースのメールボックス トランスポート配信サービスへの接続をキューが試行する頻度を指定します。</p>
<p>値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。</p>
<p>このキーの有効な入力値は 00:00:01 ～ 1.00:00:00 です。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージの手動再試行の構成オプション

配信キューの状態が "再試行" の場合、Exchange ツールボックスのキュー ビューアーまたはシェルの **Retry-Queue** コマンドレットを使用して、手動で直ちに接続を試行することができます。手動による再試行は、次に予定されている再試行より優先されます。接続に失敗すると、再試行の間隔がリセットされます。この操作を有効にするには、配信キューの状態が "再試行" である必要があります。

詳細については、「[キューを管理する](manage-queues-exchange-2013-help.md)」の「キューを再試行する」を参照してください。

ページのトップへ

## 遅延 DSN メッセージの構成オプション

メッセージの配信が失敗するたびに、エッジ トランスポート サーバーまたはメールボックス サーバーのトランスポート サービスは遅延配信状態通知 (DSN) メッセージを生成し、未配信のメッセージの送信者に配信できるようにキューに格納します。この遅延 DSN メッセージは、指定した遅延通知タイムアウト間隔が経過しても、その間に失敗したメッセージを配信できなかった場合にのみ送信されます。既定では、遅延通知タイムアウト間隔は 4 時間です。この遅延によって、一時的なメッセージ転送障害による不要な遅延 DSN メッセージの送信を防ぐことができます。遅延 DSN 通知メッセージの送信は、Exchange 組織の内部または外部から送信されたメッセージごとに選択的に有効または無効にすることができます。

次の表は、遅延 DSN 通知メッセージに使用できる構成オプションを説明したものです。

### 遅延 DSN 通知メッセージに使用できる構成オプション

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名</th>
<th>既定値</th>
<th>場所</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 時間</p></td>
<td><p>EAC の <strong>Set-TransportService</strong> またはサーバーのプロパティ</p></td>
<td><p>このパラメーターには、サーバーが遅延 DSN メッセージを送信者に送信するまでの待機時間を指定します。このパラメーターの値は、<em>TransientFailureRetryCount</em> パラメーターの値に <em>TransientFailureRetryInterval</em> パラメーターの値を掛けた値よりも常に大きくなっている必要があります。</p>
<p>値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>このパラメーターには、Exchange 組織の外部にいるメッセージ送信者に遅延 DSN メッセージを送信できるかどうかを指定します。</p>
<p>このパラメーターの有効な入力値は、<code>$true</code> または <code>$false</code> です。</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>このパラメーターには、Exchange 組織の内部にいるメッセージ送信者に遅延 DSN メッセージを送信できるかどうかを指定します。</p>
<p>このパラメーターの有効な入力値は、<code>$true</code> または <code>$false</code> です。</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Exchange&nbsp;2007 ハブ トランスポート サーバーでは、すべての <EM>ExternalDSN*</EM> パラメーターと <EM>InternalDSN*</EM> パラメーターを <STRONG>Set-TransportConfig</STRONG> コマンドレットではなく、<STRONG>Set-TransportServer</STRONG> コマンドレットで使用できます。Exchange&nbsp;2007 ハブ トランスポート サーバーが組織にある場合は、それぞれの Exchange&nbsp;2007 ハブ トランスポート サーバーで <STRONG>Set-TransportServer</STRONG> コマンドレットを使用してこの値を変更する必要があります。



ページのトップへ

## メッセージの再送信の構成オプション

メッセージを再送信すると、配信不能のメッセージが送信キューに戻され、カテゴライザーによって再度処理されます。

## メッセージの自動再送信

配信キューの状態が "再試行" で、指定した期間内にメッセージをまったく配信できなかった場合、未配信のメッセージは自動的に再送信されます。この期間は、EdgeTransport.exe.config アプリケーション構成ファイルの *MaxIdleTimeBeforeResubmit* キーで制御されます。配信キューのメッセージのみが自動再送信の候補になります。

値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。

既定値は `12:00:00`、つまり 12 時間です。

## メッセージの手動再送信

メールボックス サーバーのトランスポート サービスかエッジ トランスポート サーバーで次の状態にあるメッセージは、手動で再送信できます。

  - 状態が "再試行" の配信キュー。キュー内のメッセージの状態は "中断" であってはいけません。

  - 到達不能キュー内にあり、"中断" 以外の状態にあるメッセージです。

  - 有害メッセージ キュー内にあるメッセージです。

有害メッセージ キューと到達不能キューの詳細については、「[キュー](queues-exchange-2013-help.md)」の「有害メッセージ キューと到達不能キューについて」を参照してください。

配信キューまたは到達不能キューにあるメッセージを、*MaxIdleTimeBeforeResubmit* パラメーターで指定した時間を待たずに手動で再送信する場合は、*Resubmit* パラメーターを設定して **Retry-Queue** コマンドレットを使用する必要があります。有害メッセージ キューにあるメッセージを手動で再送信するには、キュー ビューアーまたは **Resume-Message** コマンドレットを使用して、メッセージを再開することができます。詳細については、「[キューを管理する](manage-queues-exchange-2013-help.md)」の「キュー内のメッセージを再送信する」を参照してください。

メッセージを手動で再送信するその他の方法は、メッセージを中断し、そのメッセージを .eml ファイル名拡張子を持つテキスト ファイルにエクスポートし、その .eml ファイルを任意のメールボックス サーバーかエッジ トランスポート サーバーにある再生ディレクトリにコピーすることです。この再送信方法は、配信キューまたは到達不能キューにあるメッセージで使用できます。有害メッセージ キューにあるメッセージは、既に "中断" 状態です。送信キューにあるメッセージを中断したり、エクスポートしたりすることはできません。


> [!NOTE]
> キュー内のメッセージをエクスポートしたときに、メッセージはキューから削除されません。メッセージをエクスポートし、再生ディレクトリを使用してそれらを正常に再送信した後で、メッセージの重複配信を避けるために、中断されたメッセージを削除する必要があります。



詳細については、「[キューからメッセージをエクスポートする](export-messages-from-queues-exchange-2013-help.md)」を参照してください。

ページのトップへ

## メッセージの有効期限の構成オプション

*メッセージの有効期限のタイムアウト間隔*には、エッジ トランスポート サーバーまたはメールボックス サーバーのトランスポート サービスが、失敗したメッセージの配信を試みる最長時間を指定します。有効期限のタイムアウト間隔が経過する前にメッセージを正常に配信できない場合は、元のメッセージまたはメッセージ ヘッダーを含む NDR が送信者に配信されます。

## メッセージの有効期限の自動設定

メッセージの有効期限のタイムアウト間隔は、**Set-TransportService** コマンドレットまたは EAC のサーバーのプロパティの *MessageExpirationTimeOut* パラメーターによって制御されます。

値を指定するには、dd.hh:mm:ss の形式で期間として入力します。ここで、d = 日、h = 時間、m = 分、s = 秒です。

既定値は `2.00:00:00`、つまり 2 日間です。このパラメーターの有効な入力の範囲は、`00:00:05` ～ `90.00:00:00` です。

## メッセージの有効期限の手動設定

メッセージの有効期限を手動で失効させることはできませんが、NDR を使用するかどうかに関係なく、送信キュー以外の任意のキュー内のメッセージを手動で削除することができます。

詳細については、「[キュー内のメッセージを管理する](manage-messages-in-queues-exchange-2013-help.md)」の「キューからメッセージを削除する」を参照してください。

ページのトップへ

