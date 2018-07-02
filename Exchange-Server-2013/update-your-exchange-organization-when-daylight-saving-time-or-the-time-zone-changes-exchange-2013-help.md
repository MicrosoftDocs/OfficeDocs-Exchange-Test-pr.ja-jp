---
title: '夏時間またはタイム ゾーンが変更された場合の Exchange 組織の更新: Exchange 2013 Help'
TOCTitle: 夏時間またはタイム ゾーンが変更された場合の Exchange 組織の更新
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 66452416
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 夏時間またはタイム ゾーンが変更された場合の Exchange 組織の更新

 

_**適用先:** Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

組織が存在するまたは一部のユーザーが住んでいる国または地域で、夏時間 (DST) を識別するポリシーに変更があった場合、または世界標準時 (UTC) からのローカル時間のオフセットが変更された場合は、それらの変更に対応するために、Microsoft Windows、Microsoft Exchange、Microsoft Outlook、または他のプログラムを更新する必要がある場合があります。

世界中の DST 変更の詳細については、「[夏時間のヘルプとサポート](https://go.microsoft.com/fwlink/p/?linkid=99640)」をリンクも含めて参照してください。また、他のソフトウェアの製造元のサポート Web サイトにアクセスして、追加の更新が必要かどうかを確認します。

お住まいの地域のタイム ゾーンに変更がない場合でも、他のコンピューターまたはユーザーとグローバルに通信する場合、世界の別の場所のイベントに対して、お使いのコンピューターが正確な日付と時刻の計算を行える必要があります。

タイム ゾーンの更新をできる限り早くインストールすることで、古い時刻から新しい時刻への移行中にスケジュールされる会議または予約の数が最小化されます。

## 実行方法

## 手順 1: すべてのクライアントおよびデスクトップ コンピューターに Windows DST 更新プログラムをインストールします

Office 365 認証システムは DST またはタイム ゾーンの変更時に更新されるため、すべての Office 365 クライアント コンピューターを更新する必要があります。更新をしない場合、接続の問題が発生する場合があります。

  - すべてのクライアントおよびデスクトップ コンピューターに Windows DST 更新プログラムがインストールされていることをご確認ください。詳細については、「[Microsoft Windows オペレーティング システムで夏時間を構成する方法](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=914387)」を参照してください。

## 手順 2: すべてのサーバーに Windows DST 更新プログラムをインストールします

1.  すべての社内サーバーを Windows DST 更新プログラムで更新します。

2.  Office 365 を実行している場合は、DirSync または AD FS サーバーなどの Office 365 認証システムと通信するすべてのサーバーを更新します。これらのサーバーは稼働時間を保証するために更新する必要があります。

**注**   サーバー クラスターを更新する場合は、クラスター更新の通常のプロセスに従ってください。パッシブ サーバーをまず最初に更新し、パッシブ サーバーにフェールオーバーを行い (それによりアクティブになります)、次に以前はアクティブだった (現在はパッシブな) サーバーを更新します。サーバー クラスターおよび高可用性サーバー クラスターの更新方法については、「[Exchange Server クラスターと高可用性サーバーの更新](https://technet.microsoft.com/ja-jp/library/hh530052\(v=exchg.150\))」および「[Windows Server フェールオーバー クラスターを更新する方法](https://support.microsoft.com/ja-jp/kb/174799)」を参照してください。

## 手順 3: 必要に応じてクライアントとデスクトップ コンピューター上の Exchange および Outlook を更新します

1.  ユーザーが Outlook 2007 以前のクライアントを使用している場合、この手順の後に示す表に従って、Exchange または Outlook タイム ゾーン ツールのどのツールを実行する必要があるのかを判断します。

2.  コンピューターを更新する必要があるユーザーにメッセージを送信し、適切なツールへのリンクを提供します。

次の表は、ユーザーが [Exchange 予定表更新ツール](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879)または [Microsoft Office Outlook 用タイム ゾーン データ更新ツール](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667)を実行する必要がある時期を示します。組織のサーバーがどのバージョンを実行しているかを確認し、次にユーザーが実行しているクライアント プログラムを確認します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>クライアント バージョン</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>組織のバージョン</strong></p></td>
<td><p><strong>Outlook 2003 または Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>社内の Exchange 2003</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Exchange 予定表更新ツール</a>または</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a></p></td>
<td><p>操作は不要</p></td>
</tr>
<tr class="even">
<td><p><strong>社内の Exchange 2007</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Exchange 予定表更新ツール</a>または</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a></p></td>
<td><p>操作は不要</p></td>
</tr>
<tr class="odd">
<td><p><strong>社内の Exchange 2010</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Exchange 予定表更新ツール</a>または</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a></p></td>
<td><p>操作は不要</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2013 オンプレミス</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a></p></td>
<td><p>操作は不要</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S (Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a></p></td>
<td><p>操作は不要</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-S (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a></p></td>
<td><p>操作は不要</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365 (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a> (Outlook 2003 はサポート対象外)</p></td>
<td><p>操作不要</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Microsoft Office Outlook 用タイム ゾーン データ更新ツール</a> (Outlook 2003 はサポート対象外)</p></td>
<td><p>操作不要</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

