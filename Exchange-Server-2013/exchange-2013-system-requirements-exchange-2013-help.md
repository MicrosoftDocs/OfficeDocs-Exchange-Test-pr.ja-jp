---
title: 'Exchange 2013 のシステム要件: Exchange 2013 Help'
TOCTitle: Exchange 2013 のシステム要件
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 48269253
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 のシステム要件

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange 2013 をインストールする前に確認しておく必要がある Exchange 2013 の要件について説明します。たとえば、ハードウェア、ネットワーク、およびオペレーティング システムの要件について説明します。

Microsoft Exchange Server 2013 をインストールする前に、このトピックで説明する内容に目を通し、お使いのネットワーク、ハードウェア、ソフトウェア、クライアント、およびその他の要素が Exchange 2013 の要件を満たすことを確認することをお勧めします。また、Exchange 2013 および Exchange の以前のバージョンでサポートされる共存シナリオを理解しておくようにしてください。

## サポートされている共存シナリオ

次の表に、Exchange 2013 と以前のバージョンの Exchange との間で共存がサポートされるシナリオを示します。

### Exchange 2013 と以前のバージョンの Exchange Server の共存

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange のバージョン</th>
<th>Exchange 組織の共存</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 および以前のバージョン</p></td>
<td><p>非サポート</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>最小で以下のバージョンの Exchange でサポートされます。</p>
<ul>
<li><p>1 Exchange 2007 Service Pack 3 (SP3) の更新プログラムのロールアップ 10 (エッジ トランスポート サーバーを含む、組織内のすべての Exchange 2007 サーバー)。</p></li>
<li><p>Exchange 2013 累積更新プログラム 2 (CU2) またはそれ以降 (組織内のすべての Exchange 2013 サーバー)。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>最小で以下のバージョンの Exchange でサポートされます。</p>
<ul>
<li><p>2 Exchange 2010 SP3 (エッジ トランスポート サーバーを含む、組織内のすべての Exchange 2010 サーバー)。</p></li>
<li><p>Exchange 2013 CU2 またはそれ以降 (組織内のすべての Exchange 2013 サーバー)。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2010 および Exchange 2007 が混在する組織</p></td>
<td><p>最小で以下のバージョンの Exchange でサポートされます。</p>
<ul>
<li><p>1 Exchange 2007 SP3 の更新プログラムのロールアップ 10 (エッジ トランスポート サーバーを含む、組織内のすべての Exchange 2007 サーバー)。</p></li>
<li><p>2 Exchange 2010 SP3 (エッジ トランスポート サーバーを含む、組織内のすべての Exchange 2010 サーバー)。</p></li>
<li><p>Exchange 2013 CU2 またはそれ以降 (組織内のすべての Exchange 2013 サーバー)。</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Exchange 2007 ハブ トランスポート サーバーと Exchange 2013 SP1 エッジ トランスポート サーバーの間に EdgeSync サブスクリプションを作成するには、Exchange 2007 SP3 更新プログラムのロールアップ 13 以降を Exchange 2007 ハブ トランスポート サーバーにインストールする必要があります。

2   Exchange 2010 ハブ トランスポート サーバーと Exchange 2013 SP1 エッジ トランスポート サーバーの間に EdgeSync サブスクリプションを作成するには、Exchange 2010 SP3 更新プログラムのロールアップ 5 以降を Exchange 2010 ハブ トランスポート サーバーにインストールする必要があります。

## サポートされているハイブリッド展開シナリオ

Exchange 2013 は、最新バージョンの Office 365 にアップグレードされた Office 365 テナントとのハイブリッド展開をサポートします。特定のハイブリッド展開の詳細については、「[ハイブリッド展開の前提条件](https://technet.microsoft.com/ja-jp/library/hh534377\(v=exchg.150\))」を参照してください。

## ネットワークとディレクトリ サーバー

次の表に、Exchange 2013 組織におけるネットワークおよびディレクトリ サーバーの要件の一覧を示します。

**Exchange 2013 のネットワークおよびディレクトリ サーバーの要件**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>スキーマ マスター</p></td>
<td><p>既定で、スキーマ マスターはフォレスト内に最初にインストールされた Active Directory ドメイン コントローラー上で動作します。スキーマ マスターは次のいずれかで実行する必要があります。</p>
<ul>
<li><p>Windows Server 2012 R2 Standard または Datacenter1</p></li>
<li><p>Windows Server 2012 Standard または Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard または Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 以降</p></li>
<li><p>Windows Server 2008 Standard または Enterprise (32 ビットまたは 64 ビット)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 以降</p></li>
<li><p>Windows Server 2003 Standard Edition、Service Pack 2 (SP2) 以降 (32 ビットまたは 64 ビット)</p></li>
<li><p>Windows Server 2003 Enterprise Edition、SP2 以降 (32 ビットまたは 64 ビット)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>グローバル カタログ サーバー</p></td>
<td><p>Exchange 2013 のインストールを計画している Active Directory サイトごとに、次のいずれかを実行する 1 つ以上のグローバル カタログ サーバーを用意する必要があります。</p>
<ul>
<li><p>Windows Server 2012 R2 Standard または Datacenter1</p></li>
<li><p>Windows Server 2012 Standard または Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard または Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 以降</p></li>
<li><p>Windows Server 2008 Standard または Enterprise (32 ビットまたは 64 ビット)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 以降</p></li>
<li><p>Windows Server 2003 Standard Edition、Service Pack 2 (SP2) 以降 (32 ビットまたは 64 ビット)</p></li>
<li><p>Windows Server 2003 Enterprise Edition、SP2 以降 (32 ビットまたは 64 ビット)</p></li>
</ul>
<p>グローバル カタログ サーバーの詳細については、「<a href="http://go.microsoft.com/fwlink/p/?linkid=178996">グローバル カタログについて</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>ドメイン コントローラー</p></td>
<td><p>Exchange 2013 のインストールを計画している Active Directory サイトごとに、次のいずれかを実行する 1 つ以上の書き込み可能なドメイン コントローラーを用意する必要があります。</p>
<ul>
<li><p>Windows Server 2012 R2 Standard または Datacenter1</p></li>
<li><p>Windows Server 2012 Standard または Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard または Enterprise SP1 以降</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 以降</p></li>
<li><p>Windows Server 2008 Standard または Enterprise SP1 以降 (32 ビットまたは 64 ビット)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 以降</p></li>
<li><p>Windows Server 2003 Standard Edition、Service Pack 2 (SP2) 以降 (32 ビットまたは 64 ビット)</p></li>
<li><p>Windows Server 2003 Enterprise Edition、SP2 以降 (32 ビットまたは 64 ビット)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Active Directory フォレスト</p></td>
<td><p>Active Directory はWindows Server 2003 フォレスト機能モード以降にする必要があります2</p></td>
</tr>
<tr class="odd">
<td><p>DNS 名前空間のサポート</p></td>
<td><p>Exchange 2013 は、次のドメイン ネーム システム (DNS) 名前空間をサポートします。</p>
<ul>
<li><p>連続</p></li>
<li><p>非連続</p></li>
<li><p>単一ラベルのドメイン</p></li>
<li><p>不整合</p></li>
</ul>
<p>Exchange でサポートされる DNS 名前空間の詳細については、Microsoft サポート技術情報の記事 2269838「<a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=2269838">単一ラベルのドメイン、不整合の名前空間、および非連続の名前空間と Microsoft Exchange の互換性</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>IPv6 サポート</p></td>
<td><p>Exchange 2013 で、IPv6 がサポートされるのは、IPv4 もインストールされ、有効になっている場合のみです。Exchange 2013 がこの構成で展開されており、ネットワークで IPv4 と IPv6 がサポートされている場合は、すべての Exchange サーバーが、IPv6 アドレスを使用するデバイス、サーバー、およびクライアントとの間でデータを送受信できます。詳細については、「<a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Exchange 2013 での IPv6 サポート</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2 は Exchange 2013 SP1 以降でのみサポートされます。

2   Windows Server 2012 R2 フォレスト機能モードは Exchange 2013 SP1 以降でのみサポートされます。

## ディレクトリ サーバーのアーキテクチャ

64 ビットの Active Directory ドメイン コントローラーを使用すると、Exchange 2013 のディレクトリ サービスのパフォーマンスが向上します。


> [!NOTE]
> 複数ドメイン環境で、Active Directory 言語ロケールを日本語に設定している Windows Server 2008 ドメイン コントローラーで、受信レプリケーション中にオブジェクトに格納される属性をサーバーが受信できない場合があります。詳細については、Microsoft サポート技術情報の文書番号 949189「<A href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=949189">日本語言語ロケールで構成されている Windows Server 2008 ドメイン コントローラーが受信レプリケーション中にオブジェクトの属性に更新を適用できない場合がある</A>」を参照してください。



## ディレクトリ サーバーによる Exchange 2013 のインストール

セキュリティとパフォーマンス上の理由から、Exchange 2013 をメンバー サーバーにのみインストールし、Active Directory ディレクトリ サーバーにはインストールしないことをお勧めします。ただし、Exchange 2013 を実行しているコンピューター上では DCPromo を実行できません。Exchange 2013 をインストールした後は、メンバー サーバーからディレクトリ サーバー、または、ディレクトリ サーバーからメンバー サーバーへの役割の変更がサポートされなくなります。

## ハードウェア

Exchange 2013 サーバーに対して推奨するハードウェア要件は、インストールされるサーバーの役割や、サーバー上で予測される負荷などのさまざまな要素によって異なります。

展開を適切にサイズ変更して構成する方法の詳細については、「[Exchange 2013 のサイズ変更と構成の推奨事項](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md)」を参照してください。

仮想化環境における Exchange の展開の詳細については、「[Exchange 2013 仮想化](exchange-2013-virtualization-exchange-2013-help.md)」を参照してください。

**Exchange 2013 のハードウェア要件**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>要件</th>
<th>メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>プロセッサ</p></td>
<td><ul>
<li><p>Intel 64 アーキテクチャ (以前の Intel EM64T) をサポートする Intel プロセッサを搭載する x64 アーキテクチャ ベースのコンピューター</p></li>
<li><p>AMD64 プラットフォームをサポートする AMD プロセッサ</p></li>
<li><p>Intel Itanium IA64 プロセッサはサポートされていません</p></li>
</ul></td>
<td><p>サポート対象のオペレーティング システムについては、このトピック後半の「オペレーティング システム」のセクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>メモリ</p></td>
<td><p>インストールする Exchange の役割によって異なります。</p>
<ul>
<li><p><strong>メールボックス</strong>   最小 8 GB</p></li>
<li><p><strong>クライアント アクセス</strong>   最小 4 GB</p></li>
<li><p><strong>メールボックスとクライアント アクセスの組み合わせ</strong>   最小 8 GB</p></li>
<li><p><strong>エッジ トランスポート</strong>   最小 4 GB</p></li>
</ul></td>
<td><p>なし。</p></td>
</tr>
<tr class="odd">
<td><p>ページング ファイル サイズ</p></td>
<td><p>ページ ファイルの最小および最大サイズは、物理的な RAM の容量 + 10 MB に設定する必要があります。32 GB より大きい RAM を使用している場合、最大サイズを 32778 MB に設定する必要があります。</p></td>
<td><p>ページファイルの推奨事項の詳細については、「<a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Exchange 2013 のサイズ変更と構成の推奨事項</a>」の「ページファイル」セクションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>ディスク領域</p></td>
<td><ul>
<li><p>Exchange をインストールするドライブ上に 30 GB 以上</p></li>
<li><p>インストールするユニファイド メッセージング (UM) の言語パックごとに、さらに 500 MB のディスクの空き領域</p></li>
<li><p>システム ドライブに 200 MB 以上のディスクの空き領域</p></li>
<li><p>メッセージ キュー データベースを保存する空き領域 500 MB 以上のハード ディスク</p></li>
</ul></td>
<td><p>記憶域の推奨事項の詳細については、「<a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Exchange 2013 記憶域構成オプション</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>ドライブ</p></td>
<td><p>ローカル、またはネットワーク経由でアクセス可能な DVD-ROM ドライブ</p></td>
<td><p>なし。</p></td>
</tr>
<tr class="even">
<td><p>画面解像度</p></td>
<td><p>1024 x 768 ピクセル以上</p></td>
<td><p>なし。</p></td>
</tr>
<tr class="odd">
<td><p>ファイル形式</p></td>
<td><p>NTFS ファイル システムとしてフォーマットされたディスク パーティションは、次のいずれかのパーティションが適用されます。</p>
<ul>
<li><p>システム パーティション</p></li>
<li><p>Exchange のバイナリ ファイルまたは Exchange 診断ログによって生成されたファイルを保管するパーティション</p></li>
</ul>
<p>次の種類のファイルを含むディスク パーティションは、ReFS としてフォーマットできます。</p>
<ul>
<li><p>トランザクション ログ ファイルを格納するパーティション</p></li>
<li><p>データベース ファイルを格納するパーティション</p></li>
<li><p>コンテンツのインデックス処理に関するファイルを格納するパーティション</p></li>
</ul></td>
<td><p>なし。</p></td>
</tr>
</tbody>
</table>


## オペレーティング システム

次の表に、Exchange 2013 でサポートされるオペレーティング システムの一覧を示します。


> [!IMPORTANT]
> Windows Server Core モードで実行しているコンピューターに Exchange 2013 はインストールできません。インストールできるのは、Windows サーバーの完全インストールで実行しているコンピューターです。Windows Server Core モードで実行しているコンピューターに Exchange 2013 をインストールする場合は、以下のどれか 1 つの操作で Windows Server の完全インストールにサーバーを変換してください。 
> <UL>
> <LI>
> <P><STRONG>Windows Server 2008 R2</STRONG>&nbsp;&nbsp;&nbsp;Windows Server を再インストールし、<STRONG>[完全インストール]</STRONG> オプションを選択します。</P>
> <LI>
> <P><STRONG>Windows Server 2012 R2</STRONG> または <STRONG>Windows Server 2012</STRONG>&nbsp;&nbsp;&nbsp;次のコマンドを実行することによって、Windows Server Core モード サーバーを完全インストールに変換します。</P><PRE><CODE>Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart</CODE></PRE></LI></UL>



**Exchange 2013 でサポートされるオペレーティング システム**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メールボックス サーバー、クライアント アクセス サーバー、およびエッジ トランスポート サーバーの役割</p></td>
<td><p>次のいずれかが必要です。</p>
<ul>
<li><p>Windows Server 2012 R2 Standard または Datacenter1</p></li>
<li><p>Windows Server 2012 Standard または Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Enterprise Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 以降</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>管理ツール</p></td>
<td><p>次のいずれかが必要です。</p>
<ul>
<li><p>Windows Server 2012 R2 Standard または Datacenter1</p></li>
<li><p>Windows Server 2012 Standard または Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard SP1</p></li>
<li><p>Windows Server 2008 R2 Enterprise SP1</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 以降</p></li>
<li><p>64 ビット版の Windows 8.12</p></li>
<li><p>64 ビット版の Windows 8</p></li>
<li><p>64 ビット版の Windows 7 Service Pack 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2 は、Exchange 2013 SP1 以降でのみサポートされています。

2   Windows 8.1 は、Exchange 2013 SP1 以降でのみサポートされています。

**サポートされる Exchange 2013 の Windows Management Framework のバージョン**

Exchange 2013 は Exchange をインストールしている Windows Server のリリースに組み込まれている Windows Management Framework のバージョンのみをサポートしています。Exchange を実行しているサーバーでスタンドアロンのダウンロードとして利用できる Windows Management Framework のバージョンはインストールしないでください。

## .NET Framework

インストールする Exchange のリリースによってサポートされる最新バージョンの .NET Framework を使用することを強くお勧めします。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange のバージョン</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## サポートされるクライアント

Exchange 2013 は、Outlook と Entourage for Mac の以下のバージョンをサポートします。

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 for Mac, Web Services Edition

  - Outlook for Mac for Office 365

  - Outlook for Mac 2011

Exchange がサポートする Outlook リリースのリストについては、「[Outlook 更新プログラム](https://go.microsoft.com/fwlink/p/?linkid=513459)」を参照してください。


> [!IMPORTANT]
> 入手可能な最新のサービス パックと更新プログラムをインストールして、Exchange への接続時に、可能な限り最良のユーザー エクスペリエンスが得られるようにすることをお勧めします。



Outlook 2007 より前の Outlook クライアントは、サポートされていません。Entourage 2008 for Mac RTM や Entourage 2004 などの DAV が必要な、Mac オペレーティング システムで実行する電子メール クライアントはサポートしていません。

Outlook Web App は、さまざまなオペレーティング システムやデバイスで各種ブラウザーをサポートしています。詳細情報については、「[Exchange 2013 の Outlook Web App の新機能](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md)」を参照してください。

