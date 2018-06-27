---
title: 'Exchange 2000 または Exchange 2003 サーバーが含まれているフォレストで Exchange 2013 をインストールできない: Exchange 2013 Help'
TOCTitle: Exchange 2000 または Exchange 2003 サーバーが含まれているフォレストで Exchange 2013 をインストールできない
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 49129647
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2000 または Exchange 2003 サーバーが含まれているフォレストで Exchange 2013 をインストールできない

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2016-12-09_

Exchange 2000 Server または Exchange Server 2003 を実行している 1 台以上のコンピューターが Active Directory フォレストで検出されたため、Microsoft Exchange Server 2013 は処理を継続できません。Exchange 2013 をインストールするには、その前に、すべての Exchange 2000 と Exchange 2003 サーバーをフォレストから削除する必要があります。メールボックス、パブリック フォルダー、および他のすべての Exchange オブジェクトやコンポーネントを Exchange Server 2007 または Exchange Server 2010 のいずれかにアップグレードする必要があります。Exchange 2000 または Exchange 2003 から直接 Exchange 2013 にアップグレードすることはできません。

組織に Exchange 2013 をインストールするために使用する必要があるパスは、フォレストに現在インストールされている Exchange のバージョンによって異なります。詳細については、以下の表を参照してください。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>組織にインストールされているバージョン</th>
<th>Exchange 2013 にアップグレードするために使用する必要があるパス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>Exchange 2007 を Exchange 2000 組織にインストールします。</p></li>
<li><p>Exchange 2007 と Exchange 2000 の共存を構成します。</p></li>
<li><p>Exchange 2000 メールボックス、パブリック フォルダー、およびその他のコンポーネントを Exchange 2007 に移行します。</p></li>
<li><p>すべての Exchange 2000 サーバーを使用停止して、削除します。</p></li>
<li><p>Exchange 2013 を Exchange 2007 組織にインストールします。</p></li>
<li><p>Exchange 2013 と Exchange 2007 の共存を構成します。</p></li>
<li><p>Exchange 2007 メールボックス、パブリック フォルダー、およびその他のコンポーネントを Exchange 2013 に移行します。</p></li>
<li><p>すべての Exchange 2007 サーバーを使用停止して、削除します。</p></li>
</ol>
<p>詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=103281">Exchange 2007 へのアップグレード</a>」と「<a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Exchange 2007 から Exchange 2013 へのアップグレード</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>Exchange 2010 を Exchange 2003 組織にインストールします。</p></li>
<li><p>Exchange 2010 と Exchange 2003 の共存を構成します。</p></li>
<li><p>Exchange 2003 メールボックス、パブリック フォルダー、およびその他のコンポーネントを Exchange 2010 に移行します。</p></li>
<li><p>すべての Exchange 2003 サーバーを使用停止して、削除します。</p></li>
<li><p>Exchange 2013 を Exchange 2010 組織にインストールします。</p></li>
<li><p>Exchange 2013 と Exchange 2010 の共存を構成します。</p></li>
<li><p>Exchange 2010 メールボックス、パブリック フォルダー、およびその他のコンポーネントを Exchange 2013 に移行します。</p></li>
<li><p>すべての Exchange 2010 サーバーを使用停止して、削除します。</p></li>
</ol>
<p>詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003 - アップグレードと共存のロードマップ計画</a>」と「<a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Exchange 2010 から Exchange 2013 へのアップグレード</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


Exchange 2010 または Exchange 2013 にアップグレードする場合、Exchange 展開アシスタントを使うと簡単に展開を行えます。詳細については、以下のリンクを参照してください。

  - [Exchange 2010 展開アシスタント](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Exchange 2013 展開アシスタント](https://go.microsoft.com/fwlink/p/?linkid=277105)

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

