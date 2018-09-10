---
title: 'メッセージング レコード管理用のパフォーマンス カウンター: Exchange 2013 Help'
TOCTitle: メッセージング レコード管理用のパフォーマンス カウンター
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51407566
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージング レコード管理用のパフォーマンス カウンター

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

本トピックのパフォーマンス カウンターは管理フォルダー アシスタントを監視します。管理フォルダー アシスタントは Microsoft Exchange Server 2010 のメッセージング レコード管理 (MRM) を実装します。管理フォルダー アシスタントの実行はリソースを多く消費するため、サーバーが追加の負荷に耐えられる場合にのみ実行してください。また、管理フォルダー アシスタントの実行中はサーバーのパフォーマンスを監視してください。このトピックで示すパフォーマンス カウンターに加えて、ディスク パフォーマンスや CPU の使用量などを監視する他のパフォーマンス カウンターも使用できます。

MRM を実行するコンピューターの監視の詳細については、「[メッセージング レコード管理の監視](monitoring-https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/messaging-records-management/messaging-records-management)」を参照してください。

## MRM のパフォーマンス カウンター

次の表では、MRM のパフォーマンス カウンターについて説明します。

### パフォーマンス カウンター、パフォーマンス オブジェクト、および説明

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>パフォーマンス カウンター</th>
<th>パフォーマンス オブジェクト</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Average Mailbox Processing Time In Seconds</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>時間ベースのアシスタントに対するメールボックスの平均処理時間です。</p></td>
</tr>
<tr class="even">
<td><p>Mailboxes Processed</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>サービスが開始してから時間ベースのアシスタントが処理したメールボックスの数です。</p></td>
</tr>
<tr class="odd">
<td><p>Mailboxes processed/sec</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>時間ベースのアシスタントによって 1 秒間に処理されるメールボックスの数を決定します。</p></td>
</tr>
<tr class="even">
<td><p>Items Deleted but Recoverable</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>最新のスケジュール間隔の開始以降に、管理フォルダー アシスタントによって削除されたアイテムの数です(アイテムは、回復可能なアイテム フォルダーから回復可能です)この値は、スケジュール間隔中に処理されるように予定されたメールボックス内のアイテムと、処理するように指定した任意のメールボックス内のアイテムの合計数です。このカウンターは、各スケジュール間隔の開始時に 0 にリセットされます。</p></td>
</tr>
<tr class="odd">
<td><p>Items Journaled</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>最新のスケジュール間隔の開始以降、管理フォルダー アシスタントによって記録されたアイテムの合計数です。この数値には、現在の作業サイクル中に処理がスケジュールされたメールボックス内の項目数、および処理対象として指定したメールボックス内の項目数が含まれます。このカウンターは、各作業サイクルの開始時に 0 にリセットされます。</p></td>
</tr>
<tr class="even">
<td><p>Items Marked as Past Retention Date</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>最新のスケジュール間隔の開始以降に、管理フォルダー アシスタントによって保存期限切れとマークされたアイテムの数です。この数値には、スケジュール間隔中に処理がスケジュールされたメールボックス内の項目数、および処理対象として指定したメールボックス内の項目数が含まれます。このカウンターは、各スケジュール間隔の開始時に 0 にリセットされます。</p></td>
</tr>
<tr class="odd">
<td><p>Items Moved</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>最新のスケジュール間隔の開始以降に、管理フォルダー アシスタントによって移動されたアイテムの数です。この数値には、スケジュール間隔中に処理がスケジュールされたメールボックス内の項目数、および処理対象として指定したメールボックス内の項目数が含まれます。このカウンターは、各スケジュール間隔の開始時に 0 にリセットされます。</p></td>
</tr>
<tr class="even">
<td><p>Items Permanently Deleted</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>最新のスケジュール間隔の開始以降に、管理フォルダー アシスタントによって完全に削除されたアイテムの数です。この数値には、スケジュール間隔中に処理がスケジュールされたメールボックス内の項目数、および処理対象として指定したメールボックス内の項目数が含まれます。このカウンターは、各スケジュール間隔の開始時に 0 にリセットされます。</p></td>
</tr>
<tr class="odd">
<td><p>Items Subject to Retention Policy</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>最新のスケジュール間隔の開始以降に、管理フォルダー アシスタントのアイテム保持ポリシーに従う必要のあるアイテムの数です。この数値には、スケジュール間隔中に処理がスケジュールされたメールボックス内の項目数、および処理対象として指定したメールボックス内の項目数が含まれます。このカウンターは、各スケジュール間隔の開始時に 0 にリセットされます。このカウンターは、次に示す 4 つの有効期限関連カウンターの合計です。</p>
<ul>
<li><p>Items Journaled</p></li>
<li><p>Items Marked as Past Retention Date</p></li>
<li><p>Items Moved</p></li>
<li><p>Items Permanently Deleted</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - Size of Items subject to Retention Policy (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>管理フォルダー アシスタントによって終了した項目の合計サイズを示します (SoftDelete、HardDelete、MoveToArchive)。</p>
<p>以下の項目が含まれます。</p>
<ul>
<li><p>管理フォルダー メールボックス ポリシーにより、削除や管理カスタム フォルダーへの移動対象となったメッセージ</p></li>
<li><p>ユーザーのアイテム保持ポリシーにより、削除やアーカイブへの移動対象となったメッセージ</p></li>
<li><p>収集ポリシーにより終了するメッセージ</p></li>
<li><p>システム クリーンアップ タグによりクリーンアップされるメッセージ</p></li>
</ul>
<p>このカウンターは、管理フォルダー アシスタントの作業サイクルの各作業サイクル チェックポイントで 0 にリセットされます。</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - Size of Items Deleted but Recoverable (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>管理フォルダー アシスタントにより完全に削除された項目の合計サイズを示します。</p>
<p>以下の項目が含まれます。</p>
<ul>
<li><p>管理フォルダー メールボックス ポリシーにより削除 (回復可能) されたメッセージ</p></li>
<li><p>アイテム保持ポリシーにより削除 (回復可能) されたメッセージ</p></li>
</ul>
<p>このカウンターは、管理フォルダー アシスタントの作業サイクルの各作業サイクル チェックポイントで 0 にリセットされます。</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - Size of Items Permanently Deleted (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>管理フォルダー アシスタントにより完全に削除された項目の合計サイズを示します。</p>
<p>以下の項目が含まれます。</p>
<ul>
<li><p>管理フォルダー メールボックス ポリシーにより物理的に削除されたメッセージ</p></li>
<li><p>アイテム保持ポリシーにより物理的に削除されたメッセージ</p></li>
<li><p>回復可能なアイテム ポリシーにより物理的に削除されたメッセージ</p></li>
</ul>
<p>このカウンターは、管理フォルダー アシスタントの作業サイクルの各作業サイクル チェックポイントで 0 にリセットされます。</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - Size of Items Moved due to an Archive policy tag (In Bytes)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>管理フォルダー アシスタントにより、フォルダーやアーカイブに移動した項目の合計サイズを示します。</p>
<p>以下の項目が含まれます。</p>
<ul>
<li><p>管理フォルダー メールボックス ポリシーにより、管理カスタム フォルダーに移動したメッセージ</p></li>
<li><p>アイテム保持ポリシーにより個人アーカイブに移動したメッセージ</p></li>
</ul>
<p>このカウンターは、管理フォルダー アシスタントの作業サイクルの各作業サイクル チェックポイントで 0 にリセットされます。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - Items stamped with Personal Tag (Expiry or Archive)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>ユーザーが個人タグを使用して項目にタグ付けした回数を示します。</p>
<p>これには、削除とアーカイブの両方のタグが含まれます。</p>
<p>次に例を示します。</p>
<ul>
<li><p>個人タグでタグ付けされた項目。</p></li>
<li><p>個人タグの付いた項目が、別の個人タグで再度タグ付けされます。</p></li>
</ul>
<p>フォルダーが個人タグでタグ付けされると、カウンターはそのフォルダー内の項目の合計数だけ増加します。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - Items stamped with Default Tag (Expiry or Archive)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>ユーザーの操作 (ユーザーが個人タグの付いたメッセージを選択し <strong>[フォルダー ポリシーの使用]</strong> を選択するなど) に基づいて、既定のポリシー タグ (DPT) が割り当てられた項目数を示します。</p>
<p>新しいユーザーにDPT の付いたアイテム保持ポリシーが割り当てられると、カウンターはアイテム保持ポリシーによって DPT が割り当てられる項目数だけ増加します。</p>

> [!NOTE]
> ユーザーに DPT の付いたアイテム保持ポリシーが割り当てられている場合、トランスポート経由で届く新規メッセージには既定タグが付けられ、このカウンターでは追跡されません。


</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - Items stamped with System Cleanup Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>システム クリーンアップ タグがタグ付けされた項目数を示します。これには、ユーザーに表示されないメールボックス メタデータ項目が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - Items expired due to a default Expiry Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>アイテム保持ポリシー内の個人以外 (既定やシステム) のタグのために管理フォルダー アシスタントによって終了した (削除 (回復可能) または削除された) アイテムの数を示します。</p>
<p>これには、回復可能なアイテムのクリーン アップやシステム クリーン アップによって終了したアイテムは含まれません。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - Items expired due to a personal Expiry Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>アイテム保持ポリシー内の個人タグのために管理フォルダー アシスタントにより終了した (削除 (回復可能) または物理的に削除された) 項目数を示します。</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - Items moved due to a default Archive Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>アイテム保持ポリシー内の個人以外 (既定やシステム) のタグのために管理フォルダー アシスタントによりアーカイブに移動した項目数を示します。</p>
<p>これには、回復可能なアイテムのクリーン アップにより、アーカイブの回復可能なアイテム フォルダーに移動したアイテムは含まれません。</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - Items Moved due to an Archive Tag</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>アイテム保持ポリシー内の個人タグのために管理フォルダー アシスタントによりアーカイブに移動した項目数を示します。</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - Mailbox Dumpsters Moved Items</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>回復可能なアイテムのクリーン アップにより、アーカイブの回復可能なアイテム フォルダーに移動したアイテムの数を示します。</p></td>
</tr>
</tbody>
</table>

