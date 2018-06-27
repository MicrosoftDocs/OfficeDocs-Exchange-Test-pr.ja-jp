---
title: 'DSN メッセージ テキスト: Exchange 2013 Help'
TOCTitle: DSN メッセージ テキスト
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 49896537
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DSN メッセージ テキスト

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Microsoft Exchange Server 2013 のカスタマイズした配信状態通知 (DSN) メッセージにテキストを追加して、そのテキストを HTML でフォーマットできます。

DSN メッセージの受信者に表示する任意の情報を含めることができます。たとえば、DSN の詳細な説明、ヘルプ デスクの連絡先情報、およびサポート部門の Web サイトへのリンクを含めることができます。各 DSN メッセージには、最大で 512 文字まで含めることができます。

DSN メッセージは HTML 形式で表示できるため、HTML の書式タグを DSN テキストに埋め込むことができます。たとえば、DSN メッセージのテキストの一部を太字にする場合は、テキストを HTML タグ \<B\> と \</B\> で囲みます。次の表に、DSN メッセージ テキストで使用できる有効な HTML タグの例をいくつか示します。

### DSN メッセージで使用できる有効な HTML タグ

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>HTML タグ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;B&gt;</p></td>
<td><p>太字の開始</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B&gt;</p></td>
<td><p>太字の終了</p></td>
</tr>
<tr class="odd">
<td><p>&lt;A HREF=&quot;url&quot;&gt;</p></td>
<td><p>ハイパーリンクの開始</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A&gt;</p></td>
<td><p>ハイパーリンクの終了</p></td>
</tr>
<tr class="odd">
<td><p>&lt;BR&gt;</p></td>
<td><p>改行</p></td>
</tr>
<tr class="even">
<td><p>&lt;EM&gt;</p></td>
<td><p>斜体の開始</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/EM&gt;</p></td>
<td><p>斜体の終了</p></td>
</tr>
<tr class="even">
<td><p>&lt;P&gt;</p></td>
<td><p>段落の開始</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/P&gt;</p></td>
<td><p>段落の終了</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 既定では、Exchange は HTML DSN メッセージを送信しますが、Exchange が HTML DSN メッセージを内部送信者、外部送信者、または両方に送信するかどうかを構成することができます。この動作を構成するには、<STRONG>Set-TransportService</STRONG> コマンドで <EM>InternalDsnSendHtml</EM> パラメーターと <EM>ExternalDsnSendHtml</EM> パラメーターを変更します。<BR><EM>InternalDsnSendHtml</EM> パラメーターが <CODE>$false</CODE> に設定されている場合、Exchange は内部送信者に送信される DSN メッセージの HTML タグを無効にします。<EM>ExternalDsnSendHtml</EM> パラメーターが <CODE>$false</CODE> に設定されている場合、Exchange は外部送信者に送信される DSN メッセージの HTML タグを無効にします。



DSN メッセージ テキストで Exchange が使用する以下の文字は、特別な意味を持ちます。

  - 不等号 (より大) (\>)

  - 不等号 (より小) (\<)

  - アンパサンド (&)

  - 引用符 (")

これらの文字は、HTML タグの開始と終了、および送信者に表示されるテキストの開始と終了を判断するために使用されます。DSN メッセージでこれらの文字を表示するには、次の表のエスケープ コードを使用する必要があります。

たとえば、`"Please contact the Help Desk at <1234>."` というメッセージを表示する場合は、DSN メッセージ テキストに `"Please contact the Help Desk at &lt;1234&gt;." ` を追加する必要があります。

### DSN メッセージの文字のエスケープ コード

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>エスケープ コード</th>
<th>文字</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp;gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp;amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> <CODE>&lt;A HREF="url"&gt;</CODE> など、引用符 (") を含む HTML タグを DSN メッセージ テキストに含める場合は、DSN メッセージ テキスト全体を単一引用符 (') で囲む必要があります。DSN メッセージ テキスト全体や HTML タグを二重引用符で囲むと、エラー メッセージが表示されます。


