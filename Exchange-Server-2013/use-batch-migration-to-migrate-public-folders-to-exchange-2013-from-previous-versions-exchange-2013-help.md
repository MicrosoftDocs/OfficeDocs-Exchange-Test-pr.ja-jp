---
title: 'バッチ移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する: Exchange 2013 Help'
TOCTitle: バッチ移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64129764
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# バッチ移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2018-03-26_

**概要**:この記事では、パブリック フォルダーを Exchange 2007 または Exchange 2010 から Exchange 2013 に移動する方法について説明します。

この記事では、パブリック フォルダーを Exchange Server 2010 SP3 RU8 または Exchange 2007 SP3 RU15 から、同じフォレスト内にある Microsoft Exchange Server 2013 CU7 以降に移行する方法について説明します。

ここでは、Exchange 2010 SP3 RU8 サーバーと Exchange 2007 SP3 RU15 サーバーを、*従来の Exchange サーバー*と呼びます。


> [!NOTE]
> この記事で説明されているバッチの移行方法は、従来のパブリック フォルダーを Exchange 2013 に移行するための方法としてサポートされている唯一のものです。古いシリアル移行方法によるパブリック フォルダー移行は廃止される予定であり、Microsoft はこれをサポートしなくなりました。



**\*MigrationBatch** コマンドレットを使用することで移行を実行し、トラブルシューティングには **\*PublicFolderMigrationRequest** コマンドレットを使用します。さらに、次の PowerShell スクリプトを使用します。

  - `Export-PublicFolderStatistics.ps1`   このスクリプトは、フォルダー名からフォルダー サイズへのマッピング ファイルを作成します。

  - ` Export-PublicFolderStatistics.psd1` このサポート ファイルは Export-PublicFolderStatistics.ps1 スクリプトが使用します。同じ場所にダウンロードする必要があります。

  - `PublicFolderToMailboxMapGenerator.ps1`   このスクリプトは、パブリック フォルダーからメールボックスへのマッピング ファイルを作成します。

  - `PublicFolderToMailboxMapGenerator.strings.psd1` このサポート ファイルは PublicFolderToMailboxMapGenerator.ps1 スクリプトで使用されます。同じ場所にダウンロードする必要があります。

  - `Create-PublicFolderMailboxesForMigration.ps1` このスクリプトは、移行のターゲットのパブリック フォルダーのメールボックスを作成します。また、このスクリプトでは、[パブリック フォルダーの制限](limits-for-public-folders-exchange-2013-help.md) で推奨されるパグリック フォルダーのメールボックスごとのユーザー ログオン数に基づいて、予想されるユーザー負荷を処理するために必要なメールボックス数も計算します。

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` このサポート ファイルは Create-PublicFolderMailboxesForMigration.ps1 スクリプトで使用されます。同じ場所にダウンロードする必要があります。

手順 1:移行スクリプトをダウンロードする。このスクリプトは、これらのスクリプトのダウンロード場所に関する詳細を提供します。すべてのスクリプトは、同じ場所にダウンロードする必要があります。

パブリック フォルダーに関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

## パブリック フォルダーから Exchange 2013 への移行がサポートされている Exchange のバージョン

Exchange では、次のレガシ バージョンの Exchange Server からのパブリック フォルダーの移行をサポートします。

  - Exchange 2010 SP3 RU8 以降

  - Exchange 2007 SP3 RU15 以降

Exchange 2013 にパブリック フォルダーを移動する必要がありながら、オンプレミスのサーバーで Exchange 2010 や Exchange 2007 の最小サポート バージョンが稼働していない場合には、[シリアル移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する](https://technet.microsoft.com/ja-jp/library/jj150486\(v=exchg.150\))ことを検討してください。シリアル移行もオプションですが、オンプレミスのサーバーをアップグレードしてバッチ移行を使用するように強くお勧めします。バッチ移行では、大幅に高速になり、信頼性が向上します。

Exchange 2003 からパブリック フォルダーを直接移行することはできません。組織で Exchange 2003 を実行している場合、すべてのパブリック フォルダー データベースとレプリカを Exchange 2010 SP3 RU8 以降または Exchange 2007 SP3 RU15 以降に移動する必要があります。Exchange 2003 でパブリック フォルダーのレプリカを保持することはできません。さらに、Exchange 2013 パブリック フォルダー宛ての電子メールを Exchange 2003 サーバーを介してルーティングすることはできません。

## 始める前に把握しておくべき情報

  - 一部の手順ではダウンタイムが必要になるため、この手順を始める前に、このトピック全体に目を通してください。

  - Exchange 2010 サーバーでは、Exchange 2010 SP3 RU8 以降が稼働している必要があります。

  - Exchange 2007 サーバーでは、Exchange 2007 SP3 RU15 以降が稼働している必要があります。

  - 一度に Exchange 2013 に移行できるパブリック フォルダーの最大数は 500,000 です。

  - Exchange 2013 では、組織の管理役割グループのメンバーである必要があります。組織の管理役割グループを有効にする方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

  - Exchange 2010 では、組織の管理役割グループまたはサーバーの管理 RBAC 役割グループのメンバーになっている必要があります。詳細については、「[役割グループにメンバーを追加する](https://go.microsoft.com/fwlink/?linkid=299212)」を参照してください。

  - Exchange 2007 では、Exchange 組織の管理役割または Exchange サーバー管理者の役割の割り当てが必要です。さらに、パブリック フォルダー管理者の役割と、対象サーバーに対するローカルの Administrators グループの割り当ても必要です。詳細については、「[管理者の役割にユーザーまたはグループを追加する方法](https://go.microsoft.com/fwlink/p/?linkid=81779)」を参照してください。

  - Exchange 2007 サーバーで [Windows PowerShell 2.0 および WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930) にアップグレードします。

  - 移行する前に、[パブリック フォルダーの制限](limits-for-public-folders-exchange-2013-help.md)を考慮する必要があります。

  - 移行する前に、すべてのユーザーのメールボックスを Exchange 2013 に移動してください。Exchange 2007 または Exchange 2010 のメールボックスを持つユーザーは Exchange 2013 のパブリック フォルダーにアクセスできないからです。詳細については、「[Exchange 2013 でのメールボックスの移動](mailbox-moves-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - 複数ドメイン環境では、パブリック フォルダーのメールが有効なは子ドメインで Exchange が実行されている場合、Exchange 2013 への移行後の作業を停止します。Exchange 2013、パブリック フォルダーのメールが有効なオブジェクトに必要なルート ドメインの下になるためにです。この問題を解決するには、メールが有効なパブリック フォルダーのメールを無効にし、メールを有効にしてもう一度、適切なドメインの場所に移動することがある必要があります。

  - 移行の完了後、移行済みのメールが有効なパブリック フォルダーに外部の送信者がメールを送信する場合、<strong>匿名</strong>ユーザーに <strong>アイテムの作成</strong> 以上のアクセス許可が付与されている必要があります。このアクセス許可の付与を行っていない場合、外部のユーザーは配信失敗の通知を受け取り、メッセージは移行済みのメールが有効なパブリック フォルダーに配信されません。匿名ユーザーにアクセス許可を設定する方法について詳しくは、「[パブリック フォルダーのメールの有効化またはメールの無効化](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1: 移行スクリプトをダウンロードする

1.  「[パブリック フォルダー移行スクリプト](https://go.microsoft.com/fwlink/?linkid=299838)」からすべてのスクリプトとサポート ファイルをダウンロードします。

2.  PowerShell を実行するローカル コンピューターにスクリプトを保存します。たとえば C:\\PFScripts などです。すべてのスクリプトは同じ場所に保存する必要があります。

## 手順 2: 移行の準備

移行を開始する前に、以下の前提となる手順を実行します。

**従来の Exchange サーバー上で前提となる手順**

1.  移行終了時に確認できるよう、最初に従来の Exchange サーバーで次のコマンドを実行して、現在のパブリック フォルダー展開のスナップショットを取得することをお勧めします。
    
      - 移行元のフォルダー構造のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
      - アイテム数、サイズ、所有者などのパブリック フォルダーの統計情報のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
      - アクセス許可のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    移行の完了後に比較するため、上記のコマンドから取得した情報を保存します。

2.  パブリック フォルダーの名前にバックスラッシュ (**\\**) が含まれる場合、そのパブリック フォルダーは移行時に親パブリック フォルダー内に作成されます。移行を実行する前に、名前にバックスラッシュが含まれているパブリック フォルダーの名前を変更することをお勧めします。
    
    1.  Exchange 2010 では、名前にバックスラッシュが含まれているパブリック フォルダーを特定するには、次のコマンドを実行します。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  Exchange 2007 では、名前にバックスラッシュが含まれているパブリック フォルダーを特定するには、次のコマンドを実行します。
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  パブリック フォルダーが返された場合、次のコマンドを実行することで、名前を変更することができます。
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  以前に成功した移行の記録がないことを確認します。
    
    1.  次の例では、パブリック フォルダーの移行ステータスを確認します。
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
        
        以前に移行が成功したことがある場合、*PublicFoldersLockedforMigration* または *PublicFolderMigrationComplete* プロパティの値は `$true` です。手順 3b のコマンドを使用して、この値を `$false` に設定します。値が `$true` に設定されていると移行要求が失敗します。
    
    2.  *PublicFoldersLockedforMigration* プロパティまたは *PublicFolderMigrationComplete* プロパティの状態が `$true` の場合は、以下のコマンドを実行して値を `$false` に設定します。
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    

    > [!WARNING]
    > 上記のプロパティをリセットした後は、Exchange が新しい設定を検出するまで待機する必要があります。この処理が完了するまで最大 2 時間かかる場合があります。



構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-PublicFolder](https://technet.microsoft.com/ja-jp/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ja-jp/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/ja-jp/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/ja-jp/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Exchange 2013 サーバーの前提となる手順**

1.  既存のパブリック フォルダーの移行要求がないことを確認します。要求がある場合、その要求をクリアしないと、自身が行っている移行要求が失敗します。このステップはすべてのケースで必要というわけではありません。これは、パイプラインに既存の移行要求が存在している可能性がある場合にのみ必要です。
    
    既存の移行要求は、バッチ移行とシリアル移行の 2 種類のうちのいずれかです。それぞれの種類の要求を検出するコマンドと、それぞれの種類の要求を削除するコマンドは以下のとおりです。
    

    > [!IMPORTANT]
    > 移行要求を削除する前に、既存の要求がなぜ存在するかを理解することが重要です。次のコマンドを実行して、以前の要求がいつ実行されたかを特定し、発生した可能性がある問題の診断に役立てることができます。なぜ変更したかを特定するには、場合によって、組織内の他の管理者と連絡を取る必要があります。

    
    次の例では、既存のシリアル移行要求を検出します。
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    次の例では、既存のパブリック フォルダーのシリアル移行要求を削除します。
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    次の例では、既存のバッチ移行要求を検出します。
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    次の例では、既存のパブリック フォルダーのバッチ移行要求を削除します。
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Exchange 2013 サーバーにパブリック フォルダーまたはパブリック フォルダー メールボックスが存在しないことを確認します。
    
    1.  次のコマンドを実行し、パブリック フォルダー メールボックスが存在するかどうかを確認します。
        
            Get-Mailbox -PublicFolder 
    
    2.  コマンドを実行しても、パブリック フォルダー メールボックスが返されなかった場合は、Step 3: Generate the CSV files に進んでください。上記のコマンドによってパブリック フォルダーが返された場合は、以下のコマンドを使って、パブリック フォルダーが存在するかどうかを確認します。
        
            Get-PublicFolder
    
    3.  パブリック フォルダーが存在する場合は、次の PowerShell コマンドを実行し、パブリック フォルダーを削除します。パブリック フォルダーに含まれている情報が保存してあることを確認してください。
        

        > [!NOTE]
        > パブリック フォルダーを削除すると、そこに含まれるすべての情報が完全に削除されます。

        
            Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
            Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/ja-jp/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/ja-jp/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/ja-jp/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/ja-jp/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/ja-jp/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/ja-jp/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/ja-jp/library/aa995948\(v=exchg.150\))

## 手順 3: .csv ファイルを生成する

1.  従来の Exchange サーバーで `Export-PublicFolderStatistics.ps1` スクリプトを実行し、フォルダー名からフォルダー サイズへのマッピング ファイルを作成します。このスクリプトはローカル管理者が実行する必要があります。このファイルには、2 つの列があります。**FolderName** と **FolderSize** です。**FolderSize** 列の値は、バイト単位で表示されます。**\\PublicFolder01,10000** などです。
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* は、パブリック フォルダー階層をホストしているメールボックス サーバーの完全修飾ドメイン名です。
    
      - *Folder to size map path* は .csv ファイルを保存するネットワーク共有フォルダーのパスとファイル名です。このトピックの後半で、Exchange 2013 サーバーからこのファイルにアクセスする必要があります。ファイル名だけを指定すると、ローカル コンピューター上の現在の PowerShell ディレクトリにファイルが生成されます。

2.  `PublicFolderToMailboxMapGenerator.ps1` スクリプトを実行して、パブリック フォルダーとメールボックスとのマッピング ファイルを作成します。このファイルは、Exchange 2013 メールボックス サーバー上のパブリック フォルダー メールボックスの正しい数を計算するために使用されます。
    

    > [!NOTE]
    > パブリック フォルダーの名前にバックスラッシュ (<STRONG>\</STRONG>) が含まれる場合、そのパブリック フォルダーは親パブリック フォルダー内に作成されます。.csv ファイルを見直して、バックスラッシュを含む名前を編集することをお勧めします。

    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
      - *Maximum mailbox size in bytes* は、新しいパブリック フォルダー メールボックス用に設定する最大サイズです。パブリック フォルダー メールボックスのサイズを増やせるように、拡張が可能なサイズを指定する必要があります。
    
      - *Folder to size map path* は、`Export-PublicFolderStatistics.ps1` スクリプトを実行したときに作成される .csv ファイルのファイル パスと同じです。
    
      - *Folder to mailbox map path* は、この手順で作成するフォルダーからメールボックスへのマッピング .csv ファイルのファイル名とパスです。ファイル名だけを指定すると、ローカル コンピューター上の現在の PowerShell ディレクトリにファイルが生成されます。

## 手順 4: Exchange 2013 でパブリック フォルダー メールボックスを作成する

1.  次のコマンドを実行し、ターゲットのパブリック フォルダー メールボックスを作成します。手順 3 で PublicFoldertoMailboxMapGenerator.ps1 スクリプトを実行して生成した .csv ファイルにある各メールボックスのターゲットのメールボックスを、このスクリプトは作成します。
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* は、手順 3 で PublicFoldertoMailboxMapGenerator.ps1 スクリプトによって生成されるファイルです。通常、パブリック フォルダー階層を参照する同時ユーザー接続の推定値は、組織内のユーザー数の合計より少なくなります。

## 手順 5:移行要求を開始する

Exchange 2007 のパブリック フォルダーを移行する手順は、Exchange 2010 のパブリック フォルダーを移行する手順とは異なります。


> [!TIP]
> Exchange 2007、Exchange 2010 のどちらから移行する場合でも、適切なコマンドレットでバッチ移行要求が作成されると、EAC でその要求を表示および管理できるようになります。



**Exchange 2007 のパブリック フォルダーの移行**

1.  Exchange 2007 の OWAScratchPad フォルダーやスキーマ ルート フォルダーのサブツリーなど、レガシ システムのパブリック フォルダーは、Exchange 2013 では認識されないため、「無効」なアイテムとして処理されます。これにより移行は失敗します。移行要求の一部として、`BadItemLimit` パラメーターの値を指定する必要があります。この値は、保有するパブリック フォルダー データベースの数によって異なります。次のコマンドでは、保有しているパブリック フォルダー データベースの数を決定し、移行要求に対して `BadItemLimit` を計算します。
    
    ```
    $PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
    ```
    ```
    $BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)
    ```

2.  Exchange 2013 サーバーで次のコマンドを実行します。
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 

3.  次のコマンドを使用して移行を開始します。
    
        Start-MigrationBatch PFMigration

**Exchange 2010 のパブリック フォルダーの移行**

1.  Exchange 2013 サーバーで次のコマンドを実行します。
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
    
    `NotificationEmails` パラメーターは省略可能です。

2.  次のコマンドを使用して移行を開始します。
    
        Start-MigrationBatch PFMigration
    
    または
    
    EAC で移行を開始できます。
    
    1.  Exchange Online にログインし、EAC を開きます。
    
    2.  <strong>受信者</strong> \> <strong>移行</strong> に移動します。
    
    3.  作成した移行バッチを選択し、開始ボタンをクリックします。

<strong>状態</strong> 列にバッチの初期状態が <strong>作成済み</strong> と表示されます。移行中は状態が <strong>同期中</strong> に変わります。移行要求が完了すると、状態は <strong>同期済み</strong> になります。バッチをダブルクリックして、バッチに含まれる個々のメールボックスの状態を表示できます。メールボックスのジョブは <strong>キューに登録済み</strong> の状態で開始します。ジョブが開始すると状態は <strong>同期中</strong> になり、`InitialSync` が完了すると、状態は <strong>同期済み</strong> と表示されます。

移行の進行状況と完了を EAC で表示および管理できます。**New-migrationBatch** コマンドレットは、各パブリック フォルダー メールボックスのメールボックス移行要求を開始するので、メールボックスの移行ページを使用してこれらの要求の状態を表示することができます。以下の手順により、メールボックス移行ページにアクセスして、メールで受信可能な移行レポートを作成することができます。

1.  Exchange Online にログインし、EAC を開きます。

2.  <strong>メールボックス</strong> \> <strong>移行</strong> に移動します。

3.  作成した移行要求を選択して、<strong>詳細</strong> ウィンドウの <strong>詳細の表示</strong> をクリックします。

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/ja-jp/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ja-jp/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/ja-jp/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/ja-jp/library/jj218697\(v=exchg.150\))

## 手順 6: 従来の Exchange サーバーでパブリック フォルダーを最後の移行用にロック ダウンする (ダウンタイムが必要)

移行のこの時点まで、ユーザーはパブリック フォルダーにアクセスできます。次の手順では、ユーザーは従来のパブリック フォルダーからログ オフされ、移行で最終的な同期が完了するまでフォルダーはロックされます。このプロセスの間、ユーザーはパブリック フォルダーにアクセスできません。また、メール対応パブリック フォルダーに送信されたメールはキューに格納され、パブリック フォルダーの移行が完了するまで配信されません。

以下に示すように `PublicFoldersLockedForMigration` コマンドを実行する前に、すべてのジョブの状態が**同期済み**であることを確認します。これを行うには `Get-PublicFolderMailboxMigrationRequest` コマンドを実行します。すべてのジョブの状態が**同期済み**であることを確認した後にのみ、この手順を続行します。

従来の Exchange サーバーで次のコマンドを実行すると、最終処理のために従来のパブリック フォルダーがロックされます。

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true


> [!NOTE]
> 何らかの理由で移行バッチ ファイルが最終処理されなかった (<STRONG>PublicFolderMigrationComplete</STRONG> に <STRONG>False</STRONG> と表示された) 場合は、従来のサーバー上で、インフォメーション ストア (IS) を再起動してください。



構文およびパラメーターの詳細については、「[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))」を参照してください。

組織に複数のパブリック フォルダー データベースがある場合、パブリック フォルダーのレプリケーションが完了するまで待ち、すべてのパブリック フォルダー データベースの `PublicFoldersLockedForMigration` フラグが解除されたこと、およびフォルダーに対して最近実行した保留中の変更が組織全体で統合されたことを確認する必要があります。この処理には数時間かかる場合があります。

## 手順 7: パブリック フォルダーの移行の終了処理をする (ダウンタイムが必要)

最初に、次のコマンドレットを実行して、Exchange 2013 の展開の種類を**リモート**に変更します。

    Set-OrganizationConfig -PublicFoldersEnabled Remote

完了したら、次のコマンドを実行して、パブリック フォルダーの移行を実行できます。

    Complete-MigrationBatch PublicFolderMigration

または EAC で <strong>この移行バッチの完了</strong> をクリックして、移行を完了できます。

移行を完了すると、Exchange は、従来の Exchange サーバーと Exchange 2013 の間の最終的な同期を実行します。最終的な同期が成功した場合は、Exchange 2013 サーバー上のパブリック フォルダーのロックが解除され、**完了**、および、**完了**する移行バッチのステータスが変更されます。移行バッチ**の完了**に**同期**からのステータスの変更の前に、いくつかの時間を実行するが一般的、その時点で最終的な同期が開始されます。

## 手順 8: パブリック フォルダーの移行をテストして、ロックを解除する

パブリック フォルダーの移行を完了した後、次のテストを実行して移行が成功したことを確認します。これで Exchange 2013 パブリック フォルダーの使用に切り替える前に、移行済みのパブリック フォルダー階層をテストすることができます。

1.  PowerShell で次のコマンドを実行してテスト メールボックスをいくつか割り当て、新規に移行済みのいずれかのパブリック フォルダー メールボックスを既定のパブリック フォルダー メールボックスとして使用します。
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  前の手順で識別されたテスト ユーザーを使って Outlook 2007 以降にログオンし、次のパブリック フォルダー テストを実行します。
    
      - 階層の表示
    
      - アクセス許可のチェック
    
      - パブリック フォルダーの作成と削除
    
      - パブリック フォルダーに対する内容の追加と削除

3.  問題が発生した場合は、後述する「Roll back the migration」を参照してください。パブリック フォルダーのコンテンツと階層に特に問題がなく期待どおりに機能している場合には、次のコマンドを実行して他のすべてのユーザーが使えるようにパブリック フォルダーをロック解除します。
    
        Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
    

    > [!IMPORTANT]
    > 最初の移行確認完了後は <EM>IsExcludedFromServingHierarchy</EM> パラメータは使わないでください。このパラメータは Exchange Online の自動ストレージ管理サービスが使用するためです。



4.  従来の Exchange サーバーで次のコマンドを実行すると、パブリック フォルダーの移行が完了したことが示されます。
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  移行が完了したことを確認したら、次のコマンドを実行します。
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

6.  最後に、移行済みのメールが有効なパブリック フォルダーに外部の送信者がメールを送信する場合、<strong>匿名</strong> ユーザーに <strong>アイテムの作成</strong> 以上のアクセス許可が付与されている必要があります。このアクセス許可の付与を行っていない場合、外部のユーザーは配信失敗の通知を受け取り、メッセージは移行済みのメールが有効なパブリック フォルダーに配信されません。
    
    匿名ユーザーのアクセス許可を設定するには、シェルや Outlook を使用できます。匿名ユーザーにアクセス許可を設定する方法について詳しくは、「[パブリック フォルダーのメールの有効化またはメールの無効化](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)」を参照してください。

## 設定が適用されたことを確認する方法

「Step 2: Prepare for the migration」で、移行を開始する前にパブリック フォルダーの構造、統計、アクセス許可のスナップショットを取得する指示がありました。以下の手順では、移行完了後に同じスナップショットを取得して、パブリック フォルダーの移行が正しく行われたことを確認します。両方のファイルのデータを比較して、移行が正しく行われたことを確認します。

1.  新しいフォルダー構造のスナップショットを取得するには、次のコマンドを実行します。
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  アイテム数、サイズ、所有者などのパブリック フォルダーの統計情報のスナップショットを取得するには、次のコマンドを実行します。
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  アクセス許可のスナップショットを取得するには、次のコマンドを実行します。
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## 従来の Exchange サーバーからパブリック フォルダー データベースを削除する

移行完了後に Exchange 2013 のパブリック フォルダーが期待どおりに動作することを確認したら、レガシ Exchange サーバーのパブリック フォルダー データベースを削除する必要があります。

  - Exchange 2007 サーバーからパブリック フォルダー データベースを削除する方法の詳細は、「[パブリック フォルダ データベースの削除](https://go.microsoft.com/fwlink/?linkid=123678)」を参照してください。

  - Exchange 2010 サーバーからパブリック フォルダー データベースを削除する方法の詳細は、「[パブリック フォルダ データベースの削除](https://go.microsoft.com/fwlink/?linkid=81409)」を参照してください。

## 移行のロールバック

移行に関して何らかの問題が発生し、従来の Exchange パブリック フォルダーを再度アクティブにする必要がある場合は、次の手順を実行します。


> [!WARNING]
> 従来の Exchange サーバーに移行をロールバックすると、移行後に Exchange 2013 でメール対応パブリック フォルダーに送信されたすべての電子メール、またはパブリック フォルダーに投稿された内容がすべて失われます。この内容を保存するには、パブリック フォルダーの内容を .pst ファイルにエクスポートして、ロールバック終了後に従来のパブリック フォルダーにインポートする必要があります。



1.  従来の Exchange サーバーで次のコマンドを実行すると、従来の Exchange パブリック フォルダーのロックが解除されます。この処理には数時間かかる場合があります。
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  Exchange 2013 サーバーで、次のコマンドを実行してパブリック フォルダー メールボックスを削除します。
    
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false

3.  従来の Exchange サーバーで次のコマンドを実行すると、`PublicFolderMigrationComplete` フラグが `$false` に設定されます。
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

