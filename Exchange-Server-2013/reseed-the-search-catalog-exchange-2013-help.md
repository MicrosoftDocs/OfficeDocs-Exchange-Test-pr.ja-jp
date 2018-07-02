---
title: '検索カタログを再シードする: Exchange 2013 Help'
TOCTitle: 検索カタログを再シードする
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52057840
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 検索カタログを再シードする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

メールボックス データベースのコピーのコンテンツ インデックス カタログが壊れた場合は、カタログを再シードする必要があります。壊れたコンテンツ インデックスは、アプリケーション イベント ログに次のイベントによって示されます。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント ID</th>
<th>レベル</th>
<th>ソース</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>エラー</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>&lt;<em>タイムスタンプ</em>&gt; に、このサーバー上の Microsoft Exchange インフォメーション ストア データベース &lt;<em>ID</em>&gt; のコピーで、検索カタログの破損が発生しました。エラーの詳細については、サーバー上のイベント ログで、その他の &quot;ExchangeStoreDb&quot; および &quot;MSExchange Search Indexer&quot; イベントを参照してください。'Update-MailboxDatabaseCopy' タスクを通してカタログを再シードすることをお勧めします。</p></td>
</tr>
</tbody>
</table>


メールボックス データベース コピーがデータベース可用性グループ (DAG) の一部となっているサーバーにある場合、別の DAG メンバーからコンテンツ インデックス カタログを再シードすることができます。

メールボックス データベースのコピーが唯一のコピーの場合、新しいコンテンツ インデックス カタログを手動で作成する必要があります。

Exchange Search に関連するその他の管理タスクについては、「[Exchange Search の手順](exchange-search-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。実際の再シード時間は、再シードするコンテンツ インデックス カタログのサイズによって異なる可能性があります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「Exchange Search (Exchange 検索)」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## メールボックス データベースが DAG の一部である場合にコンテンツ インデックス カタログを再シードする

DAG の一部であるサーバー上にメールボックス データベースがある場合は、次のいずれかの手順を使用します。

## 任意のソースからコンテンツ インデックス カタログを再シードする

この例では、データベースのコピーを持つ DAG の送信元サーバーから、メールボックス サーバー MBX1 上のデータベース コピー DB1 のコンテンツ インデックス カタログを再シードします。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

構文およびパラメーターの詳細については、「[Update-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335201\(v=exchg.150\))」を参照してください。

## 特定のソースからコンテンツ インデックス カタログを再シードする

この例では、メールボックス サーバー MBX1 のデータベース コピー DB1 のコンテンツ インデックス カタログを、このデータベースのコピーを持つメールボックス サーバー MBX2 から再シードします。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly

構文およびパラメーターの詳細については、「[Update-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335201\(v=exchg.150\))」を参照してください。

## メールボックス データベースのコピーが 1 つだけ存在する場合にコンテンツ インデックス カタログを再シードする

メールボックス データベースのコピーが 1 つだけ存在する場合、コンテンツ インデックス カタログを再作成することによって、検索カタログを手動で再シードする必要があります。

1.  次のコマンドを実行して、Microsoft Exchange Search サービスと Microsoft Exchange Search Host Controller サービスを停止します。
    
        Stop-Service MSExchangeFastSearch
    
        Stop-Service HostControllerService

2.  Exchange コンテンツ インデックス カタログを格納するフォルダーを削除、移動、または名前変更します。このフォルダーは、`%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single` という名前になります。たとえば、フォルダー `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD` を名前変更するかもしれません。
    

    > [!NOTE]
    > このフォルダーを削除すると、追加のディスク領域が使用可能になります。あるいは、トラブルシューティングの目的で保持するために、そのフォルダーを名前変更するか、移動するかもしれません。



3.  次のコマンドを実行して、Microsoft Exchange Search サービスと Microsoft Exchange Search Host Controller サービスを再起動します。
    
        Start-Service MSExchangeFastSearch
    
        Start-Service HostControllerService
    
    これらのサービスを再起動すると、Exchange Search はコンテンツ インデックス カタログを再構築します。

## 正常な動作を確認する方法

Exchange Search がコンテンツ インデックス カタログを再シードするにはしばらく時間がかかることがあります。再シード プロセスの状態を表示するには、次のコマンドを実行します。

    Get-MailboxDatabaseCopyStatus | FL Name,*Index*

検索カタログの再シードが進行中である場合、*ContentIndexState* プロパティの値は **\[クロール\]** になります。再シードが完了したら、この値は **\[正常\]** に変更されます。

