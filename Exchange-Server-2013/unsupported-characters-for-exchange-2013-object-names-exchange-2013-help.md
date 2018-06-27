---
title: 'Exchange 2013 オブジェクト名でサポートされていない文字: Exchange 2013 Help'
TOCTitle: Exchange 2013 オブジェクト名でサポートされていない文字
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54652974
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 オブジェクト名でサポートされていない文字

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

この記事では、Microsoft Exchange 2013 のオブジェクト名またはコンポーネント名で使用できない文字について説明します。Exchange 2013 でオブジェクトまたはコンポーネントの名前を作成した場合、サポート対象外の文字を使ってオブジェクトを作成できたとしても、名前にサポート対象外の文字を含めることはできません。また、サポートされていない文字を含む名前を持つオブジェクトをインポートしようとするか、そのようなオブジェクトに接続しようとすると、エラー メッセージが表示されるか、予期しない動作が発生することがあります。

## サポートされていない文字

次の表に、Exchange 関連オブジェクトまたはコンポーネントの名前の使用でサポートされていない文字を一覧表示します。この表には、サポートされていない文字を使用した場合に問題が発生する可能性があるシナリオも一覧表示します。この表に一覧表示されている各オブジェクトの最長文字数が 64 文字である点にも注意してください。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange のオブジェクトまたはコンポーネント</th>
<th>Exchange のシナリオ</th>
<th>サポートされていない文字</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>電子メール ドメイン名</p></td>
<td><p>簡易メール転送プロトコル (SMTP) コネクタ</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>コネクタ アドレス スペースのホスト名</p></td>
<td><p>メール フロー</p></td>
<td><p><code>..</code> (2 つのピリオド)</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server のホスト名</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code> (アンダースコア)</p></td>
</tr>
<tr class="even">
<td><p>組織またはサイトの名前</p></td>
<td><p>セットアップ プログラムの実行またはメールボックスの移動</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>組織の内部ディレクトリ名</p></td>
<td><p>ディレクトリ</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダー ツリー名</p></td>
<td><p>パブリック フォルダーの表示と作成</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>受信者名</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>受信者ポリシー SMTP アドレス</p></td>
<td><p>パブリック フォルダー階層の表示</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>受信者ポリシー SMTP アドレス ホスト名</p></td>
<td><p>メール フロー</p></td>
<td><p><code>..</code> (2 つのピリオド)</p></td>
</tr>
<tr class="even">
<td><p>サイトの内部ディレクトリ名</p></td>
<td><p>パブリック フォルダー階層の表示</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>スマート ホスト名</p></td>
<td><p>SMTP</p></td>
<td><p>先頭または末尾のスペース</p></td>
</tr>
</tbody>
</table>

