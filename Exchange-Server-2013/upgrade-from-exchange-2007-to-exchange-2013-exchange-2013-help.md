---
title: 'Exchange 2007 から Exchange 2013 へのアップグレード: Exchange 2013 Help'
TOCTitle: Exchange 2007 から Exchange 2013 へのアップグレード
ms:assetid: a604b96d-2a51-480f-937f-45ad753c2cad
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ898581(v=EXCHG.150)
ms:contentKeyID: 51407558
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2007 から Exchange 2013 へのアップグレード

 

_**適用先:** Exchange Online, Exchange Server, Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Microsoft Exchange Server 2010 および Exchange Server 2007 には複数のサーバーの役割があります。クライアント アクセス、メールボックス、ハブ トランスポート、ユニファイド メッセージング、およびエッジ トランスポート。Exchange Server 2013 では、サーバー役割の数が少なくなり、以前は 5 個でしたが、クライアント アクセス、メールボックス、エッジ トランスポートの 3 個になりました。ユニファイド メッセージングは、Exchange 2013 で提供されている音声関連機能のコンポーネントまたはサブ機能と位置づけられるようになりました。(変更の詳細については、「[Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md)」の「Exchange 2013 アーキテクチャ」を参照してください。)

既存の Exchange 2007 組織を Exchange 2013 にアップグレードする際、Exchange 2007 サーバーと Exchange 2013 サーバーが組織内に共存する期間があります。このモードは無期限に維持できます。または、Exchange 2007 から Exchange 2013 にすべてのリソースを移動し、Exchange 2007 サーバーの使用を停止することで、Exchange 2013 へのアップグレードをすぐに完了することもできます。以下の条件が満たされている場合は、共存シナリオになっています。

  - Exchange 2013 が既存の Exchange 組織内に展開されている。

  - 複数のバージョンの Microsoft Exchange が組織にメッセージング サービスを提供している。

既存の Exchange 2003 組織を直接 Exchange 2013 にアップグレードすることはできません。最初に Exchange 2003 組織を Exchange 2007 組織または Exchange 2010 組織にアップグレードしてから、その Exchange 2007 組織または Exchange 2010 組織を Exchange 2013 にアップグレードできます。組織を Exchange 2003 から Exchange 2010 にアップグレードし、Exchange 2010 から Exchange 2013 にアップグレードすることをお勧めします。


> [!WARNING]
> Exchange 2013 にアップグレードする前に、組織から Exchange 2003 のすべてのインスタンスを削除する必要があります。



すべての Exchange 2003 メールボックスを Exchange Online に移行できます。この方法の詳細については、「[複数のメール アカウントを Office 365 に移行する方法](https://go.microsoft.com/fwlink/p/?linkid=524030)」をご覧ください。

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

## Exchange 2007 および Exchange 2010 と Exchange 2013 の混在モードの共存

Active Directory サイトに Exchange 2010 と Exchange 2007 の両方がインストールされている場合は、Exchange 2010 と Exchange 2007 の両方のアップグレード方法に従って必要なアップグレード手順を実行します。

## アップグレード プロセスの概要

Exchange 2007 から Exchange 2013 へのアップグレード プロセスの概要を把握しやすいように、主要な各タスクに関連するリソースを次の表にまとめました。具体的な手順については、「[チェックリスト: Exchange 2007 からのアップグレード](checklist-upgrade-from-exchange-2007-exchange-2013-help.md)」を参照してください。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスク</th>
<th>トピック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 の役割とコンポーネントに関する詳細情報</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013 の新機能</a></p>
<p><a href="client-access-server-exchange-2013-help.md">クライアント アクセス サーバー</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">メールボックス サーバー</a></p>
<p><a href="mail-flow-exchange-2013-help.md">メール フロー</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">ユニファイド メッセージング</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 をインストールする</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用した Exchange 2013 のインストール</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">セットアップ ウィザードを使用して Exchange 2013 エッジ トランスポートの役割をインストールする</a> (省略可能)</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 のインストールの確認</a></p></td>
</tr>
<tr class="odd">
<td><p>クライアント アクセス サーバー上でデジタル証明書を追加する</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 クライアント アクセス サーバーの構成</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">デジタル証明書と SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">デジタル証明書の要求を作成する</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 関連の仮想ディレクトリを構成する</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Exchange 仮想ディレクトリの既定の設定</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010 からメールボックスを移動する</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 でのメールボックスの移動</a></p></td>
</tr>
<tr class="even">
<td><p>トランスポート コンポーネントを構成する</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">エッジ サブスクリプション</a> (エッジ トランスポート サーバーがインストールされている場合にのみ必要)</p>
<p><a href="mail-routing-exchange-2013-help.md">メール ルーティング</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">シャドウ冗長</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">管理者用の配信レポート</a></p></td>
</tr>
<tr class="odd">
<td><p>UM を構成および展開する</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">ユニファイド メッセージングの計画</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">ボイス メールと UM の展開</a></p></td>
</tr>
</tbody>
</table>

