---
title: 'チェックリスト: アイテム保持ポリシーの展開: Exchange 2013 Help'
TOCTitle: 'チェックリスト: アイテム保持ポリシーの展開'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 49896260
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# チェックリスト: アイテム保持ポリシーの展開

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange Server 2013 組織に保持ポリシーを展開するには、このチェックリストを使用します。このチェックリストで作業を開始する前に、以下のトピックの概念精通している必要があります。

  - [メッセージング レコード管理](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/messaging-records-management)

  - [保持タグおよびアイテム保持ポリシー](retention-tags-and-retention-policies-exchange-2013-help.md)

## 保持ポリシーの展開のチェックリスト


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完了?</th>
<th>タスク</th>
<th>リソース</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>異なるユーザー セットに対するメッセージング レコード管理 (MRM) の要件を評価します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/messaging-records-management">メッセージング レコード管理</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>使用している Microsoft Outlook クライアントのバージョンを確認します。</p></td>
<td><p><code>%ExchangeInstallPath%Logging\RPC Client Access</code> にある RPC クライアント アクセスのログ ファイルを解析します。</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>保持タグを作成します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">アイテム保持ポリシーの作成</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>保持ポリシーを作成します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">アイテム保持ポリシーの作成</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>保持タグを保持ポリシーに追加します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/add-or-remove-retention-tags">アイテム保持ポリシーへの保持タグの追加、またはアイテム保持ポリシーからの保持タグの削除</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>メールボックスの保存機能を有効にします。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">メールボックスの保存機能を有効にする</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>テストのため、1 つのメールボックスに保持ポリシーを適用します。</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">メールボックスにアイテム保持ポリシーを適用する</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>オプション: 従来の Outlook クライアントにクライアント ブロックを実装します。</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">メッセージング レコード管理用に Outlook クライアントのブロックを構成する</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>ユーザーとのコミュニケーションとトレーニング活動を開始します。保持ポリシーが処理され、アイテムが移動または削除される期限を含めます。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>他のメールボックスにも保持ポリシーを適用します。</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">メールボックスにアイテム保持ポリシーを適用する</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>数日前に、期限についてユーザーに伝えます。</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>期限になったら、メールボックスから保存機能を削除します。</p></td>
<td><p><a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">メールボックスの保存機能を有効にする</a></p></td>
</tr>
</tbody>
</table>

