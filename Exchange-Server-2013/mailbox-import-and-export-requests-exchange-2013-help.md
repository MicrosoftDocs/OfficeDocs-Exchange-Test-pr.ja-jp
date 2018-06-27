---
title: 'メールボックスのインポート要求とエクスポート要求: Exchange 2013 Help'
TOCTitle: メールボックスのインポート要求とエクスポート要求
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 49895265
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスのインポート要求とエクスポート要求

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-07_

Exchange 管理シェルの **MailboxImportRequest** または **MailboxExportRequest** のコマンドレット セットで pst ファイルにデータのインポートやエクスポートができます。メールボックスのインポートまたはエクスポート要求を開始すると、Microsoft Exchange メールボックス レプリケーション サービス (MRS) によってこのプロセスが非同期的に実行されます。MRS はすべての Exchange 2010 クライアント アクセス サーバーに常駐し、メールボックスの移動と, .pst ファイルのインポートとエクスポートを担当するサービスです。

**目次**

メールボックス データのインポートやエクスポートをする理由

インポート要求とエクスポート要求を使用するメリット

考慮事項

メールボックス データをインポートする

メールボックス データのエクスポート

## メールボックス データのインポートやエクスポートをする理由

メールボックス データは以下のような場合にインポートやエクスポートします。

  - **規制順守要件を満たす**   メールボックスの内容を法的な証拠開示目的でエクスポートできます。エクスポートが完了したら、内容を特に規制順守要件用に使用されるメールボックスにインポートできます。

  - **ある時点でのメールボックスのスナップショットを作成する**   特定のメールボックスのスナップショットを作成することで、メールボックス データベースのバックアップ セット全体を保持する必要がなくなります。

  - **ユーザーの .pst ファイルを、そのユーザーのメールボックスや個人用アーカイブに移動する**   Microsoft Outlook ユーザーは、電子メールを .pst ファイルとしてローカルに保存できます。[New-MailboxImportRequest](https://technet.microsoft.com/ja-jp/library/ff607310\(v=exchg.150\)) コマンドレットを使用すると、データをユーザーの .pst ファイルからそのメールボックスまたは個人用アーカイブに移動できます。こうすれば、ユーザーのローカル コンピューターから Exchange サーバーに電子メールを簡単に転送できます。

## インポート要求とエクスポート要求を使用するメリット

Exchange 2013 でインポート要求とエクスポート要求の使用には、以下のようなメリットが考えられます。

  - Exchange 2013 には, .pst ファイルを読み書きできる .pst プロバイダーが組み込まれています。

  - インポートおよびエクスポート要求は非同期です。このプロセスは、キューイングおよび調整フレームワークを活用する MRS によって実行されます。

  - .pst ファイルは、直接ユーザーの個人用アーカイブにインポートできます。

  - 複数の .pst ファイルを同時にインポートまたはエクスポートできます。

  - .pst ファイルは、Exchange サーバーからアクセス可能な共有ネットワーク ドライブに常駐させることができます。

  - Exchange 2013 は、これらの .pst ファイルをサポートしています。Office Outlook 2007 および Outlook 2010 によって作成された Unicode ファイル

## 考慮事項

メールボックス データをインポートまたはエクスポートする前に、次のことを考慮します。

  - メールボックス データをインポートまたはエクスポートするには、Exchange サーバーからアクセス可能なネットワーク共有フォルダーを設定する必要があります。Exchange Trusted Subsystem グループに読み取り/書き込みのアクセス許可を付与して、そのグループがメールボックス データをインポートおよびエクスポートするネットワーク共有にアクセスできるようにする必要もあります。このアクセス許可を付与しない場合、Exchange が対象のメールボックスへの接続を確立できないというエラー メッセージが表示されます。

  - Outlook によってサポートされる .pst ファイルの最大サイズは 50 GB です。このため、50 GB を超える .pst ファイルをインポートしないことをお勧めします。50 GB を超えるメールボックスに対して複数の .pst ファイルを作成するには、含めるフォルダーまたは除外するフォルダーを指定するか、コンテンツ フィルターを使用します。

  - インポートおよびエクスポート要求は、移動要求とメールボックス復元要求も処理する MRS によって実行されます。すべての要求は MRS がキューに格納し、調整します。

  - メールボックス データのインポートとエクスポートには、ファイル サイズ、ネットワーク帯域幅、および MRS 調整に応じて数時間かかる場合があります。

  - パブリック フォルダーまたはパブリック フォルダー データベースにデータをインポートすることはできません。

## メールボックス データをインポートする

**MailboxImportRequest** コマンドレット セットを使用して, .pst ファイルからメールボックスまたは個人用アーカイブにメールボックス データをインポートします。次に, .pst ファイルからメールボックス データをインポートするときに指定できるオプションの一覧を示します。


> [!NOTE]
> データのインポート先にはメールボックスが存在しなければなりません。メールボックスを持たないユーザー アカウントにデータをインポートすることはできません。



  - データをインポートするユーザー アカウントは、エクスポート元であったユーザー アカウントと異なってかまいません。たとえば、john@contoso.com からデータをエクスポートして、そのデータを legaldiscovery@contoso.com にインポートできます。

  - アイテムをユーザーの個人用アーカイブにのみインポートするには、*IsArchive* パラメーターを指定します。

  - 関連付けられているフォルダー メッセージが .pst ファイルに存在する場合は、*AssociatedMessagesCopyOption* パラメーターを使用してそれらのメッセージをインポートできます。関連付けられたメッセージには、ルール、ビュー、およびフォームに関する情報を持つ、隠されたデータが含まれます。それらのデータが .pst ファイルにある場合、セーフティ ネットートからのメッセージがすべてインポートされます。

  - 特定のフォルダーを含めるか、除外するには、*IncludeFolders* パラメーターまたは *ExcludeFolders* パラメーターを使用します。

  - 回復可能なアイテム フォルダーを除外するには、*ExcludeDumpster* パラメーターを使用します。既定では、インポート要求にユーザーの回復可能なアイテム フォルダー (.pst ファイルに存在する場合) が含まれています。

## メールボックスのインポート要求コマンドレット

メールボックスのインポート要求には、次のコマンドレットを使用します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンドレット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>.pst ファイルをメールボックスまたは個人用アーカイブにインポートするプロセスを開始します。メールボックスごとに複数のインポート要求を作成できます。各要求には、一意な名前を設定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>要求の作成後または失敗した要求からの回復後に、インポート要求オプションを変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>インポート要求の作成後で、かつ要求の状態が [完了] になる前の任意の時点で要求を中断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>中断したインポート要求や失敗したインポート要求を再開します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>完全に完了したインポート要求や部分的に完了したインポート要求を削除します。完了したインポート要求が自動的に消去されることはありません。それらを削除するには、このコマンドレットを使用する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>インポート要求に関する一般的な情報を表示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>インポート要求に関する詳細情報を表示します。</p></td>
</tr>
</tbody>
</table>


## メールボックス データのエクスポート

**MailboxExportRequest** コマンドレット セットを使用して、メールボックス データを .pst ファイルにエクスポートします。1つまたは複数のメールボックスをエクスポートできますが、一度に 1 つの要求のみ各 .pst ファイルに書き込まれます。次に, .pst ファイルにメールボックス データをエクスポートするときに指定できるオプションの一覧を示します。

  - 個人用アーカイブ データをエクスポートするには、*IsArchive* パラメーターを使用します。

  - エクスポートするメッセージにフィルターを適用するには、*ContentFilter* パラメーターを使用します。メッセージ コンテンツ、添付ファイル、送信者、受信者、受信トレイのカテゴリ、重要度、メッセージの種類、メッセージのサイズ、およびメッセージの送信時刻、受信時刻、または有効期限でフィルターを適用できます。

  - 含めるフォルダーまたは除外するフォルダーを指定するには、*IncludeFolders* パラメーターまたは *ExcludeFolders* パラメーターを使用します。Exchange 2013 メールボックスからデータをエクスポートする場合、*ExcludeDumpster* パラメーターを使用して、回復可能なアイテム フォルダーを除外することもできます。

  - 関連付けられたメッセージをエクスポートするには、*AssociatedMessagesCopyOption* パラメーターを使用します。関連付けられたメッセージには、ルール、ビュー、およびフォームに関する情報を持つ、隠されたデータが含まれます。既定では、関連付けられたアイテムは .pst ファイルにコピーされません。

## メールボックスのエクスポート要求コマンドレット

メールボックスのエクスポート要求には、次のコマンドレットを使用します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンドレット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>プライマリ メールボックスまたは個人用アーカイブのデータを .pst ファイルにエクスポートするプロセスを開始します。メールボックスごとに複数のエクスポート要求を作成できます。各要求には、一意な名前を設定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>要求の作成後または失敗した要求の回復後に、エクスポート要求オプションを変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>エクスポート要求の作成後で、かつ要求の状態が [完了] になる前の任意の時点で要求を中断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>中断したエクスポート要求や失敗したエクスポート要求を再開します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>完全に完了したエクスポート要求や部分的に完了したエクスポート要求を削除します。完了したエクスポート要求が自動的に消去されることはありません。それらを削除するには、このコマンドレットを使用する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>エクスポート要求に関する一般的な情報を表示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ja-jp/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>エクスポート要求に関する詳細情報を表示します。</p></td>
</tr>
</tbody>
</table>

