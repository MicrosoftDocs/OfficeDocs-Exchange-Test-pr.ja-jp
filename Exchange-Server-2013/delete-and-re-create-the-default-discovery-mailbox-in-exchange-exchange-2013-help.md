---
title: 'Exchange で既定の探索メールボックスを削除して再作成する: Exchange Online Help'
TOCTitle: Exchange で既定の探索メールボックスを削除して再作成する
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371322
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange で既定の探索メールボックスを削除して再作成する

 

_**適用先:** Exchange Online, Exchange Server 2013_

Exchange 管理シェルを使用すれば、既定の探索メールボックスを削除して、それを再作成し、それにアクセス許可を割り当てることができます。

## これを行う理由は何でしょうか。

Exchange Server 2013 と Exchange Online では、既定の探索メールボックスの最大サイズは 50 GB です。このメールボックスはインプレース電子情報開示の検索結果を格納するために使用されます。サイズ制限が変更される前は、組織で記憶域クォータを 50 GB 以上に増やすことができました。そのため、探索メールボックスは 50 GB 以上に拡大できました。50 GB を超える既定の探索メールボックスには、次の 3 つの問題点があります。

  - サポートされていない。

  - Office 365 に移行できない。

  - Exchange Server 2010 内の既定の探索メールボックスの場合は、Exchange Server 2013 にアップグレードできない。

この解決方法は、50 GB を超える既定の探索メールボックスからの検索結果を保存したいかどうかによって異なります。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>検索結果を保存したいか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>いいえ</p></td>
<td><p>このトピックの手順に従って、既定の探索メールボックスを削除してから再作成します。</p></td>
</tr>
<tr class="even">
<td><p>はい</p></td>
<td><p>「<a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Exchange の証拠開示用メールボックスのサイズを小さくする</a>」の手順に従います。</p></td>
</tr>
</tbody>
</table>


## Exchange 管理シェル を使用して既定の証拠開示用メールボックスを削除し、再作成する


> [!NOTE]
> 証拠開示用メールボックスは Exchange 管理センター (EAC) に表示されないため、EAC を使用することはできません。



1.  次のコマンドを実行して、既定の探索メールボックスを削除します。
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  メールボックスと対応する Active Directory ユーザー オブジェクトを削除するかどうかの確認を促すメッセージで、「**Y**」と入力してから、Enter を押します。
    
    次の手順で探索メールボックスを作成すると、Active Directory で新しいユーザー オブジェクトが作成されます。

3.  次のコマンドを実行して、既定の探索メールボックスを再作成します。
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  次のコマンドを実行して、既定の探索メールボックスを開いて検索結果を表示するために Discovery Management 役割グループのアクセス許可を割り当てます。
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all

