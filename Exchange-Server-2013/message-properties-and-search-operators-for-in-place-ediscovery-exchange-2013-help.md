---
title: 'インプレース電子情報開示のためのメッセージ プロパティと検索演算子: Exchange Online Help'
TOCTitle: インプレース電子情報開示のためのメッセージ プロパティと検索演算子
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62617788
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インプレース電子情報開示のためのメッセージ プロパティと検索演算子

 

_**適用先:** Exchange Online, Exchange Server 2013_

このトピックでは、Exchange Server 2013 および Exchange Online でインプレース電子情報開示とインプレース保持を使用して検索可能な、Exchange 電子メール メッセージのプロパティについて説明されています。このトピックではまた、電子情報開示の検索結果を絞り込むために使用できる、ブール検索演算子や他の検索クエリ技法についても説明します。

インプレース電子情報開示では、キーワード クエリ言語 (KQL) が使用されます。詳しくは、「[キーワード クエリ言語 (KQL) 構文のリファレンス](https://go.microsoft.com/fwlink/?linkid=269603)」を参照してください。

## Exchange の検索可能なプロパティ

次の表には、インプレース電子情報開示を使用して、または **New-MailboxSearch** や **Set-MailboxSearch** コマンドレットを使用して検索できる、電子メール メッセージのプロパティがリストされています。表には、各プロパティの *property:value* 構文の例、およびその例で返される検索結果の説明が含まれています。


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
<th>プロパティの説明</th>
<th>例</th>
<th>例で返される検索結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>電子メール メッセージに添付されているファイルの名前。</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:annual*</p></td>
<td><p>annualreport.ppt という名前の添付ファイルのあるメッセージ。</p>
<p>2 番目の例では、ワイルドカードを使用して、添付ファイルのファイル名に「annual」の語が含まれるメッセージを返します。</p></td>
</tr>
<tr class="even">
<td><p>Bcc</p></td>
<td><p>メール メッセージの BCC フィールド。1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>どの例も Bcc フィールドに「Pilar Pinilla」が含まれているメッセージを返します。</p></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>検索するカテゴリ。カテゴリは、ユーザーが Outlook または Outlook Web アプリを使用して決めることができます。値は次のいずれかです。</p>
<ul>
<li><p>blue</p></li>
<li><p>green</p></li>
<li><p>orange</p></li>
<li><p>purple</p></li>
<li><p>red</p></li>
<li><p>yellow</p></li>
</ul></td>
<td><p>category:&quot;Red Category&quot;</p></td>
<td><p>元のメールボックスで「red」のカテゴリが割り当てられているメッセージ。</p></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>メール メッセージの CC フィールド。1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>どちらの例も、CC フィールドに Pilar Pinilla が指定されたメッセージ。</p></td>
</tr>
<tr class="odd">
<td><p>From</p></td>
<td><p>メール メッセージの送信者。1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>指定されたユーザーによって送信された、または指定されたドメインから送信されたメッセージ。</p></td>
</tr>
<tr class="even">
<td><p>Importance</p></td>
<td><p>送信者がメッセージを送信するときに指定できる電子メール メッセージの重要度。既定では、送信者が重要度を <strong>high</strong> または <strong>low</strong> に設定していない限り、メッセージは普通の重要度で送信されます。</p></td>
<td><p>importance:high</p>
<p>importance:medium</p>
<p>importance:low</p></td>
<td><p>高重要度、中重要度、または低重要度とマークされているメッセージ。</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>検索するメッセージの種類。可能な値:</p>
<ul>
<li><p>contacts</p></li>
<li><p>docs</p></li>
<li><p>email</p></li>
<li><p>faxes</p></li>
<li><p>im</p></li>
<li><p>journals</p></li>
<li><p>meetings</p></li>
<li><p>notes</p></li>
<li><p>posts</p></li>
<li><p>rssfeeds</p></li>
<li><p>tasks</p></li>
<li><p>voicemail</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OR kind:im OR kind:voicemail</p></td>
<td><p>検索条件に一致する電子メール メッセージ。2 番目の例では、検索条件を満たす電子メール メッセージ、インスタント メッセージングのスレッド、およびボイス メッセージを返します。</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>メール メッセージ内のすべての送受信者フィールド。すなわち、From、To、CC、BCC の各フィールドです。1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>garthf@contoso.com が送信元または送信先のメッセージ。</p>
<p>2 番目の例は、contoso.com ドメイン内のユーザーが送信元または送信先のすべてのメッセージを返します。</p></td>
</tr>
<tr class="odd">
<td><p>Received</p></td>
<td><p>電子メール メッセージが受信者によって受信された日付。</p></td>
<td><p>received:04/15/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=03/31/2014</p></td>
<td><p>2014 年 4 月 15 日に受信されたメッセージ。2 番目の例は、2014 年 1 月 1 日から 2014 年 3 月 31 日までの間に受信したすべてのメッセージを返します。</p></td>
</tr>
<tr class="even">
<td><p>Recipients</p></td>
<td><p>メール メッセージ内のすべての受信者フィールド。すなわち、To、CC、BCC の各フィールドです。1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>garthf@contoso.com に送信されたメッセージ。</p>
<p>2 番目の例では、contoso.com ドメイン内のすべての受信者に送信されたメッセージを返します。</p></td>
</tr>
<tr class="odd">
<td><p>Sent</p></td>
<td><p>送信者によって電子メール メッセージが送信された日付。</p></td>
<td><p>sent:07/01/2014</p>
<p>sent&gt;=06/01/2014 AND sent&lt;=07/01/2014</p></td>
<td><p>指定された日付に送信された、または指定された日付範囲内に送信されたメッセージ。</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>アイテムのサイズ (バイト数)。</p></td>
<td><p>size&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>25 MB を超えるメッセージ。</p>
<p>2 番目の例は 1 ～ 1,048,576 バイト (1 MB) のサイズのメッセージを返します。</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>電子メール メッセージの件名行に含まれるテキスト。</p></td>
<td><p>subject:&quot;Quarterly Financials&quot;</p>
<p>subject:northwind</p></td>
<td><p>件名行のテキストのいずれかの場所に「Quarterly Financials」と完全一致する語句を含むメッセージ。</p>
<p>2 番目の例では、件名行に「northwind」の語が含まれているすべてのメッセージを返します。</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>メール メッセージの To フィールド。1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>to:&quot;Ann Beebe&quot;</p></td>
<td><p>どの例も、To: 行に「Ann Beebe」が指定されているメッセージを返します。</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;受信者プロパティの値には、SMTP アドレス、表示名、または別名を使用してユーザーを指定できます。たとえば、ユーザー Ann Beebe を指定するために、annb@contoso.com、annb、または "Ann Beebe" を使用できます。



## サポートされている検索演算子

**AND**、**OR** などのブール検索演算子は、検索クエリで特定の語を含めたり除去したりすることにより、メールボックス検索をより詳細に定義するために役立ちます。その他の技法、たとえばプロパティ演算子 (\>= や .. など)、疑問符、括弧、ワイルドカードの使用などは、電子情報開示の検索クエリを詳細にするために役立ちます。検索結果を絞り込んだり、その範囲を広げたりするために使用できる演算子を次の表に示します。


> [!IMPORTANT]
> 検索クエリでは大文字のブール演算子を使用する必要があります。たとえば、<STRONG>and</STRONG> ではなく、<STRONG>AND</STRONG> を使用します。検索クエリで小文字の演算子を使用すると、エラーが返されます。




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>演算子</th>
<th>用途</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>keyword1 AND keyword2</p></td>
<td><p>指定されたすべてのキーワードまたは <code>property:value</code> 式が含まれるメッセージを返します。</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>keyword1 +keyword2 +keyword3</p></td>
<td><p><code>keyword1</code> が含まれている <code>keyword2 </code> または <code>keyword3</code> の<em>いずれか</em>が入っている項目を返します。したがって、この例は <code>(keyword2 OR keyword3) AND keyword1</code> というクエリと等価です。</p>
<p>クエリ <code>keyword1 + keyword2</code> (<strong>+</strong> 記号の後にスペースがあります) は、<strong>AND</strong> 演算子を使用する場合と同じではありません。このクエリは <code>&quot;keyword1 + keyword2&quot;</code> と同じになり、<code>&quot;keyword1 + keyword2&quot;</code> というフェーズがそのまま含まれている項目を返します。</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>keyword1 OR keyword2</p></td>
<td><p>指定された 1 つ以上のキーワードまたは <code>property:value</code> 式が含まれるメッセージを返します。</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>keyword1 NOT keyword2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>キーワードまたは <code>property:value</code> 式で指定されたメッセージを除外します。たとえば、<code>NOT from:&quot;Ann Beebe&quot;</code> は Ann Beebe によって送信されたメッセージを除外します。</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>keyword1 -keyword2</p></td>
<td><p><strong>NOT</strong> 演算子と同じです。このクエリは、<code>keyword1</code> が含まれている項目のうち、<code>keyword2</code> が含まれていない項目を返します。</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>keyword1 NEAR(n) keyword2</p></td>
<td><p>含まれる単語が互いの近くにあるメッセージを返します。n は各単語の間にある単語数です。たとえば、<code>best NEAR(5) worst</code> は、単語「worst」が単語「best」から 5 文字以内にあるメッセージを返します。数値が指定されていない場合、既定の間隔は 8 単語です。</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:value</p></td>
<td><p><code>property:value</code> 構文内のコロン (:) は、検索対象のプロパティ値が指定の値と等しいことを示します。たとえば、<code>recipients:garthf@contoso.com</code> は garthf@contoso.com に送信されたすべてのメッセージを返します。</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;value</p></td>
<td><p>検索対象のプロパティが指定の値より小さいことを意味します。1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;value</p></td>
<td><p>検索対象のプロパティが指定の値より大きいことを意味します。1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=value</p></td>
<td><p>検索対象のプロパティが特定の値以下であることを意味します。1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=value</p></td>
<td><p>検索対象のプロパティが特定の値以上であることを意味します。1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>検索対象のプロパティが value1 以上で value2 以下であることを意味します。1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;fair value&quot;</p>
<p>subject:&quot;Quarterly Financials&quot;</p></td>
<td><p>二重引用符 (&quot; &quot;) は、キーワードや <code>property:value</code> 検索クエリで、完全一致する語句を検索するために使用します。</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>前方一致ワイルドカード検索 (アスタリスクが語尾にある) は、キーワードや <code>property:value</code> クエリで、0 個以上の文字に一致します。たとえば、<code>subject:set*</code> は、件名行に set、setup、setting の語 (および &quot;set&quot; で始まるその他の語) が含まれるメッセージを返します。</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(fair OR free) AND from:contoso.com</p>
<p>(IPO OR initial) AND (stock OR shares)</p>
<p>(quarterly financials)</p></td>
<td><p>括弧は、ブール演算子の文字列、<code>property:value</code> アイテム、およびキーワードをグループにまとめます。たとえば、<code>(quarterly financials)</code> は quarterly および financials の語を含むアイテムを返します。</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;この演算子は、日付や数値を含むプロパティに使用します。



## 検索クエリでサポートされていない文字

検索クエリでサポートされていない文字は、通常、検索エラーが発生するか、予期しない結果を返します。多くの場合サポートされていない文字は非表示で、通常、他のアプリケーション (Microsoft Word、Microsoft Excel など) からのクエリまたはクエリの一部を、インプレース電子情報開示検索のクエリ ページのキーワード ボックスにコピーすると、クエリに追加されます。

これは、インプレース電子情報開示の検索クエリでサポートされていない文字の一覧です。

  - **スマート引用符**   スマート単一引用符とスマート二重引用符 (*カーリー引用符*とも呼ばれる) はサポートされていません。検索クエリでは、ストレート引用符のみ使用できます。

  - **印刷不可能な文字と制御文字**   印刷不可能な文字と制御文字は、英数字などの筆記記号ではありません。印刷不可能な文字と制御文字には、テキストを書式設定する文字や個別のテキスト行などが含まれます。

  - **左から右のマークと右から左のマーク**   これらの制御文字は、テキスト方向が左から右の言語 (英語やスペイン語など) と右から左の言語 (アラビア語やヘブライ語など) を表すために使用します。

  - **小文字のブール演算子**   前に説明したとおり、検索クエリでは、**AND** や **OR** などの大文字のブール演算子を使用する必要があります。クエリ構文では、小文字の演算子が使われていてもブール演算子が使われていることを示すことがよくあります。たとえば、`(WordA or WordB) and (WordC or WordD)` です。

**サポートされていない文字を検索クエリで使用しないようにするには、どうすればよいですか?**サポートされていない文字を使用しないようにする最善の方法は、キーワード ボックスにクエリを入力することです。また、Word や Excel からクエリをコピーして、メモ帳などのテキスト エディターでファイルに貼り付けることもできます。テキスト ファイルを保存し、<strong>エンコード</strong> ドロップダウン リストで <strong>ANSI</strong> を選択します。これにより、すべての書式設定とサポートされない文字が削除されます。その後、テキスト ファイルからクエリをコピーして、キーワード クエリ ボックスに貼り付けることができます。

## 検索のヒントと秘訣

  - キーワード検索では大文字と小文字は区別されません。たとえば、"**cat**" と "**CAT**" では同じ結果が返されます。

  - 2 つのキーワードや 2 つの `property:value` 式の間にスペースを置くと、**AND** を使用することと同じになります。たとえば、`from:"Sara Davis" subject:reorganization` は、Sara Davis が送信して件名行に **reorganization** の語を含むすべてのメッセージを返します。

  - `property:value` 形式と一致する構文を使用します。値は大文字小文字を区別しません。また、演算子の後を空白にすることはできません。スペースがある場合、目的の値は単にフルテキスト検索されます。たとえば、**to: pilarp** は、pilarp に送信されたメッセージではなく、「pilarp」をキーワードとした検索を行います。

  - To、From、Cc、Recipients などの受信者プロパティを検索するとき、SMTP アドレス、別名、または表示名を使用して受信者を指定できます。たとえば、pilarp@contoso.com、pilarp、または "Pilar Pinilla" を使用できます。

  - 前方一致ワイルドカード検索 (たとえば **cat\*** や **set\***) だけが使用可能です。後方一致ワイルドカード検索 (\*cat) やサブストリング ワイルドカード検索 (\*cat\*) はサポートされていません。

  - 検索プロパティを検索するとき、検索値が複数の単語で構成される場合は、二重引用符 (" ") を使用します。たとえば、**subject:budget Q1** は、件名行に **budget** を含み、メッセージ内またはいずれかのメッセージ プロパティ内のいずれかの場所に **Q1** を含むメッセージを返します。**subject:"budget Q1"** を使用すると、件名行のいずれかの場所に **budget Q1** を含むすべてのメッセージを返します。

