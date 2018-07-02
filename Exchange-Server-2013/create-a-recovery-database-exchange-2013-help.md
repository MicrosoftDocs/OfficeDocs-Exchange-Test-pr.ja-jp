---
title: '回復用データベースを作成する: Exchange 2013 Help'
TOCTitle: 回復用データベースを作成する
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 48269350
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 回復用データベースを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-01-21_

シェルを使用して回復用データベースを作成できます。回復用データベースは、回復操作の一環としてデータをマウントして、復元したデータベースからデータを抽出するために使用される特別なメールボックス データベースです。回復用データベースを作成した後、回復または復元されたメールボックス データベースを回復用データベースに移動し、[New-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829875\(v=exchg.150\)) コマンドレットを使用して、回復されたデータベースからデータを抽出できます。抽出後に、データをフォルダーにエクスポートしたり、既存のメールボックスに結合したりできます。回復用データベースを使用すると、現在のデータへのユーザー アクセスを妨げずに、データベースのバックアップやコピーからデータを回復できます。

回復用データベースに関連する他の管理タスクについては、「[回復用データベース](recovery-databases-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間: 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス回復」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して回復用データベースを作成する

この例では、メールボックス サーバー MBX2 上に回復用データベース RDB1 を作成します。

    New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2

この例では、データベース ファイルとログ フォルダーのカスタム パスを使用して、メールボックス サーバー MBX1 上に回復用データベース RDB2 を作成します。

    New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"

構文およびパラメーターの詳細については、「[New-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/aa997976\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

回復用データベースが正常に作成されたことを確認するには、次の手順を実行します。

  - シェルで次のコマンドを実行して、回復用データベースの構成情報を表示します。
    
        Get-MailboxDatabase <RecoveryDatabaseName> | Format-List

## その他のタスク

回復用データベースを作成した後、回復用データベースを使用して、データを回復することもできます。詳細な手順については、「[回復用データベースを使用してデータを復元する](restore-data-using-a-recovery-database-exchange-2013-help.md)」を参照してください。

