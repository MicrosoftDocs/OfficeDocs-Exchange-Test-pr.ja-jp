---
title: '古いデータベース ファイルが存在する_FirstSGFilesExist: Exchange 2013 Help'
TOCTitle: 古いデータベース ファイルが存在する_FirstSGFilesExist
ms:assetid: 907faeb8-1c6d-49fc-95a1-417f415a9d79
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.firstsgfilesexist(v=EXCHG.150)
ms:contentKeyID: 48269792
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 古いデータベース ファイルが存在する\_FirstSGFilesExist

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-06-05_

対象のインストール パスに既存の Microsoft Exchange データベース ファイルが検出されたため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムを実行するには、対象のインストール パスに Microsoft Exchange データベース ファイルが存在しない状態になっている必要があります。

この問題を解決するには、対象のインストール パスから既存のすべてのファイルを削除した後、セットアップ プログラムを再実行します。

**対象のインストール パスから既存の Exchange Server データベース ファイルを削除するには、次の操作を行います。**

1.  \[マイ コンピューター\] またはエクスプローラーで、対象のインストール パスを見つけます。
    

    > [!NOTE]
    > 既定では、データベース ファイルは次の場所にあります。<BR>&lt;システム ドライブ&gt;:\Program Files\Microsoft\Exchange Server\Mailbox\First Storage Group



2.  削除するファイルを右クリックし、**\[削除\]** を選択します。

3.  **\[ファイルの削除の確認\]** ダイアログ ボックスで、**\[はい\]** をクリックします。

4.  対象のインストール パスにあるすべてのファイルに対して、手順 2. と 3. を繰り返します。

