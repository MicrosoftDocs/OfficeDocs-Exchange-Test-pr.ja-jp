---
title: 'トランスポート エージェント: Exchange 2013 Help'
TOCTitle: トランスポート エージェント
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 48270184
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート エージェント

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

トランスポート エージェントを使用すると、Exchange サーバーに、Microsoft、サード パーティ ベンダー、または組織によって作成されたカスタム ソフトウェアをインストールできます。このソフトウェアは、トランスポート パイプラインを経由する電子メール メッセージを処理できます。Microsoft Exchange Server 2013 では、トランスポート パイプラインは以下のプロセスから構成されています。

  - クライアント アクセス サーバー上のフロント エンド トランスポート サービス

  - メールボックス サーバー上のトランスポート サービス

  - メールボックス サーバー上のメールボックス トランスポート サービス

  - エッジ トランスポート サーバー上のトランスポート サービス

トランスポート パイプラインの詳細については、「[メール フロー](mail-flow-exchange-2013-help.md)」を参照してください。

前バージョンの Exchange と同様に、Exchange 2013 トランスポートは、Microsoft Exchange Server 2013 トランスポート エージェント SDK を通じて機能拡張を提供します。SDK の Exchange 2013 バージョンは、Microsoft.NET Framework バージョン 4.0 に基づいており、サード パーティによる次の定義済みクラスの実装を可能にします。

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

SDKのライブラリに対してコンパイルされる場合、最終アセンブリは Exchange 2013 に登録されます。登録するには、SMTP セッションまたはメッセージ処理の特定の段階でエージェントをロードし、それらのイベント ハンドラーを起動します。このような段階、またはイベントはエージェントの定義の一部です。エージェント登録情報は、XML 構成ファイルに格納されます。

次の一覧では、Exchange 2013 でトランスポート エージェントを使用するための要件について説明します。

  - メールボックス サーバーおよびエッジ トランスポート サーバーのトランスポート サービスは、SDK で事前定義されたすべてのクラスを完全にサポートします。そのため、Microsoft Exchange Server 2010 でハブ トランスポート サーバーおよびエッジ トランスポート サーバーの役割のために作成されたサード パーティ製トランスポート エージェントは、Exchange 2013 のトランスポート サービスでも動作します。

  - フロント エンド トランスポート サービスは、SDK 内の **SmtpReceiveAgent** クラスのみをサポートし、サード パーティ エージェントは **OnEndOfData** SMTP イベントでは動作できません。

  - メールボックス トランスポート サービスは、SDK を一切サポートしないため、メールボックス トランスポート サービスではサード パーティ製エージェントを使用できません。

バージョン 4.0 より前の .NET Framework のバージョンに基づくレガシー トランスポート エージェントのサポートは、既定では有効ではありませんが、有効にすることができます。手順については、「[従来のトランスポート エージェントのサポートを有効にする](enable-support-for-legacy-transport-agents-exchange-2013-help.md)」を参照してください。

**目次**

トランスポート エージェント管理への更新

トランスポート エージェントと SMTP イベント

トランスポート エージェントの優先度

組み込みのトランスポート エージェント

トランスポート エージェントのトラブルシューティング

## トランスポート エージェント管理への更新

Exchange 2013 トランスポート パイプラインへの更新のために、特にクライアント アクセス サーバーとメールボックス サーバーが同一のコンピューターにインストールされている場合、トランスポート エージェント コマンドレットでは、トランスポート サービスとフロント エンド トランスポート サービスを区別する必要があります。詳細については、「[トランスポート エージェントの管理](manage-transport-agents-exchange-2013-help.md)」を参照してください。

トランスポート エージェント管理コマンドレットは、`%ExchangeInstallPath%TransportRoles\Shared` にある構成ファイルを操作します。メールボックス サーバーとエッジ トランスポート サーバーのトランスポート サービスでは、このファイルは `agents.config` になります。クライアント アクセス サーバーのフロント エンド トランスポート サービスの場合、このファイルは `fetagents.config` になります。どちらのファイルも、Exchange 2010 と同じ形式を使用しています。トランスポート エージェントの管理の詳細については、「[トランスポート エージェントの管理](manage-transport-agents-exchange-2013-help.md)」を参照してください。

ページのトップへ

## トランスポート エージェントと SMTP イベント

トランスポート エージェントは、SMTP イベントを使用します。これらのイベントは、トランスポート パイプラインをメッセージが通過すると発生します。SMTP イベントによって、トランスポート エージェントは、SMTP の対話中および組織内でのメッセージ ルーティング中の特定の時点でのメッセージに対するアクセス権を与えられます。

Exchange 2013 には、新しい SMTP 受信イベントが存在します。SMTP 受信は、クライアント アクセス サーバーのフロント エンド トランスポート サービス、メールボックス サーバーとエッジ トランスポート サーバーのトランスポート サービス、およびメールボックス サーバーのメールボックス トランスポート配信サービスに存在します。カテゴライザーは、メールボックス サーバーとエッジ トランスポート サーバーのトランスポート サービスにのみ存在します。トランスポート サービスおよびカテゴライザーの詳細については、「[メール ルーティング](mail-routing-exchange-2013-help.md)」を参照してください。

次の表は、トランスポート パイプラインでメッセージに対するアクセス権を付与する SMTP イベントの一覧です。

### SMTP 受信イベント

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>順序</th>
<th>SMTP イベント</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストからの最初の接続によって発生します。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>HELO</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>EHLO</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>STARTTLS</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>AUTH</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストでの認証が処理されるときに発生します。</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストが認証を完了すると発生します。</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>XSESSIONPARAMS</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>MAIL FROM</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>RCPT TO</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>DATA</code> (テキスト) または <code>BDAT</code> (バイナリ データ) コマンドが発行されると発生します。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストが電子メール メッセージのヘッダーの送信を完了すると発生します。これは、メッセージ ヘッダーとメッセージ本文を分ける空白行 (<code>&lt;CRLF&gt;</code>) によって示されます。</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>このイベントは、クライアント アクセス サーバーのフロント エンド トランスポート サービスによって受信 SMTP セッションがメールボックス サーバーのトランスポート サービスに中継される、または<em>プロキシされる</em>と発生します。</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストがデータの終了コマンドを発行すると発生します。<code>DATA</code> コマンドによってテキスト セッションが開始された場合、データの終了インジケーターは <code>&lt;CRLF&gt;.&lt;CRLF&gt;</code> になります。<code>BDAT</code> コマンドによってバイナリ セッションが開始された場合、データの終了インジケーターは <code>BDAT LAST</code> になります。</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>HELP</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>このイベントは、リモート SMTP ホストによって <code>NOOP</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>このイベントは、受信側の SMTP ホストが送信側の SMTP ホストに対して、一時的または永続的な配信状態通知 (DSN) コードを発行すると発生します。</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>このイベントは、送信側 SMTP ホストによって <code>RSET</code> コマンドが発行されると発生します。</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>このイベントは、受信側または送信側のいずれかの SMTP ホストによって、SMTP 対話の接続が切断されると発生します。通常、このイベントは、リモート SMTP ホストによって <code>QUIT</code> コマンドが発行されると発生します。</p></td>
</tr>
</tbody>
</table>


\*\* これらのイベントは、**OnConnectEvent** の後、かつ **OnDisconnectEvent** の前の時点で発生します。

### カテゴライザー イベント

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>順序</th>
<th>カテゴライザー イベント</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>このイベントは、受信側のメール ボックス サーバーまたはエッジ トランスポート サーバーのトランスポート サービスにある送信キューにメッセージが到着すると発生します。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>このイベントは、すべての受信者が解決された後で、各受信者の次ホップが決定される前に発生します。<strong>OnResolvedMessage</strong> ルーティング イベントでは、受信者ごとの <strong>SetRoutingOverride</strong> メソッドを使用して、後続のイベントで既定のルーティング動作を変更することができます。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>このイベントは、メッセージが分類され、配布リストが展開され、受信者が解決された後で発生します。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>このイベントは、カテゴライザーがメッセージの処理を完了すると発生します。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## トランスポート エージェントの優先度

トランスポート パイプラインのメッセージをトランスポート エージェントが処理する順位を決定する次の 2 つの要因があります。

1.  トランスポート エージェントが登録された SMTP イベントと、その SMTP イベントでメッセージが発生するタイミング。

2.  同一の SMTP イベントに登録された複数のエージェントが存在する場合、トランスポート エージェントに割り当てられた優先度の値。最も高い優先度は 1 です。整数値が大きくなると、エージェントの優先度は低くなります。

たとえば、次のようなトランスポート エージェントを構成したとします。

  - 優先度 1 のトランスポート エージェント A と優先度 2 のトランスポート エージェント C が **OnEndOfHeaders** SMTP イベントに登録されています。

  - 優先度 4 のトランスポート エージェント B が **OnMailCommand** SMTP イベントに登録されています。

**OnMailCommand** イベントは **OnEndOfHeaders** イベントよりも前にメッセージに遭遇するため、トランスポート エージェント B が最初にメッセージに適用されます。メッセージが **OnEndOfHeaders** イベントに到達すると、トランスポート エージェント A はトランスポート エージェント C よりも優先度が高い (整数値が小さい) ため、トランスポート エージェント A はトランスポート エージェント C よりも前に適用されます。

## 組み込みのトランスポート エージェント

Exchange 2013 には、スパム対策、トランスポート ルール、ジャーナリングなどの機能を提供する多くの組み込みトランスポート エージェントがあります。Exchange 2013 メールボックス サーバーおよびクライアント アクセス サーバーの組み込みトランスポート エージェントのほとんどは、トランスポート エージェントの管理コマンドレットによって表示されず、管理することもできません。表示と管理が可能な組み込みトランスポート エージェントは事実上すべて、メールボックス サーバーおよびエッジ トランスポート サーバー上のトランスポート サービスのものです。

メールボックス サーバーの組み込みトランスポート エージェントのうち、特に興味深いものを以下の表に示します。この表には、表示されない管理不能なトランスポート エージェントの多くは含まれていないことに注意してください。

### メールボックス サーバー上の興味深い組み込みトランスポート エージェント

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>エージェント名</th>
<th>管理可能</th>
<th>Priority</th>
<th>SMTP またはカテゴライザー イベント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>トランスポート ルール エージェント</p></td>
<td><p>はい</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>マルウェア エージェント</p></td>
<td><p>はい</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>テキスト メッセージング ルーティング エージェント</p></td>
<td><p>はい</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>テキスト メッセージング配信エージェント</p></td>
<td><p>はい</p></td>
<td><p>4</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>ジャーナル エージェント</p></td>
<td><p>いいえ</p></td>
<td><p>構成不可</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>ジャーナル レポート復号化エージェント</p></td>
<td><p>いいえ</p></td>
<td><p>構成不可</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS 復号化エージェント</p></td>
<td><p>いいえ</p></td>
<td><p>構成不可</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>RMS 暗号化エージェント</p></td>
<td><p>いいえ</p></td>
<td><p>構成不可</p></td>
<td><p><strong>OnSubmittedMessage</strong>、<strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS プロトコル復号化エージェント</p></td>
<td><p>いいえ</p></td>
<td><p>構成不可</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


エッジ トランスポート サーバーでは、ほとんどの組み込みトランスポート エージェントは、トランスポート エージェント管理コマンドレットまたはその他の機能固有のコマンドレットによって表示および管理することができます。

エッジ トランスポート サーバーの組み込みトランスポート エージェントのうち、特に興味深いものを以下の表に示します。この表には、表示されない管理不能なトランスポート エージェントが含まれていないことに注意してください。

### エッジ トランスポート サーバー上の興味深い組み込みトランスポート エージェント

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>エージェント名</th>
<th>管理可能</th>
<th>Priority</th>
<th>SMTP またはカテゴライザー イベント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>接続フィルター エージェント</p></td>
<td><p>はい</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>、<strong>OnMailCommand</strong>、<strong>OnRcptComand</strong>、<strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>アドレス書き換え受信エージェント</p></td>
<td><p>はい</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong>、<strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>エッジ ルール エージェント</p></td>
<td><p>はい</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>コンテンツ フィルター エージェント*</p></td>
<td><p>はい</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>送信者 ID エージェント*</p></td>
<td><p>はい</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>送信者フィルター エージェント*</p></td>
<td><p>はい</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong>、<strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>受信者フィルター エージェント</p></td>
<td><p>はい</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>プロトコル分析エージェント*</p></td>
<td><p>はい</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>、<strong>OnEndOfHeaders</strong>、<strong>OnEndOfData</strong>、<strong>OnReject</strong>、<strong>OnRsetCommand</strong>、<strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>添付ファイル フィルター エージェント</p></td>
<td><p>はい</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>アドレス書き換え送信エージェント</p></td>
<td><p>はい</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong>、<strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* これらのスパム対策エージェントをメールボックス サーバーにインストールして構成することもできます。詳細については、「[メールボックス サーバーのスパム対策機能を有効にする](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)」を参照してください。

ページのトップへ

## トランスポート エージェントのトラブルシューティング

トランスポート エージェントに関する問題をトラブルシューティングするために、以下の機能を使用することができます。

  - **Get-TransportPipeline**   このコマンドレットは、Exchange サーバーでメッセージに遭遇する SMTP イベントおよび対応するトランスポート エージェントを示します。詳細については、「[トランスポート パイプライン内のトランスポート エージェントを表示する](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md)」を参照してください。

  - **パイプライン トレース**   パイプライン トレースは、各トランスポート エージェントに遭遇する前後に、メッセージの正確なスナップショットを作成します。この機能により、予期しない結果の原因となるトランスポート エージェントを見つけることができます。詳細については、「[パイプライン トレース](pipeline-tracing-exchange-2013-help.md)」を参照してください。

ページのトップへ

