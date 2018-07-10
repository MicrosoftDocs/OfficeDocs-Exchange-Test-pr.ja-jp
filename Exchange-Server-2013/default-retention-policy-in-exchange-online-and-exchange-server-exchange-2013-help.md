---
title: 'Exchange Online および Exchange Server の既定のアイテム保持ポリシー: Exchange Online Help'
TOCTitle: 既定のアイテム保持ポリシー
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625496
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Online および Exchange Server の既定のアイテム保持ポリシー

 

_**適用先:** Exchange Online, Exchange Server 2013_

Exchange は、Exchange Online および社内の Exchange 組織にアイテム保持ポリシー "Default MRM Policy" を作成します。このポリシーは、Exchange Online の新しいユーザーに自動的に適用されます。社内組織では、メールボックスのアーカイブを作成するときに、ポリシーが適用されます。いつでも、ユーザーに適用されるアイテム保持ポリシーを変更できます。

Default MRM Policy に含まれているタグを変更すること (保存の有効期限や保持アクションを変更するなど)、タグを無効にすること、またはポリシーを変更すること (そのタグを追加または削除する) ことができます。更新されたポリシーは、管理フォルダー アシスタントによって次回ポリシーが処理されたときにメールボックスに適用されます。

## Default MRM Policy にリンクされる保持タグ

次の表は、Default MRM Policy にリンクされる既定の保持タグの一覧です。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>種類</th>
<th>保存期限 (日)</th>
<th>保持アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>既定 - 2 年でアーカイブへ移動</p></td>
<td><p>既定ポリシー タグ (DPT)</p></td>
<td><p>730</p></td>
<td><p>アーカイブへ移動</p></td>
</tr>
<tr class="even">
<td><p>回復可能なアイテム - 14 日でアーカイブへ移動</p></td>
<td><p>[回復可能なアイテム] フォルダー</p></td>
<td><p>14</p></td>
<td><p>アーカイブへ移動</p></td>
</tr>
<tr class="odd">
<td><p>個人 - 1 年でアーカイブへ移動</p></td>
<td><p>個人タグ</p></td>
<td><p>365</p></td>
<td><p>アーカイブへ移動</p></td>
</tr>
<tr class="even">
<td><p>個人 - 5 年でアーカイブへ移動</p></td>
<td><p>個人タグ</p></td>
<td><p>1,825</p></td>
<td><p>アーカイブへ移動</p></td>
</tr>
<tr class="odd">
<td><p>個人 - アーカイブへ移動しない</p></td>
<td><p>個人タグ</p></td>
<td><p>該当なし</p></td>
<td><p>アーカイブへ移動</p></td>
</tr>
<tr class="even">
<td><p>1 週間で削除</p></td>
<td><p>個人タグ</p></td>
<td><p>7</p></td>
<td><p>削除して回復を許可する</p></td>
</tr>
<tr class="odd">
<td><p>1 か月で削除</p></td>
<td><p>個人タグ</p></td>
<td><p>30</p></td>
<td><p>削除して回復を許可する</p></td>
</tr>
<tr class="even">
<td><p>6 か月で削除</p></td>
<td><p>個人タグ</p></td>
<td><p>180</p></td>
<td><p>削除して回復を許可する</p></td>
</tr>
<tr class="odd">
<td><p>1 年で削除</p></td>
<td><p>個人タグ</p></td>
<td><p>365</p></td>
<td><p>削除して回復を許可する</p></td>
</tr>
<tr class="even">
<td><p>5 年で削除</p></td>
<td><p>個人タグ</p></td>
<td><p>1,825</p></td>
<td><p>削除して回復を許可する</p></td>
</tr>
<tr class="odd">
<td><p>削除しない</p></td>
<td><p>個人タグ</p></td>
<td><p>該当なし</p></td>
<td><p>削除して回復を許可する</p></td>
</tr>
</tbody>
</table>


## Default MRM Policy で実行できること


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>以下のことを行うことができます。</th>
<th>Exchange Online</th>
<th>Exchange Server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>新しいユーザーに Default MRM Policy を自動的に適用する</p></td>
<td><p>はい。既定で適用されます。必要なアクションはありません。</p></td>
<td><p>はい。新しいユーザーのアーカイブを作成する場合も、既定で適用されます。</p>
<p>後からユーザーのアーカイブを作成する場合、そのユーザーに既存のアイテム保持ポリシーがない場合に限り、ポリシーが自動的に適用されます。</p></td>
</tr>
<tr class="even">
<td><p>ポリシーにリンクされた保持タグの保有期間または保持アクションを変更する</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>ポリシーにリンクされた保持タグを無効にする</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>ポリシーに保持タグを追加する</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>ポリシーから保持タグを削除する</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>新しいユーザーに自動的に適用されるように別のポリシーを既定のアイテム保持ポリシーとして設定する</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
</tbody>
</table>


## 詳細情報

  - 保持タグは 1 つ以上のアイテム保持ポリシーにリンクできます。[保持タグおよびアイテム保持ポリシー](retention-tags-and-retention-policies-exchange-2013-help.md)の管理の詳細については、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

  - Default MRM Policy には、自動的にアイテムを削除する DPT は含まれていません (ただし、ユーザーがメールボックス アイテムに適用できる削除の保持アクションの個人タグは含まれています)。指定した期間が経過した後でアイテムを自動的に削除したい場合は、必要な削除アクションを指定した DPT を作成し、それをポリシーに追加できます。詳細については、「[アイテム保持ポリシーの作成](create-a-retention-policy-exchange-2013-help.md)」および「[アイテム保持ポリシーへの保持タグの追加、またはアイテム保持ポリシーからの保持タグの削除](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md)」を参照してください。

  - アイテム保持ポリシーはメールボックス ユーザーに適用されます。ユーザーのメールボックスとアーカイブに同じポリシーが適用されます。

