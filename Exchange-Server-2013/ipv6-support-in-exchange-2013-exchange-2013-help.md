---
title: 'Exchange 2013 での IPv6 サポート: Exchange 2013 Help'
TOCTitle: Exchange 2013 での IPv6 サポート
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 48269353
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 での IPv6 サポート

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

インターネット プロトコル Version 6 (IPv6) は、インターネット プロトコル (IP) の最新バージョンです。IPv6 は、以前のバージョンの IP である IPv4 の多くの短所を取り除くことを目的としています。

Microsoft Exchange Server 2013 で、IPv6 がサポートされるのは、IPv4 もインストールされ、有効になっている場合のみです。Exchange 2013 がこの構成で展開されており、ネットワークで IPv4 と IPv6 がサポートされている場合は、すべての Exchange サーバーが、IPv6 アドレスを使用するデバイス、サーバー、およびクライアントとの間でデータを送受信できます。

ここでは、Exchange 2013 の IPv6 のアドレス指定について説明します。IPv6 の詳細については、[IPv6](https://go.microsoft.com/fwlink/p/?linkid=92582)を参照してください (このサイトは英語の場合があります)。

**目次**

Exchange 2013 コンポーネントの IPv6 サポート

オペレーティング システムでプロトコルを有効または無効にする

IPv6 アドレスの基本

## Exchange 2013 コンポーネントの IPv6 サポート

次の表では、IPv6 から影響を受ける Exchange 2013 のコンポーネントについて説明します。

### Exchange 2013 の機能と IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>IPv6 サポート</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>接続フィルター エージェントの IP 許可一覧と IP 禁止一覧</p></td>
<td><p>はい</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>接続フィルター エージェントの IP 許可一覧プロバイダーと IP 禁止一覧プロバイダー</p></td>
<td><p>いいえ</p></td>
<td><p>現在、IPv6 アドレスを検索するための業界標準プロトコルとして、広く受け入れられているものはありません。ほとんどの IP 禁止一覧プロバイダーは、IPv6 アドレスをサポートしていません。受信コネクタで不明 IPv6 アドレスからの匿名接続を許可すると、スパムの発信者が IP 禁止一覧プロバイダーをバイパスし、組織にスパムを送り込むことに成功する危険性が高くなります。</p></td>
</tr>
<tr class="odd">
<td><p>プロトコル分析エージェントにおける送信者評価</p></td>
<td><p>いいえ</p></td>
<td><p>プロトコル分析エージェントは、IPv6 送信者から発信されたメッセージの送信者評価レベル (SRL) を計算しません。送信者評価の詳細については、「<a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">送信者評価とプロトコル分析エージェント</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>Sender ID</p></td>
<td><p>はい</p></td>
<td><p>詳細については、「<a href="sender-id-exchange-2013-help.md">送信者 ID</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>受信コネクタ</p></td>
<td><p>はい</p></td>
<td><p>IPv6 アドレスは、次のコンポーネントで使用できます。</p>
<ul>
<li><p>ローカル IP アドレスのバインド</p></li>
<li><p>リモート IP アドレス</p></li>
<li><p>IP アドレスの範囲</p></li>
</ul>
<p>不明な IPv6 アドレスからの匿名接続を受け付けないように受信コネクタを構成することを強くお勧めします。IPv6 アドレスを使用している送信者からのメールを受信する必要がある組織の場合、その送信者が使用している特定の IPv6 アドレスのみにリモート IP アドレスを制限する、専用の受信コネクタを作成してください。</p>
<p>詳細については、「<a href="receive-connectors-exchange-2013-help.md">受信コネクタ</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>送信コネクタ</p></td>
<td><p>はい</p></td>
<td><p>IPv6 アドレスは、次のコンポーネントで使用できます。</p>
<ul>
<li><p>スマート ホストの IP アドレス</p></li>
<li><p>エッジ トランスポート サーバー上に構成されている送信コネクタの <em>SourceIPAddress</em> パラメーター</p></li>
</ul>

> [!NOTE]
> <EM>SourceIPAddress</EM> パラメーターに IPv6 アドレスを指定する場合は、DNS の適切な AAAA レコードとメール交換 (MX) レコードが正しく構成されていることを確認してください。この構成は、リモート メッセージング サーバーが指定された IPv6 アドレスに対してどのような種類の逆引き参照テストを試みた場合でも、メッセージが確実に配信される助けになります。


<p>詳細については、「<a href="send-connectors-exchange-2013-help.md">送信コネクタ</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>受信メッセージの各種制限値</p></td>
<td><p>一部</p></td>
<td><p>受信コネクタに対して設定できる、<em>MaxInboundConnectionPercentagePerSource</em> パラメーター、<em>MaxInboundConnectionPerSource</em> パラメーター、<em>TarpitInterval</em> パラメーターなどの受信メッセージの各種制限値は、グローバル IPv6 アドレスにのみ適用されます。リンクローカル IPv6 アドレスとサイトローカル IPv6 アドレスは、指定された受信メッセージの各種制限値によって影響されません。</p></td>
</tr>
<tr class="even">
<td><p>ユニファイド メッセージング</p></td>
<td><p>はい</p></td>
<td><p>詳細については、「<a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">ユニファイド メッセージングでの IPv6 サポート</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>データベース可用性グループ (DAG) のメンバー</p></td>
<td><p>はい</p></td>
<td><p>静的 IPv6 アドレスは Windows Server およびクラスター サービスでサポートされています。ただし、静的 IPv6 アドレスを使用すると、ベスト プラクティスに従わないことになります。Exchange 2013 では、セットアップ中の静的 IPv6 アドレスの構成はサポートされません。</p>
<p>フェールオーバー クラスターでは、ISATAP (Intra-site Automatic Tunnel Addressing Protocol) がサポートされます。この場合、DNS への動的な登録を許可する IPv6 アドレスのみがサポートされます。クラスター内ではリンクローカル アドレスを使用できません。</p>
<p>DAG ネットワーク要件の詳細については、「<a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">高可用性とサイトの復元計画</a>」の「ネットワーク要件」セクションを参照してください。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## オペレーティング システムでプロトコルを有効または無効にする

Exchange 2013 サーバーは、IPv6 ネットワークを完全にサポートしています。したがって、IPv6 を使用していなくても、Exchange サーバーで IPv6 を無効にする必要はありません。

すべての Exchange 2013 サーバーに IPv4 がインストールされ、有効になっていることが、Exchange 2013 の IPv6 サポートの条件です。ただし、Exchange 2013 サーバーから IPv4 をアンインストールすることはできません。

Microsoft Windows での IPv6 サポートの詳細については、「[Pv6 for Microsoft Windows: よく寄せられる質問](https://go.microsoft.com/fwlink/p/?linkid=147465)」を参照してください (このサイトは英語の場合があります)。

ページのトップへ

## IPv6 アドレスの基本

IPv6 アドレスの長さは 128 ビットです。このアドレスは、コロン形式 16 進表記法を使用して表されます。コロン形式 16 進表記法は、16 ビットが 8 つある、4 桁の 16 進数をコロン (:) で区切ることにより、128 ビットのアドレスを表現します。コロン形式 16 進表記法の IPv6 アドレスの例は、2001:0DB8:0000:0000:02AA:00FF:C0A8:640A のようになります。

IPv6 アドレスは、以下の方法を使用して表現できます。

  - **先頭側にある 0 の省略**   IPv6 アドレスの中に 8 つある、4 桁の 16 進数それぞれで、先頭側にある 0 を省略できます。

  - **二重コロンによる要約**   2 つのコロン (::) を使用して、16 ビットすべてが 0 である、連続する 16 進数を表せます。すべてが 0 の 16 進数は、IPv6 アドレスの先頭、中間、または末尾に存在する場合があります。二重コロンによる要約は、1 つの IPv6 アドレス内で 1 回のみ使用できます。

  - **末尾のドット形式 10 進表記法**   IPv6 アドレス末尾の 32 ビットは、8 ビットの 10 進数をピリオド (.) で区切るドット形式 10 進表記法で表現してもかまいません。末尾のドット形式 10 進表記法は、IPv4 と互換性のあるアドレスでよく使用されます。

次の表に、IPv6 アドレスの表記法と、同じものを IPv6 アドレスの構文で表記した例を示します。

### IPv6 アドレスの表記法と構文

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>IPv6 アドレスの表記法</th>
<th>IPv6 アドレスの構文</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>完全な IPv6 アドレス</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>先頭側にある 0 の省略を使用した IPv6 アドレス</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>二重コロンによる要約を使用した IPv6 アドレス</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>末尾のドット形式 10 進表記法を使用した IPv6 アドレス</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


IPv6 アドレスは、以下の種類に分類されます。

  - **ユニキャスト アドレス**   パケットは 1 つのインターフェイスに配信されます。

  - **マルチキャスト アドレス**   パケットは複数のインターフェイスに配信されます。

  - **エニーキャスト アドレス**   パケットは複数のインターフェイスの中で最も近いインターフェイスに配信されます。インターフェイス間の距離は、ルーティング コストによって定義されます。

IPv6 ユニキャスト アドレスには以下のスコープを指定できます。

  - **リンクローカル**   IPv6 アドレスのスコープは、ローカル サブネットです。IPv6 リンクローカル アドレスは、自動プライベート IP アドレス指定 (APIPA) で使用される IPv4 リンクローカル アドレスと互換性があります。

  - **サイトローカル**   IPv6 アドレスのスコープは、ローカルの組織です。サイトローカル アドレスは、RFC 3879 で廃止され、RFC 4193 で定義された一意のローカル アドレスに置き換えられました。IPv6 サイトローカル アドレスと IPv6 一意ローカル アドレスは、IPv4 プライベート IP アドレスと互換性があります。

  - **グローバル**   IPv6 アドレスのスコープは、世界全体です。IPv6 グローバル アドレスは、IPv4 パブリック IP アドレスと互換性があります。

次の表は、IPv4 の要素と IPv6 の要素を比較したものです。

### IPv4 と IPv6 の要素の比較

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>プライベート IP アドレス</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00::/8</p></td>
</tr>
<tr class="even">
<td><p>リンクローカル アドレス</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80::/64</p></td>
</tr>
<tr class="odd">
<td><p>ループバック アドレス</p></td>
<td><p>127.0.0.1</p></td>
<td><p>::1</p></td>
</tr>
<tr class="even">
<td><p>不明アドレス</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>アドレス解決</p></td>
<td><p>アドレス解決プロトコル (ARP)</p></td>
<td><p>近隣探索 (ND)</p></td>
</tr>
<tr class="even">
<td><p>ドメイン ネーム システム (DNS) のホスト名解決</p></td>
<td><p>アドレス レコード (A レコード)</p></td>
<td><p>AAAA レコードまたは A6 レコード</p></td>
</tr>
</tbody>
</table>


IPv6 アドレス指定の詳細については、「[IPv6 アドレスの種類](https://go.microsoft.com/fwlink/p/?linkid=98357)」を参照してください (このサイトは英語の場合があります)。

## サポートされる IPv6 の入力形式

Exchange 2013 でサポートされる IPv6 アドレスの入力形式は以下の種類です。

  - 単一の IPv6 アドレス

  - IPv6 アドレスの範囲

  - サブネット マスクを指定した IPv6 アドレス

  - クラスレス ドメイン間ルーティング (CIDR) 表記法でサブネット マスクを指定した IPv6 アドレス

Exchange 2013 で使用できる IPv6 アドレスの入力形式の例を、次の表に示します。

### IPv6 アドレスの例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>IPv6 アドレスの例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>単一のアドレス</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>アドレスの範囲</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>サブネット マスクを指定したアドレス</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>CIDR 表記法でサブネット マスクを指定したアドレス</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A/64</p></td>
</tr>
</tbody>
</table>


Exchange 2013 では、以下の入力形式がサポートされます。

  - 先頭側にある 0 の省略

  - 二重コロンによる要約

  - 末尾のドット形式 10 進表記法

ページのトップへ

