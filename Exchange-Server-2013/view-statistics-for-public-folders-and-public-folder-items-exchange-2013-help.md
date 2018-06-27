---
title: 'パブリック フォルダーおよびパブリック フォルダー アイテムの統計情報の表示: Exchange Online Help'
TOCTitle: パブリック フォルダーおよびパブリック フォルダー アイテムの統計情報の表示
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 49896243
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダーおよびパブリック フォルダー アイテムの統計情報の表示

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ここでは、表示名、作成日時、最終変更日時、最終アクセス日時、アイテム サイズなど、パブリック フォルダーの統計情報を取得する方法について説明します。この情報を使用すると、パブリック フォルダーを削除または保持するかを決定できます。


> [!NOTE]
> Exchange 管理センター (EAC) では、<STRONG>[パブリック フォルダー]</STRONG> &gt; <STRONG>[編集]</STRONG><IMG title=編集アイコン alt=編集アイコン src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> &gt; <STRONG>[メールボックスの使用状況]</STRONG> の順に移動して、パブリック フォルダーのクォータと使用状況に関する情報の一部を表示できます。ただし、この情報は不完全なため、シェルを使用してパブリック フォルダーの統計情報を確認することをお勧めします。



パブリック フォルダーの管理に関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

パブリック フォルダーに関するその他の管理タスクについては、「[Office 365 と Exchange Online のパブリック フォルダーの手順](https://technet.microsoft.com/ja-jp/library/jj966272\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - EAC を使用してパブリック フォルダーの統計情報を取得することはできません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してパブリック フォルダーの統計情報を取得する

この例では、Marketing という名前のパブリック フォルダーの統計情報を返し、パイプ コマンドを使用して書式設定します。

    Get-PublicFolderStatistics -Identity \Marketing | Format-List


> [!NOTE]
> <EM>Identity</EM> パラメーターの値には、パブリック フォルダーへのパスを含める必要があります。たとえば、Business という名前の親フォルダーの下に Marketing という名前のパブリック フォルダーがある場合は、<CODE>\Business\Marketing</CODE>



構文およびパラメーターの詳細については、「[Get-PublicFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa998663\(v=exchg.150\))」を参照してください。

## シェルを使用してパブリック フォルダー アイテムの統計情報を表示する

パブリック フォルダー内のアイテムについて、次の情報を表示できます。

  - アイテムの種類

  - 件名

  - 最終変更日時

  - 最終アクセス日時

  - 作成時刻

  - 添付ファイル

  - \[メッセージ サイズ\]

この情報を使用して、どのパブリック フォルダーを削除するかといった、パブリック フォルダーに対する操作を決定できます。たとえば、アイテムが 2 年間以上アクセスされていないパブリック フォルダーを削除したり、ドキュメント リポジトリとして使用されているパブリック フォルダーを他のクライアント アクセス アプリケーションに変換できます。

この例では、\\Marketing\\2013 パス下の Pamphlets パブリック フォルダー内のすべてのアイテムに関する既定の統計情報を返します。既定の情報には、項目 ID、作成日時、および件名が含まれます。

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

この例では、件名、最終変更日時、作成日時、添付ファイル、メッセージ サイズ、アイテムの種類など、Pamphlets パブリック フォルダー内のアイテムに関する追加情報を返します。これには、リストの書式を設定するパイプされたコマンドも含まれています。

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

構文およびパラメーターの詳細については、「[Get-PublicFolderItemStatistics](https://technet.microsoft.com/ja-jp/library/ee332344\(v=exchg.150\))」を参照してください。

## シェルを使用して Get-PublicFolderItemStatistics コマンドレットの出力を .csv ファイルにエクスポートする

この例では、コマンドレットの出力を PFItemStats.csv ファイルにエクスポートします。このファイルには、\\Marketing\\Reports パブリック フォルダー内のすべてのアイテムで使用されている次の情報が含まれます。

  - メッセージの件名 (`Subject`)

  - アイテムが最後に変更された日時 (`LastModificationTime`)

  - アイテムに添付ファイルがあるかどうか (`HasAttachments`)

  - アイテムの種類 (`ItemType)`

  - アイテムのサイズ (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

構文およびパラメーターの詳細については、「[Get-PublicFolderItemStatistics](https://technet.microsoft.com/ja-jp/library/ee332344\(v=exchg.150\))」を参照してください。

