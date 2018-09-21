---
title: 'メールボックス復元要求を管理する: Exchange 2013 Help'
TOCTitle: メールボックス復元要求を管理する
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50555828
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス復元要求を管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

メールボックスの復元要求は、未接続のメールボックスの復元に使用します。切断されたメールボックスとは、Active Directory のユーザー アカウントに関連付けられていない、Exchange メールボックス データベース内のメールボックスのことを指します。メールボックスは無効化、削除、または別のデータベースへの移動の際に切断されます。詳細については、「[未接続のメールボックス](disconnected-mailboxes-exchange-2013-help.md)」を参照してください。

切断されたメールボックスは、メールボックス データベースの削除済みメールボックスの保持設定で指定された期間内はメールボックス データベースに残ります。既定では、未接続のメールボックスは 30 日間保存されます。この保持期間中には、削除済みのメールボックスの内容を既存のメールボックスに復元 (コピー) できます。このトピックでは、シェルを使用してメールボックス復元要求を管理する方法について説明します。

切断されたメールボックスに関連する追加の管理タスクについては、次のトピックを参照してください。

[メールボックスの無効化または削除](disable-or-delete-a-mailbox-exchange-2013-help.md)

[無効にされたメールボックスを接続する](connect-a-disabled-mailbox-exchange-2013-help.md)

[削除されたメールボックスの接続または復元](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[回復可能な削除によって削除されたメールボックスを復元する](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[メールボックスの完全削除](permanently-delete-a-mailbox-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス復元要求」。

  - このトピックの手順は、シェルでのみ実行できます。EAC を使用して、メールボックス復元要求を管理することはできません。

  - すべてのメールボックス復元要求の *Identity* プロパティの値を表示するには、次のコマンドを実行します。
    
    ```powershell
Get-MailboxRestoreRequest | Format-Table Identity
```
    
    このトピックの手順を実行する際には、この ID 値を使用して特定のメールボックス復元要求を指定できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して復元要求のプロパティを表示する

メールボックス復元要求のプロパティを表示できます。これにより、メールボックス復元要求の状態に関する基本的な情報を確認できます。

すべてのメールボックス復元要求の *Identity* プロパティの一覧および値を表示するには、次のコマンドを実行します。

```powershell
Get-MailboxRestoreRequest | Format-Table Identity
```

ID を使用して、特定のメールボックス復元要求に関する情報を入手できます。

この例では、*Identity* パラメーターを使用して、復元要求 "Pilar Pinilla \\MailboxRestore" の状態が返されます。

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"
```

この例では、Pilar Pinilla ターゲット メールボックスの 2 番目の復元要求に関するすべての情報が返されます。

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List
```

この例では、復元元データベース MBD01 から復元される復元要求の状態を返します。

```powershell
Get-MailboxRestoreRequest -SourceDatabase MBD01
```

この例では、現在進行中のすべての復元要求が返されます。

```powershell
Get-MailboxRestoreRequest -Status InProgress
```

その他の役立つ状態には、`Queued`、`Completed`、`Suspended`、および `Failed` があります。

この例では、中断されているすべての復元要求が返されます。

```powershell
Get-MailboxRestoreRequest -Suspend $true
```

構文およびパラメーターの詳細については、「[Get-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829907\(v=exchg.150\))」を参照してください。

## Get-MailboxRestoreRequest の出力

既定では、**Get-MailboxRestoreRequest** コマンドレットは、要求の名前、データが復元される対象のメールボックス、および要求の状態を返します。次の表は、コマンドレットを **Format-List** コマンドレットにパイプ処理する場合に返される有用な情報を示しています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>復元対象の切断されたメールボックスを含むデータベースを指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>データの復元先のメールボックスを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>要求の名前を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Microsoft Exchange メールボックス レプリケーション サービス (MRS) により要求の詳細な状態が格納されるデータベースを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>要求の状態を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>要求が中断されているかどうかを指定します。作成時に <strong>New-MailboxRestoreRequest</strong> コマンドレットと <em>Suspend</em> パラメーターを使用することにより、メールボックスの復元を中断できます。また、メールボックスの復元操作が失敗した場合や、管理者が <strong>Suspend-MailboxRestoreRequest</strong> コマンドレットを使用することによっても中断できます。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>要求の ID を指定します。この ID は、復元先のメールボックス名と要求名を組み合わせたものです。</p></td>
</tr>
</tbody>
</table>


## 正常な動作を確認する方法

**Get-MailboxRestoreRequest** コマンドレットを実行して、メールボックス復元要求のプロパティを表示できることを確認します。コマンドレットによりエラーが返された場合は、正しい構文および ID を使用していることを確認します。場合によっては、コマンドレットが成功し、結果が返されない場合があります。たとえば、メールボックス復元要求を送信し、`Get-MailboxRestoreRequest -Status InProgress` コマンドを実行した場合に結果が返されず、復元要求がいずれも現在実行中ではない場合があります。

## シェルを使用して復元要求の統計を表示する

メールボックス復元要求の統計を表示できます。これにより、トラブルシューティング目的に使用できる詳細な情報を確認できます。

この例では、復元要求 danp\\MailboxRestore1 に関する既定の統計を返します。既定では、返される情報には、名前、メールボックス、状態、および達成率が含まれます。

```powershell
Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1
```

この例では、Dan Park のメールボックスに関する情報を返し、レポートを .csv ファイルへエクスポートします。

    Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv

この例では、*IncludeReport* パラメーターを使用し、結果を **Format-List** コマンドレットにパイプ処理することによって、Pilar Pinilla のメールボックスに対する復元要求に関する追加情報を返します。

    Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 

この例では、*IncludeReport* パラメーターを使用し、`Failed` の状態のすべての復元要求に関する追加情報を返し、コマンドを実行した場所にあるファイル AllRestoreReports.txt 内に情報を保存します。

    Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt

構文およびパラメーターの詳細については、「[Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ja-jp/library/ff829912\(v=exchg.150\))」と「[Get-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829907\(v=exchg.150\))」を参照してください。

## Get-MailboxRestoreRequestStatistics の出力

既定では、[Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ja-jp/library/ff829912\(v=exchg.150\)) コマンドレットは、要求の名前、要求の状態、ターゲット メールボックスのエイリアス、完了率を返します。次の表は、コマンドレットを **Format-List** コマンドレットにパイプライン処理する場合に返される、その他の有用な情報を示しています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>要求の名前を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>要求の状態を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>要求の状態に関する詳細情報を指定します。たとえば、<code>Status</code> 値が <code>InProgress</code> を返す場合、<code>StatusDetail</code> 値は、<code>InProgress</code> や <code>CreatingFolderHierarchy</code> など、<code>CopyingMessages</code> 状態の特定の段階を返します。</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>復元プロセスにおける要求の進捗状況を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>復元要求が中断されているかどうかを指定します。この値は、次のようなシナリオでは <code>true</code> です。</p>
<ul>
<li><p>MRS は、エラーが発生したため、要求を停止したか、停止中である。</p></li>
<li><p>管理者が要求を中断した。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>データの復元元のメールボックスの GUID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>データの復元元のメールボックスの階層のルート フォルダーを指定します。この値が空白の場合、データがフォルダー Top of Information Store から復元されます。</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>ソース メールボックスが置かれているデータベースの名前を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>復元対象のメールボックスが <code>Disabled</code> または <code>Soft-Deleted</code> であるかを指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>ターゲット メールボックスのエイリアスを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>メールボックスをアーカイブに復元しているかどうかを指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>ターゲット メールボックスの GUID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>データを復元する対象となるターゲット メールボックスの階層のルート フォルダーの名前を指定します。この値が空白の場合、データがフォルダー Top of Information Store に復元されます。</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>ターゲット メールボックスが置かれているデータベースの名前を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>ターゲット メールボックスの ID を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>復元処理中に含めるフォルダーの一覧を指定します。この値が空白の場合は、要求の作成時にフォルダーが指定されていません。すべてのフォルダーがメールボックスに復元されます (<em>ExcludeFolders</em> パラメーターを使用して特定のフォルダーを除外した場合は除きます)。</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>復元処理中に除外するフォルダーの一覧を指定します。この値が空白の場合、要求の作成時にフォルダーが指定されていません。すべてのフォルダーがメールボックスに復元されます (<em>IncludeFolders</em> パラメーターを使用して特定のフォルダーを含めた場合は除きます)。</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>要求を作成したときに回復可能なアイテム フォルダーが除外されたかどうかを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>ターゲット フォルダーとソース フォルダーに一致するメッセージが存在する場合に MRS が実行する操作を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>要求を処理するときに関連付けられているメッセージをコピーするかどうかを指定します。関連付けられたメッセージとは、ルール、ビュー、およびフォームに関する情報を持つ非表示のデータが含まれる、特別なメッセージです。</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>要求が破損したメッセージを検出した場合に MRS がスキップする無効なアイテムの数を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>コマンドで検出された破損メッセージの数を指定します。<em>BadItemsEncountered</em> 値が <em>BadItemLimit</em> 値より大きいと、要求が失敗します。</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>要求が MRS に対して開始された日時を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>MRS が復元要求の処理を開始した日時を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>要求に対して最後の変更が行われた日時を指定します。変更は、管理者または MRS によって行われた可能性があります。</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>要求が中断された日時を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>要求を完了するためにかかった時間を指定します。要求が <code>Failed</code> 状態の場合、この値は、要求が開始されてから要求が失敗するまでの時間を指定します。要求が完了していない場合、この値は、要求が開始されてから <strong>Get-MailboxRestoreRequestStatistics</strong> コマンドレットが実行されるまでの時間を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>要求が <code>Suspended</code> 状態であった時間を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>要求が <code>Failed</code> 状態であった時間を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>要求が <code>Queued</code> 状態であった時間を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>要求が <code>In Progress</code> 状態であった時間を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>高可用性により要求が停止した時間を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>要求を処理したクライアント アクセス サーバーの名前を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>復元された合計ファイル サイズ、または要求が <code>In Progress</code> 状態である場合は MRS が復元すると予測されるファイル サイズを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>復元されたアイテム数、または要求が <code>In Progress</code> 状態である場合は MRS が復元すると予測されるアイテム数を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>1 分あたりの転送されたバイト数の平均を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>転送されたアイテムの数を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>完了した要求の割合を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>削除されるまでに、完了した復元要求が保持される時間の長さを指定します。既定値は 30 日です。</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>要求が開始されていない場合、この値には、要求のキュー内の位置を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>エラーが発生した場合、この値は、エラー コードを指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>エラーが発生した場合、この値は、エラーの種類を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>エラーが発生した場合、この値は、エラーがターゲット メールボックスまたはソース メールボックスで発生したかを指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>エラーが発生した場合、この値は、エラー メッセージを指定します。この値には、中断に関するコメントも指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>要求が失敗した場合、この値には、要求が失敗した日時を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>要求が失敗した場合、この値は、エラー発生時に実行されていた操作に関する情報を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>要求が有効でなかった場合、この値は理由を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>MRS により要求の詳細な状態が格納されるデータベースを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>要求の ID を指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p><em>IncludeReport</em> パラメーターを使用していた場合、この値は、要求のトラブルシューティングに使用できる情報を指定します。</p></td>
</tr>
</tbody>
</table>


## 正常な動作を確認する方法

**Get-MailboxRestoreRequestStatistics** コマンドレットを実行して、メールボックス復元要求の統計を表示できることを確認します。コマンドレットによりエラーが返された場合は、復元要求の正しい ID を使用していることを確認します。

## シェルを使用して復元要求のプロパティを変更する

メールボックス復元要求が失敗した場合は、**Set-MailboxRestoreRequest** コマンドレットを使用して要求のプロパティを変更し、失敗から復元を試行できます。

この例では、Debra Garcia のメールボックスに対する復元要求 MailboxRestore1 が 10 個の破損メール ボックス アイテムをスキップすることを指定しています。

```powershell
Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10
```

この例では、Florence Flipo のメールボックスに対する復元要求 MailboxRestore1 が 100 個の破損アイテムをスキップすることを指定しています。*BadItemLimit* の値が 50 より大きいため、*AcceptLargeDataLoss* パラメーターを指定する必要があります。

    Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss

構文およびパラメーターの詳細については、「[Set-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829909\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

復元要求のプロパティが正常に変更されたことを確認するには、**Get-MailboxRestoreRequestStatistics** コマンドレットを実行して、復元要求の変更済みのプロパティを表示します。復元要求が正常に作成された場合は、*Status* プロパティの値が `Queued`、`InProgress`、または `Completed` になります。復元要求が完了した後には、回復可能な削除によって削除されたメールボックスの内容がターゲット メールボックスに表示されます。

構文およびパラメーターの詳細については、「[Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ja-jp/library/ff829912\(v=exchg.150\))」を参照してください。

## シェルを使用して復元要求を中断する

メールボックスのエクスポート要求が作成された後は、要求の状態が "`Completed`" になる前であればいつでも復元要求を中断できます。[Resume-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829908\(v=exchg.150\)) コマンドレットを使用して復元要求を再開するコマンド構文の詳細については、このトピックの後半の「シェルを使用して復元要求を再開する」を参照してください。

この例では、Pilar Pinilla のメールボックスに対する復元要求 MailboxRestore1 を中断します。

```powershell
Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

この例では、まずステータスが "`InProgress`" の復元要求をすべて取得し、次に "Resume after FY13Q2 Maintenance" という中断コメントと共に出力を **Suspend-MailboxRestoreRequest** コマンドレットにパイプ処理して、進行中の復元要求をすべて中断します。

    Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"

構文およびパラメーターの詳細については、「[Suspend-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829906\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックス復元要求が正常に中断されたことを確認するには、次のコマンドを実行します。

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

*Suspend* プロパティの値が `True` と等しい場合は、復元要求が正常に中断されています。また、*Status* プロパティの `Suspended` の値は、復元要求が中断されたことを示します。

## シェルを使用して復元要求を再開する

**Resume-MailboxRestoreRequest** コマンドレットを使用して、失敗または中断した復元要求を再開します。

この例では、復元要求 Pilar Pinilla\\MailboxRestore1 を再開します。

```powershell
Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

この例では、失敗の状態の復元要求をすべて再開します。

```powershell
Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest
```

構文およびパラメーターの詳細については、「[Resume-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829908\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

復元要求が再開されたことを確認するには、次のコマンドを実行します。

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

*Suspend* プロパティの値が `False` と等しい場合は、復元要求が正常に再開されています。また、*Status* プロパティの `InProgress` の値は、復元要求が再開されたことを示します。

## シェルを使用して復元要求を削除する

**Remove-MailboxRestoreRequest** コマンドレットを使用して、メールボックス復元要求を削除できます。メールボックス データが移動先メールボックスにコピーされ始めてから復元要求を削除した場合、コピーされたメールボックス データはターゲット メールボックス内に保持されます。


> [!NOTE]
> 前述したように、完了した復元要求は自動的に削除されるまで既定では 30 日間保持されます。



この例では、復元要求 Pilar Pinilla\\MailboxRestore1 を削除します。

```powershell
Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

この例では、Completed の状態の復元要求をすべて削除します。

```powershell
Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
```

この例では、*RequestGuid* パラメーターを使用して、MBXDB01 に格納されている要求に対する復元要求を取り消します。*RequestGuid* および *RequestQueue* パラメーターを必須とするパラメーター セットは、Microsoft Replication Service のデバッグ目的にのみ使用されます。このパラメーター セットは、Microsoft カスタマー サービス & サポートからの指示があった場合に限り使用してください。

```powershell
Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f
```

構文およびパラメーターの詳細については、「[Remove-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829910\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックス復元要求が正常に削除されたことを確認するには、次のコマンドを実行します。

```powershell
Get-MailboxRestoreRequest -Identity <identity of removed restore request>
```

このコマンドでは、復元要求が存在しないことを示すエラーが返されます。

**Get-MailboxRestoreRequest** コマンドレットを実行することもできます。復元要求が正常に削除された場合、復元要求は結果に含まれません。

