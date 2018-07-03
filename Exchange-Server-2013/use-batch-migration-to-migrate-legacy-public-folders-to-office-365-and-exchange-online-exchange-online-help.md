---
title: 'バッチ移行を使用して、従来のパブリック フォルダーを Office 365 と Exchange Online に移行する: Exchange 2013 Help'
TOCTitle: バッチ移行を使用して、従来のパブリック フォルダーを Office 365 と Exchange Online に移行する
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63892230
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# バッチ移行を使用して、従来のパブリック フォルダーを Office 365 と Exchange Online に移行する

 

_**適用先:** Exchange Online, Exchange Server, Exchange Server 2013_

_**トピックの最終更新日:** 2018-03-26_

**概要**:以下に示す手順で、Exchange 2007 および Exchange 2010 パブリック フォルダーを Office 365 に移動します。

このトピックでは、一括移行または段階的な移行で、パブリック フォルダーを Update Rollup 8 for Exchange Server 2010 Service Pack 3 (SP3) または Update Rollup 15 for Exchange 2007 SP3 から Office 365 または Exchange Online に移行する方法について説明します。

このトピックでは、Exchange 2010 SP3 RU8 サーバーと Exchange 2007 SP3 RU15 サーバーを、*従来の Exchange サーバー*と呼びます。さらに、このトピックの手順は Exchange Online と Office 365 の両方に適用されます。このトピックでは用語を同じ意味で使用する場合があります。


> [!NOTE]
> この記事で説明されているバッチの移行方法は、従来のパブリック フォルダーを Office 365 と Exchange Online に移行するための方法としてサポートされている唯一のものです。古いシリアル移行方法によるパブリック フォルダー移行は廃止される予定であり、Microsoft はこれをサポートしなくなりました。



パブリック フォルダーを Office 365 または Exchange Online に移行する場合、Outlook の PST エクスポート機能を使用しないことをお勧めします。Office 365 および Exchange Online パブリック フォルダー メールボックスの容量は、自動分割機能により管理されており、パブリック フォルダー メールボックスがサイズ クォータを超えると、この機能によって分割されます。PST エクスポートを使ってパブリック フォルダーを移行すると、自動分割機能はパブリック フォルダー メールボックスの急激な容量増加に対処できなくなり、自動分割機能によってプライマリ メールボックスからデータが移動されるまで、最大で 2 週間待たなければならない場合があります。パブリック フォルダーを Office 365 および Exchange Online に移行するには、このドキュメントに記載されたコマンドレット ベースの手順を使用することをお勧めします。PST エクスポートを使ってパブリック フォルダーを移行する方法を選ぶ場合は、このトピックの「Outlook の PST エクスポートを使ってパブリック フォルダーを Office 365 に移行する」をご覧ください。

次の PowerShell スクリプトに加えて、**\*-MigrationBatch** コマンドレットを使用することで、移行を実行します。

  - `Export-PublicFolderStatistics.ps1`   このスクリプトは、フォルダー名からフォルダー サイズへのマッピング ファイルを作成します。このスクリプトは、従来の Exchange サーバーで実行します。

  - `Export-PublicFolderStatistics.psd1`   このサポート ファイルは `Export-PublicFolderStatistics.ps1` スクリプトが使用するもので、同じ場所にダウンロードする必要があります。

  - `PublicFolderToMailboxMapGenerator.ps1`   このスクリプトは、`Export-PublicFolderStatistics.ps1` スクリプトからの出力を使用して、パブリック フォルダーからメールボックスへのマッピング ファイルを作成します。このスクリプトは、従来の Exchange サーバーで実行します。

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   このサポート ファイルは `PublicFolderToMailboxMapGenerator.ps1` スクリプトが使用するもので、同じ場所にダウンロードする必要があります。

  - `Create-PublicFolderMailboxesForMigration.ps1` このスクリプトは、移行のターゲットのパブリック フォルダーのメールボックスを作成します。また、このスクリプトでは、[パブリック フォルダーの制限](limits-for-public-folders-exchange-2013-help.md) で推奨されるパグリック フォルダーのメールボックスごとのユーザー ログオン数に基づいて、予想されるユーザー負荷を処理するために必要なメールボックス数も計算します。

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` このサポート ファイルは Create-PublicFolderMailboxesForMigration.ps1 スクリプトで使用されます。同じ場所にダウンロードする必要があります。

  - `Sync-MailPublicFolders.ps1`   このスクリプトは、ローカルの Exchange 展開と Office 365 との間で、メールが有効なパブリック フォルダー オブジェクトを同期します。このスクリプトは、従来の Exchange サーバーで実行します。

  - `SyncMailPublicFolders.strings.psd1`    これは、`Sync-MailPublicFolders.ps1` スクリプトが使用するサポート ファイルで、前述のスクリプトと同じ場所にコピーする必要があります。

手順 1:移行スクリプトをダウンロードする。このスクリプトは、これらのスクリプトのダウンロード場所に関する詳細を提供します。すべてのスクリプトは、同じ場所にダウンロードする必要があります。

パブリック フォルダーに関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

## Office 365 および Exchange Online へのパブリック フォルダーの移行をサポートしている Exchange のバージョン

Exchange は、次のバージョンの従来の Exchange サーバーから Office 365 および Exchange Online へのパブリック フォルダーの移動をサポートしています。

  - Exchange 2010 SP3 RU8 以降

  - Exchange 2007 SP3 RU15 以降

Exchange Online にパブリック フォルダーを移動する必要がありながら、オンプレミスのサーバーで Exchange 2010 や Exchange 2007 の最小サポート バージョンが稼働していない場合には、オンプレミスのサーバーをアップグレードし、バッチ移行を使用することを強くお勧めします。これはパブリック フォルダー移行方法としてサポートされている唯一のものです。

Exchange 2003 からパブリック フォルダーを直接移行することはできません。組織で Exchange 2003 を実行している場合、すべてのパブリック フォルダー データベースとレプリカを Exchange 2010 SP3 RU8 以降または Exchange 2007 SP3 RU10 以降に移動する必要があります。Exchange 2003 でパブリック フォルダーのレプリカを保持することはできません。さらに、Exchange 2013 パブリック フォルダー宛ての電子メールを Exchange 2003 サーバーを介してルーティングすることはできません。

## 始める前に把握しておくべき情報

  - Exchange 2010 サーバーでは、Exchange 2010 SP3 RU8 以降が稼働している必要があります。

  - Exchange 2007 サーバーでは、Exchange 2007 SP3 RU15 以降が稼働している必要があります。

  - Office 365 および Exchange Online で組織の管理役割グループのメンバーになっている必要があります。この役割グループは、Office 365 または Exchange Online にサブスクライブした場合に割り当てられるアクセス許可とは異なるものです。組織の管理役割グループを有効にする方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

  - Exchange 2010 では、組織の管理役割グループまたはサーバーの管理 RBAC 役割グループのメンバーになっている必要があります。詳細については、「[役割グループにメンバーを追加する](https://go.microsoft.com/fwlink/?linkid=299212)」を参照してください。

  - Exchange 2007 では、Exchange 組織の管理役割または Exchange サーバー管理者の役割の割り当てが必要です。さらに、パブリック フォルダー管理者の役割と、対象サーバーに対するローカルの Administrators グループの割り当ても必要です。詳細については、「[管理者の役割にユーザーまたはグループを追加する方法](https://go.microsoft.com/fwlink/p/?linkid=81779)」を参照してください。

  - Exchange 2007 サーバーで [Windows PowerShell 2.0 および WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930) にアップグレードします。

  - 組織内のパブリック フォルダーのサイズが 2 GB を超えている場合は、移行する前に、そのフォルダーの内容を削除するか、複数のパブリック フォルダーに分割することをお勧めします。この 2 つのオプションがどちらも実行できない場合、パブリック フォルダーを Office 365 および Exchange Online に移動しないことをお勧めします。

  - Office 365 および Exchange Online では、最大 1,000 個のパブリック フォルダー メールボックスを作成できます。

  - パブリック フォルダ－を移行する前に、最初にすべてのユーザー メールボックスを Office 365 および Exchange Online に移動することをお勧めします。詳細については、「[複数のメール アカウントを Office 365 に移行する方法](https://go.microsoft.com/fwlink/p/?linkid=524030)」をご覧ください。

  - 従来の Exchange サーバーで Outlook Anywhere が有効になっている必要があります。Exchange 2010 サーバーで Outlook Anywhere を有効にする方法の詳細については、「[Outlook Anywhere を有効にする](https://go.microsoft.com/fwlink/p/?linkid=187249)」を参照してください。Exchange 2007 サーバーで Outlook Anywhere を有効にする方法の詳細については、「[Outlook Anywhere を有効にする方法](https://go.microsoft.com/fwlink/p/?linkid=167210)」を参照してください。

  - Exchange 管理センター (EAC) または Exchange 管理コンソール (EMC) を使用して、この手順を実行することはできません。従来の Exchange サーバーでは、Exchange 管理シェル を使用する必要があります。Exchange Online の場合、Exchange Online PowerShell を使用する必要があります。詳細については、「[リモート PowerShell による Exchange への接続](https://technet.microsoft.com/ja-jp/library/jj984289\(v=exchg.150\))」を参照してください。

  - 一部の手順ではダウンタイムが必要になるため、この手順を始める前に、このトピック全体に目を通してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1: 移行スクリプトをダウンロードする

1.  「[パブリック フォルダー移行スクリプト](https://go.microsoft.com/fwlink/?linkid=299838)」からすべてのスクリプトとサポート ファイルをダウンロードします。

2.  PowerShell を実行するローカル コンピューターにスクリプトを保存します。たとえば C:\\PFScripts などです。すべてのスクリプトは同じ場所に保存する必要があります。

3.  以下のファイルを、[メールが有効なパブリック フォルダー - ディレクトリ同期スクリプト](https://go.microsoft.com/fwlink/p/?linkid=532376) からダウンロードします。
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  手順 2 と同じ場所 (C:\\PFScripts など) にスクリプトを保存します。

## 手順 2: 移行の準備

移行を開始する前に、以下の前提となる手順を実行します。

**前提条件となる手順の概要**

  - Active Directory 内に孤立したパブリック フォルダー メール オブジェクト (対応する Exchange オブジェクトがない Active Directory 内のオブジェクト) が存在しないことを確認します。

  - Active Directory 内のパブリック フォルダー用に構成された SMTP メール アドレスが、Exchange オブジェクトの SMTP メール アドレスと一致することを確認します。

  - 複数の Active Directory オブジェクトが、メールが有効な同一のパブリック フォルダーを指す状況を回避するため、Active Directory 内に重複するパブリック フォルダー オブジェクトがないことを確認します。

**従来の Exchange サーバー上で前提となる手順**

1.  組織が現在存在している Office 365 または Exchange Online DNS をポイントするようにすべてのインターネットを介した DNS キャッシュが更新されるまで、従来の Exchange サーバーで Office 365 または Exchange Online に存在するメール対応パブリック フォルダーへのルーティングが確実に継続して動作するようにします。そのためには、次のコマンドを実行して、メール メッセージを Office 365 または Exchange Online ドメインに適切にルーティングする既知の名前を使って、承認済みドメインを構成します。
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  パブリック フォルダーの名前にバックスラッシュ (**\\**) が含まれる場合、そのパブリック フォルダーは移行時に親パブリック フォルダー内に作成されます。移行を実行する前に、名前にバックスラッシュが含まれているパブリック フォルダーの名前を変更することをお勧めします。
    
    1.  Exchange 2010 では、名前にバックスラッシュが含まれているパブリック フォルダーを特定するには、次のコマンドを実行します。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  Exchange 2007 では、名前にバックスラッシュが含まれているパブリック フォルダーを特定するには、次のコマンドを実行します。
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  パブリック フォルダーが返された場合、次のコマンドを実行することで、名前を変更することができます。
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  以前に成功した移行の記録がないことを確認します。以前に成功した移行の記録がある場合は、その値を `$false` に設定する必要があります。値が `$true` に設定されていると移行要求が失敗します。
    
    1.  次の例では、パブリック フォルダーの移行ステータスを確認します。
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  *PublicFoldersLockedforMigration* プロパティまたは *PublicFolderMigrationComplete* プロパティの状態が `$true` の場合は、以下のコマンドを実行して値を `$false` に設定します。
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    

    > [!WARNING]
    > 上記のプロパティをリセットした後は、Exchange が新しい設定を検出するまで待機する必要があります。この処理が完了するまで最大 2 時間かかる場合があります。



4.  移行終了時に確認できるよう、最初に従来の Exchange サーバーで次の Exchange 管理シェル コマンドを実行して、現在のパブリック フォルダー展開のスナップショットを取得することをお勧めします。
    
    1.  移行元のフォルダー構造のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  アイテム数、サイズ、所有者などのパブリック フォルダーの統計情報のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  アクセス許可のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    移行の最後で比較するために、上記のコマンドから取得した情報を保存します。

5.  Microsoft Azure Active Directory Connect (Azure AD Connect) を使用してオンプレミスのディレクトリを Azure Active Directory と同期させる場合は、以下を実行する必要があります (Azure AD Connect を使用していない場合は、この手順を省略できます)。
    
    1.  オンプレミスのコンピューターで、Microsoft Azure Active Directory Connect を開き、**\[構成\]** を選択します。
    
    2.  **\[追加のタスク\]** 画面で、**\[同期オプションのカスタマイズ\]** を選択し、**\[次へ\]** をクリックします。
    
    3.  **\[Azure AD へ接続\]** 画面で、適切な資格情報を入力し、**\[次へ\]** をクリックします。接続したら、**\[オプションの機能\]** 画面が表示されるまで **\[次へ\]** をクリックし続けます。
    
    4.  **\[Exchange メール パブリック フォルダー\]** が選択されていないことを確認します。選択されていない場合には、次のセクションの「*Office 365 または Exchange Online の事前に必要な手順*」に進むことができます。選択されている場合には、クリックしてチェック ボックスをオフにし、**\[次へ\]** をクリックします。
        

        > [!NOTE]
        > <STRONG>[オプションの機能]</STRONG> 画面で <STRONG>[Exchange メール パブリック フォルダー]</STRONG> がオプションとして表示されない場合は、Microsoft Azure Active Directory Connect を終了して次のセクションの「<EM>Office 365 または Exchange Online の事前に必要な手順</EM>」に進むことができます。

    
    5.  **\[Exchange メール パブリック フォルダー\]** の選択を解除した後、**\[構成の準備完了\]** 画面が表示されるまで **\[次へ\]** をクリックし、**\[構成\]** をクリックします。

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [New-AcceptedDomain](https://technet.microsoft.com/ja-jp/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/ja-jp/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ja-jp/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/ja-jp/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/ja-jp/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Office 365 または Exchange Online の前提条件の手順**

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

2.  Office 365 内にパブリック フォルダーまたはパブリック フォルダー メールボックスが存在しないことを確認します。
    

    > [!IMPORTANT]
    > Office 365 または Exchange Online 内のパブリック フォルダーを表示する場合は、理由があると、パブリック フォルダーとパブリック フォルダーのメールボックスを削除する前にパブリック フォルダー階層の開始、組織内のユーザーを確認しておくこと。

    
    1.  Office 365 または Exchange Online PowerShell で次のコマンドを実行し、パブリック フォルダー メールボックスが存在するかどうかを確認します。
        
            Get-Mailbox -PublicFolder 
    
    2.  コマンドを実行しても、パブリック フォルダー メールバックスが返されなかった場合は、Step 3: Generate the CSV files に進んでください。上記のコマンドによってパブリック フォルダー メールボックスが返された場合は、以下のコマンドを使って、パブリック フォルダーが存在するかどうかを確認します。
        
            Get-PublicFolder
    
    3.  Office 365 または Exchange Online にパブリック フォルダーが存在する場合は、次の PowerShell コマンドを実行し、パブリック フォルダーを削除します。Office 365 内のパブリック フォルダーに含まれていたすべての情報を保存したかどうかを確認します。パブリック フォルダーを削除すると、パブリック フォルダーに含まれていたすべての情報は完全に削除されます。
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  パブリック フォルダ－を削除した後、次のコマンドを実行して、パブリック フォルダー メールボックスをすべて削除します。
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

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

1.  従来の Exchange サーバーで `Export-PublicFolderStatistics.ps1` スクリプトを実行し、フォルダー名からフォルダー サイズへのマッピングのファイルを作成します。このスクリプトは必ずローカル管理者が実行する必要があります。このファイルには、**FolderName** と **FolderSize** の 2 つの列があります。**FolderSize** 列の値は、バイト単位で表示されます。**\\PublicFolder01,10000** などとなります。
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* は、パブリック フォルダー階層をホストしているメールボックス サーバーの完全修飾ドメイン名です。
    
      - *Folder to size map path* は .csv ファイルを保存するネットワーク共有フォルダーのパスとファイル名です。このトピックでは後ほど、Exchange Online PowerShell を使って、このファイルにアクセスする必要があります。ファイル名だけを指定すると、ローカル コンピューター上の現在の PowerShellディレクトリにファイルが生成されます。
    
      - 必要に応じて、処理を続行する前にスクリプトの出力から、メールが有効なシステム フォルダーを削除します。

2.  `PublicFolderToMailboxMapGenerator.ps1` スクリプトを実行して、パブリック フォルダーとメールボックスとのマッピング ファイルを作成します。このファイルは、Exchange Online のパブリック フォルダー メールボックスの適正数を計算するために使用されます。
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    

    > [!IMPORTANT]
    > パブリック フォルダーのメールボックスへのマッピング ファイルは、1,000 行を超えないようにしてください。このファイルでは、1,000 行を超えている場合、パブリック フォルダーの構造を単純化する必要があります。1,000 行以上のファイルを使用して作業を進めるはお勧めできませんし、移行エラーが発生する可能性があります。

    
      - スクリプトを実行する前に、Exchange Online のテナントの現在のパブリック フォルダーの制限を確認するのには次のコマンドレットを使用します。パブリック フォルダーの現在のクォータ値をメモします。 `Get-OrganizationConfig | fl *quota*`
        
        Exchange online では、既定値は 1.7 GB **DefaultPublicFolderIssueWarningQuotaDefaultPublicFolderProhibitPostQuota**用に 2 GB です。
    
      - *Maximum mailbox size in bytes*では、新しいパブリック フォルダーのメールボックスに設定する最大サイズと同じです。Exchange Online では、パブリック フォルダーのメールボックスの最大サイズは 100 GB です。できるように、各パブリック フォルダーのメールボックスには、将来の拡張には、15 GB の設定を使用することをお勧めします。Exchange Online では、2 GB の既定パブリック フォルダーの \[投稿を禁止する"クォータは、です。2 GB を超える個々 のパブリック フォルダーがあれば、この問題を解決するのには次のオプションのいずれかを使用できます。
        
          - 移行バッチを開始する前に、次のコマンドレットを実行して既定のパブリック フォルダーの \[投稿を禁止する"クォータを増やします。
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - 移行バッチを開始する前に、コンテンツのコンテンツのサイズを 2 GB に減らす、または以下のパブリック フォルダーを削除します。
        
          - 移行バッチを開始する前に、以内各 2 GB は、複数のパブリック フォルダーにパブリック フォルダーを分割します。
        

        > [!NOTE]
        > パブリック フォルダーは、30 GB を超えていていない場合はコンテンツを削除するか、複数のパブリック フォルダーに分割するは不可能、ことをお勧めは、Exchange Online にパブリック フォルダーを移動しません。

    
      - *Folder to size map path*では、 `Export-PublicFolderStatistics.ps1`スクリプトを実行するときに作成した .csv ファイルのファイル パスと同じです。
    
      - *Folder to mailbox map path*は、この手順で作成したフォルダーのメールボックスを .csv ファイルのパスとファイル名と同じです。ファイル名だけを指定すると、ローカル コンピューター上の現在の PowerShell ディレクトリにファイルが生成されます。


> [!NOTE]
> スクリプトを実行し, .csv ファイルが生成された、すべての新しいパブリック フォルダーまたは既存のパブリック フォルダーへの更新は収集されません。



## 手順 4: Exchange Online でパブリック フォルダー メールボックスを作成する

1.  次のコマンドを実行し、ターゲットのパブリック フォルダー メールボックスを作成します。手順 3 で PublicFoldertoMailboxMapGenerator.ps1 スクリプトを実行して生成した .csv ファイルにある各メールボックスのターゲットのメールボックスを、このスクリプトは作成します。
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* は、手順 3 で PublicFoldertoMailboxMapGenerator.ps1 スクリプトによって生成されるファイルです。通常、パブリック フォルダー階層を参照する同時ユーザー接続の推定値は、組織内のユーザー数の合計より少なくなります。

## 手順 5:移行要求を開始する

1.  従来の Exchange サーバーにおいて次のコマンドを実行することにより、メールが有効なパブリック フォルダーを、ローカル Active Directory から Exchange Online に同期します。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` は Office 365 のユーザー名とパスワードです。`CsvSummaryFile` は、同期操作やエラーのログを .CSV 形式で記録する先のファイル パスです。
    

    > [!NOTE]
    > 実際にスクリプトを実行する前に、まず、そのスクリプトによるアクションをシミュレートすることをお勧めします。そのためには、スクリプトに <CODE>-WhatIf</CODE> パラメーターを指定して実行します。



2.  従来の Exchange サーバーで、移行要求を実行するために必要な以下の情報を取得します。
    
    1.  パブリック フォルダー管理者の役割が割り当てられたメンバーであるユーザーのアカウントの `LegacyExchangeDN` を検索します。これは、この手順の手順 3 で資格情報が必要だったユーザーと同じユーザーです。
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  パブリック フォルダー データベースが格納されているメールボックス サーバーの `LegacyExchangeDN` を検索します。
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  Outlook Anywhere ホスト名の FQDN を検索します。Outlook Anywhere に複数のインスタンスが存在する場合、従来の Exchange 組織で移行エンドポイントに一番近いインスタンスか、パブリック フォルダー レプリカに一番近いインスタンスのいずれかを選択します。次のコマンドを実行すると、Outlook Anywhere のすべてのインスタンスが検索されます。
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  Office 365 PowerShell で次のコマンドを実行すると、前の手順で返された情報が、移行要求で使われる変数に渡されます。
    
    1.  従来の Exchange サーバーで管理アクセス許可を持つユーザーの資格情報が、変数 `$Source_Credential` に渡されます。Exchange Online で実行される移行要求では、この資格情報を使って、コンテンツをコピーするために従来の Exchange サーバーにアクセスします。
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  手順 2a で検出された従来の Exchange サーバー上の移行ユーザーの `ExchangeLegacyDN` を使って、それを変数 `$Source_RemoteMailboxLegacyDN` に渡します。
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  前述の手順 2b で検出されたパブリック フォルダー サーバーの `ExchangeLegacyDN` を使って、それを変数 `$Source_RemotePublicFolderServerLegacyDN` に渡します。
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  前述の手順 2c で検出された Outlook Anywhere の外部ホスト名を使って、それを変数 `$Source_OutlookAnywhereExternalHostName` に渡します。
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  最後に Exchange Online PowerShell で次のコマンドを実行し、移行要求を作成します。
    

    > [!NOTE]
    > 以下の Exchange 管理シェル の例の認証方法は、Outlook Anywhere の設定と一致している必要があります。一致していない場合、コマンドは失敗します。

    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    ここで \<*folder\_mapping.csv*\> ファイルは Step 3: Generate the .csv files で生成されたファイルです。

5.  次のコマンドを使用して移行を開始します。
    
        Start-MigrationBatch PublicFolderMigration

バッチ移行は Exchange 管理シェル で **New-MigrationBatch** コマンドレットを使用して作成する必要がありますが、移行の進行と完了は EAC で表示および管理できます。**New-MigrationBatch** コマンドレットは、各パブリック フォルダー メールボックスのメールボックス移行要求を開始するので、メールボックスの移行ページを使用してこれらの要求の状態を表示することができます。以下の手順により、メールボックス移行ページにアクセスして、メールで受信可能な移行レポートを作成することができます。

1.  Exchange Online にログインし、EAC を開きます。

2.  **\[メールボックス\]** \> **\[移行\]** に移動します。

3.  作成した移行要求を選択して、**\[詳細\]** ウィンドウの **\[詳細の表示\]** をクリックします。

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/ja-jp/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/ja-jp/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/ja-jp/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ja-jp/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/ja-jp/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/ja-jp/library/jj218697\(v=exchg.150\))

## 手順 6: 従来の Exchange サーバーでパブリック フォルダーを最後の移行用にロック ダウンする (ダウンタイムが必要)

移行プロセスのこの時点まで、ユーザーはパブリック フォルダーにアクセスできます。次の手順では、ユーザーは従来のパブリック フォルダーからログ オフされ、移行で最終的な同期が完了するまでフォルダーはロックされます。このプロセスの間、ユーザーはパブリック フォルダーにアクセスできません。また、メール対応パブリック フォルダーに送信されたメールはキューに格納され、パブリック フォルダーの移行が完了するまで配信されません。

以下に示すように `PublicFoldersLockedForMigration` コマンドを実行する前に、すべてのジョブの状態が**同期済み**であることを確認します。これを行うには `Get-PublicFolderMailboxMigrationRequest` コマンドを実行します。すべてのジョブの状態が**同期済み**であることを確認した後にのみ、この手順を続行します。

従来の Exchange サーバーで次のコマンドを実行すると、最終処理のために従来のパブリック フォルダーがロックされます。

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

構文およびパラメーターの詳細については、「[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))」を参照してください。

組織に複数のパブリック フォルダー データベースがある場合、パブリック フォルダーのレプリケーションが完了するまで待ち、すべてのパブリック フォルダー データベースの `PublicFoldersLockedForMigration` フラグが解除されたこと、およびフォルダーに対して最近実行した保留中の変更が組織全体で統合されたことを確認する必要があります。この処理には数時間かかる場合があります。

## 手順 7: パブリック フォルダーの移行の終了処理をする (ダウンタイムが必要)

パブリック フォルダーの移行を完了するには、次のコマンドを実行します。

    Complete-MigrationBatch PublicFolderMigration

移行を完了すると、Exchange は、従来の Exchange サーバーと Exchange Online との間で最終的な同期を実行します。最終的な同期が成功すると、Exchange Online のパブリック フォルダーのロックが解除され、移行バッチの状態が**完了**に変更されます。一般的に、移行バッチの状態が**同期済み**から**完了処理中**に変わるまでに数時間かかり、この時点で最終的な同期が開始されます。

オンプレミスの Exchange サーバーと Office 365 の間のハイブリッド展開を構成した場合は、移行完了後に Exchange Online PowerShell で次のコマンドを実行する必要があります。

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 手順 8: パブリック フォルダーの移行をテストして、ロックを解除する

パブリック フォルダーの移行を完了した後、次のテストを実行して移行が成功したことを確認します。これにより、移行したパブリック フォルダー階層をテストしてから、Office 365 または Exchange Online のパブリック フォルダーを使用するように切り替えることができます。

1.  Office 365 または Exchange Online PowerShell で、移行したばかりのパブリック フォルダー メールボックスにテスト用のメールボックスを、既定のパブリック フォルダー メールボックスとして割り当てます。
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  前の手順で識別されたテスト ユーザーを使って Outlook 2007 以降にログオンし、次のパブリック フォルダー テストを実行します。
    
      - 階層の表示
    
      - アクセス許可のチェック
    
      - パブリック フォルダーの作成と削除
    
      - パブリック フォルダーに対する内容の追加と削除

3.  問題が発生した場合は、このトピックで後で、移行をロールバックを参照してください。階層とパブリック フォルダーの内容は、期待どおりに機能する場合は、次の手順に進みます。

4.  従来の Exchange サーバーで次のコマンドを実行すると、パブリック フォルダーの移行が完了したことが示されます。
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  移行が完了したことを確認した後、**Set-OrganizationConfig** の *PublicFoldersEnabled* パラメーターが `Local` に設定されていることを確認して、Exchange Online PowerShell で次のコマンドを実行します。
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

構文およびパラメーターの詳細については、以下のトピックを参照してください。

[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))

## 設定が適用されたことを確認する方法

「Step 2: Prepare for the migration」で、移行を開始する前にパブリック フォルダーの構造、統計、アクセス許可のスナップショットを取得する指示がありました。以下の手順では、移行完了後に同じスナップショットを取得して、パブリック フォルダーの移行が正しく行われたことを確認します。両方のファイルのデータを比較して、移行が正しく行われたことを確認します。

1.  新しいフォルダー構造のスナップショットを取得するには、Exchange Online PowerShell で次のコマンドを実行します。
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  アイテム数、サイズ、所有者などのパブリック フォルダーの統計情報のスナップショットを取得するには、Exchange Online PowerShell で次のコマンドを実行します。
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  アクセス許可のスナップショットを取得するには、Exchange Online PowerShell で次のコマンドを実行します。
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## 従来の Exchange サーバーからパブリック フォルダー データベースを削除する

移行が完了して Exchange Online パブリック フォルダーが想定どおりに動作することを確認したら、従来の Exchange サーバーのパブリック フォルダー データベースを削除する必要があります。


> [!IMPORTANT]
> パブリック フォルダー移行の前に、すべてのメールボックスは Office 365 に移行されているので、オンプレミス環境を介した一元的なメール フローではなく、Office 365 経由のトラフィックをルーティングすること (分散型のメール フロー) を強くお勧めします。一元的なメール フローのままにすることを選択した場合、オンプレミス組織からパブリック フォルダーのメールボックス データベースを削除しているため、パブリック フォルダーへの配信に問題が発生する可能性があります。



  - Exchange 2007 サーバーからパブリック フォルダー データベースを削除する方法の詳細は、「[パブリック フォルダ データベースの削除](https://go.microsoft.com/fwlink/?linkid=123678)」を参照してください。

  - Exchange 2010 サーバーからパブリック フォルダー データベースを削除する方法の詳細は、「[パブリック フォルダ データベースの削除](https://go.microsoft.com/fwlink/?linkid=81409)」を参照してください。

## 移行のロールバック

移行に関して何らかの問題が発生し、従来の Exchange パブリック フォルダーを再度アクティブにする必要がある場合は、次の手順を実行します。


> [!WARNING]
> 従来の Exchange サーバーに移行をロールバックすると、移行後にメール対応パブリック フォルダーに送信されたすべての電子メール、またはパブリック フォルダーに投稿された内容がすべて失われます。この内容を保存するには、パブリック フォルダーの内容を .pst ファイルにエクスポートして、ロールバック終了後に従来のパブリック フォルダーにインポートする必要があります。



1.  従来の Exchange サーバーで次のコマンドを実行すると、従来の Exchange パブリック フォルダーのロックが解除されます。この処理には数時間かかる場合があります。
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  Exchange Online PowerShell で次のコマンドを実行し、Exchange Online パブリック フォルダーをすべて削除します。
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  従来の Exchange サーバーで次のコマンドを実行すると、`PublicFolderMigrationComplete` フラグが `$false` に設定されます。
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## Outlook の PST エクスポートを使ってパブリック フォルダーを Office 365 に移行する

オンプレミスのパブリック フォルダー階層が 30 GB を超えている場合は、パブリック フォルダーを Office 365 または Exchange Online に移行するときに Outlook の PST エクスポートを使用しないことをお勧めします。Office 365 のオンライン パブリック フォルダー メールボックスの容量は、自動分割機能により管理されており、パブリック フォルダー メールボックスがサイズ クォータを超えると、この機能によって分割されます。PST エクスポートを使ってパブリック フォルダーを移行すると、自動分割機能はパブリック フォルダー メールボックスの急激な容量増加に対処できなくなり、自動分割機能によってプライマリ メールボックスからデータが移動されるまで、最大で 2 週間待たなければならない場合があります。また、Outlook の PST を使って Office 365 または Exchange Online にパブリック フォルダーをエクスポートする前に、次の点を考慮してください。

  - パブリック フォルダーのアクセス許可は、この処理の実行中に失われます。移行の前に、現在のアクセス許可をキャプチャし、移行の完了後に手動で追加します。

  - 複雑なアクセス許可を使用している場合や移行するフォルダーが多い場合は、コマンドレットを使って移行する方法をお勧めします。

  - PST エクスポートでの移行中に行われた元のパブリック フォルダーに対するアイテムやフォルダーの変更は失われます。したがって、エクスポートとインポート処理の完了に時間がかかる場合は、コマンドレットを使用する方法をお勧めします。

PST ファイルを使ってパブリック フォルダーを移行する場合は、移行を正常に実行するため以下の手順に従ってください。

1.  「Step 1: Download the migration scripts」の手順に従って、移行スクリプトをダウンロードします。`PublicFolderToMailboxMapGenerator.ps1` ファイルのダウンロードのみで十分です。

2.  「Step 3: Generate the .csv files」の手順 2 に従って、パブリック フォルダーとメールボックスとのマッピング ファイルを作成します。このファイルは、Exchange Online のパブリック フォルダー メールボックスの適正数を計算するために使用されます。

3.  マッピング ファイルに基づいて、必要なパブリック フォルダー メールボックスを作成します。詳細については、「[パブリック フォルダー メールボックスを作成する](create-a-public-folder-mailbox-exchange-2013-help.md)」を参照してください。

4.  New-PublicFolder コマンドレットで、*Mailbox* パラメータを使って各パブリック フォルダー メールボックスの最上位のパブリック フォルダーを作成します。

5.  Outlook を使って、PST ファイルをエクスポートし、インポートします。

6.  EAC を使って、パブリック フォルダーのアクセス許可を設定します。詳細については、「[新しい組織でパブリック フォルダーをセットアップする](set-up-public-folders-in-a-new-organization-exchange-2013-help.md)」トピックの「[Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md)」を参照してください。


> [!WARNING]
> PST 移行を既に開始しているが、プライマリ メールボックスがいっぱいであるという問題が生じた場合、PST 移行を回復するには次の 2 つの方法があります。 
> <OL>
> <LI>
> <P>自動分割によってプライマリ メールボックスからデータが移動されるまで待ちます。最大で 2 週間かかる場合があります。ただし、パブリック フォルダー メールボックスが完全にいっぱいになると、自動分割が完了するまで、そのすべてのパブリック フォルダーは新しいコンテンツを受信できません。</P>
> <LI>
> <P>「<A href="create-a-public-folder-mailbox-exchange-2013-help.md">パブリック フォルダー メールボックスを作成する</A>」を実行した後、<STRONG>New-PublicFolder</STRONG> コマンドレットで <EM>Mailbox</EM> パラメータを使用して、セカンダリ パブリック フォルダー メールボックスに残りのパブリック フォルダーを作成します。次の例は、セカンダリ パブリック フォルダー メールボックスに PF201 という新しいパブリック フォルダーを作成します。</P><PRE><CODE>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</CODE></PRE></LI></OL>



## Office 365 を初めて使用する場合


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning の小さいアイコン" alt="LinkedIn Learning の小さいアイコン" /> <strong>Office 365 を初めて使用する場合は、</strong><br />
LinkedIn Learning が提供する <a href="https://support.office.com/ja-jp/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> のための無料のビデオ コースをご覧ください。</p></td>
</tr>
</tbody>
</table>

