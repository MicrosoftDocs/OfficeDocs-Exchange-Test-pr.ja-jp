---
title: 'メッセージ追跡: Exchange 2013 Help'
TOCTitle: メッセージ追跡
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51407573
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージ追跡

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange Server 2013 のメッセージ追跡ログは、メッセージがメールボックス サーバーのトランスポート サービス、メールボックス サーバーのメールボックス、およびエッジ トランスポート サーバーとの間で転送される際のすべてのアクティビティを詳細に記録したものです。メッセージ追跡ログを使用して、メッセージ フォレンシック、メール フロー分析、レポート、およびトラブルシューティングを行うことができます。

Exchange 2013 では、Exchange 2013 メールボックス サーバーにトランスポート サービスとメールボックスがあるため、**Set-TransportService** コマンドレットまたは **Set-MailboxServer** コマンドレットを使用してメッセージ追跡のすべての構成タスクを実行できます。これらのコマンドレットのいずれかを使用すると、メッセージ追跡に関する以下の構成変更が行えます。

  - メッセージ追跡を有効または無効にします。既定では有効になっています。

  - メッセージ追跡ログ ファイルの場所を指定します。

  - 個々のメッセージ追跡ログ ファイルの最大サイズを指定します。既定値は 10 MB です。

  - メッセージ追跡ログ ファイルが格納されるディレクトリの最大サイズを指定します。既定値は 1,000 MB です。

  - メッセージ追跡ログ ファイルの最大保存期間を指定します。既定値は 30 日です。

  - メッセージ追跡ログで、メッセージの件名のログ収集を有効または無効にします。既定では有効になっています。


> [!NOTE]
> Exchange 管理センター (EAC) を使用してメッセージ追跡の有効/無効化、およびメッセージ追跡ログ ファイルの場所を指定することができます。



既定では、メッセージ追跡ログ ファイルが使用するハード ディスク容量を抑えるために、Exchange は循環ログを使用してファイルのサイズと保存期間に基づいてメッセージ追跡ログを制限します。

**目次**

メッセージ追跡ログを検索する

メッセージ追跡ログ ファイルの構造

メッセージ追跡ログ ファイルのフィールド

メッセージ追跡ログのイベントの種類

メッセージ追跡ログのソースの値

メッセージ追跡ログのエントリの例

メッセージ追跡ログに関するセキュリティ上の考慮事項

## メッセージ追跡ログを検索する

メッセージ追跡ログには、Exchange 2013 メールボックス サーバーを通過するメッセージに関する膨大なデータが含まれています。メッセージ追跡ログの検索にはいくつかの方法があります。

  - **Get-MessageTrackingLog**   このコマンドレットにより、管理者はさまざまなフィルター条件で、メッセージに関する情報をメッセージ追跡ログから検索できます。詳細については、「[メッセージ追跡ログの検索](search-message-tracking-logs-exchange-2013-help.md)」を参照してください。

  - **管理者用配信レポート**   管理者は、Exchange 管理センター (EAC) の <strong>配信レポート</strong> タブ、またはそのベースになっている **Search-MessageTrackingReport** コマンドレットと **Get-MesageTrackingReport** コマンドレットを使用して、組織内の特定のメールボックスによって送受信されたメッセージに関する情報をメッセージ追跡ログから検索できます。詳細については、「[管理者用の配信レポート](delivery-reports-for-administrators-exchange-2013-help.md)」を参照してください。

  - **ユーザー用配信レポート**   ユーザーは、Outlook Web App の <strong>配信レポート</strong> タブを使用して、自分のメールボックスで送受信したメッセージに関する情報をメッセージ追跡ログから検索できます。詳細については、「[配信レポート](https://go.microsoft.com/fwlink/?linkid=279920)」を参照してください。

ページのトップへ

## メッセージ追跡ログ ファイルの構造

既定では、メッセージ追跡ログ ファイルは %exchangeinstallpath%transportroles\\logs\\messagetracking にあります。

メッセージ追跡ログ ディレクトリ内のログ ファイルの名前付け規則は、`MSGTRK`*yyyymmdd-nnnn*`.log`、`MSGTRKMA`*yyyymmdd-nnnn*`.log`、`MSGTRKMD`*yyyymmdd-nnnn*`.log`、および`MSGTRKMS`*yyyymmdd-nnnn*`.log` です。それぞれのログは以下のサービスで使用されます。

  - **MSGTRK**   トランスポート サービスに関するログです。

  - **MSGTRKMA**   モデレート トランスポートの許可と拒否に関するログです。詳細については、「[メッセージ承認の管理](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-message-approval)」を参照してください。

  - **MSGTRKMD**   メールボックス トランスポート配信サービスによってメールボックスに配信されたメッセージに関するログです。

  - **MSGTRKMD**   メールボックス トランスポート発信サービスによってメールボックスから送信されたメッセージに関するログです。

ログ ファイル名に含まれるプレースホルダーは以下の情報を表しています。

  - プレースホルダー *yyyymmdd* は、ログ ファイルを作成した世界協定時刻 (UTC) の日付です。ここで、*yyyy* = 年、*mm* = 月、*dd* = 日を表しています。

  - プレースホルダー *nnnn* はインスタンス番号で、メッセージ追跡ログ ファイルの名前のプレフィックスごとに、毎日値 1 から始まります。

ファイル サイズが、ログ ファイルごとに指定されている最大値に達するまで、それぞれのログ ファイルに情報を書き込みます。ファイル サイズがこの最大値に達したら、インスタンス番号を増やした新しいログ ファイルを開きます。このプロセスを終日繰り返します。ログ ファイル ローテーション機能では、次のいずれかの条件が満たされると、最も古いログ ファイルが削除されます。

  - ログ ファイルが指定された最大保存期間に達する。

  - メッセージ追跡ログ ディレクトリが指定された最大サイズに達する。
    

    > [!IMPORTANT]
    > メッセージ追跡ログ ディレクトリの最大サイズは、名前のプレフィックスが同じログ ファイルの合計サイズとして計算されます。同じプレフィックスの表記規則に従っていない他のファイルは、合計ディレクトリ サイズの計算には含まれません。古いログ ファイルの名前を変更したり、他のファイルをメッセージ追跡ログ ディレクトリにコピーしたりすると、ディレクトリが指定した最大サイズを超える場合があります。<BR>Exchange 2013 メールボックス サーバーのメッセージ追跡ログ ディレクトリの最大サイズは、指定した値の 3 倍です。異なる 4 つのサービスによって生成されるメッセージ追跡ログ ファイルは、それぞれ異なるファイル名プレフィックスを持っていますが、<STRONG>MSGTRKMA</STRONG> ログ ファイルに書き込まれるデータの量と頻度は、他の 3 つに比べてごくわずかなものです。



メッセージ追跡ログ ファイルは、データをコンマ区切り (CSV) 形式で格納するテキスト ファイルです。個々のメッセージ追跡ログ ファイルには、以下の情報を含むヘッダーがあります。

  - **\#Software:**    メッセージ追跡ログ ファイルを作成したソフトウェアの名前です。通常、値は Microsoft Exchange Server です。

  - **\#Version:**    メッセージ追跡ログ ファイルを作成したソフトウェアのバージョン番号です。現在、この値は 15.0.0.0 です。

  - **\#Log-Type**   ログの種類を示す値で、メッセージ追跡ログになります。

  - **\#Date:**    ログ ファイルが作成された UTC の日時です。UTC の日時は次のような ISO 8601 の日時形式で表されます。*yyyy-mm-dd*T*hh:mm:ss.fff*Z。ここで *yyyy* = 年、*mm* = 月、*dd* = 日です。T は時刻部分の先頭を表します。*hh* = 時、*mm* = 分、*ss* = 秒、*fff* = 秒の端数です。Z は Zulu (UTC の別称) を表します。

  - **\#Fields:**    メッセージ追跡ログ ファイルで使用されているフィールド名をコンマで区切ったものです。

ページのトップへ

## メッセージ追跡ログ ファイルのフィールド

メッセージ追跡ログでは、個々のメッセージ イベントがログの 1 行として格納されます。メッセージ イベント情報はフィールドで構成され、各フィールドはコンマで区切られています。通常、フィールド名はフィールドに含まれる情報の種類を判断できる程度に説明的な名前です。ただし、場合によってはフィールドが空であったり、メッセージ イベントの種類やイベントが記録されるメッセージ追跡ログ ファイルの種類によってフィールドに格納される情報の種類が変わったりすることがあります。以下の表に、メッセージ追跡イベントの分類に使用されるフィールドの概要を示します。


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
<td><p><strong>date-time</strong></p></td>
<td><p>メッセージ追跡イベントの日時です (UTC)。UTC の日時は次のような ISO 8601 の日時形式で表されます。<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z。ここで <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日です。T は時刻部分の先頭を表します。<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒の端数です。Z は Zulu (UTC の別称) を表します。</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>メッセージを発信したメッセージング サーバーまたはメッセージング クライアントのアドレスです (IPv4 または IPv6)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>メッセージを発信したメッセージング サーバーまたはメッセージング クライアントのホスト名または FQDN です。</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>送信元または送信先の Exchange サーバーのアドレスです (IPv4 または IPv6)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>送信先サーバーのホスト名または FQDN です。</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p><strong>source</strong> フィールドに関連する追加情報です。トランスポート エージェントの情報などが該当します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>送信元または送信先の送信コネクタまたは受信コネクタの名前です。たとえば、<em>サーバー名</em>\<em>ConnectorName</em> または <em>ConnectorName</em> となります。</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>メッセージ追跡イベントを担当する Exchange トランスポート コンポーネントです。フィールド内の値については、「メッセージ追跡ログのソースの値」セクションで後述します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>メッセージ イベントの種類です。イベントの種類については、「メッセージ追跡ログのイベントの種類」セクションで後述します。</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>現在メッセージを処理している Exchange サーバーによって割り当てられたメッセージ ID です。</p>
<p>各メッセージの <strong>internal-message-id</strong> の値は、そのメッセージの配信に携わった Exchange サーバーのメッセージ追跡ログごとに異なります。たとえば、<code>73014444033</code> のような値になります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>メッセージ ヘッダー内で検出された <strong>Message-Id:</strong> ヘッダー フィールドの値です。<strong>Message-Id:</strong> ヘッダー フィールドが存在しないか、空白の場合、任意の値が割り当てられます。この値は、メッセージの有効期間全体にわたって不変です。Exchange で作成されたメッセージの場合、値は山かっこ (<code>&lt; &gt;</code>) を含む <code>&lt;GUID@ServerFQDN&gt;</code> の形式になります。たとえば、<code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code> などです。他のメッセージング システムは異なる構文や値を使用する可能性があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>メッセージのコピー同士で共通かつ一意のメッセージ ID です。メッセージのコピーはメッセージの分割や配布グループの展開により作成される場合があります。たとえば、<code>1341ac7b13fb42ab4d4408cf7f55890f</code> のような値になります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>メッセージ受信者の電子メール アドレスです。複数の電子メール アドレスがある場合は、セミコロン (;) で区切られます。</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>このフィールドには、セミコロン (;) で区切られた各受信者の状態が含まれます。各受信者の状態値の並び順は、<strong>recipient-address</strong> フィールドの値と同じです。状態値は、<code>250 2.1.5 Recipient OK</code> や <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code> のようになります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>添付ファイルを含むメッセージのサイズを、バイト単位で表します。</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>メッセージ内の受信者の数です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>このフィールドは、<strong>EXPAND</strong>、<strong>REDIRECT</strong>、および <strong>RESOLVE</strong> イベントの場合に、そのメッセージに関連する他の受信者の電子メール アドレスを表示するために使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>このフィールドには、イベントの種類に応じた追加情報が含まれます。たとえば、</p>
<p><strong>DSN</strong>   レポート リンクが含まれ、このイベントの後に配信状態通知 (DSN) が生成された場合に、関連する DSN の <strong>Message-Id</strong> の値が入ります。これが DSN メッセージの場合は、この DSN を生成した元のメッセージの <strong>Message-Id</strong> の値が <strong>Reference</strong> フィールドに入ります。</p>
<p><strong>EXPAND</strong>   reference フィールドには、関連するメッセージの <strong>related-recipient-address</strong> の値が入ります。</p>
<p><strong>RECEIVE</strong>   ジャーナリングや受信トレイ ルールといった他のプロセスによってメッセージが生成された場合、reference フィールドには、関連するメッセージの <strong>Message-Id</strong> の値が入ります。</p>
<p><strong>SEND</strong>   reference フィールドには、任意の DSN メッセージの <strong>Internal-Message-Id</strong> の値が入ります。</p>
<p><strong>THROTTLE</strong>   reference フィールドには、メッセージが調整された理由が入ります。</p>
<p><strong>TRANSFER</strong>   reference フィールドには、フォークされているメッセージの internal-message-id が含まれます。</p>
<p>受信トレイ ルールによって生成されたメッセージの場合、<strong>Reference</strong> フィールドには、受信トレイ ルールでこの送信メッセージが生成される原因となった受信メッセージの <strong>Internal-Message-Id</strong> の値が入ります。</p>
<p>その他の種類のイベントの場合、<strong>Reference</strong> フィールドには、フォークされたメッセージの <strong>Internal-Message-Id</strong> の値が入ります。</p>
<p>その他の種類のイベントの場合、<strong>Reference</strong> フィールドは通常空白です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p><code>Subject:</code> ヘッダー フィールドにあるメッセージの件名です。メッセージの件名の追跡は、<strong>Set-TransportService</strong> コマンドレットまたは <strong>Set-MailboxServer</strong> コマンドレットの <em>MessageTrackingLogSubjectLoggingEnabled</em> パラメーターで制御します。既定では、メッセージの件名の追跡は有効になっています。</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p><code>Sender:</code> ヘッダー フィールド (<code>Sender:</code> がない場合は <code>From:</code> ヘッダー フィールド) に指定されている電子メール アドレスです。</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>メッセージ エンベロープの <code>MAIL FROM:</code> で指定されているリターン電子メール アドレスです。このフィールドが空であることはありませんが、<code>&lt;&gt;</code> と表される空の送信者アドレス値である場合があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>メッセージに関する追加情報です。たとえば、</p>
<ul>
<li><p><strong>DELIVER</strong> イベントおよび <strong>SEND</strong> イベントのメッセージ発生 UTC 日時。発生日時とは、そのメッセージが最初に Exchange 組織に入った日時です。UTC の日時は次のような ISO 8601 の日時形式で表されます。<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z。ここで <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日です。T は時刻部分の先頭を表します。<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒の端数です。Z は Zulu (UTC の別称) を表します。</p></li>
<li><p>認証エラー。たとえば認証エラーが発生すると、<code>11a</code> という値と使用された認証方式が表示されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>メッセージの方向です。<code>Incoming</code>、<code>Undefined</code>、<code>Originating</code> などの値があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>このフィールドは社内 Exchange 2013 組織では使用されません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>元のクライアントのアドレス (IPv4 または IPv6)。</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>元のサーバーのアドレス (IPv4 または IPv6)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>このフィールドには、イベントの種類に応じたデータが入ります。たとえば、トランスポート ルール エージェントはこのフィールドに、メッセージに適用されたトランスポート ルールまたは DLP ポリシーの GUID を記録します。トランスポート ルール エージェントが記録する値の詳細については、「<a href="view-dlp-policy-detection-reports-exchange-2013-help.md">DLP ポリシー検出のレポートの表示</a>」の「データ ログ」セクションを参照してください。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージ追跡ログのイベントの種類

メッセージ追跡 ログのメッセージ イベントは、**event-id** フィールドのさまざまなイベントの種類によって分類されます。メッセージ イベントの中には、1 種類のメッセージ追跡ログ ファイルにしか出現しないものもあれば、すべての種類のメッセージ追跡ログ ファイルに出現するものもあります。各メッセージ イベントの分類に使用されるイベントの種類を次の表に示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>このイベントは、トランスポート エージェントがカスタム データを記録するために使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>ピックアップ ディレクトリまたは再生ディレクトリによって、配信または返却できないメッセージが発信された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>メッセージの配信の遅延が発生した。</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>メッセージがローカル メールボックスに配信された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>メッセージは、配信状態通知 (DSN、バウンス メッセージ、配信不能レポート、または NDR とも呼ばれる) なしでドロップされました。次に例を示します。</p>
<ul>
<li><p>完了したモデレート承認依頼メッセージ。</p></li>
<li><p>スパム メッセージは NDR なしでドロップされました。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>配信状態通知 (DSN) が生成された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>重複するメッセージが受信者に配信された。重複は、受信者が複数の入れ子になった配布グループのメンバーである場合に発生することがあります。重複するメッセージはインフォメーション ストアによって検出され、削除されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>配布グループの展開中に、重複する受信者が検出された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>メッセージの代理受信者がすでに受信者になっていた。</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>配布グループが展開された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>メッセージの配信が失敗した。ソースには、<strong>SMTP</strong>、<strong>DNS</strong>、<strong>QUEUE</strong>、および <strong>ROUTING</strong> が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>プライマリ コピーが次のホップに配信された後、シャドウ メッセージが破棄された。詳細については、「<a href="shadow-redundancy-exchange-2013-help.md">シャドウ冗長</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>ローカルのデータベース可用性グループ (DAG) または Active Directory サイトがシャドウ メッセージを受信した。</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>シャドウ メッセージが作成された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>シャドウ メッセージの作成に失敗した。詳細は、<strong>source-context</strong> フィールドに格納されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>モデレート受信者に送信されたメッセージが、承認のために調停メールボックスに送信された。詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-message-approval">メッセージ承認の管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>起動時にメッセージが正常に読み込まれた。</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>モデレート受信者のモデレーターがメッセージの承認も拒否もしなかったため、メッセージが期限切れになった。モデレート受信者の詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-message-approval">メッセージ承認の管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>モデレート受信者のモデレーターがメッセージを承認したため、メッセージがモデレート受信者に配信された。</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>モデレート受信者のモデレーターがメッセージを拒否したため、メッセージがモデレート受信者に配信されなかった。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>モデレート受信者のモデレーター全員に送られた承認依頼がすべて配信不能だったため、配信不能レポート (NDR) が生成された。</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>ローカル サーバーのメールボックスの送信トレイでメッセージが検出された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>ローカル サーバーのメールボックスの送信トレイでメッセージが検出され、メッセージのシャドウ コピーを作成する必要がある。</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>メッセージが有害メッセージ キューに格納されたか、または有害メッセージ キューから削除された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>メッセージが正常に処理された。</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>会議メッセージは、メールボックス トランスポート配信サービスによって処理されました。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>トランスポート サービスの SMTP 受信コンポーネントによりメッセージが受信されたかピックアップまたは再生ディレクトリからのメッセージを受信した (送信元: <code>SMTP</code>)、またはメールボックスからメールボックス トランスポート送信サービスへメッセージが送信された (送信元: <code>STOREDRIVER</code>)。</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>Active Directory 参照の後に、メッセージが代替受信者にリダイレクトされた。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>Active Directory 参照の後に、メッセージの受信者が別の電子メール アドレスに解決された。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>メッセージがセーフティ ネットから自動的に再送信された。詳細については、「<a href="safety-net-exchange-2013-help.md">セーフティ ネット</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>セーフティ ネットからのメッセージの再送信が遅延した。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>セーフティ ネットからのメッセージの再送信が失敗した。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>トランスポート サービス間でメッセージが SMTP で送信された。</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>メールボックス トランスポート発信サービスからトランスポート サービスへのメッセージの送信が成功した。<strong>SUBMIT</strong> イベントの場合、<strong>source-context</strong> プロパティには以下の詳細情報が格納されます。</p>
<ul>
<li><p><strong>MDB</strong>   メールボックス データベースの GUID。</p></li>
<li><p><strong>Mailbox</strong>   メールボックスの GUID。</p></li>
<li><p><strong>Event</strong>   イベントのシーケンス番号。</p></li>
<li><p><strong>MessageClass</strong>   メッセージの種類。たとえば、<code>IPM.Note</code> などです。</p></li>
<li><p><strong>CreationTime</strong>   メッセージの送信日時。</p></li>
<li><p><strong>ClientType</strong>   <code>User</code>、<code>OWA</code>、<code>ActiveSync</code> など。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>メールボックス トランスポート発信サービスからトランスポート サービスへのメッセージの送信が遅延した。</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>メールボックス トランスポート発信サービスからトランスポート サービスへのメッセージの送信が失敗した。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>メッセージの送信が止められた。</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>メッセージが調整された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>コンテンツ変換、メッセージの受信者制限、またはエージェントが原因で、フォークされているメッセージに受信者が移動された。ソースには、<strong>ROUTING</strong> または <strong>QUEUE</strong> が含まれます。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージ追跡ログのソースの値

メッセージ追跡ログの **source** フィールドの値は、そのメッセージ追跡イベントを担当するトランスポート コンポーネントを示します。次の表は、**source** フィールドの値の一覧です。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>source の値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>人の介入がイベント ソース。たとえば、管理者がキュー ビューアーでメッセージを削除した。または、再生ディレクトリを使用してメッセージを送信した。</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>トランスポート エージェントがイベント ソース。</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>モデレート受信者に使用される承認フレームワークがイベント ソース。詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-message-approval">メッセージ承認の管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>イベント ソースは、ブート時にサーバー上に存在する未処理のメッセージでした。これは、イベントの種類 <strong>LOAD</strong> と関係しています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>DNS がイベント ソース。</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>配信状態通知 (DSN) がイベント ソース。たとえば、配信不能レポート (NDR) など。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>外部コネクタがイベント ソース。詳細については、「<a href="foreign-connectors-exchange-2013-help.md">外部コネクタ</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>受信トレイ ルールがイベント ソース。詳細については、「<a href="https://go.microsoft.com/fwlink/?linkid=285479">受信トレイのルール</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>イベント ソースは、会議の更新情報に基づいたカレンダーを更新する会議メッセージのプロセッサでした。</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>発信者が要求した代理受信者 (ORAR) がイベント ソース。受信コネクタの ORAR のサポートを有効または無効にするには、<strong>New-ReceiveConnector</strong> コマンドレットまたは <strong>Set-ReceiveConnector</strong> コマンドレットの <em>OrarEnabled</em> パラメーターを使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>ピックアップ ディレクトリがイベント ソース。詳細については、「<a href="pickup-directory-and-replay-directory-exchange-2013-help.md">ピックアップ ディレクトリと再生ディレクトリ</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>有害メッセージ識別子がイベント ソース。有害メッセージおよび有害メッセージ キューの詳細については、「<a href="queues-exchange-2013-help.md">キュー</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>メールが有効なパブリック フォルダーがイベント ソース。</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>キューがイベント ソース。</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>シャドウ冗長がイベント ソース。詳細については、「<a href="shadow-redundancy-exchange-2013-help.md">シャドウ冗長</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>トランスポート サービスのカテゴライザーのルーティング解決コンポーネントがイベント ソース。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>セーフティ ネットがイベント ソース。詳細については、「<a href="safety-net-exchange-2013-help.md">セーフティ ネット</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>メッセージが、トランスポート サービスの SMTP 送信コンポーネントまたは SMTP 受信コンポーネントによって発信された。</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>ローカル サーバー上のメールボックスからの MAPI 送信がイベント ソース。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージ追跡ログのエントリの例

2 人のユーザー間でメッセージが問題なく送受信された場合、いくつかエントリがメッセージ追跡ログに書き込まれます。ログを参照するには、**Get-MessageTrackingLog** コマンドレットを使用します。詳細については、「[メッセージ追跡ログの検索](search-message-tracking-logs-exchange-2013-help.md)」を参照してください。

この例は、ユーザー chris@contoso.com がユーザー michelle@contoso.com にテスト メッセージを送信し、送信が成功したときに生成されたメッセージ追跡ログの要約で、2 人が同じサーバーにメールボックスを持っています。

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

ページのトップへ

## メッセージ追跡ログに関するセキュリティ上の考慮事項

メッセージ追跡ログには、メッセージのコンテンツは格納されません。既定では、電子メール メッセージの件名がメッセージ追跡ログに格納されます。セキュリティまたはプライバシーの強化された要件に従うために、メッセージの件名のログ収集を無効にする必要がある場合があります。メッセージの件名のログ収集を有効または無効にする場合は、事前に件名の情報の表示に関する組織のポリシーを確認してください。詳細については、「[メッセージ追跡を構成する](configure-message-tracking-exchange-2013-help.md)」を参照してください。

ページのトップへ

