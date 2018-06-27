---
title: 'メッセージを検索して削除する - 管理者向けヘルプ: Exchange 2013 Help'
TOCTitle: メッセージを検索して削除する - 管理者向けヘルプ
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52057470
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メッセージを検索して削除する - 管理者向けヘルプ

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2017-12-20_

管理者は **Search-Mailbox** コマンドレットを使って、ユーザーのメールボックスを検索し、メールボックスからメッセージを削除できます。

1 回の手順でメッセージを検索して削除するには、**Search-Mailbox** コマンドレットに *DeleteContent* スイッチを指定して実行します。ただし、これを実行する場合、検索によって返される結果をプレビューしたり、メッセージのログを生成したりすることはできないため、削除するつもりのないメッセージを誤って削除してしまう可能性があります。メッセージが削除される前に、検索で見つかったメッセージのログをプレビューするには、**Search-Mailbox** コマンドレットに *LogOnly* スイッチを指定して実行します。

追加の予防手段として、*TargetMailbox* および *TargetFolder* パラメーターを使用して、最初にメッセージを別のメールボックスにコピーすることができます。これにより、削除されたメッセージに再度アクセスすることが必要になる場合のために、削除されたメッセージのコピーを保持できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分。実際の時間は、メールボックスのサイズと検索クエリによって異なる場合があります。

  - Exchange 管理センター (EAC) を使用して、これらの手順を実行することはできません。シェルを使用する必要があります。

  - ユーザーのメールボックスにあるメッセージを検索し、削除するためには、次の両方の管理役割を割り当てられる必要があります。
    
      - **Mailbox Search**   この役割が割り当てられると、組織内の複数のメールボックスでメッセージを検索できます。既定ではこの役割は管理者には割り当てられません。メールボックスを検索できるようにこの役割を自分自身に割り当てるには、探索管理役割グループのメンバーとして自身を追加します。「[Exchange の電子情報開示のアクセス許可を割り当てる](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)」を参照してください。
    
      - **Mailbox Import Export**   この役割が割り当てられると、ユーザーのメールボックスからメッセージを削除できます。既定では、この役割はどの役割グループにも割り当てられていません。ユーザーのメールボックスからメッセージを削除するために、"Mailbox Import Export" 役割を "組織管理" 役割グループに追加できます。詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - メッセージの削除を行うメールボックスで単一アイテムの回復が有効になっている場合は、最初にその機能を無効にする必要があります。詳細については、「[メールボックスの単一アイテムの回復を有効または無効にする](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md)」を参照してください。

  - メッセージの削除を行うメールボックスがホールドの対象になっている場合は、ホールドを解除してメールボックスのコンテンツを削除する前に、レコード管理または法務部門に確認することをお勧めします。承認を得た後、トピック「[回復可能なアイテム フォルダーのクリーンアップ](clean-up-the-recoverable-items-folder-exchange-2013-help.md)」に一覧表示されている手順に従います。

  - **Search-Mailbox** コマンドレットを使用して、最大 10,000 個のメールボックスを検索できます。10,000 以上のメールボックスを持つ Exchange Online 組織の場合は、コンプライアンス検索機能 (または対応する **New-ComplianceSearch** コマンドレット) を使用して無制限の数のメールボックスを検索できます。その後、**New-ComplianceSearchAction** コマンドレットを使用して、コンプライアンス検索によって返されたメッセージを削除できます。詳細については、「[Office 365 組織でメール メッセージの検索と削除を行う - 管理者向けヘルプ](https://go.microsoft.com/fwlink/p/?linkid=786856)」を参照してください。

  - (*SearchQuery* パラメーターを使用していて) 検索クエリが含まれている場合、**Search-Mailbox** コマンドレットは、検索結果で最大 10,000 個のアイテムを返します。したがって、検索クエリを含める場合は、**Search-Mailbox** コマンドを複数回実行して 10,000 を超えるアイテムを削除する必要があるかもしれません。

  - **Search-Mailbox**コマンドレットを実行すると、ユーザーのアーカイブ メールボックスも検索されます。同様に、 *DeleteContent*スイッチを使用して、 **Search-Mailbox**コマンドレットを使用する場合、プライマリのアーカイブ メールボックス内のアイテムは削除されます。これを防止するには、 *DoNotIncludeArchive*スイッチを含めることができます。 また、予期しないデータ損失が発生する可能性がありますので、有効に自動拡張のアーカイブを持つメールボックスをExchange Onlineでメッセージを削除するのには*DeleteContent*スイッチを使用しないことをお勧めします。

## メッセージを検索し、検索結果をログに記録する

この例は、April Stewart のメールボックスに対し、件名フィールドに「Your bank statement」という語句が含まれるメッセージを検索し、その結果を、管理者のメールボックスの SearchAndDeleteLog フォルダーに記録します。メッセージは、対象のメールボックスにコピーまたは対象のメールボックスから削除されません。

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

次の使用例は、組織内の全メールボックスでファイル名に「Trojan」という言葉が含まれるあらゆる種類の添付ファイルが付いたメッセージを検索し、管理者のメールボックスにログ メッセージを送信します。

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

構文およびパラメーターの詳細については、「[Search-Mailbox](https://technet.microsoft.com/ja-jp/library/dd298173\(v=exchg.150\))」を参照してください。

ページのトップへ

## メッセージを検索して削除する

この例は、April Stewart のメールボックスに対し、件名フィールドに「Your bank statement」という語句が含まれるメッセージを検索し、検索結果を別のフォルダーにコピーせずに、そのメッセージをソース メールボックスから削除します。前述のように、ユーザーのメールボックスからメッセージを削除するためには、"Mailbox Import Export" 役割を割り当てられている必要があります。


> [!IMPORTANT]
> <STRONG>Search-Mailbox</STRONG> コマンドレットに <EM>DeleteContent</EM> スイッチを指定して使用すると、メッセージはソース メールボックスから完全に削除されます。メッセージを完全に削除する前に、<EM>LogOnly</EM> スイッチを使用して検索で見つかったメッセージが削除される前にログを生成するか、またはメッセージがソース メールボックスから削除される前に別のメールボックスにコピーするかのいずれかを推奨します。



    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent

この例は、April Stewart のメールボックスに対し、件名フィールドに「Your bank statement」という語句が含まれるメッセージを検索し、その結果をメールボックス BackupMailbox の AprilStewart-DeletedMessages フォルダーにコピーして、そのメッセージを April のメールボックスから削除します。

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent

次の使用例は、組織内の全メールボックスで件名が「このファイルをダウンロード」というメッセージを検索してから、完全に削除します。

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent

構文およびパラメーターの詳細については、「[Search-Mailbox](https://technet.microsoft.com/ja-jp/library/dd298173\(v=exchg.150\))」を参照してください。

ページのトップへ

## \-LogLevel Full パラメーターを使用する

前のいくつかの例では、**Search-Mailbox** コマンドレットによって返された結果に関する詳細情報をログ記録するため、`Full` 値を指定した *LogLevel* パラメーターを使用しています。 このパラメーターを含めると、メール メッセージが作成され、*TargetMailbox* パラメーターによって指定されたメールボックスに送信されます。ログ ファイル (Search Results.csv という名前の CSV 形式のファイル) はこのメール メッセージに添付され、*TargetFolder* パラメーターによって指定されたフォルダーに配置されます。ログ ファイルには、**Search-Mailbox** コマンドレットを実行すると、検索結果に含まれる各メッセージの行が含まれています。

