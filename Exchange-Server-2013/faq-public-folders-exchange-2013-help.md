---
title: 'FAQ: パブリック フォルダー: Exchange 2013 Help'
TOCTitle: 'FAQ: パブリック フォルダー'
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 49115948
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# FAQ: パブリック フォルダー

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-03-27_

このトピックでは、Exchange Server 2013 のパブリック フォルダーについてよくある質問を一覧にまとめました。パブリック フォルダーの詳細については、「[パブリック フォルダー](public-folders-exchange-2013-help.md)」を参照してください。

パブリック フォルダーについて、これ以外の質問がありますか?電子メールの宛先は以下のとおりです。[Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com)。

## パブリック フォルダーの移行に関する FAQ

このセクションでは、パブリック フォルダーの移行に関してよくある質問をまとめてあります。詳細については、「[バッチ移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)」、「[バッチ移行を使用して、従来のパブリック フォルダーを Office 365 と Exchange Online に移行する](https://docs.microsoft.com/ja-jp/exchange/collaboration-exo/public-folders/batch-migration-of-legacy-public-folders)」、「[バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Exchange Online に移行する](https://docs.microsoft.com/ja-jp/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders)」を参照してください。

## サポートされているパブリック フォルダー移行のシナリオには、どのようなものがありますか。

次の一覧は、Exchange 2013 または Exchange Online にパブリック フォルダーを移行するために使用できるオプションの詳細を示しています。

  - Exchange 2007 パブリック フォルダー (SP3 RU15 以降) は、Exchange 2013 または Exchange Online に移行できます。

  - Exchange 2010 パブリック フォルダー (SP3 RU8 以降) は、Exchange 2013 または Exchange Online に移行できます。

  - Exchange 2013 パブリック フォルダー (CU15 以降) は、Exchange Online に移行できます。

現在は、同じ Active Directory フォレスト内にある Exchange 2013 への移行のみがサポートされています。フォレスト間の移行は、今後サポートされる予定です。

## 移行後、移行元の Exchange 2010 サーバーの階層はどうなりますか?

移行の最終段階で、ユーザーのアクセスを禁止するため移行元のサーバーはロックされます。このロックは移行後に移行元のパブリック フォルダーにユーザーがアクセスするのを防ぐため解除されません。このロックは解除できますが、変更結果を Exchange 2013 と同期できなくなるのでお勧めできません。

## パブリック フォルダーを移行する場合、既存のパブリック フォルダー ルールはどうなりますか?

パブリック フォルダー ルールはデータとともに移行され、パブリック フォルダー ルールとして維持されます。パブリック フォルダー ルールはメールボックス ルールに変換されません。

## 初期 .csv ファイルの生成後、移行元で階層を変更するとどうなりますか?階層の変更はどのように移行先に反映されますか?

移行元の階層と移行先のメールボックス間のマッピングを .csv ファイルで決定します。.csv ファイルにあるのは最上位フォルダーのみです。最上位フォルダーの子フォルダーは自動的に移行します。したがって、子フォルダーを新たに追加すると、このプロセスの間にそのフォルダーも移行します。最上位フォルダーを新たに作成した場合、そのフォルダーは階層の書き込み可能なコピーが含まれるメールボックスに作成されます。

## Exchange 2013 パブリック フォルダーへの移行の間、中断と最終処理で長く時間が空く場合、最終同期処理の間にユーザーがパブリック フォルダーにアクセスできるようにデルタ同期を強制実行するにはどうすればいいですか?

以下のシェル コマンドを実行すれば、最終処理前 (ソースのロック前) にデルタ同期を強制実行できます。

    Resume-PublicFolderMigrationRequest \PublicFolderMigration

構文およびパラメーターの詳細については、「[Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/ja-jp/library/jj218689\(v=exchg.150\))」を参照してください。

## 地理的に分散している階層を移行する場合、ターゲット ユーザーに最も近い場所にパブリック フォルダーを作成するにはどうしたらいいですか?

移行プロセスの一環として、(`publicfoldertomailboxmapgenerator.ps1` スクリプトで) .csv ファイルが生成されます。このファイルには、新しい階層のフォルダーとメールボックスのマッピングが含まれています。したがって、この .csv ファイルを使用すれば適切な場所にパブリック フォルダー メールボックスを作成できます。また、このファイルを変更して、ターゲット ユーザーから近い場所にある適切なメールボックスに必要なフォルダーを配置することもできます。

入力 .csv ファイルは、ディレクトリ \<*Exchange Installation Directory*\>\\V15\\Scripts にあるスクリプト `AggregatePFData.ps1` を実行すれば生成できます。スクリプトは以下のように実行します。

    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>

## 既存のパブリック フォルダー アクセス許可は移行しますか?

はい。アクセス許可は、フォルダー レベルでデータとともに自動的に移行します。この手順は別途実行する必要はありません。

## パブリック フォルダーはなくなったのですか?

いいえ。パブリック フォルダーは、Outlook の統合、共有シナリオの簡素化、および多くの対象ユーザーによる同じデータへのアクセスの許可に役立ちます。

## パブリック フォルダーはどのクライアントがサポートしていますか?

Outlook 2007、Outlook 2010、Outlook 2013、Outlook 2011 用 Mac ユーザーがパブリック フォルダーにアクセスできます。ただし、メールボックスが Exchange 2013 サーバーにあるユーザーは、Outlook 用 Mac などの Exchange Web サービス (EWS) を使用するクライアントから Exchange 2007 または Exchange 2010 のパブリック フォルダーに接続できません。これらのユーザーが引き続きアクセスできるようにするには、従来のパブリック フォルダーを Exchange 2013 に移行することをお勧めします。

## クライアントに制限はありますか。

Outlook Web App がサポートされていますが、いくつか制限があります。お気に入りのパブリック フォルダー (それらがメール、投稿、予定表、および連絡先のパブリック フォルダーの場合) を追加および削除できます。また、投稿の作成、編集、削除や、投稿への返信などのアイテムレベルの操作も実行できます。ただし、次の操作は Outlook Web App では実行できません。

  - パブリック フォルダーの作成または削除

  - コンテンツのドラッグ アンド ドロップ

  - 以前のバージョンの Exchange を実行しているサーバー上にあるパブリック フォルダーへのアクセス


> [!NOTE]
> <STRONG>[特定のテンプレートを使って返信する]</STRONG> 要素を含んだパブリック フォルダー ルールは、メールが有効なパブリック フォルダーにのみ作成できます。<STRONG>[特定のテンプレートを使って返信する]</STRONG> を含んだ既存のルールをメールが有効でないパブリック フォルダーで引き続き使用することはできますが、このテンプレート要素を持つ新しいルールをこれらのフォルダーで作成することはできず、またこの要素を持つ既存のルールを編集することもできません。



ハイブリッド シナリオの場合、Outlook on the web と Outlook 2011 for Mac ではクロスプレミスのパブリック フォルダーがサポートされていません。Outlook 2011 for Mac または Outlook on the web を利用してパブリック フォルダーにアクセスする場合、ユーザーはパブリック フォルダーと同じ場所にいる必要があります。「[ハイブリッド展開の手順](https://technet.microsoft.com/ja-jp/library/jj200788\(v=exchg.150\).aspx)」の手順を実行し、かつ Outlook 2016 for Mac の 2016 年 4 月の更新プログラムがすべてのクライアントにインストールされている場合は、Outlook 2016 for Mac のユーザーはハイブリッド シナリオでパブリック フォルダーにアクセスできます。

## サイズの非常に大きな階層は、どうすればパブリック フォルダー メールボックスに保存できますか?

パブリック フォルダーの記憶域の制限については、「[パブリック フォルダーの制限](limits-for-public-folders-exchange-2013-help.md)」を参照してください。

## 階層パブリック フォルダー メールボックスはどうすれば表示できますか?

次のコマンドを実行します。

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

構文およびパラメーターの詳細については、「[Get-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997571\(v=exchg.150\))」を参照してください。

## どうすれば Exchange 管理シェル コマンドレットでパブリック フォルダーのコンテンツ メールボックスを作成できますか?

以下のコマンドを実行して最初のマスター階層パブリック フォルダー メールボックスと第 2 の階層メールボックスを作成します。

    New-Mailbox -PublicFolder -Name <name of public folder>

詳細については、「[パブリック フォルダーの作成](https://docs.microsoft.com/ja-jp/exchange/collaboration-exo/public-folders/create-public-folder)」を参照してください。

## Exchange の以前のバージョンには、メールボックス データベースごとにそのパブリック フォルダー データベースを指定するオプションがありました。Exchange 2013 では、このオプションはどのように機能しますか?

Exchange 2013 にデータベースレベルの設置はありません。Exchange 2013 ではパブリック フォルダー メールボックスをメールボックスレベルで指定できますが、既定では Exchange がユーザーごとの階層メールボックスを自動的に計算します。

## Exchange 2013 ではパブリック フォルダー メトリック ツールをどのように使用していますか?

Exchange 2013 では、[Get-PublicFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa998663\(v=exchg.150\)) および [Get-PublicFolderItemStatistics](https://technet.microsoft.com/ja-jp/library/ee332344\(v=exchg.150\)) コマンドレットを使用してパブリック フォルダー メトリック データを取得できます。これは、Exchange 2010 の場合と同じ解決方法です。ここは何も変わっていません。パブリック フォルダーには追加のレポート作成アドオンは必要ありません。

## パブリック フォルダーでは、パブリック フォルダーに対する内部アクセスとサードパーティ アクセスを区別できますか?

Exchange 2013 では、パブリック フォルダーのアクセス許可は役割ベースのアクセス制御 (RBAC) を使用して管理します。Exchange 2013 ではアクセス制御リスト (ACL) を使用しません。[Get-PublicFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa998663\(v=exchg.150\)) コマンドレットと [Get-PublicFolderItemStatistics](https://technet.microsoft.com/ja-jp/library/ee332344\(v=exchg.150\)) コマンドレットを使用して、管理タスクを実行しているアカウントを追跡し、それに応じてアクセスを監査できます。RBAC の詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

## メールボックスの監査ログはパブリック フォルダーに対して機能しますか?

いいえ、現時点では機能しません。

## パブリック フォルダーの上限値はいくつですか?推奨事項には何がありますか?

パブリック フォルダーの制限については、「[パブリック フォルダーの制限](limits-for-public-folders-exchange-2013-help.md)」を参照してください。

## パブリック フォルダー メールボックスを分割するときのアドバイスとしては何がありますか?パブリック フォルダー メールボックスは同じデータベースにある必要がありますか?

旧バージョンの Exchange では、パブリック フォルダー データベース間でパブリック フォルダーを分割できます。パブリック フォルダー メールボックスの内容を同じメールボックス データベースのメールボックスに分割するか、別のデータベースのメールボックスに分割するかを決めることが可能です。一般的には、ストレージと I/O のバランスを取るために、個別のデータベースに分割することをお勧めします。

## パブリック フォルダーではアイテム保持ポリシーを設定できますか?

以前のバージョンの Exchange と同様に、アイテムには保存期限を設定できます。詳細については、「[パブリック フォルダーの制限](limits-for-public-folders-exchange-2013-help.md)」を参照してください。

## 特定のパブリック フォルダー メールボックスを使用できるユーザーを指定できますか?

Exchange 2007 と Exchange 2010 では、特定のパブリック フォルダーにアクセスできるユーザーを指定できました。Exchange 2013 では、ユーザーごとに既定のパブリック フォルダー メールボックスを指定できます。これを行うには、*DefaultPublicFolderMailbox* パラメーターを指定して [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットを実行します。

    Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"

## マスター階層が停止するとユーザーにはどのような影響がありますか?

マスター階層パブリック フォルダー メールボックスが停止しても、ユーザーはパブリック フォルダーを表示できます。ただし、パブリック フォルダーへの書き込みはできなくなります。階層が停止するのを防ぐには、パブリック フォルダーをデータベース可用性グループ (DAG) に入れておくことをお勧めします。DAG の詳細については、「[データベース可用性グループ (DAG)](database-availability-groups-dags-exchange-2013-help.md)」を参照してください。

## マスター階層メールボックスにするパブリック フォルダー メールボックスを変更できますか?

いいえ。マスター階層メールボックスを変更しようとすると、エラーになります。

## パブリック フォルダーにフル テキスト検索機能はありますか?

はい、フル テキスト検索は Exchange 2013 のパブリック フォルダーで使用可能です。ただし、複数のパブリック フォルダー間で検索することはできません。

