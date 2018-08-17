---
title: 'POP3 および IMAP4 のプロトコル ログ出力: Exchange 2013 Help'
TOCTitle: POP3 および IMAP4 のプロトコル ログ出力
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50555745
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 および IMAP4 のプロトコル ログ出力

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

プロトコル ログ出力を使用して、Exchange 環境で POP3 接続と IMAP4 接続を確認できます。これは、POP3 または IMAP4 のパフォーマンスに関する問題のトラブルシューティングする際に便利です。

## POP3 と IMAP4 プロトコル ログ出力の有効化

Exchange 管理シェルを使用すると、プロトコル ログ出力の有効化、無効化、または変更を行うことができます。シェルを使用してプロトコル ログ出力を有効にする場合、既定のプロトコル ログ出力設定が使用されます。通常はこれらの既定の設定で十分です。

また、Microsoft Exchange Server 2013 クライアント アクセス サーバーに存在する Microsoft.Exchange.Pop3.exe.config 構成ファイルと Microsoft.Exchange.Imap4.exe.config 構成ファイルを編集することで、プロトコル ログ出力のオプションを有効または無効にしたり、変更したりすることもできます。POP3 および IMAP4 プロトコル設定を管理する方法の詳細については、「[POP3 および IMAP4 のプロトコル ログ出力の構成](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)」を参照してください。

## プロトコル ログの確認

プロトコル ログ ファイルは、データをコンマ区切り (CSV) ファイル形式で格納するテキスト ファイルです。プロトコル ログでは、各プロトコル イベントが 1 つの行に格納されます。各行の情報は、フィールドごとにまとめられています。これらのフィールドはコンマで区切られています。次の表は、各プロトコル イベントの分類に使用されるフィールドの説明です。

### 各プロトコル イベントの分類に使用されるフィールド

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
<td><p>date-time</p></td>
<td><p>プロトコル イベントの日時です。値は <em>yyyy-mm-ddhh:mm:ss.fffZ</em> 形式で記述されます。ここで、<em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日、<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒の端数、<em>Z</em> は Zulu を表しています。Zulu は、世界協定時刻 (UTC) の別の呼び方です。</p></td>
</tr>
<tr class="even">
<td><p>connector-id</p></td>
<td><p>このフィールドは、POP3 および IMAP4 のプロトコル ログ出力では使用されません。</p></td>
</tr>
<tr class="odd">
<td><p>session-id</p></td>
<td><p>プロトコル イベントに関連する SMTP セッションを一意に識別する GUID です。</p></td>
</tr>
<tr class="even">
<td><p>sequence-number</p></td>
<td><p>0 から始まり、同一セッション内でイベントごとに増やされるカウンターです。</p></td>
</tr>
<tr class="odd">
<td><p>local-endpoint</p></td>
<td><p>POP3 または IMAP4 セッションのローカル エンドポイントです。IP アドレスと TCP ポート番号で構成され、次の形式で記述されます。<em>&lt;IP アドレス&gt;</em>:<em>&lt;ポート&gt;</em></p></td>
</tr>
<tr class="even">
<td><p>remote-endpoint</p></td>
<td><p>POP3 または IMAP4 セッションのリモート エンドポイントです。IP アドレスと TCP ポート番号で構成され、次の形式で記述されます。<em>&lt;IP アドレス&gt;</em>:<em>&lt;ポート&gt;</em></p></td>
</tr>
<tr class="odd">
<td><p>event</p></td>
<td><p>プロトコル イベントを 1 文字で表したものです。イベントの取り得る値は以下のとおりです。</p>
<ul>
<li><p>+   接続</p></li>
<li><p>-   切断</p></li>
<li><p>&gt;   送信</p></li>
<li><p>&lt;   受信</p></li>
<li><p>*   情報</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>data</p></td>
<td><p>POP3 または IMAP4 イベントに関連するテキスト情報です。</p></td>
</tr>
<tr class="odd">
<td><p>context</p></td>
<td><p>このフィールドは、POP3 および IMAP4 のプロトコル ログ出力では使用されません。</p></td>
</tr>
</tbody>
</table>

