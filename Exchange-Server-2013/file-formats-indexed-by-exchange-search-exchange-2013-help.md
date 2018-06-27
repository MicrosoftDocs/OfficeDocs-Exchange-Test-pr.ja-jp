---
title: 'Exchange Search によってインデックス処理されるファイル形式: Exchange 2013 Help'
TOCTitle: Exchange Search によってインデックス処理されるファイル形式
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52057868
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Search によってインデックス処理されるファイル形式

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2015-07-21_

MicrosoftExchange Server 2013 および Exchange Online では、Exchange Search に、メッセージの添付ファイルとして含まれる最も一般的な種類のファイル形式をインデックス処理するためのフィルターが組み込まれています。フィルターをインストールして、別の種類のファイルをインデックス処理することもできます。


> [!NOTE]
> Exchange 2013 では、Microsoft Office フィルター パックをインストールおよび登録する必要はありません。



Exchange Search と依存機能 ([インプレース電子情報開示 (eDiscovery)](in-place-ediscovery-exchange-2013-help.md) など) を管理または使用する場合は、検索不能アイテムと、インデックス処理が無効か、またはインデックス処理できないコンテンツを含むファイル形式との相違点を考慮してください。

  - **検索不能アイテム**   フィルターがインストールされていないなどの理由で、Exchange Search が特定の種類のファイルをインデックス処理できない場合、そのファイルの種類の検索は失敗します。このような添付ファイルを含むメッセージは、*部分的にインデックス処理された*ものとしてマークされます。検索不能アイテムは、[Get-FailedContentIndexDocuments](https://technet.microsoft.com/ja-jp/library/dd351154\(v=exchg.150\)) コマンドレットを使用して取得することができます。インプレース電子情報開示の検索結果を探索メールボックスにコピーする場合、または検索結果を PST ファイルにエクスポートする場合、検索不能アイテムを含めることができます。詳細については、「[Exchange 電子情報開示の検索不能アイテム](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)」を参照してください。

  - **インデックス処理できないコンテンツがあるファイル形式**   Windows Media Video (WMV) などの特定のファイルの種類には、インデックス処理可能なコンテンツが含まれていないため、インデックス処理が行われません。このようなファイルの種類の添付ファイルを含むメッセージも、インプレース電子情報開示検索で検索不能アイテムとして返されます。

  - **無効なファイル形式** 社内組織では、管理者は指定したファイル形式のインデックス処理を無効にすることができます。無効な形式の添付ファイルを含むメッセージは検索不能アイテムとして返されます。


> [!IMPORTANT]
> メッセージの添付ファイルが検索不能である場合、またはインデックスを作成できないファイル形式の場合でも、メッセージの件名、本文、その他のメタデータのインデックスを作成して、そのメッセージを検索することができます。



社内組織での Exchange Search に関連するその他の管理タスクについては、「[Exchange Search の手順](exchange-search-procedures-exchange-2013-help.md)」を参照してください。

## 既定のフィルター

次の表に、Exchange 2013 メールボックス サーバーおよび Exchange Online にインストールされている既定の検索フィルターを示します。[Get-SearchDocumentFormat](https://technet.microsoft.com/ja-jp/library/jj873755\(v=exchg.150\)) コマンドレットを使用して、既定のフィルターの一覧を取得できます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィルター</th>
<th>ファイル拡張子</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>電子メール メッセージ</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>グラフィックス交換形式</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>Excel ファイル</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office バインダー</p></td>
<td><p>.obt、obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XML Paper Specification</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument プレゼンテーション</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument スプレッドシート</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument テキスト</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Outlook アイテム</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>Portable Document Format</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>リッチ テキスト</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>Text</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>Web アーカイブ</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>[Web ページ]</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>XML ドキュメント</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>ZIP アーカイブ</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## 無効なファイル形式

次の表は、Exchange 2013 メールボックス サーバーと Exchange Online で既定でインデックスが無効になっている検索フィルターの一覧を示します。Exchange 2013 で、管理者は [Set-SearchDocumentFormat](https://technet.microsoft.com/ja-jp/library/jj873756\(v=exchg.150\)) コマンドレットを使用して、索引作成のためにサポートされるファイル形式を無効にしたり再度有効にしたりすることができます。このコマンドレットは Exchange Online では使用できません。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィルター</th>
<th>ファイル拡張子</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>ビットマップ</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows Wave Audio</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>

