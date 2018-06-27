---
title: '-ContentFilter パラメーターのフィルター可能なプロパティ: Exchange 2013 Help'
TOCTitle: -ContentFilter パラメーターのフィルター可能なプロパティ
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50555874
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# \-ContentFilter パラメーターのフィルター可能なプロパティ

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-09-10_

ここでは、*ContentFilter* パラメーターのフィルター可能なプロパティについて説明します。*ContentFilter* パラメーターは、フィルターに一致するメッセージを .pst ファイルにエクスポートするのに使用します。*ContentFilter* パラメーターは、[New-MailboxExportRequest](https://technet.microsoft.com/ja-jp/library/ff607299\(v=exchg.150\)) コマンドレットで使用されます。

## フィルター可能なプロパティ

*ContentFilter* パラメーターの多くのプロパティでは、ワイルドカード文字を使用できます。ワイルドカード文字を使用する場合、**-eq** 演算子の代わりに **-like** 演算子を使用します。**-like** 演算子は、文字列などのさまざまな種類のパターン マッチを検索するために使用されますが、**-eq** 演算子は完全な一致を検索するために使用されます。

次の表には、*ContentFilter* パラメーターのフィルター可能なプロパティの一覧が含まれています。この表には、プロパティの名前、説明、取り得る値、および構文の例の一覧が示されています。OPATH フィルターの詳細については、「[受信者のシェル コマンドのフィルター](https://technet.microsoft.com/ja-jp/library/bb124268\(v=exchg.150\))」を参照してください。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>説明</th>
<th>値</th>
<th>構文の例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All</p></td>
<td><p>このプロパティは、インデックス プロパティ内に、特定の文字列を含むすべてのメッセージを返します。たとえば、受信者、送信者に &quot;Ayla&quot; を含む、またはメッセージの本文にその名前を含むすべてのメッセージをエクスポートする場合、このプロパティを使用します。</p></td>
<td><p>文字列</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {All -like &#39;*Ayla*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>このプロパティは、添付ファイルの内容または添付ファイル名に、指定した文字列を含むメッセージを返します。</p></td>
<td><p>文字列</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {Attachment -like &#39;*.jpg&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>このプロパティは、指定した受信者が Bcc フィールドに含まれる、送信済みのメッセージを返します。</p></td>
<td><p>表示名</p>
<p>エイリアス</p>
<p>SMTP アドレス</p>
<p>LegacyDN</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {(BCC -eq &#39;ayla@contoso.com&#39;) -or (BCC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>このプロパティは、メッセージの本文に、特定の文字列を含むメッセージを返します。</p></td>
<td><p>文字列</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {Body -like &#39;*prospectus*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>このプロパティは、一致するカテゴリを持つメッセージを返します。カテゴリは、ユーザーまたは受信トレイ ルールにより設定されます。</p></td>
<td><p>文字列</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {Category -like &#39;*Blue*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>このプロパティは、指定した受信者が Cc フィールドに含まれる、送信済みのメッセージを返します。</p></td>
<td><p>表示名</p>
<p>エイリアス</p>
<p>SMTP アドレス</p>
<p>LegacyDN</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {(CC -eq &#39;ayla@contoso.com&#39;) -or (CC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Expires</p></td>
<td><p>このプロパティは、指定された有効期限のタイム スタンプを持つメッセージを返します。</p></td>
<td><p>タイム スタンプの日時</p></td>
<td><pre><code>-ContentFilter {Expires -lt &#39;01/01/2013&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>このプロパティは、メッセージの添付ファイルの有無を返します。</p></td>
<td><p>ブール値</p>
<p><code>$true</code> または<code>$false</code></p></td>
<td><pre><code>-ContentFilter {HasAttachment -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>このプロパティは、指定した重要度レベルを持つメッセージを返します。</p></td>
<td><p>0 または Low</p>
<p>1 または Normal</p>
<p>2 または High</p></td>
<td><pre><code>-ContentFilter {Importance -eq &#39;high&#39;}</code></pre>
<pre><code>-ContentFilter {Importance -eq 2}</code></pre></td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>このプロパティは、ユーザーまたは受信トレイ ルールによりフラグが付けられたメッセージを返します。</p></td>
<td><p>ブール値</p>
<p><code>$true</code> または<code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsFlagged -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>このプロパティは、メッセージがユーザーにより読まれたかどうかを返します。</p></td>
<td><p>ブール値</p>
<p><code>$true</code> または<code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsRead -eq $true}</code></pre></td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>このプロパティは、指定したタイプのメッセージを返します。</p></td>
<td><p>予定表</p>
<p>連絡先</p>
<p>文書</p>
<p>Email</p>
<p>Fax</p>
<p>InstantMessage</p>
<p>ジャーナル</p>
<p>メモ</p>
<p>投稿</p>
<p>RSS フィード</p>
<p>タスク</p>
<p>Voicemail</p></td>
<td><pre><code>-ContentFilter {MessageKind -eq &#39;Calendar&#39;}</code></pre>
<pre><code>-ContentFilter {MessageKind -ne &#39;Email&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>このプロパティは、指定したロケールのメッセージを返します。</p></td>
<td><p>CultureInfo</p></td>
<td><pre><code>-ContentFilter {MessageLocale -ne &#39;en-US&#39;}</code></pre>
<pre><code>-ContentFilter {MessageLocale -eq &#39;tr-TR&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>このプロパティは、指定した受信者が To、Bcc、または Cc フィールドに含まれるメッセージを返します。</p></td>
<td><p>表示名</p>
<p>エイリアス</p>
<p>SMTP アドレス</p>
<p>LegacyDN</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {(Participants -eq &#39;ayla@contoso.com&#39;) -or (Participants -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>このプロパティは、ポリシー タグを持つメッセージを返します。Exchange ストアは引き続きポリシー タグを GUID として保持します。そのため、文字列には、PR_POLICY_TAG により検索されることになる明示的な GUID 値か、またはワイルドカード文字列のいずれかを指定することができます。</p>
<p>指定した値が GUID ではない場合、コマンドは Active Directory 情報を使用して GUID へ名前を解決します。</p></td>
<td><p>文字列</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {PolicyTag -ne &#39;00000000-0000-0000-0000-000000000000&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>このプロパティは、指定した受信タイム スタンプで受信されたメッセージを返します。</p></td>
<td><p>タイム スタンプの日時</p></td>
<td><pre><code>-ContentFilter {Received -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Received -lt &#39;01/01/2013&#39;) -and (Received -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>このプロパティは、指定した送信者から受信したメッセージを返します。</p></td>
<td><p>表示名</p>
<p>エイリアス</p>
<p>SMTP アドレス</p>
<p>LegacyDN</p>
<p>ワイルドカード</p></td>
<td><pre><code>ContentFilter {Sender -eq &#39;tony&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>このプロパティは、指定した送信タイム スタンプで送信されたメッセージを返します。</p></td>
<td><p>タイム スタンプの日時</p></td>
<td><pre><code>-ContentFilter {Sent -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Sent -lt &#39;01/01/2013&#39;) -and (Sent -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>このプロパティは、特定のサイズのメッセージを返します。</p></td>
<td><p>B (バイト)</p>
<p>KB (キロバイト)</p>
<p>MB (メガバイト)</p></td>
<td><pre><code>-ContentFilter {Size -gt &#39;10KB&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>このプロパティは、メッセージの件名に、特定の文字列を含むメッセージを返します。</p></td>
<td><p>文字列</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {Subject -like &#39;*meeting*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>このプロパティは、指定した受信者が &quot;宛先&quot; フィールドに含まれる、送信済みのメッセージを返します。</p></td>
<td><p>表示名</p>
<p>エイリアス</p>
<p>SMTP アドレス</p>
<p>LegacyDN</p>
<p>ワイルドカード</p></td>
<td><pre><code>-ContentFilter {To -eq &#39;aylakol&#39;}</code></pre></td>
</tr>
</tbody>
</table>

