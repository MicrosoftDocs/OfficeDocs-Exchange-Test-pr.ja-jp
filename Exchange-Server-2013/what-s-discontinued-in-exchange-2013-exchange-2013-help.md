---
title: 'Exchange 2013 で廃止された機能: Exchange 2013 Help'
TOCTitle: Exchange 2013 で廃止された機能
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 49115901
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 で廃止された機能

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

ここでは、Microsoft Exchange Server 2013 で削除、サポートが中止、または置き換えられたコンポーネントまたは機能について説明します。


> [!NOTE]  
> 次のトピックも役立つ内容です。 
> <UL>
> <LI>
> <P><A href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013 の新機能</A>Exchange Server 2013 での新しい特徴と機能についての情報。</P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=267479">Exchange 2013の開発者ロードマップ</A>Exchange 2013 で廃止された API と開発機能に関する情報については、「Exchange から削除された開発テクノロジ」セクションを参照してください。</P></LI></UL>



## Exchange 2010 から Exchange 2013 で廃止された機能

ここでは、Exchange 2013 で利用できなくなる Exchange Server 2010 機能を示します。

## アーキテクチャ


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ハブ トランスポート サーバーの役割</p></td>
<td><p>ハブ トランスポート サーバーの役割は、メールボックスおよびクライアント アクセス サーバーの役割で実行するトランスポート サービスに置き換えられました。メールボックス サーバーの役割には、Microsoft Exchange Transport、Microsoft Exchange Mailbox Transport Delivery、Microsoft Exchange Mailbox Transport Submission サービスなどがあります。クライアント アクセス サーバーの役割には、Microsoft Exchange Frontend Transport サービスなどがあります。詳細については、「<a href="mail-flow-exchange-2013-help.md">メール フロー</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>ユニファイド メッセージング サーバーの役割</p></td>
<td><p>ユニファイド メッセージング サーバーの役割は、メールボックスおよびクライアント アクセス サーバーの役割で実行するユニファイド メッセージング サービスに置き換えられました。メールボックス サーバーの役割には Microsoft Exchange ユニファイド メッセージング サービスなどがあり、クライアント アクセス サーバーの役割には Microsoft Exchange ユニファイド メッセージング コール ルーター サービスなどがあります。詳細については、「<a href="voice-architecture-changes-exchange-2013-help.md">ボイスのアーキテクチャの変更</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


## 管理インターフェイス


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 管理コンソールおよび Exchange コントロール パネル</p></td>
<td><p>Exchange 管理コンソールおよび Exchange コントロール パネルは、Exchange 管理センター (EAC) に置き換えられました。EAC では、同じ仮想ディレクトリ (/ecp) を Exchange コントロール パネルとして使用します。詳細については、「<a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013 の Exchange 管理者センター</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


## クライアント アクセス


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2003 はサポート対象外です</p></td>
<td><p>Microsoft Outlook を Exchange 2013 に接続するには、自動検出サービスの使用が必要になります。ただし、Microsoft Outlook 2003 は、自動検出サービスの使用をサポートしません。</p></td>
</tr>
<tr class="even">
<td><p>Outlook クライアントの RPC/TCP アクセス</p></td>
<td><p>Exchange 2013 では、Microsoft Outlook クライアントは Outlook Anywhere (RPC/HTTP)、または Exchange 2013 Service Pack 1 および Outlook 2013 Service Pack 1 以降では MAPI over HTTP を使用して接続します。組織内に Outlook クライアントがある場合は、Outlook Anywhere および MAPI over HTTP またはそのいずれかを使用する必要があります。詳細については、「<a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a>」および「<a href="mapi-over-http-exchange-2013-help.md">MAPI over HTTP</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


## Outlook Web App と Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>スペル チェック</p></td>
<td><p>Outlook Web App にはスペル チェック サービスが組み込まれなくなりました。代わりに、Web ブラウザーのスペル チェック機能を使用します。</p></td>
</tr>
<tr class="even">
<td><p>カスタマイズ可能なフィルター</p></td>
<td><p>Outlook Web App ではフィルター ビューのカスタマイズが使用できなくなりました。また [お気に入り] へのフィルター ビューの保存がサポートされなくなりました。カスタマイズ可能なフィルターは、すべてのメッセージ、未読メッセージ、ユーザーに送信されたメッセージ、またはフラグが設定されたメッセージの表示に使用できる固定フィルターで置き換えられました。</p></td>
</tr>
<tr class="odd">
<td><p>メッセージ フラグ</p></td>
<td><p>メッセージ フラグにカスタム日付を設定する機能は、Outlook Web App では利用できません。カスタム日付は Outlook で設定できます。</p></td>
</tr>
<tr class="even">
<td><p>チャット連絡先一覧</p>
<p></p></td>
<td><p>Outlook Web App for Exchange 2010 のフォルダー一覧に表示されていたチャット連絡先一覧は使用できなくなりました。</p></td>
</tr>
<tr class="odd">
<td><p>検索フォルダー</p></td>
<td><p>ユーザーが検索フォルダーを使用する機能は現在、Outlook Web App では使用できません。</p></td>
</tr>
</tbody>
</table>


## メール フロー


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リンクされたコネクタ</p></td>
<td><p>送信コネクタを受信コネクタにリンクする機能は、削除されました。具体的には、<em>LinkedReceiveConnector</em> パラメーターが <a href="https://technet.microsoft.com/ja-jp/library/aa998936(v=exchg.150)">New-SendConnector</a> および <a href="https://technet.microsoft.com/ja-jp/library/aa998294(v=exchg.150)">Set-SendConnector</a> から削除されました。</p></td>
</tr>
</tbody>
</table>


## スパム対策とマルウェア対策


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EMC でのスパム対策エージェント管理</p></td>
<td><p>Exchange 2010 では、ハブ トランスポート サーバー上でスパム対策エージェントを有効にした場合、Exchange 管理コンソール (EMC) でスパム対策エージェントを管理できました。Exchange 2013 では、メールボックス サーバーでスパム対策エージェントを有効にする場合、EAC でエージェントを管理できません。シェルを使用する必要があります。メールボックス サーバーでスパム対策エージェントを有効にする方法の詳細については、「<a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">メールボックス サーバーのスパム対策機能を有効にする</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>ハブ トランスポート サーバー上の接続フィルター エージェント</p></td>
<td><p>Exchange 2010 では、ハブ トランスポート サーバー上でスパム対策エージェントを有効にした場合、使用できない唯一のスパム対策エージェントが添付ファイル フィルター エージェントでした。Exchange 2013 では、メールボックス サーバーでスパム対策エージェントを有効にする場合、添付ファイル フィルター エージェントと接続フィルター エージェントが使用できません。接続フィルター エージェントには IP 許可一覧と IP 禁止一覧機能があります。メールボックス サーバーでスパム対策エージェントを有効にする方法の詳細については、「<a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">メールボックス サーバーのスパム対策機能を有効にする</a>」を参照してください。</p>

> [!NOTE]  
> Exchange 2013 クライアント アクセス サーバー上ではスパム対策エージェントを有効にすることができません。そのため、エッジ トランスポート サーバーを境界ネットワークにインストールすることが接続フィルター エージェントを取得する唯一の方法です。詳細については、「<A href="edge-transport-servers-exchange-2013-help.md">エッジ トランスポート サーバー</A>」を参照してください。


</td>
</tr>
</tbody>
</table>


## メッセージングのポリシーと準拠


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理フォルダー</p></td>
<td><p>Exchange 2010 では、メッセージング保持管理 (MRM) 用に管理フォルダーを使用します。Exchange 2013 では、管理フォルダーはサポートされません。MRM のアイテム保持ポリシーを使用する必要があります。</p>

> [!NOTE]  
> 管理フォルダーに関連するコマンドレットはまだ利用可能です。管理フォルダー、管理コンテンツの設定、管理フォルダー メールボックス ポリシーを作成し、管理フォルダー メールボックス ポリシーをユーザーに適用できますが、MRM アシスタントは、管理フォルダー メールボックス ポリシーが適用されているメールボックスの処理をスキップします。


</td>
</tr>
<tr class="even">
<td><p>管理フォルダーの移植ウィザード</p></td>
<td><p>Exchange 2010 では、管理フォルダーの移植ウィザードを使用して、管理フォルダーおよび管理コンテンツ設定に基づいて保持タグを作成します。Exchange 2013 では、Exchange 管理センターにこの機能が含まれていません。<strong>New-RetentionPolicyTag</strong> コマンドレットを <em>ManagedFolderToUpgrade</em> パラメーターとともに使用して、管理フォルダーに基づいて保持タグを作成します。</p></td>
</tr>
</tbody>
</table>


## ユニファイド メッセージングおよびボイス メール


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自動音声認識 (ASR) を使用したディレクトリ参照</p></td>
<td><p>Exchange 2010 では、Outlook Voice Access のユーザーは 自動音声認識 (ASR) を利用した音声入力を使用して、ディレクトリにリストされたユーザーを検索することができます。Outlook Voice Access で音声入力を使用して、メニュー、メッセージおよびその他のオプションへ移動することもできます。しかし、Outlook Voice Access のユーザーが音声入力を使用できる場合でも、PIN を入力したりユーザーのオプション間を移動するには電話のキー パッドを使用する必要があります。</p>
<p>Exchange 2013 では、認証済みおよび認証されていない Outlook Voice Access のユーザーはどの言語でも、音声入力または ASR を使用してディレクトリのユーザーの検索をすることはできません。ただし自動応答を呼び出した発信者は、複数の言語で音声入力を使用して自動応答メニュー間を移動したり、ディレクトリのユーザーを検索したりすることができます。</p></td>
</tr>
</tbody>
</table>


## ツール


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange ベスト プラクティス アナライザー</p></td>
<td><p>Exchange 2010 では、Exchange ベスト プラクティス アナライザーが Exchange 展開を検査して、構成が Microsoft ベスト プラクティスに合っているかどうかを確認しました。Exchange 2013 では、Exchange ベスト プラクティス アナライザーが <a href="https://go.microsoft.com/fwlink/p/?linkid=391077">Exchange Server 2013 用 Office 365 ベスト プラクティス アナライザー</a>に置き換えられています。</p></td>
</tr>
<tr class="even">
<td><p>メール フロー トラブルシューティング ツール</p></td>
<td><p>Exchange 2010 では、メール フロー トラブルシューティングが一般的なメール フローの問題のトラブルシューティングを支援しました。Exchange 2013 では、メール フロー トラブルシューティング ツールが廃止されました。Exchange 2013 では、EAC のメッセージング トラッキング機能を使用できます。詳細については、「<a href="track-messages-with-delivery-reports-exchange-2013-help.md">配信レポートによるメッセージの追跡</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>パフォーマンス モニター</p></td>
<td><p>Exchange 2010 では、パフォーマンス モニターが Exchange ツールボックスに含まれており、メッセージング システムのパフォーマンスに関する情報を収集できました。一般に、パフォーマンス モニターはパフォーマンスに関する問題のトラブルシューティング中に主要なパラメーターを表示するときに使用されます。Exchange 2013 では、パフォーマンス モニターがツールボックスから廃止されました。パフォーマンス モニターは Windows Server 2008 の <strong>[管理ツール]</strong> の下にまだ見つけることができます。</p></td>
</tr>
<tr class="even">
<td><p>パフォーマンス トラブルシューティング ツール</p></td>
<td><p>Exchange 2013 では、パフォーマンスのトラブルシューティング ツール が廃止されました。</p></td>
</tr>
<tr class="odd">
<td><p>ルーティング ログ ビューアー</p></td>
<td><p>Exchange 2013 では、ルーティング ログ ビューアーが廃止されました。</p></td>
</tr>
</tbody>
</table>


## メールボックス データベース コピー


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>メールボックス データベース コピーの更新ウィザード</p></li>
</ul></td>
<td><p>コンテンツ インデックス カタログのシード処理は、レプリケーション ネットワーク経由では実行できなくなりました。この処理は、MAPI ネットワーク経由でのみ実行できます。これは、Update-MailboxDatabaseCopy コマンドレットに <code>-Network</code> パラメーターを使用する場合にも当てはまります。</p></td>
</tr>
</tbody>
</table>


## Exchange 2007 から Exchange 2013 で廃止された機能

ここでは、Exchange 2013 で利用できなくなる Exchange Server 2007 機能を示します。

## API および開発


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange WebDAV</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=167197">Exchange Web サービス</a> または <a href="https://go.microsoft.com/fwlink/p/?linkid=157179">EWS マネージ API</a> を使用します。あるいは、WebDAV を使用するアプリケーションによって管理されるメールボックスの Exchange 2007 サーバーを管理できます。詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=169474">WebDAV からの移行</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


## アーキテクチャ


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ストレージ グループ</p></td>
<td><p>Exchange 2013 では、ストレージ グループの作成を使用しなくなった代わりに、単にメールボックス データベースを管理します。詳細については、「<a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Exchange 2013 のメールボックス データベースの管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>Extensible Storage Engine (ESE) ストリーミング バックアップ API</p></td>
<td><p>Exchange 2013 がサポートしているのは、Exchange 対応のボリューム シャドウ コピー サービス (VSS) ベースのバックアップのみです。Exchange 2013 には、データのバックアップと復元ができる Windows サーバー バックアップ用プラグインが含まれています。詳細については、「<a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">バックアップ、復元、および障害回復</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>ユーザー データグラム プロトコル (UDP) 通知</p></td>
<td><p>ユーザー データグラム プロトコル (UDP) 通知のサポートは、Exchange 2013 から除外されます。これは、Outlook 2003 クライアントが Exchange 2013 サーバー上のメールボックスに接続するときのユーザー エクスペリエンスに影響します。この問題の詳細については、Microsoft サポート技術情報の資料 2009942「<a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=2009942">Exchange Server 2010 のユーザーがオンライン モードで Outlook 2003 を使用する場合にフォルダーの更新に時間がかかる</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


## 高可用性


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>クラスター連続レプリケーション (CCR)</p></td>
<td><p>Exchange 2013 は、データベース可用性グループ (DAG) およびメールボックス データベース コピーを使用します。詳細については、「<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性とサイトの復元</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>ローカル連続レプリケーション (LCR)</p></td>
<td><p>Exchange 2013 は、DAG およびメールボックス データベース コピーを使用します。詳細については、「<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性とサイトの復元</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>スタンバイ連続レプリケーション (SCR)</p></td>
<td><p>Exchange 2013 は、DAG およびメールボックス データベース コピーを使用します。詳細については、「<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性とサイトの復元</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>シングル コピー クラスター (SCC)</p></td>
<td><p>Exchange 2013 は、DAG およびメールボックス データベース コピーを使用します。詳細については、「<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性とサイトの復元</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013 は、Setup /m:recoverServer を使用します。詳細については、「<a href="recover-an-exchange-server-exchange-2013-help.md">Exchange Server を回復する</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>クラスター化メールボックス サーバー</p></td>
<td><p>Exchange 2013 は、DAG およびメールボックス データベース コピーを使用します。詳細については、「<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性とサイトの復元</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


## クライアント アクセス


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>POP3 と IMAP4 ユーザーに対する統合 Windows 認証 (NTLM) を使用したクライアント認証</p></td>
<td><p>NTLM は Exchange 2013 の POP3 または IMAP4 クライアントの接続ではサポートされません。NTLM を使用した POP3 または IMAP4 クライアント プログラムからの接続は失敗します。Exchange 2013 の RTM バージョンを実行している場合、推奨される NTLM の代替方法は、SSL でのテキスト形式の認証を使用することです。</p>
<p>Exchange 2013 を使用して NTLM を使用するには、Exchange 2013 組織内に Exchange 2007 サーバーを残す必要があります。</p></td>
</tr>
</tbody>
</table>


## Outlook Web App と Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ドキュメントへのアクセス</p></td>
<td><p>Outlook Web App は、Microsoft SharePoint ドキュメント ライブラリと Windows ファイル共有にアクセスするために使用することはできません。</p></td>
</tr>
<tr class="even">
<td><p>メッセージ フラグ</p></td>
<td><p>Outlook Web App 2013 では、ユーザー設定の日付をメッセージ フラグに設定する機能はありません。ユーザー設定の日付は Outlook を使用して設定できます。</p></td>
</tr>
<tr class="odd">
<td><p>スペル チェック</p></td>
<td><p>Outlook Web App では、Web ブラウザーのスペル チェック機能を使用します。</p></td>
</tr>
<tr class="even">
<td><p>検索フォルダー</p></td>
<td><p>ユーザーが検索フォルダーを使用する機能は現在、Outlook Web App では使用できません。</p></td>
</tr>
<tr class="odd">
<td><p>最大キャッシュ ビュー</p></td>
<td><p>Exchange 2007 では、Outlook クライアントでデータベースごとにキャッシュされるビューの最大数を変更する (msExchMaxCachedViews) パラメーターがサポートされていました。Exchange 2013 では、このパラメーターが使用されなくなりました。</p></td>
</tr>
</tbody>
</table>


## 受信者関連の機能


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Export-Mailbox</strong> および <strong>Import-Mailbox</strong> コマンドレット</p></td>
<td><p>Exchange 2013 では、エクスポート要求またはインポート要求を使用します。詳細については、「<a href="mailbox-import-and-export-requests-exchange-2013-help.md">メールボックスのインポート要求とエクスポート要求</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>Move-Mailbox</strong> コマンドレット セット</p></td>
<td><p>Exchange 2013 では、メールボックスを移動するには、移動要求を使用します。詳細については、「<a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 でのメールボックスの移動</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>Exchange 2013 では、<a href="https://technet.microsoft.com/ja-jp/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a> を使用します。</p></td>
</tr>
</tbody>
</table>


## メッセージングのポリシーと準拠


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理フォルダー</p></td>
<td><p>Exchange 2007 では、メッセージング保持管理 (MRM) に管理フォルダーを使用します。Exchange 2013 では、管理フォルダーはサポートされません。MRM のアイテム保持ポリシーを使用する必要があります。</p>

> [!NOTE]  
> 管理フォルダーに関連するコマンドレットはまだ利用可能です。管理フォルダー、管理コンテンツの設定、管理フォルダー メールボックス ポリシーを作成し、管理フォルダー メールボックス ポリシーをユーザーに適用できますが、MRM アシスタントは、管理フォルダー メールボックス ポリシーが適用されているメールボックスの処理をスキップします。


</td>
</tr>
</tbody>
</table>


## ユニファイド メッセージングおよびボイス メール


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>コメントとリスク軽減</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook Voice Access の 自動音声認識 (ASR) を使用したディレクトリ ルックアップ</p></td>
<td><p>Exchange 2007 では、Outlook Voice Access のユーザーは 自動音声認識 (ASR) (英語 (米国)) を利用した音声入力を使用して、ディレクトリにリストされたユーザーを検索できます。Outlook Voice Access で音声入力を使用して、メニュー、メッセージおよびその他のオプションへ移動することもできます。しかし、Outlook Voice Access のユーザーが音声入力を使用できる場合でも、PIN を入力したりユーザーのオプション間を移動するには電話のキー パッドを使用する必要があります。</p>
<p>Exchange 2013 では、認証済みおよび認証されていない Outlook Voice Access のユーザーはどの言語でも、音声入力または ASR を使用してディレクトリのユーザーの検索をすることはできません。ただし自動応答を呼び出した発信者は、複数の言語で音声入力を使用して自動応答メニュー間を移動したり、ディレクトリのユーザーを検索したりすることができます。</p></td>
</tr>
</tbody>
</table>

