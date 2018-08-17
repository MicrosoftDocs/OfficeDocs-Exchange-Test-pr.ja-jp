---
title: '接続ログ: Exchange 2013 Help'
TOCTitle: 接続ログ
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 49896458
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 接続ログ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

接続ログにより、Exchange サーバー上のトランスポート サービスからのメッセージの転送に使用される送信接続アクティビティが記録されます。接続ログの目的は、個々の電子メール メッセージの送信を追跡することではありません。むしろ接続ログでは、転送されたメッセージの数とは関係なく、送信元から宛先への接続アクティビティが追跡されます。クライアント アクセス サーバーのフロント エンド トランスポート サービス、メールボックス サーバーのハブ トランスポート サービス、およびメールボックス サーバーのメールボックス トランスポート サービスでは、接続ログが使用可能です。以下の一覧で接続ログに記録される情報の種類を説明します。

  - ソース

  - Destination

  - DNS 解決の情報

  - 接続障害についての詳細情報

  - メッセージおよび送信バイト数

接続ログのすべての構成タスクを実行するために、Exchange 管理シェルで **Set-TransportService** コマンドレット、**Set-FrontEndTransportService** コマンドレット、および **Set-MailboxTransportService** コマンドレットを使用します。接続ログでは、以下のオプションを選択できます。

  - 接続ログを有効化または無効化。既定では有効になっています。

  - 接続ログ ファイルの場所を指定します。

  - 各接続ログ ファイルの最大サイズを指定します。既定のサイズは 10 MB です。

  - 接続ログ ファイルに含まれるディレクトリの最大サイズを指定します。既定のサイズは 1,000 MB です。

  - 接続ログ ファイルの最大保存期間を指定します。既定の保存期間は 30 日です。

既定では、接続ログ ファイルが使用するハード ディスク容量を抑えるために、Exchange は循環ログを使用し、ファイル サイズとファイル保存期間に基づいて接続ログを制限します。

**目次**

接続ログ ファイルの構造

接続ログに書き込まれる情報

## 接続ログ ファイルの構造

既定では、接続ログ ファイルは以下の場所にあります。

  - **Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

接続ログ ファイルの名前付け規則は、CONNECTLOG*yyymmdd-nnnn*.log です。プレースホルダーは以下の情報を表しています。

  - プレースホルダー *yyyymmdd* は、ログ ファイルを作成した世界協定時刻 (UTC) の日付です。プレースホルダー *yyyy* は年、*mm* は月、*dd* は日を表します。

  - プレースホルダー *nnnn* はインスタンス番号で、毎日値 1 から始まります。

ファイル サイズが指定された最大値に達すると、ログ ファイルに情報を書き込むのをやめ、インスタンス番号を増やした新しいログ ファイルを開きます。このプロセスを終日繰り返します。循環ログでは、接続ログ ディレクトリが指定された最大サイズに達するか、またはログ ファイルが指定された最大保存期間に達すると、最も古いログ ファイルを削除します。

接続ログ ファイルは、データをコンマ区切りファイル (CSV) 形式で格納するテキスト ファイルです。個々の接続ログ ファイルには、以下の情報を含むヘッダーがあります。

  - **\#Software**   接続ログ ファイルを作成したソフトウェアの名前です。通常、値は Microsoft Exchange Server です。

  - **\#Version**   接続ログ ファイルを作成したソフトウェアのバージョン番号です。現在、この値は 15.0.0.0 です。

  - **\#Log-Type**   トランスポート接続ログである、ログの種類の値です。

  - **\#Date**   ログ ファイルが作成された UTC の日時です。UTC の日時は次のような ISO 8601 の日時形式で表されます。*yyyy-mm-dd*T*hh:mm:ss.fff*Z。ここで *yyyy* = 年、*mm* = 月、*dd* = 日です。T は時刻部分の先頭を表します。*hh* = 時、*mm* = 分、*ss* = 秒、*fff* = 秒の端数です。Z は Zulu (UTC の別称) を表します。

  - **\#Fields**   接続ログ ファイルで使用されているフィールド名をコンマで区切ったものです。

ページのトップへ

## 接続ログに書き込まれる情報

接続ログでは、個々の送信トランスポート サービス接続イベントが、接続ログの 1 行として格納されます。各行の情報は、フィールドごとにまとめられています。これらのフィールドはコンマで区切られています。次の表は、送信接続イベントの分類に使用されるフィールドを示します。

### 各接続イベントの分類に使用されるフィールド

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
<td><p>接続イベントの日時です (UTC)。</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>各 SMTP セッションに固有で、その SMTP セッションに関連する各イベントに共通の GUID です。メールボックス トランスポート サービスの MAPI セッションの場合、セッション フィールドは空白です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p>SMTP 接続の <strong>SMTP</strong>、ローカル メールボックス データベースへのメールボックス トランスポート サービス接続の <strong>MAPI</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>宛先の名前。</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>接続の開始、接続中、または接続の終了を 1 文字で表したものです。direction フィールドに指定できる値は以下のとおりです。</p>
<ul>
<li><p><strong>+</strong>   接続</p></li>
<li><p><strong>-</strong>   切断</p></li>
<li><p><strong>&gt;</strong>   送信</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>接続イベントに関連するテキスト情報です。以下の値は description フィールド値の例です。</p>
<ul>
<li><p>送信されたメッセージ数およびバイト数</p></li>
<li><p>送信先ドメインの DNS MX リソース レコード解決情報</p></li>
<li><p>送信先メールボックス サーバーの DNS 解決情報</p></li>
<li><p>接続確立のメッセージ</p></li>
<li><p>接続エラーのメッセージ</p></li>
</ul></td>
</tr>
</tbody>
</table>


トランスポート サービスが宛先への接続を確立すると、トランスポート サービスは、1 つのメッセージまたは複数のメッセージを送信する準備を完了できます。接続とメッセージ送信処理により、接続ログに複数行で記述された複数のイベントが生成されます。異なる送信先への同時接続は、インターレースされた異なる送信先に関する接続ログ エントリを作成します。ただし、date-time、session、source および direction フィールドを使用して、開始から終了まで各個別の接続についての接続ログ エントリを編成できます。

ページのトップへ

