---
title: 'パブリック フォルダーの制限: Exchange 2013 Help'
TOCTitle: パブリック フォルダーの制限
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170893
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダーの制限

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange Server 2013 では、パブリック フォルダーを従来のデータベース アーキテクチャからメールボックス アーキテクチャに移行しました。この変更により、データベース可用性グループ (DAG) の復元や、長年の間に拡張されたメールボックスのその他の機能のメリットをパブリック フォルダーで活用できます。ただし、新しい制限やパフォーマンスの問題などを考慮する必要があります。この資料では、パブリック フォルダーのパフォーマンスと接続性に影響を与える可能性のある構成オプションの概要について説明します。

## 制限

以下の表に、オンプレミスの Exchange Server 2013 のパブリック フォルダーに関する制限をまとめます。制限に推奨と記されていない限りは、この表に記載されている値はパブリック フォルダーでサポートされている制限です。


> [!IMPORTANT]
> Office 365 の Exchange Online の制限については、「<A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online の制限</A>」を参照してください。




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>制限</th>
<th>注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>パブリック フォルダーのメールボックスの合計数</p></td>
<td><p>100</p></td>
<td><p>100 を超える数のパブリック フォルダー メールボックスを作成できますが、これはサポートされていません。<a href="https://docs.microsoft.com/ja-jp/exchange/collaboration-exo/public-folders/create-public-folder-mailbox">パブリック フォルダー メールボックスを作成する</a></p></td>
</tr>
<tr class="even">
<td><p>階層内のパブリック フォルダーの総数</p></td>
<td><p>1,000,000</p></td>
<td><p>1,000,000 を超える数のパブリック フォルダーを作成できますが、これはサポートされていません。100,000 以上のパブリック フォルダーを展開する場合、「<a href="considerations-when-deploying-public-folders-exchange-2013-help.md">パブリック フォルダーを展開するときの考慮事項</a>」を参照することをお勧めします。</p></td>
</tr>
<tr class="odd">
<td><p>親フォルダーの下のサブフォルダー</p></td>
<td><p>10,000</p></td>
<td><p>1 つの親フォルダーの下に 1,000 を超えるサブフォルダーを作成することは可能ですが、推奨されていません。</p>
<p><a href="https://technet.microsoft.com/ja-jp/library/bb123981(v=exchg.150)">Set-Mailbox</a> コマンドレットの <em>FolderHierarchyChildrenCountReceiveQuota</em> パラメーター。</p></td>
</tr>
<tr class="even">
<td><p>フォルダーの階層</p></td>
<td><p>300</p></td>
<td><p>フォルダーの階層とは、あるパブリック フォルダー ツリーの 1 つのブランチに存在できる入れ子になったフォルダーの階層数です。<a href="https://technet.microsoft.com/ja-jp/library/bb123981(v=exchg.150)">Set-Mailbox</a> コマンドレットの <em>FolderHierarchyDepthRecieveQuota</em> パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダー当たりの最大メッセージ数</p></td>
<td><p>100 万</p></td>
<td><p><a href="https://technet.microsoft.com/ja-jp/library/bb123981(v=exchg.150)">Set-Mailbox</a> コマンドレットの <em>MailboxMessagesPerFolderCountRecieveQuota</em> パラメーター。</p></td>
</tr>
<tr class="even">
<td><p>個々のパブリック フォルダーの最大サイズ</p></td>
<td><p>10 GB</p></td>
<td><p>この制限には、1 つのフォルダーの下にあるサブフォルダーは含まれません。</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">メールボックスのストレージ クォータを構成する</a></p></td>
</tr>
<tr class="odd">
<td><p>パブリック フォルダーのメールボックスのサイズ</p></td>
<td><p>100 GB</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">メールボックスのストレージ クォータを構成する</a></p></td>
</tr>
<tr class="even">
<td><p>パブリック フォルダーのメールボックスあたりのユーザー ログオン数</p></td>
<td><p>2,000 同時ユーザー ログオン</p></td>
<td><p>パブリック フォルダー メールボックスあたりのユーザー数が 2,000 を超えないように階層を構成することをお勧めします。たとえば、ユーザー数 が 20,000 であれば、パブリック フォルダー メールボックスの数を 10 にします。</p></td>
</tr>
<tr class="odd">
<td><p>移動された項目の保存期間</p></td>
<td><p>推奨値は 14 日間</p></td>
<td><p><strong>Set-OrganizationConfig</strong> コマンドレットの <em>DefaultPublicFolderMovedItemRetention</em> パラメーターを使用します。</p></td>
</tr>
<tr class="even">
<td><p>有効期限</p></td>
<td><p>通常のメールボックスで使用する既定値と同じ設定にすることをお勧めします。</p></td>
<td><p>これらの設定は、次のレベルで設定できます。</p>
<ul>
<li><p><strong>組織レベル:</strong> <strong>Set-OrganizationConfig</strong> コマンドレットの <em>DefaultPublicFolderAgeLimit</em> パラメーター。</p></li>
<li><p><strong>メールボックス レベル:</strong> <strong>Set-Mailbox</strong> コマンドレットの <em>AgeLimit</em> パラメーター。</p></li>
<li><p><strong>フォルダー レベル:</strong> <strong>Set-PublicFolder</strong> コマンドレットの <em>AgeLimit</em> パラメーター。</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>削除された項目の保存期間</p></td>
<td><p>通常のメールボックスで使用する既定値と同じ設定にすることをお勧めします。</p></td>
<td><p>これらの設定は、次のレベルで設定できます。</p>
<ul>
<li><p><strong>組織レベル:Set-OrganizationConfig コマンドレットの</strong> <em>DefaultPublicFolderMovedItemRetention</em> パラメーターを使用します。</p></li>
<li><p><strong>メールボックス レベル:</strong> <strong>Set-Mailbox</strong> コマンドレットの <em>RetainDeletedItemsFor</em>。</p></li>
<li><p><strong>フォルダー レベル:</strong> <strong>Set-PublicFolder</strong> コマンドレットの <em>RetainDeleteItemsFor</em> パラメーター。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 に移行できるパブリック フォルダーの最大数</p></td>
<td><p>500,000</p></td>
<td><p>これは、1 回の移行で従来のバージョンの Exchange から Exchange 2013 に移動することができるパブリック フォルダーの最大数です。パブリック フォルダーの移行の詳細については、<a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">バッチ移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する</a> を参照してください。</p></td>
</tr>
</tbody>
</table>

