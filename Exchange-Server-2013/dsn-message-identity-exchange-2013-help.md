---
title: 'DSN メッセージ ID: Exchange 2013 Help'
TOCTitle: DSN メッセージ ID
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 49896306
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DSN メッセージ ID

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

カスタマイズされた配信状態通知 (DSN) メッセージは、その構文に基づいて識別できます。識別子とは、カスタマイズされた DSN メッセージの GUID、または次の値から構成される文字列です。

  - **Locale**   この変数は、DSN メッセージが表示される言語のロケールを指定します。**New-SystemMessage** コマンドで使用できるロケール コードの一覧については、「[システム メッセージでサポートされている言語](supported-languages-for-system-messages-exchange-2013-help.md)」を参照してください。

  - **Internal または External**   この変数は、DSN メッセージを内部の Microsoft Exchange Server 2013 組織に属する送信者にのみ送信するか、Exchange 組織の外部の送信者にも送信するかを指定します。Internal オプションは、内部の送信者に送信される DSN メッセージには特定の電子メール連絡先または解決を含めるが、組織外の送信者にはその情報を公開しない場合に使用します。

  - **DSN code**   この変数は、カスタマイズされた DSN メッセージの DSN コードを指定します。

DSN メッセージの識別子の構文は `<Locale>\<Internal or External>\<DSN code>` です。

DSN コードごとに、内部の送信者または外部の送信者、および異なるロケールを対象としたカスタマイズされた DSN メッセージを複数作成できます。たとえば、次の表に、DSN コード 5.1.2 と対応する DSN メッセージ ID 用に使用できるいくつかの構成を示します。

### DSN の構成と ID の例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>DSN 構成</th>
<th>DSN ID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DSN メッセージを内部の送信者に英語 (en) のロケールで表示します。</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>DSN メッセージを外部の送信者に英語 (en) のロケールで表示します。</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>DSN メッセージを内部の送信者に日本語 (ja) のロケールで表示します。</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>DSN メッセージを外部の送信者に日本語 (ja) のロケールで表示します。</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

