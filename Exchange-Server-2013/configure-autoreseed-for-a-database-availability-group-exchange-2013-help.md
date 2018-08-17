---
title: 'データベース可用性グループの AutoReseed の構成: Exchange 2013 Help'
TOCTitle: データベース可用性グループの AutoReseed の構成
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 49129423
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# データベース可用性グループの AutoReseed の構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-04-15_

AutoReseed は、ディスクに障害が発生した後にデータベースの冗長性を迅速に復元するための機能です。ディスクに障害が発生した場合、そのディスクに格納されているデータベース コピーが、メールボックス サーバー上の構成済みのスペア ディスクに自動的に再シードされます。データベース可用性グループ (DAG) の AutoReseed を構成するには、このトピックで説明している手順を実行してください。


> [!NOTE]
> AutoReseed 機能は、前提条件の構成タスクを実行しません。ディスクの適切なインストール、スペア ディスクのシステムへの追加、不良ディスクの交換、新しいディスクのフォーマットは、管理者が手動で実施する必要があります。



DAG に関連する追加の管理タスクについては、「[データベース可用性グループの管理](managing-database-availability-groups-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。

  - 物理ディスクごとに 1 つずつの論理ディスク/パーティションを作成する必要があります。

  - 後述する手順に記載された特定のデータベースとログ フォルダー構造を使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 実行方法

## 手順 1: データベースとボリュームのルート パスを構成する

最初の手順では、DAG が使用するデータベース (*AutoDagDatabasesRootFolderPath*) とボリューム (*AutoDagVolumesRootFolderPath*) のルート ディレクトリを構成します。既定では各ルート ディレクトリは、それぞれ C:\\ExchangeDatabases と C:\\ExchangeVolumes になります。既定のパスを使用している場合は、この手順を省略できます。

この例では、データベースのルート パスを構成する方法を示します。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

この例では、ストレージ ボリュームのルート パスを構成する方法を示します。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## このステップの検証方法

データベースとボリュームのルート パスが正常に構成されたことを確認するには、次のコマンドを実行します。

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabasesRootFolderPath* と *AutoDagVolumesRootFolderPath* の出力は、構成したパスを反映する必要があります。

## 手順 2: ボリュームごとのデータベース数を構成する

次に、DAG のボリュームごとのデータベース数 (*AutoDagDatabaseCopiesPerVolume*) を構成します。

この例では、ボリュームごとに 4 つずつのデータベースで構成されている DAG にこの AutoReseed 設定を構成する方法を示します。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## このステップの検証方法

ボリュームごとのデータベース数が正常に構成されたことを確認するには、次のコマンドを実行します。

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabaseCopiesPerVolume* の出力は、構成した値を反映する必要があります。

## 手順 3: データベースとボリュームのルート ディレクトリを作成する

次に、手順 1 で構成したルート ディレクトリに対応するディレクトリを作成します。この例では、コマンド プロンプトを使用して既定のディレクトリを作成する方法を示します。

    md C:\ExchangeDatabases
    md C:\ExchangeVolumes

## このステップの検証方法

データベースとボリュームのルート ディレクトリが正常に構成されたことを確認するには、次のコマンドを実行します。

    Dir C:\

作成されたディレクトリの出力の一覧が表示されます。

## 手順 4: ボリューム フォルダーをマウントする

データベースに使用するすべてのボリューム (スペア ボリュームを含む) について、Windows ディスク管理アプリケーション (diskmgmt.msc) を使用して、C:\\ExchangeVolumes\\ の下にマウントされたフォルダー内の各ボリュームをマウントします。たとえば、データベースを備えた 2 つのボリュームと 1 つのスペア ボリュームが存在する場合、これらのボリュームを次のマウントされたフォルダーにマウントします。

  - C:\\ExchangeVolumes\\Volume1

  - C:\\ExchangeVolumes\\Volume2

  - C:\\ExchangeVolumes\\Volume3

マウントされたフォルダーの名前は、そのフォルダーがルート ボリュームのパスの下にマウントされている限り、任意の名前にすることができます。

## このステップの検証方法

ボリューム フォルダーが正常にマウントされたことを確認するには、次のコマンドを実行します。

    Dir C:\

マウントされたボリュームの出力の一覧が表示されます。

## 手順 5: データベース フォルダーを作成する

次に、ルート パス C:\\ExchangeDatabases の下にデータベース ディレクトリを作成します。この例では、各ボリューム上に 4 つのデータベースが存在するストレージ構成のディレクトリの作成方法を示します。
```
md c:\ExchangeDatabases\db001
```
```
md c:\ExchangeDatabases\db002
```
```
md c:\ExchangeDatabases\db003
```
```
md c:\ExchangeDatabases\db004
```

## このステップの検証方法

データベース フォルダーが正常にマウントされたことを確認するには、次のコマンドを実行します。

    Dir C:\ExchangeDatabases

作成されたディレクトリの出力の一覧が表示されます。

## 手順 6: データベースのマウント ポイントを作成する

各データベースのマウント ポイントを作成し、マウント ポイントを適切なボリュームにリンクします。たとえば、db001 のマウントされたフォルダーは、C:\\ExchangeDatabases\\db001 にあることが必要です。これを行うには、diskmgmt.msc または mountvol.exe を使用します。この例では、mountvol.exe を使用して db001 を C:\\ExchangeDatabases\\db001 にマウントする方法を示します。

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## このステップの検証方法

データベースのマウント ポイントが正常に作成されたことを確認するには、次のコマンドを実行します。

    Mountvol.exe C:\ExchangeDatabases\db001 /L

マウントされたボリュームのマウント ポイントの一覧が表示されます。

## 手順 7: データベースのディレクトリ構造を作成する

次に、手順 5 で作成したフォルダーの直下に 2 つのディレクトリを作成します。1 つは各データベース用に、もう 1 つはデータベースの各ログ ストリーム用に作成します。これらは同じボリュームに保存されます。ディレクトリ構造には、次の形式を使用する必要があります。

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.db

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.log

この例では、ボリューム 1 に保存される 4 つのデータベース用のディレクトリを作成する方法を示します。
```
md c:\ExchangeDatabases\db001\db001.db
```
```
md c:\ExchangeDatabases\db001\db001.log
```
```
md c:\ExchangeDatabases\db002\db002.db
```
```
md c:\ExchangeDatabases\db002\db002.log
```
```
md c:\ExchangeDatabases\db003\db003.db
```
```
md c:\ExchangeDatabases\db003\db003.log
```
```
md c:\ExchangeDatabases\db004\db004.db
```
```
md c:\ExchangeDatabases\db004\db004.log
```

すべてのボリューム上のデータベースについて、上記のコマンドを繰り返します。

## このステップの検証方法

データベースのディレクトリ構造が正常に作成されたことを確認するには、次のコマンドを実行します。

    Dir C:\ExchangeDatabases /s

作成されたディレクトリの出力の一覧が表示されます。

## 手順 8: データベースを作成する

適切なフォルダーを使用して構成されたログ パスとデータベース パスでデータベースを作成します。この例では、新しく作成したディレクトリとマウント ポイント構造に保存されるデータベースを作成する方法を示します。

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## このステップの検証方法

適切なフォルダーにデータベースが正常に作成されたことを確認するには、次のコマンドを実行します。

    Get-MailboxDatabase db001 | Format List *path*

返されるデータベース プロパティが、データベース ファイルとログ ファイルが上記のフォルダーに保存されようとしていることを示す必要があります。

## このタスクの検証方法

DAG に AutoReseed が構成されたことを確認するには、次の手順を実行します。

1.  DAG が正しく構成されていることを確認するには、次のコマンドを実行します。
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  ディレクトリ構造が正しく構成されていることを確認するには、次のコマンドを実行します (既定のパスは以下のとおりです。必要に応じて、パスを使用しているパスに置き換えてください)。
    ```
    Dir c:\ExchangeDatabases /s
    ```
    ```
    Dir c:\ExchangeVolumes /s
    ```
