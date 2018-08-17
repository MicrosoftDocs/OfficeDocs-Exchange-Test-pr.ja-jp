---
title: 'Outlook Web App の Web パーツの使用: Exchange 2013 Help'
TOCTitle: Outlook Web App の Web パーツの使用
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70090462
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App の Web パーツの使用

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-07-31_

MicrosoftOfficeOutlook Web App の Web パーツを使用して、開くメールボックス、そのメールボックスの中で開くフォルダー、使用するコンテンツ ビューを指定できます。

Outlook Web App の Web パーツを使用すると、URL から Outlook Web App のコンテンツに直接アクセスできます。URL は、Web ブラウザーで入力するか、アプリケーションに埋め込むことができます。一般に、Web パーツは手動では作成しません。ユーザー インターフェイス (UI) での選択に基づいてプログラムで作成するか、または SharePoint Server ページなどのアプリケーションに直接埋め込みます。UI の背後にあるコードが、URL を作成します。Outlook Web App の Web パーツの用途の 1 つは、SharePoint ページにユーザーの受信トレイまたは予定表を表示することです。


> [!NOTE]
> Outlook Web App の Web パーツを使用するには、ユーザーのメールボックスおよび Web パーツを使用して開くメールボックスの両方が、同じ Active Directory&nbsp;フォレスト内にある必要があります。



## Outlook Web Access の Web パーツを使用するためのアクセス許可

Outlook Web App の Web パーツを使用するには、少なくとも、開くコンテンツに対する "参照者" アクセスを委任される必要があります。認証が必要な Outlook Web App Web パーツをアプリケーションに埋め込む場合は、Web パーツに対する要求と共に認証情報を渡す必要があります。そのための方法の 1 つは、Outlook Web App 仮想ディレクトリを構成して統合 Windows 認証を使用するものです。統合 Windows 認証を使用すると、Active Directory アカウントを使用して既にログオンしているユーザーは、資格情報をもう一度入力しなくても Outlook Web App を使用できます。

## Outlook Web App の Web パーツの構文

Exchange 2013 の Outlook Web App には、/owa 仮想ディレクトリに対する要求に使用する URL 形式があります。このような要求は、Web ブラウザーに URL を直接入力することで、または SharePoint Server ページなどの Web アプリケーションに URL を埋め込むことで、行うことができます。

Outlook Web App の Web パーツを使用すると、さまざまな複雑さの URL を作成できます。メールボックスの受信トレイを開くには、簡単な Web パーツ URL を使用できます。開くメールボックス、そのメールボックスの中で開くフォルダー、使用するコンテンツ ビューを指定するには、さらに複雑な Web パーツ URL を使用する場合があります。

ネットワークに適用されているセキュリティ手段によっては、Web パーツ URL のエンコーディングの構成が必要になる場合があります。エンコーディングを構成すると、UI の背後にあるコードが、URL エンコード パラメーターを使用して URL を作成します。URL エンコード パラメーターでは、空白の代わりに %20 が、またパス区切り文字 "/" の代わりに %2f が使用されます。このトピックのすべての例では、エンコードされたパラメーターを使用します。

次の表は、Web パーツのパラメーターとその使用例の一覧です。

### Web パーツのパラメーターとその使用方法

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>URL パラメーター</th>
<th>説明</th>
<th>値と例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>サーバー名とディレクトリ (必須)</p></td>
<td><p>Outlook Web App 仮想ディレクトリの URL。</p></td>
<td><p>これは、ユーザーが Outlook Web App へのサインインに使用するもとの同じ URL の場合があります。次はその例です。</p>
<p>https://&lt;<em>server name</em>&gt;/owa</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 の明示的なログオン メールボックス ID (省略可能)</p></td>
<td><p>開くメールボックスに関連付けられている任意の SMTP アドレス。</p>
<p>URL のこのセクションがないと、認証されたユーザーの既定のメールボックスが開きます。</p>
<p>他のパラメーターが指定されていない場合は、既定の動作として受信トレイが開きます。</p></td>
<td><p>SMTP アドレス tsmith@fourthcoffee.com のメールボックスを開くには、次の URL を使用します。</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd (明示的なログオン メールボックス ID 以外のパラメーターを指定する場合は必須)</p></td>
<td><p>?cmd=contents は、完全な Outlook Web App ユーザー インターフェイスの代わりにパラメーターで指定されている Outlook Web App Web パーツを表示します。</p></td>
<td><p>メールボックスが指定されていない場合は、cmd パラメーターは次のように、サインイン アドレスの後に記述します。</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents</p>
<p>メールボックスが指定されている場合は、cmd パラメーターは次のように、明示的なメールボックス ID の後に記述します。</p>
<p>https://&lt;<em>server name</em>&gt;/owa/&lt;<em>SMTP address</em>&gt;/?cmd=contents</p>
<p>他のパラメーターが指定されていない場合は、既定の動作として受信トレイが開きます。</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>LiveID 認証を使用する場合は、このパラメーターを含める必要があります。</p>
<p>&quot;exsvurl=1&quot; が存在しない場合は、LiveID 認証時にすべてのパラメーターが破棄されます。このパラメーターは、Office 365 のメールボックスにのみ適用されます。</p></td>
<td><p>https://&lt;server name&gt;/owa/?cmd=contents&amp;exsvurl=1</p></td>
</tr>
<tr class="odd">
<td><p>fpath (省略可能)</p></td>
<td><p>URL のこの部分は、ファイアウォールを通過できるように、URL エンコーディングを使用して記述することが必要になる場合があります。</p>
<p>URL エンコーディングを使用するときは、空白は %20 になり、パス区切り文字 (/) は %2f になります。</p>
<p>フォルダーの階層は、メールボックス ルートから開始する必要があります。</p>
<p>このフォルダー パスは、通常のフォルダーまたは検索フォルダーを示すことができます。</p></td>
<td><p>受信トレイのサブフォルダー Projects を開くには、次の URL を使用します。</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;fpath= inbox%2fprojects</p></td>
</tr>
<tr class="even">
<td><p>module (省略可能)</p></td>
<td><p>このパラメーターを使用すると、ローカライズされた名前を知らなくても、既定フォルダーを指定できます。</p></td>
<td><p>module パラメーターの値では大文字と小文字は区別されず、次の値を使用できます。</p>
<ul>
<li><p>Inbox</p></li>
<li><p>Calendar</p></li>
<li><p>Teammailbox</p></li>
</ul>
<p>ローカライズに関係なくメールボックスの予定表を開くには、次の URL を使用します。</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;module=calendar</p></td>
</tr>
<tr class="odd">
<td><p>view (省略可能)</p></td>
<td><p>このパラメーターは、フォルダーに対して表示するビューを指定します。</p>
<p>このパラメーターを指定しない場合の既定のビューは、次のとおりです。</p>
<ul>
<li><p>Calendar   Daily</p></li>
<li><p>Messages   Messages</p></li>
</ul>

> [!NOTE]
> 既定のビューの文字列は、自動的に URL でエンコードされます。


<p>ビューの既定の並べ替えは、フォルダーが Outlook Web App クライアントで開かれる場合の並べ替え方法です。</p>
<p>ビューを識別する文字列はローカライズされず、大文字と小文字は区別されません。</p></td>
<td><p>使用できるビューは、フォルダーの種類によって異なります。</p>
<p>Calendar のビュー :</p>
<ul>
<li><p>Daily   日単位の予定表のビュー</p></li>
<li><p>Weekly   週単位の予定表のビュー</p></li>
<li><p>Monthly   月単位の予定表のビュー</p></li>
</ul>
<p>Message のビュー :</p>
<ul>
<li><p>Messages   メッセージ ビュー、既定の並べ替え</p></li>
<li><p>By%20Sender   送信元で並べ替えられたメッセージ ビュー (&quot;a&quot; から始まる送信者名が最初に配置される)</p></li>
<li><p>By%20Subject   件名で並べ替えられたメッセージ ビュー (&quot;a&quot; から始まる件名が最初に配置される)</p></li>
<li><p>By%20Conversation%20Topic   スレッド ビュー、Outlook Web App の Light バージョンでは利用できません</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d、m、y (省略可能)</p></td>
<td><p>予定表を表示する日付を指定します。これらのパラメーターは、任意の順序で指定でき、単独でも複数を組み合わせても使用できます。</p>
<p>これらのパラメーターを指定しない場合の既定値は、当日の年、月、日の値です。たとえば、当日が 2016 年 5 月 3 日で、月の値に 9 月を示す &quot;9&quot; を指定すると、表示される日付は 2016 年 9 月 3 日になります。</p></td>
<td><p>日付パラメーターの有効な値は次のとおりです。</p>
<p>d=[1 から 31]</p>
<p>m=[1 から 12]</p>
<p>y=[4 桁の年]</p>
<p>2016 年 5 月 3 日の日付の予定表を開くには、次の URL を使用します。https://&lt;<em>server name</em>&gt;/owa/?cmd=content&amp;fpath=calendar&amp;view=daily&amp;d=3&amp;m=5&amp;y=2016</p></td>
</tr>
<tr class="odd">
<td><p>part (省略可能)</p></td>
<td><p>小さい Web パーツを表示するよう Outlook Web App に指定します。</p></td>
<td><p>Web パーツを使用して Outlook Web App のコンテンツにアクセスするとき、表示される UI は、完全な Outlook Web App UI より小さくなります。part パラメーターは、UI をさらに小さくします。次の URL の例では、最小の Web パーツ形式でタスクの一覧を表示します。</p>
<p>https://&lt;<em>server name</em>&gt;/owa/?cmd=contents&amp;part=1</p>
<p>この part パラメーターは、予定表モジュールには適用されません。</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>このパーツ パラメーターには、ユーザーがサブフォルダーを切り替えるためのフォルダー リスト コントロールが含まれています。これは、メール フォルダーにのみ適用されます。</p></td>
<td><p>https://&lt;server name&gt;/owa/?cmd=contents&amp;folderlist=1</p></td>
</tr>
</tbody>
</table>


## Outlook Web App の Web パーツの手入力

Outlook Web App の Web パーツは、Web ブラウザーで手動で入力することもできます。たとえば、ユーザーは、Outlook Web App Web パーツの URL を使用して、別のユーザーの予定表を開くことができます。

次の例では、Outlook Web App の一般的なビューに直接アクセスする方法を示します。

  - **受信トレイ:**  https://*\<server name\>*/owa/?cmd=contents\&module=inbox

  - **予定表 (今日):** https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&exsvurl=1

  - **予定表 (週):**  https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=weekly\&exsvurl=1

  - **予定表 (月):**  https://*\<server name\>*/owa/?cmd=contents\&module=calendar\&view=monthly\&exsvurl=1

## 詳細情報

  - [Outlook Web App サインイン、言語選択、エラー ページをカスタマイズする](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [Outlook Web App のテーマの作成](create-a-theme-for-outlook-web-app-exchange-2013-help.md)

