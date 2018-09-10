---
title: 'Exchange Search によってインデックス処理されるメッセージのプロパティ: Exchange 2013 Help'
TOCTitle: Exchange Search によってインデックス処理されるメッセージのプロパティ
ms:assetid: a9754dc1-44aa-4076-8b59-a5d39246d5b0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ983804(v=EXCHG.150)
ms:contentKeyID: 52057850
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Search によってインデックス処理されるメッセージのプロパティ

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-17_

Exchange Search は、電子メール メッセージの送信者、受信者、メッセージ本文、添付ファイルなど、多くの項目のプロパティをインデックス処理します。

## Exchange Search によってインデックス処理されるプロパティ

次の表に、Exchange Search によってインデックス処理されるすべての項目のプロパティの一覧を示します。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>種類</th>
<th>クエリ可能</th>
<th>検索可能</th>
<th>取得可能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Account</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Assistantname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>添付ファイル</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Attachmentfilenames</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Attachmentmetaproperties</p></td>
<td><p>文字列</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Attachmentcount</p></td>
<td><p>整数</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Businessaddress</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Businessmainphone</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Businessphonenumber</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Carphonenumber</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>カテゴリ</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Companyname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Compositeitemid</p></td>
<td><p>文字列</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Conversationid</p></td>
<td><p>整数</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>Conversationtopic</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Departmentname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Displayname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Displaynameprefix</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Documentid</p></td>
<td><p>整数</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Emailaddress</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Emaildisplayname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Emailoriginaldisplayname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Errorcode</p></td>
<td><p>整数</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Fileas</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Firstname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Folderid</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>From</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Homeaddress</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Homephone</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>整数</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Ispartiallyprocessed</p></td>
<td><p>ブール値</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Ispermanentfailure</p></td>
<td><p>ブール値</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>Itemclass</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Lastattempttime</p></td>
<td><p>DateTime</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Lastname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Mailboxguid</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Manager</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Meetinglocation</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Middlename</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Mobilephonenumber</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Nickname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Officelocation</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Otheraddress</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Primarytelephonenumber</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>DateTime</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Receivedby</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Receivedrepresenting</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Recipients</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>DateTime</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Sharinginfo</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>整数</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Tasktitle</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Title</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Umaudionotes</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Watermark</p></td>
<td><p>整数</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Yomicompanyname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>Yomifirstname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>Yomilastname</p></td>
<td><p>文字列</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
</tbody>
</table>


**インデックス処理されるプロパティのメモ**:

  - Outlook Web App などの検索クライアントによる AQS クエリでは、**クエリ可能なプロパティ**を `property:value` ペアの形式で使用できます (例: `from:bsuneja@cotoso.com`)。前の表にリストされたクエリ可能なプロパティのサブセットは、インプレース電子情報開示の検索クエリにも使用できます。これらのプロパティの一覧については、「[インプレース電子情報開示のためのメッセージ プロパティと検索演算子](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/message-properties-and-search-operators)」を参照してください。

  - **検索可能なプロパティ**は、`property:value` ペアでは指定できないプロパティですが、これが検索可能なプロパティに含まれていれば、キーワード検索によって値が返されます。たとえば、`body:Contoso` を使用してメッセージ本文内の文字列 `contoso` のみを検索することはできません。ただし、この文字列を検索すると、検索可能なプロパティに含まれているプロパティを持つすべての項目が返されます。

  - `documenteid` や `ispartiallyprocessed` などの**取得可能なプロパティ**が検索するたびに返されます。

