---
title: 'Exchange Server 2013 サービスの概要: Exchange 2013 Help'
TOCTitle: Exchange Server 2013 サービスの概要
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479250
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 サービスの概要

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-10-20_

Exchange Server 2013 のインストール時に、Microsoft Windows の新しいサービスをインストールする一連のタスクがセットアップ プログラムによって実行されます。サービスは、サーバーの起動時に Windows のサービス コントロール マネージャーによって起動されるバックグラウンド プロセスです。サービスは、管理操作なしに独立して機能するよう設計された実行可能ファイルです。サービスは、グラフィカル ユーザー インターフェイス (GUI) モードまたはコンソール モードを使用して実行できます。

Exchange の以前のすべてのバージョンには、サービスとして実装されたコンポーネントが含まれていました。それぞれの Exchange サーバーの役割には、サーバーの役割の一部を成すサービスや、サーバーの役割の機能を実行するために必要なサービスが含まれています。一部のサービスは特定の機能を使用する場合にのみアクティブになることに注意してください。

このトピックの各セクションでは、Exchange 2013 によってメールボックス サーバー、クライアント アクセス サーバー、エッジ トランスポート サーバーにインストールされる各種サービスについて説明します。省略可とラベル付けされているサービスについては、そのサービスにより提供される機能は組織に必要ないと判断する場合、無効化することができます。

## Exchange 2013 メールボックス サーバーの Exchange サービス

次の表では、メールボックス サーバーにインストールされる Exchange サービスについて説明します。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>サービス名</th>
<th>サービスの短縮名</th>
<th>説明および依存関係</th>
<th>既定の開始方法</th>
<th>セキュリティ コンテキスト</th>
<th>依存関係</th>
<th>必須または省略可</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Active Directory トポロジ情報を Exchange サービスに提供します。このサービスが停止すると、大部分の Exchange サービスは開始できません。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Net.TCP ポート共有サービス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Anti-spam Update</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Exchange SmartScreen スパム定義の更新を提供します。</p>

> [!NOTE]
> 2016 年 11 月 1 日に Microsoft は、Exchange と Outlook の SmartScreen フィルターのスパム定義の更新を停止しました。既存の SmartScreen スパム定義はそのままですが、その効果は時間とともに低下する可能性があります。詳しくは、「<A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook と Exchange での SmartScreen サポートの廃止</A>」をご覧ください。


</td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange DAG Management</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>データベース可用性グループ (DAG) のメールボックス サーバーに、ストレージとデータベース レイアウト管理機能を提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p>
<p>Net.TCP ポート共有サービス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 診断</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Exchange サーバーの状態を監視するエージェントを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>なし</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>Secure LDAP チャネル経由で、構成データと受信者データをメールボックス サーバーとサブスクライブしているエッジ トランスポート サーバーの UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) の間でレプリケートします。</p>
<p>サブスクライブしているエッジ トランスポート サーバーがない場合は、このサービスを無効化することができます。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Exchange サーバー上の主要なコンポーネントの状態を監視する可用性管理の一部</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Windows イベント ログ</p>
<p>Windows Management Instrumentation</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4 バックエンド</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>クライアント アクセス サーバー上の IMAP4 サービスからのプロキシされたクライアント接続を受信します。既定ではこのサービスは実行されていないため、このサービスが開始されるまでは、IMAP4 クライアントは Exchange サーバーに接続することができません。</p>
<p>IMAP4 クライアントがない場合は、このサービスを無効にすることができます。</p></td>
<td><p>手動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Information Store</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>サーバー上のメールボックス データベースを管理します。このサービスが停止している場合は、サーバー上のメールボックス データベースは使用できません。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p>
<p>リモート プロシージャ コール (RPC)</p>
<p>サーバー</p>
<p>Windows イベント ログ</p>
<p>ワークステーション</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange メールボックス アシスタント</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>サーバー上のメールボックス データベースのメールボックスをバックグラウンドで処理します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange メールボックス レプリケーション</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>メールボックスの移動と移動要求を処理します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p>
<p>Net.TCP ポート共有サービス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange メールボックス トランスポート配信</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>Microsoft Exchange トランスポート サービス (ローカル サーバー上またはリモート メールボックス サーバー上) から SMTP メッセージを受信し、RPC を使ってそれをローカルのメールボックス データベースに配信します。</p></td>
<td><p>自動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange メールボックス トランスポート送信</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>ローカルのメールボックス データベースから RPC メッセージを受信して、それを SMTP 経由でMicrosoft Exchange トランスポート サービス (ローカル サーバー上またはリモート メールボックス サーバー上) に送ります。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange POP3 バックエンド</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>クライアント アクセス サーバー上の POP3 サービスからのプロキシされたクライアント接続を受信します。既定ではこのサービスは実行されていないため、このサービスが開始されるまでは、POP3 クライアントは Exchange サーバーに接続することができません。</p></td>
<td><p>手動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange レプリケーション サービス</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>データベース可用性グループ (DAG) のメールボックス データベースにレプリケーション機能を提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange RPC クライアント アクセス</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>Exchange のクライアント RPC 接続を管理します。</p></td>
<td><p>自動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Search</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>メールボックスのコンテンツのインデックスを提供します。これにより、コンテンツの検索のパフォーマンスが向上します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Search Host Controller</p></td>
<td><p>HostControllerService</p></td>
<td><p>ローカル Exchange サーバー上でアプリケーションの展開と管理を行うサービスを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>HTTP サービス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Windows Server バックアップ用の Microsoft Exchange Server 拡張機能</p></td>
<td><p>WSBExchange</p></td>
<td><p>Exchange サーバーのデータのバックアップと復元を行うため、Windows Server バックアップを有効にします。</p></td>
<td><p>手動</p></td>
<td><p>ローカル システム</p></td>
<td><p>なし</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>独自のサービスを持たない Exchange コンポーネントのサービス ホストを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Throttling</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>ユーザー操作の速度 (以前のユーザー調整) を制限するユーザー ワークロード管理を提供します。</p></td>
<td><p>自動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Transport</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>SMTP サーバーおよびトランスポート スタックを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p>
<p>Microsoft Filtering Management サービス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Transport Log Search</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>トランスポート ログ ファイルのリモート検索機能を提供します (例: メッセージ追跡)。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange ユニファイド メッセージング</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>ユニファイド メッセージング (UM) 機能を提供します。これにより、ボイス メッセージおよび FAX メッセージが Exchange に格納され、ユーザーが電話で電子メール、ボイス メール、予定表、連絡先、または自動応答にアクセスできるようになります。このサービスが停止している場合、ユニファイド メッセージングを使用することはできません。</p>
<p>UM を使用しない場合は、このサービスを無効にすることができます。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>CNG キー分離</p>
<p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 クライアント アクセス サーバーの Exchange サービス

次の表では、クライアント アクセス サーバーにインストールされる Exchange サービスについて説明します。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>サービス名</th>
<th>サービスの短縮名</th>
<th>説明および依存関係</th>
<th>既定の開始方法</th>
<th>セキュリティ コンテキスト</th>
<th>依存関係</th>
<th>必須または省略可</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Active Directory トポロジ情報を Exchange サービスに提供します。このサービスが停止すると、大部分の Exchange サービスは開始できません。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Net.TCP ポート共有サービス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 診断</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Exchange サーバーの状態を監視するエージェントを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>なし</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange フロントエンド トランスポート</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>外部ホストからメールボックス サーバー上の Microsoft Exchange トランスポート サービスへの SMTP 接続をプロキシします。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Exchange サーバー上の主要なコンポーネントの状態を監視する可用性管理の一部</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Windows イベント ログ</p>
<p>Windows Management Instrumentation</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>メールボックス サーバー上の IMAP4 サービスへの IMAP4 クライアント接続をプロキシします。既定ではこのサービスは実行されていないため、このサービスが開始されるまでは、IMAP4 クライアントは Exchange サーバーに接続することができません。</p>
<p>IMAP4 クライアントがない場合は、このサービスを無効にすることができます。</p></td>
<td><p>手動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>メールボックス サーバー上の IMAP4 サービスへの POP3 クライアント接続をプロキシします。既定ではこのサービスは実行されていないため、このサービスが開始されるまでは、POP3 クライアントは Exchange サーバーに接続することができません。</p></td>
<td><p>手動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Search Host Controller</p></td>
<td><p>HostControllerService</p></td>
<td><p>ローカル Exchange サーバー上でアプリケーションの展開と管理を行うサービスを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>HTTP サービス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>独自のサービスを持たない Exchange コンポーネントのサービス ホストを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange ユニファイド メッセージング呼び出しルーター</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>メールボックス サーバー上のユニファイド メッセージング サービスに、UM クライアント接続をリダイレクトします。</p>
<p>UM を使用しない場合は、このサービスを無効にすることができます。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>CNG キー分離</p>
<p>Microsoft ExchangeActive Directory トポロジ</p></td>
<td><p>省略可</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 エッジ トランスポート サーバーの Exchange サービス

次の表では、エッジ トランスポート サーバーにインストールされる Exchange サービスについて説明します。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>サービス名</th>
<th>サービスの短縮名</th>
<th>説明</th>
<th>既定の開始方法</th>
<th>セキュリティ コンテキスト</th>
<th>依存関係</th>
<th>必須または省略可</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>エッジ トランスポート サーバーに構成データと受信者データを格納します。このサービスは、Exchange のセットアップ プログラムによって自動的に作成される UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) の名前付きインスタンスを表します。</p></td>
<td><p>自動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>COM+ Event System</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Anti-spam Update</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Exchange SmartScreen スパム定義の更新を提供します。</p>

> [!NOTE]
> 2016 年 11 月 1 日に Microsoft は、Exchange と Outlook の SmartScreen フィルターのスパム定義の更新を停止しました。既存の SmartScreen スパム定義はそのままですが、その効果は時間とともに低下する可能性があります。詳しくは、「<A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook と Exchange での SmartScreen サポートの廃止</A>」をご覧ください。


</td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>省略可</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Credential Service</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) 内の資格情報の変更を監視し、変更をエッジ トランスポート サーバーにインストールします。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 診断</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Exchange サーバーの状態を監視するエージェントを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>なし</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Health Manager</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Exchange サーバー上の主要なコンポーネントの状態を監視する可用性管理の一部</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Windows イベント ログ</p>
<p>Windows Management Instrumentation</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Service Host</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>独自のサービスを持たない Exchange コンポーネントのサービス ホストを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Transport</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>SMTP サーバーおよびトランスポート スタックを提供します。</p></td>
<td><p>自動</p></td>
<td><p>ネットワーク サービス</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Transport Log Search</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>トランスポート ログ ファイルのリモート検索機能を提供します (例: メッセージ追跡)。</p></td>
<td><p>自動</p></td>
<td><p>ローカル システム</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>省略可</p></td>
</tr>
</tbody>
</table>

