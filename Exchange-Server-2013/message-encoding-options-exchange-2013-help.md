---
title: 'メッセージ エンコーディング オプション: Exchange 2013 Help'
TOCTitle: メッセージ エンコーディング オプション
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 49896456
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージ エンコーディング オプション

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Exchange で使用できるメッセージ エンコーディング オプションは、メッセージの特性を指定します（例：MIME およびそれ以外の文字セット、バイナリ エンコーディング、添付ファイルの形式）。メッセージ エンコーディング オプションは、次の場所で指定できます。

  - リモート ドメイン設定

  - メール ユーザーおよびメール連絡先設定

  - Microsoft Outlook の設定
    
      - メッセージ形式
    
      - インターネット メッセージ形式
    
      - インターネット受信者のメッセージ形式
    
      - メッセージ文字セットのエンコーディング オプション

**コンテンツ**

リモート ドメインに送信されるメッセージのメッセージ エンコーディング オプション

メール ユーザーおよびメール連絡先のメッセージ エンコーディング オプション

Outlook で使用できるメッセージ エンコーディング オプション

Outlook Web App ではメッセージ エンコード オプションが利用可能

メッセージ エンコーディング オプションの優先順位

詳細情報

## リモート ドメインに送信されるメッセージのメッセージ エンコーディング オプション

リモート ドメインのメッセージ エンコーディング オプションを構成する場合、特定の設定が、そのドメインに送信されるすべてのメッセージに適用されます。組織のリモート ドメインでは、次の構成オプションを使ってメッセージをエンコードできます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>設定</strong></p></td>
<td><p><strong>Exchange Online 専用の EAC で利用可能</strong></p></td>
<td><p><strong>シェルで利用可能</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>MIME 文字セット</strong>   指定した文字セットは、文字セットが指定されていない MIME メッセージに対してのみ使用されます。このパラメーターを設定しても、送信メールに既に指定されている文字セットが上書きされることはありません。</p>
<p><strong>MIME以外の文字セット</strong>   この設定は、次の条件のいずれかが当てはまる場合に使用されます。</p>
<ul>
<li><p>リモート ドメインからの受信メッセージの MIME Content-Type: ヘッダー フィールドに <em>charset=</em> 設定の値がない場合。</p></li>
<li><p>リモート ドメインへの送信メッセージに、MIME 文字セットの値がない場合。</p></li>
</ul>
<p></p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p><strong>コンテンツの種類</strong>   リモート ドメインの受信者に送信される MIME メッセージのコンテンツの種類を指定できます。次の設定を使用できます。</p>
<ul>
<li><p><strong>MimeHtmlText</strong>   元のメッセージがテキスト メッセージの場合を除き、すべてのメッセージを HTML 書式を使用する MIME メッセージに変換します。元のメッセージがテキスト メッセージの場合、送信メッセージはテキスト書式を使用する MIME メッセージになります。これは既定の設定です。</p></li>
<li><p><strong>MimeText</strong>   すべてのメッセージを、テキスト書式を使用する MIME メッセージに変換します。</p></li>
<li><p><strong>MimeHtml</strong>   すべてのメッセージを、HTML 書式を使用する MIME メッセージに変換します。</p></li>
</ul></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p><strong>折り返しサイズ</strong>   電子メール メッセージの本文のテキストの 1 行に含めることができる最大文字数を指定できます。古い電子メール クライアント アプリケーションでは、1 行に 78 文字が優先される場合があります。このオプションは、シェルを使用する場合にのみ利用可能です。</p>
<p></p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メール ユーザーおよびメール連絡先のメッセージ エンコーディング オプション

メール連絡先またはメール ユーザーのメッセージ エンコーディング オプションを構成する場合、これらのオプションが、特定の受信者に送信されるすべてのメッセージに適用されます。組織内のメール連絡先とメール ユーザーには、メッセージ エンコーディング用の次の構成オプションがあります。

  - **UsePreferMessageFormat**   このパラメーターでは、メール連絡先で構成されているメッセージ形式の設定を、リモート ドメインで構成されているグローバル設定より優先するかどうかを指定します。この設定を無効にすると、Exchange はこの受信者について他のメッセージ エンコーディング オプションを無視します。メッセージ エンコーディングは、リモート ドメインの構成、またはメッセージ送信者が構成した設定により決定されます。

  - **MessageFormat**   このパラメーターは、メッセージ形式を指定します。メッセージ形式としてテキストまたは MIME を指定できます。この設定の値は、*MessageBodyFormat* パラメーターに依存しています。メッセージ本文が HTML または TextAndHtml の場合、このパラメーターを MIME に設定する必要があります。

  - **MessageBodyFormat**   このパラメーターは、メッセージ本文の形式を指定します。テキスト、HTML、または TextAndHtml を指定できます。この設定の値は、*MessageFormat* パラメーターに依存しています。メッセージ形式がテキストの場合、このパラメーターもテキストに設定する必要があります。

  - **MacAttachmentFormat**   このパラメーターは、メッセージの、Apple Macintosh オペレーティング システムの添付ファイルの形式を指定します。BinHex、UUEncode、AppleSingle、または AppleDouble を指定できます。この設定の値は、*MessageFormat* パラメーターに依存しています。メッセージ形式がテキストに設定されている場合は、このパラメーターを BinHex または UUEncode に設定する必要があります。メッセージ形式が MIME に設定されている場合は、このパラメーターを BinHex、AppleSingle、または AppleDouble に設定する必要があります。

メール ユーザーおよびメール連絡先のメッセージ エンコーディング オプションを設定するには、Exchange 管理シェルのこれらのパラメーターを使用する必要があります。詳細については、以下のトピックを参照してください。

  - [Enable-MailContact](https://technet.microsoft.com/ja-jp/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/ja-jp/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/ja-jp/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/ja-jp/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/ja-jp/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/ja-jp/library/aa995971\(v=exchg.150\))

ページのトップへ

## Outlook で使用できるメッセージ エンコーディング オプション

送信者は、次のどの段階でも Outlook でメッセージ エンコーディング オプションを指定できます。

  - 既定のメッセージ形式をテキストまたは HTML に構成する。

  - **\[オプション\]** タブの **\[形式\]** 領域を使用し、作成中にメッセージ形式をテキストまたは HTML に設定する。

  - Exchange 組織外のすべての受信者に送信されるメッセージのメッセージ エンコーディング オプションを構成する。これらのオプションは、*インターネット メッセージ形式*オプションと呼ばれます。これらはリモート受信者にのみ適用され、Exchange 組織の受信者には適用されません。

  - Exchange 組織外の特定の受信者に送信されるメッセージのメッセージ エンコーディング オプションを構成する。これらのオプションは*インターネット受信者メッセージ形式*オプションと呼ばれます。これらは連絡先フォルダーにあるリモート受信者にのみ適用され、Exchange 組織の受信者には適用されません。

既定では、Outlook は送信メッセージのテキスト全体をスキャンしてそのメッセージに使用する適切なエンコーディングを決定することで、自動文字セット メッセージ エンコーディングを使用します。この設定は、インターネット受信者、および Exchange 組織の受信者に送信されるメッセージに適用されます。ただし、これを省略し、送信メッセージの優先エンコーディングを指定できます。

ページのトップへ

## Outlook Web App ではメッセージ エンコード オプションが利用可能

送信者は、Outlook Web App のメッセージ エンコード オプションを、以下のいずれかの段階で指定することができます。

  - \[**設定**\] \> \[**オプション**\] \> \[**設定**\] ページの \[**メッセージ形式**\] セクションで、既定のメッセージ形式をテキストまたは HTML のどちらかに構成します。

  - メッセージ形式の設定は、\[**詳細オプション**\] (…) メニューを使用し、さらに \[**テキスト形式に切り替え**\] または \[**HTML に切り替え**\] を選択することで、テキストまたは HTML のどちらかに構成して行います。

ページのトップへ

## メッセージ エンコーディング オプションの優先順位

Exchange では、Exchange 組織外の受信者への送信メッセージに適用されるメッセージ エンコーディング オプションは、次に示す優先順位に従って決まります。

1.  リモート ドメインの設定

2.  Outlook または Outlook Web App の設定

3.  メール ユーザーまたはメール連絡先の設定

このリストでは、優先順位が低い順に上から下へ並べられています。優先順位の高い設定が低い設定よりも優先されます。

次の表で、最も低い順位から最も高い順位へ、メッセージ文字セット エンコーディング オプションの優先順位を説明します。

### メッセージ文字セット エンコーディング オプションの、最も低い順位から最も高い順位への優先順位

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ソース</th>
<th>パラメーター</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EAC または <strong>Set-RemoteDomain</strong> を使用したリモート ドメイン エントリの設定</p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>指定済み</p></td>
</tr>
<tr class="even">
<td><p>EAC または <strong>Set-RemoteDomain</strong> を使用したリモート ドメイン エントリの設定</p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>指定済み</p></td>
</tr>
<tr class="odd">
<td><p>Outlook の設定</p></td>
<td><p>メッセージ文字セット エンコーディング</p></td>
<td><ul>
<li><p>自動選択</p></li>
<li><p>指定済み</p></li>
</ul></td>
</tr>
</tbody>
</table>


Set-RemoteDomain に NonMimeCharacterSet を設定した場合、文字セットは次の種類のメッセージに割り当てられます。

  - 指定された文字セットが含まれない、構成済みのリモート ドメインへの送信メッセージ

  - 指定された文字セットが含まれない、構成済みのリモート ドメインからの受信メッセージ

トランスポート サーバーの Windows ANSI コード ページの値は、文字セットを次の種類のメッセージに割り当てるために使用されます。

  - 指定された文字セットが含まれない、内部メッセージ

  - 指定された文字セットが含まれるが、指定されたサーバー コード ページが含まれない、内部メッセージ

メッセージに、指定されているが無効な文字セットが含まれる場合、トランスポート サーバーは無効な文字セットを有効な文字セットに置換しようとします。

次の表で、最も低い順位から最も高い順位へ、テキスト形式のメッセージ エンコーディング オプションの優先順位を説明します。

### テキスト形式のメッセージ エンコーディング オプションの、最も低い順位から最も高い順位への優先順位

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ソース</th>
<th>パラメーター</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>0 ～ 132</p></li>
<li><p>無制限</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook の設定</p></td>
<td><p>メッセージ形式</p></td>
<td><p>テキスト</p></td>
</tr>
<tr class="odd">
<td><p>Outlook の設定</p></td>
<td><p>インターネット メッセージ形式</p></td>
<td><p>テキスト形式オプション :</p>
<ul>
<li><p>テキスト形式のメッセージを送信する際、添付ファイルを UUEncode でエンコードする</p></li>
<li><p><em>nn</em> 文字で自動的に文字列を折り返す</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook の設定</p></td>
<td><p>インターネット受信者のメッセージ形式</p></td>
<td><p>テキスト形式 :</p>
<ul>
<li><p>UUEncode 添付ファイルの形式の添付ファイルをエンコードする</p></li>
<li><p>BinHex Mac 添付ファイルの書式を使用する</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>値が <code>$false</code> の場合、または Exchange 組織で受信者がメール ユーザーまたはメール連絡先として定義されていない場合、メール ユーザーまたはメール連絡先の設定は無視される。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>Text</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>Text</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UuEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


次の表で、最も低い順位から最も高い順位へ、MIME メッセージ エンコーディング オプションの優先順位を説明します。

### MIME メッセージ エンコーディング オプションの、最も低い順位から最も高い順位への優先順位

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ソース</th>
<th>パラメーター</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook または Outlook Web App の設定</p></td>
<td><p>メッセージ形式</p></td>
<td><ul>
<li><p>テキスト</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook の設定</p></td>
<td><p>インターネット受信者のメッセージ形式</p></td>
<td><p>MIME メッセージ形式</p>
<ul>
<li><p>テキスト</p></li>
<li><p>テキストと HTML の両方</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>値が <code>$false</code> の場合、または Exchange 組織で受信者がメール ユーザーまたはメール連絡先として定義されていない場合、メール ユーザーまたはメール連絡先の設定は無視される。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>Text</p></li>
<li><p>Mime</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


ページのトップへ

## 詳細情報

[メッセージ エンコーディング オプション](message-encoding-options-exchange-2013-help.md)

[TNEF 変換オプション](tnef-conversion-options-exchange-2013-help.md)

[リモート ドメイン](remote-domains-exchange-2013-help.md)

[Exchange Online のリモート ドメイン](https://technet.microsoft.com/ja-jp/library/jj966211\(v=exchg.150\))

[メール ユーザーの管理](manage-mail-users-exchange-2013-help.md)

[メール連絡先の管理](manage-mail-contacts-exchange-2013-help.md)

[Outlook でメッセージ形式を変更する](https://go.microsoft.com/fwlink/p/?linkid=397890)

