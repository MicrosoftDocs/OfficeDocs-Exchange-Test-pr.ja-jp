---
title: 'スパム対策エージェントのログ: Exchange 2013 Help'
TOCTitle: スパム対策エージェントのログ
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 49896511
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# スパム対策エージェントのログ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

エージェント ログには、Microsoft Exchange Server 2013 の特定のスパム対策エージェントによってメッセージに対して実行された処理が記録されます。エージェント ログに情報を書き込むことができるのは、以下のエージェントのみです。

  - 接続フィルター エージェント

  - コンテンツ フィルター エージェント

  - エッジ ルール エージェント

  - 受信者フィルター エージェント

  - 送信者フィルター エージェント

  - Sender ID エージェント


> [!NOTE]
> メールボックス サーバーでは、接続フィルター エージェントおよびエッジ ルール エージェントを使用できません。



エージェント ログに書き込まれる情報は、エージェント、SMTP イベント、およびメッセージに対して実行された処理によって異なります。

エージェント ログのすべての構成タスクを実行するために、Exchange 管理シェルで **Set-TransportService** コマンドレットを使用します。エージェント ログでは、以下のオプションを選択できます。

  - エージェント ログを有効または無効にします。既定では有効になっています。

  - エージェント ログ ファイルの場所を指定します。既定値は、%ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog です。

  - 各エージェント ログ ファイルの最大サイズを指定します。既定のサイズは 10 MB です。

  - エージェント ログ ファイルに含まれるディレクトリの最大サイズを指定します。既定のサイズは 250 MB です。

  - エージェント ログ ファイルの最大保存期間を指定します。既定の保存期間は 7 日です。

ログ ファイルが使用するハード ディスク容量を抑えるために、Exchange は循環ログを使用し、ファイル サイズとファイル保存期間に基づいてエージェント ログを制限します。

**目次**

トランスポート エージェントの概要

エージェント ログ ファイルの構造

エージェント ログに書き込まれる情報

エージェント ログの検索

## トランスポート エージェントの概要

メールボックス サーバーまたはエッジ トランスポート サーバー上のトランスポート サービスを介してメッセージを送受信する際に SMTP コマンド シーケンスが使用されますが、エージェントがメッセージを処理できるのは、SMTP コマンド シーケンス内の特定のポイントに限られます。SMTP コマンド シーケンス内のこれらのアクセス ポイントは、*SMTP イベント*と呼ばれます。各エージェントには、割り当て可能な優先度があります。ただし SMTP イベントは、必ず特定の順序で発生します。したがって、エージェントの優先度は SMTP イベントによって異なります。2 つのエージェントが、同一の SMTP イベントでメッセージを処理する場合、優先度が高い方のエージェントが先にメッセージを処理します。

次の表に、SMTP イベントを発生順に、およびそれらの各 SMTP イベントにおいてエージェント ログに情報を書き込むエージェントを優先度の順に示します。

### SMTP イベント (発生順)、および各 SMTP イベントにおいてエージェント ログに情報を書き込むエージェント (優先度の順)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>SMTP イベント</th>
<th>Agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>接続フィルター エージェント</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>接続フィルター エージェント</p>
<p>送信者フィルター エージェント</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>接続フィルター エージェント</p>
<p>受信者フィルター エージェント</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>接続フィルター エージェント</p>
<p>Sender ID エージェント</p>
<p>送信者フィルター エージェント</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>エッジ ルール エージェント</p>
<p>コンテンツ フィルター エージェント</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> メールボックス サーバーでは、接続フィルター エージェントおよびエッジ ルール エージェントを使用できません。



エージェント、SMTP イベント、およびエージェントの優先度の詳細については、「[トランスポート エージェント](transport-agents-exchange-2013-help.md)」を参照してください。

ページのトップへ

## エージェント ログ ファイルの構造

エージェント ログは、%ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog にあります。

エージェント ログ ファイルの名前付け規則は、AGENTLOG*yyyymmdd-nnnn*.log です。プレースホルダーは以下の情報を表しています。

  - プレースホルダー *yyyymmdd* は、ログ ファイルを作成した世界協定時刻 (UTC) の日付です。プレースホルダー *yyyy* は年、*mm* は月、*dd* は日を表します。

  - プレースホルダー *nnnn* はインスタンス番号で、毎日値 1 から始まります。

ファイル サイズが指定された最大値に達すると、ログ ファイルに情報を書き込むのをやめ、インスタンス番号を増やした新しいログ ファイルを開きます。このプロセスを終日繰り返します。循環ログでは、エージェント ログ ディレクトリが指定された最大サイズに達するか、またはログ ファイルが指定された最大保存期間に達すると、最も古いログ ファイルを削除します。

エージェント ログ ファイルは、データをコンマ区切りファイル (CSV) 形式で格納するテキスト ファイルです。個々のエージェント ログ ファイルには、以下の情報を含むヘッダーがあります。

  - **\#Software**   エージェント ログ ファイルを作成したソフトウェアの名前です。通常、値は Microsoft Exchange Server です。

  - **\#Version**   エージェント ログ ファイルを作成したソフトウェアのバージョン番号です。現在、この値は 15.0.0.0 です。

  - **\#Log-Type**   エージェント ログである、ログの種類の値です。

  - **\#Date**   ログ ファイルが作成された UTC の日時です。UTC の日時は次のような ISO 8601 の日時形式で表されます。*yyyy-mm-dd*T*hh:mm:ss.fff*Z。ここで *yyyy* = 年、*mm* = 月、*dd* = 日です。T は時刻部分の先頭を表します。*hh* = 時、*mm* = 分、*ss* = 秒、*fff* = 秒の端数です。Z は Zulu (UTC の別称) を表します。

  - **\#Fields**   エージェント ログ ファイルで使用されているフィールド名をコンマで区切ったものです。

ページのトップへ

## エージェント ログに書き込まれる情報

エージェント ログでは、個々のエージェント トランザクションがログの 1 行として格納されます。各行の情報は、フィールドごとにまとめられています。これらのフィールドはコンマで区切られています。通常、フィールド名はフィールドに含まれる情報の種類を判断できる程度に説明的な名前です。ただし、一部のフィールドは空白になる場合もあります。また、フィールドに格納される情報の種類は、エージェントによって、またはメッセージに対して実行されたエージェントの処理によって異なる場合があります。次の表は、各エージェント トランザクションの分類に使用されるフィールドを示します。

### 各エージェント トランザクションの分類に使用されるフィールド

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Timestamp</strong></p></td>
<td><p>エージェント イベントの日時です (UTC)。UTC の日時は次のような ISO 8601 の日時形式で表されます。<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z。ここで <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日です。T は時刻部分の先頭を表します。<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒の端数です。Z は Zulu (UTC の別称) を表します。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>一意の SMTP セッション識別子です。この識別子は、16 桁の 16 進数で表されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>メッセージを受け取ったローカル IP アドレスおよびポート番号です。SMTP セッションでは、通常ポート 25 が使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>このサーバーに接続してメッセージを配信した、直前の SMTP サーバーの IP アドレスおよびポート番号です。インターネット メールが境界ネットワークのエッジ トランスポート サーバーを通過すると、メールボックス サーバー上でのエージェント ログの <strong>RemoteEndpoint</strong> の値が、エッジ トランスポート サーバーの IP アドレスになります。メッセージは SMTP によって送信されますが、送信側サーバーが使用するポート番号は、1,024 より大きい不定な値です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>最初に Exchange 組織に接続してメッセージを配信した、リモート SMTP サーバーの IP アドレスです。エッジ トランスポート サーバーでは、<strong>RemoteEndpoint</strong> と <strong>EnteredOrgFromIP</strong> の値は同じになります。スパム対策エージェントは、<strong>EnteredOrgFromIP</strong> 内の IP アドレスを使用してメッセージを調べます。</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p><code>MessageID</code> ヘッダー フィールドの値です。この値が空白である場合は、メッセージが受け付けられた場合のみ、Exchange トランスポート サーバーが任意の値を割り当てます。値が割り当てられると、<code>MessageID</code> の値はメッセージの有効期間全体にわたって不変です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>メッセージ エンベロープの <code>MAIL FROM</code> で指定されている送信者の電子メール アドレスです。この値は、SMTP メッセージング サーバー間でのメッセージの送受信に使用されます。この値が <strong>P2FromAddresses</strong> の値と比較され、メッセージ ヘッダーの送信者アドレスが偽造されていないかどうかが判定されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>メッセージ ヘッダー内の <code>From</code> ヘッダー フィールドまたは <code>Sender</code> ヘッダー フィールドで指定されている送信者の電子メール アドレスです。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>受信者の電子メール アドレスです。元のメッセージには複数の受信者が含まれていても、エージェント ログの各行には 1 人の受信者のみが格納されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>元のメッセージの受信者の合計数です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>処理を実行するエージェントの名前です。使用可能な値は次のいずれかです。</p>
<ul>
<li><p>コンテンツ フィルター エージェント</p></li>
<li><p>受信者フィルター エージェント</p></li>
<li><p>送信者フィルター エージェント</p></li>
<li><p>Sender ID エージェント</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>エージェントによる処理が発生した SMTP イベントです。<strong>Event</strong> の値はエージェントによって異なります。各エージェントが利用できる SMTP イベントについては、このトピックの最初の表で説明されています。<strong>Event</strong> の取り得る値は以下のとおりです。</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>エージェントによってメッセージに対して実行された処理です。<strong>Action</strong> の取り得る値は以下のとおりです。</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Disconnect</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>RFC 2034 で定義されている拡張 SMTP の応答です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>エージェントによって行われた処理の理由です。</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>エージェントによって行われた処理の詳細な説明です。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## エージェント ログの検索

**Get-AgentLog** コマンドレットおよび **Get-AntiSpamFilteringReport.ps1** スクリプトを使用して、エージェント ログを検索できます。

**Get-AntiSpamFilteringReport.ps1** スクリプトは、`%ExchangeInstallPath%Scripts` にあります。シェルのスクリプトは Scripts フォルダーから実行する必要があります。シェルの場所を Scripts フォルダーに変更するには、次のコマンドを実行します。

    Cd $env:ExchangeInstallPath\Scripts

Scripts フォルダーのスクリプトを実行するには、次の構文を使用します。

    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]

スクリプトの使用方法の詳細を確認するには、次のコマンドを実行します。

    Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1

ページのトップへ

