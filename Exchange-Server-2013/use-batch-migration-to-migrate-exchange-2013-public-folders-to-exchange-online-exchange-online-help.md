---
title: 'バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Exchange Online に移行する: Exchange 2013 Help'
TOCTitle: バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Exchange Online に移行する
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432689
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Exchange Online に移行する

 

_**トピックの最終更新日:**2018-03-26_

**概要:** この記事では、最新のパブリック フォルダーを Exchange 2013 から Office 365 に移動する方法について説明します。

2013 の Exchange パブリック フォルダーを Exchange Online に移行するには、Exchange Server 2013 CU15 または後で、オンプレミス環境でを実行している必要があります。


> [!NOTE]
> 組織に Exchange 2013 と Exchange 2016 の両方のパブリック フォルダーがある場合に、そのすべてを Exchange Online に移動するには、<A href="https://go.microsoft.com/fwlink/p/?linkid=845314">この記事の Exchange 2016 バージョン</A>を参照して移行を計画し、実行してください。この場合も、Exchange 2013 サーバーに CU15 以降がインストールされている必要があります。



## 始める前に把握しておくべき情報

  - Exchange Server 2013 CU15 以降にアップグレードする際には、Active Directory を準備する必要もあります。準備しないと、パブリック フォルダーの移行が失敗します。Active Directory を準備すると、関連するすべての PowerShell コマンドレットとパラメーターを使って移行を準備して実行できるようになります。詳細については、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照してください。

  - Exchange Online で組織の管理役割グループのメンバーになっている必要があります。この役割グループは、Office 365 または Exchange Online にサブスクライブした場合に割り当てられるアクセス許可とは異なるものです。組織の管理役割グループを有効にする方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

  - Exchange Server 2013 では、組織の管理役割グループまたはサーバーの管理 RBAC 役割グループのメンバーになっている必要があります。詳細については、「[役割グループにメンバーを追加する](https://go.microsoft.com/fwlink/?linkid=299212)」をご覧ください。

  - 組織に 25 GB よりも大きい単一のパブリック フォルダーがある場合は、パブリック フォルダ－の移行を始める前に、そのフォルダーからコンテンツを削除して小さくするか、そのパブリック フォルダーのコンテンツを分割して複数の小さなパブリック フォルダーにすることをお勧めします。ここで言及している 25 GB の制限はパブリック フォルダーだけに適用され、そのフォルダーに子フォルダーやサブフォルダーがあってもそれらには適用されないのでご注意ください。これらのオプションがいずれも実行できない場合、パブリック フォルダーを Exchange Online に移動しないことをお勧めします。詳細については、「[Exchange Online の制限](https://go.microsoft.com/fwlink/p/?linkid=391188)」をご覧ください。
    

    > [!NOTE]
    > Exchange Online の現在のパブリック フォルダーのクォータが 25 GB 未満の場合は、<A href="https://go.microsoft.com/fwlink/p/?linkid=844062">Set-OrganizationConfig</A> コマンドレットを使用し、DefaultPublicFolderIssueWarningQuota パラメーターと DefaultPublicFolderProhibitPostQuota パラメーターを指定してクォータを大きくすることができます。



  - Office 365 と Exchange Online では、最大 1000 個のパブリック フォルダー メールボックスを作成できます。

  - ユーザーを Office 365 に移行しようとしている場合は、パブリック フォルダーを移行する前にユーザーの移行を完了している必要があります。詳細については、「[複数のメール アカウントを Office 365 に移行する方法](https://go.microsoft.com/fwlink/p/?linkid=842798)」をご覧ください。

  - 1 つ以上の Exchange サーバー (パブリック フォルダー メールボックスのホストもしているサーバー) で MR プロキシを有効にする必要があります。詳細については、「[MRS プロキシ エンドポイントのリモート移動を有効にする](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用して、この記事の移行手順を実行することはできません。代わりに、Exchange 2013 サーバーで Exchange 管理シェルを使用する必要があります。Exchange Online では、Exchange Online PowerShell を使用する必要があります。詳細については、「[Exchange Online PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=842801)」を参照してください。

  - 削除済みのアイテムや削除済みのフォルダーの Exchange 2013 から Exchange Online への移行がサポートされています。移行を始める前に、削除済みのフォルダーとフォルダー アイテムをすべて確認し、Exchange Online で不要なものをすべて完全に削除することをお勧めします。完全に削除すると回復できないのでご注意ください。
    
    次のコマンドを使用して、(Exchange オンプレミス環境で) Exchange の削除済みアイテム収集機能にある削除済みのパブリック フォルダーの一覧を表示できます。
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    特定のフォルダーを完全に削除するには、次のコマンドを使用します (この例では、'Calendar2' という名前のフォルダーを使用しています)。
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - 作業を始める前に、この記事全体をお読みください。ダウンタイムが必要になる手順があります。このダウンタイム中には、パブリック フォルダーにだれもアクセスできません。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 手順 1: 移行スクリプトをダウンロードする

1.  [Exchange 2013/2016 パブリック フォルダー移行スクリプト](https://go.microsoft.com/fwlink/p/?linkid=844893)から、すべてのスクリプトとサポート ファイルをダウンロードします。

2.  PowerShell を実行するローカル コンピューターにスクリプトを保存します。たとえば C:\\PFScripts などです。すべてのスクリプトは同じ場所に保存する必要があります。

ダウンロードするスクリプトとファイルは次のとおりです。

  - `Sync-ModernMailPublicFolders.ps1`   このスクリプトは、Exchange オンプレミス環境と Office 365 との間で、メールが有効なパブリック フォルダー オブジェクトを同期します。このスクリプトは、Exchange 2013 サーバーで実行します。

  - `SyncModernMailPublicFolders.strings.psd1` このサポート ファイルは Sync-ModernMailPublicFolders.ps1 スクリプトが使用します。同じ場所にダウンロードする必要があります。

  - `Export-ModernPublicFolderStatistics.ps1` このスクリプトは、フォルダー名からフォルダー サイズと削除済みのアイテム サイズへのマッピング ファイルを作成します。このスクリプトは Exchange 2013 サーバーで実行します。

  - `Export-ModernPublicFolderStatistics.strings.psd1` このサポート ファイルは Export-ModernPublicFolderStatistics.ps1 スクリプトが使用します。同じ場所にダウンロードする必要があります。

  - `ModernPublicFolderToMailboxMapGenerator.ps1` このスクリプトは、Export-ModernPublicFolderStatistics.ps1 スクリプトからの出力を使用して、パブリック フォルダーからメールボックスへのマッピング ファイルを作成します。このスクリプトは、Exchange 2013 サーバーで実行します。

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` このサポート ファイルは ModernPublicFolderToMailboxMapGenerator.ps1 スクリプトが使用します。同じ場所にダウンロードする必要があります。

  - `SetMailPublicFolderExternalAddress.ps1` このスクリプトは、オンプレミス環境内のメールが有効なパブリック フォルダーの `ExternalEmailAddress` を、Exchange Online の対応するものに更新します。この更新により、移行後に、メールが有効なパブリック フォルダー宛てのメールが適切に Exchange Online にルーティングされるようになります。このスクリプトは、Exchange 2013 サーバーで実行する必要があります。

  - `SetMailPublicFolderExternalAddress.strings.psd1` このサポート ファイルは SetMailPublicFolderExternalAddress.ps1 スクリプトが使用します。同じ場所にダウンロードする必要があります。

## 手順 2: 移行の準備

パブリック フォルダーの移行を始める前に、次のセクションの前提条件となる手順をすべて実行します。

**前提条件となる手順の概要**

移行を成功させるには、次の手順を実行する必要があります。

  - Active Directory 内に孤立したパブリック フォルダー メール オブジェクトが存在しないことを確認します。孤立したオブジェクトとは、対応する Exchange オブジェクトがない Active Directory 内のオブジェクトのことです。

  - Active Directory 内のパブリック フォルダー用に構成された SMTP メール アドレスが、Exchange オブジェクトの SMTP メール アドレスと一致することを確認します。

  - Active Directory 内に重複するパブリック フォルダー オブジェクトがないことを確認します。この手順は、複数の Active Directory オブジェクトが、メールが有効な同一のパブリック フォルダーを指す状況を回避するために必要です。

**オンプレミスの Exchange 2013 サーバー環境での前提条件となる手順**

Exchange 管理シェル (オンプレミス) で、次の手順を実行します。

1.  移行が完了すると、Exchange Online 内の新しい場所にある、メールが有効なパブリック フォルダーにメッセージを送るために、インターネットを介した DNS キャッシュが行われます。これには時間がかかります。この DNS の切り替えが行われている間に、既知の名前の承認済みドメインを作成して、移行したばかりのメールが有効なパブリック フォルダーがメッセージを受信することを確認できます。確認するには、Exchange オンプレミス環境で次のコマンドを実行します。この例で、`target domain` は Office 365 または Exchange Online のドメインで、ハイブリッド構成ウィザードにより送信コネクタが既に構成済みです。
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **例**:
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    オンプレミスの環境に承認済みドメインが既にある場合は、名前を `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` に変更し、その他の属性はそのまま保持します。
    
    オンプレミスの環境に承認済みドメインが既にあるかどうか確認するには、次のようにします。
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    承認済みドメインの名前を `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` に変更するには、次のように実行します。
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    

    > [!NOTE]
    > Exchange Online 内のメールが有効なパブリック フォルダーがインターネットから外部のメールを受信することを想定している場合は、Exchange Online と Exchange Online Protection (EOP) で Directory Based Edge Blocking (DBEB) を無効にする必要があります。詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/dn600322(v=exchg.150)">ディレクトリ ベースのエッジ ブロックを使用して無効な受信者に送信されたメッセージを拒否する</A>」を参照してください。



2.  パブリック フォルダーの名前にバックスラッシュ **\\** かスラッシュ**/** が含まれていると、移行プロセス中に指定のメールボックスに移行されない可能性があります。移行する前に、このようなフォルダーの名前を変更して、これらの文字を削除してください。
    
    1.  パブリック フォルダー名にバックスラッシュが含まれているパブリック フォルダーを配置するには、次のコマンドを実行します。
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  パブリック フォルダーが返された場合、次のコマンドを実行することで、名前を変更することができます。
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  以下の手順を実行して、組織内で以前に成功した移行の記録がないことを確認します。以前に成功した移行の記録がある場合は、その値を `$false` に設定する必要があります。
    
    値を変更する前に、誤って 2 回目の移行を実行しないように、以前に試みた移行を破棄できるか確認してください。
    
    1.  次のコマンドを実行して、以前に行われた移行と、それらの移行の状態を確認します。
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        

        > [!NOTE]
        > <CODE>PublicFoldersLockedforMigration</CODE> パラメーターか <CODE>PublicFolderMigrationComplete</CODE> パラメーターが <CODE>$true</CODE> の場合は、ある時点で従来のパブリック フォルダーを移行したことを意味しています。手順 3b に進む前に、従来のパブリック フォルダー データベースが使用停止されていることを確認します。

    
    2.  返された出力で、上記のいずれかの値の設定が `$true` になっている場合は、次のコマンドを実行して `$false` にします。
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  完了時に移行が成功したことを確認するため、該当するすべての Exchange 2013 サーバーに対して次のコマンドを実行することをお勧めします。現在のパブリック フォルダーの展開のスナップショットが取得されるので、後でこのスナップショットを使用して、移行したばかりのパブリック フォルダーと比較できます。
    

    > [!NOTE]
    > Exchange 組織のサイズによっては、これらのコマンドの実行に時間がかかる可能性があります。

    
      - 移行元のフォルダー構造のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - アイテム数、サイズ、所有者などのパブリック フォルダーの統計情報のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - パブリック フォルダーのアクセス許可のスナップショットを取得するには、次のコマンドを実行します。
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - メールが有効なパブリック フォルダーのスナップショットを取得するには、次のコマンドを実行します。
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - 移行が終了した時点で比較するために、先に実行したコマンドで生成されたファイルを安全な場所に保存します。

5.  Azure Active Directory、設置ディレクトリと同期する Microsoft Azure Active Directory 接続 (Azure AD 接続) を使用する場合は、次の操作を行う必要があります (Azure AD 接続を使用していない場合、この手順はスキップ)。
    
    1.  オンプレミスのコンピューターで、Microsoft Azure Active Directory Connect を開き、**\[構成\]** を選択します。
    
    2.  **\[追加のタスク\]** 画面で、**\[同期オプションのカスタマイズ\]** を選択し、**\[次へ\]** をクリックします。
    
    3.  **\[Azure AD へ接続\]** 画面で、適切な資格情報を入力し、**\[次へ\]** をクリックします。接続したら、**\[オプションの機能\]** 画面が表示されるまで **\[次へ\]** をクリックし続けます。
    
    4.  **\[Exchange メール パブリック フォルダー\]** が選択されていないことを確認します。選択されていない場合には、次のセクションの「*Exchange Online の事前に必要な手順*」に進むことができます。選択されている場合には、クリックしてチェック ボックスをオフにし、**\[次へ\]** をクリックします。
        

        > [!NOTE]
        > <STRONG>[オプションの機能]</STRONG> 画面で <STRONG>[Exchange メール パブリック フォルダー]</STRONG> がオプションとして表示されない場合は、Microsoft Azure Active Directory Connect を終了して次のセクションの「<EM>Exchange Online の事前に必要な手順</EM>」に進むことができます。

    
    5.  **\[Exchange メール パブリック フォルダー\]** の選択を解除した後、**\[構成の準備完了\]** 画面が表示されるまで **\[次へ\]** をクリックし、**\[構成\]** をクリックします。

**Exchange Online での前提条件となる手順**

Exchange Online PowerShell で、次の操作を実行します。

1.  既存のパブリック フォルダーの移行要求がないことを確認します。要求がある場合、その要求をクリアしないと、自身が行っている移行要求が失敗します。この手順は、パイプラインに既存の移行要求 (失敗した要求や中止しようとしている要求) が存在している可能性がある場合にのみ必要です。
    
    既存の移行要求は、バッチ移行とシリアル移行の 2 種類のうちのいずれかです。それぞれの種類の要求を検出するコマンドと、それぞれの種類の要求を削除するコマンドは次のとおりです。
    
    次の例では、既存のシリアル移行要求を検出します。
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    次の例では、既存のパブリック フォルダーのシリアル移行要求を削除します。
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    次の例では、既存のバッチ移行要求を検出します。
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    次の例では、既存のパブリック フォルダーのバッチ移行要求を削除します。
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  Office 365 のテナントに対して移行機能 **PAW** を有効にする必要があります。Exchange Online PowerShell で次のコマンドを実行すると、有効になっているか確認できます。
    
        Get-MigrationConfig
    
    **Features** の下の出力に **PAW** がある場合は、この機能が有効になっており、次の手順に進むことができます。
    
    テナントに対して PAW がまだ有効になっていない場合、既存の移行バッチ (パブリック フォルダーのバッチかユーザーのバッチ) があることが原因である可能性があります。これらのバッチの状態は、完了を含めていずれの状態の場合もあり得ます。移行バッチがある場合、移行バッチを完了して削除し、`Get-MigrationBatch` の実行時にレコードが返されなくなるようにしてください。既存のバッチをすべて削除すると、PAW は自動的に有効になるはずです。なお、`Get-MigrationConfig` に変更が即時に反映されない場合がありますが、それで正常です。ユーザーの移行の場合、この手順が完了したら、引き続き新しいバッチを作成できます。

3.  Exchange Online に既存のパブリック フォルダーやパブリック フォルダー メールボックスがないことを確認します。下記の手順に従った後に Exchange Online にパブリック フォルダーが見つかる場合には、パブリック フォルダーとパブリック フォルダー メールボックスの削除を始める前に、なぜパブリック フォルダーが存在するのか、組織内のだれがパブリック フォルダー階層を開始したかを特定することが重要です。
    
    1.  Office 365 または Exchange Online PowerShell で次のコマンドを実行し、パブリック フォルダー メールボックスが存在するかどうかを確認します。
        
            Get-Mailbox -PublicFolder
    
    2.  コマンドを実行しても、パブリック フォルダー メールバックスが返されない場合は、「手順 3: .csv ファイルを生成する」に進んでください。上記のコマンドによってパブリック フォルダー メールボックスが返される場合は、次のコマンドを実行して、パブリック フォルダーが存在するかどうかを確認します。
        
            Get-PublicFolder -Recurse
    
    3.  Office 365 または Exchange Online にパブリック フォルダーが存在する場合は、次の PowerShell コマンドを実行し、パブリック フォルダーを (不要であることを確認した後に) 削除します。パブリック フォルダーを削除する前に、パブリック フォルダー内の情報をすべて保存したかどうかを確認します。パブリック フォルダーを削除すると、すべての情報が完全に削除されるからです。
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  パブリック フォルダ－を削除した後、次のコマンドを実行して、パブリック フォルダー メールボックスをすべて削除します。
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## 手順 3: .csv ファイルを生成する

以前にダウンロードしたスクリプトを使用して、移行に使用する .csv ファイルを生成します。

1.  Exchange 管理シェル (オンプレミス) から `Export-ModernPublicFolderStatistics.ps1` スクリプトを実行して、フォルダー名からフォルダー サイズへのマッピング ファイルを作成します。このスクリプトを実行するには、ローカル管理者のアクセス許可が必要です。生成されたファイルには、**FolderName**、**FolderSize**、**DeletedItemSize** の 3 つの列が含まれます。**FolderSize** 列と **DeletedItemSize** 列の値は、バイト単位で表示されます。たとえば、**\\PublicFolder01,10240, 100** は、階層のルート内にある PublicFolder01 という名前のパブリック フォルダーのサイズが 10240 バイト (10.240 MB) で、このフォルダー内に 100 バイトの回復可能なアイテムがあることを意味しています。
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **例**:
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  `ModernPublicFolderToMailboxMapGenerator.ps1` スクリプトを実行して、ソースのパブリック フォルダーを Exchange Online の宛先のパブリック フォルダー メールボックスにマップする .csv ファイルを作成します。このファイルは、Exchange Online のパブリック フォルダー メールボックスの適正数を計算するために使用されます。
    

    > [!NOTE]
    > <CODE>ModernPublicFolderToMailboxMapGenerator.ps1</CODE>によって生成されたファイルでは、組織内のすべてのパブリック フォルダーの名前は含まれません。親フォルダーへの参照が含まれているより大きなフォルダー ツリー、またはフォルダーの名前のそれ自体は非常に大きい。特定のフォルダー ツリーを確認するのには、「例外」ファイルが使用され、特定のパブリック フォルダーのメールに大きなフォルダーが配置されるように、このファイルの考えることができます。ボックスです。正常なファイルでは、パブリック フォルダーのすべての 1 つを表示しないようにします。(別のパブリック フォルダーのメールボックスへ転送したマッピング ファイル内の別の行で明示的に記載されている) 場合、このマッピング ファイルに記載されている任意のフォルダーの子フォルダーは親フォルダーと同じパブリック フォルダーのメールボックスに移行も。

    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes` は、Exchange Online の単一のパブリック フォルダー メールボックスに移行しようとしているデータの最大量です。このフィールドの最大サイズは現在 50 GB ですが、将来拡張できるように、最大サイズの 50% などの小さめのサイズを使用することをお勧めします。
    
      - `Maximum mailbox recoverable items size in bytes` は、Exchange Online メールボックス上の回復可能なアイテムのクォータです。Exchange Online のパブリック フォルダー メールボックスの最大サイズは現在 50 GB です。` RecoverableItemsQuota` を 15 GB 以下に設定することをお勧めします。
    
      - `Folder-to-size map path` は、`Export-ModernPublicFolderStatistics.ps1` スクリプトの実行時に作成された .csv ファイルのファイル パスです。
    
      - `Folder-to-mailbox map path` は、この手順で作成しているフォルダーからメールボックスへのマッピング .csv ファイルのファイル パスです。ファイル名だけを指定すると、ローカル コンピューターの現在の PowerShell ディレクトリにファイルが生成されます。

**例**:

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv


> [!NOTE]
> Exchange Online 内の一意のパブリック フォルダーのメールボックスの数が 100 以上である場合にオンラインの Exchange パブリック フォルダーの移行をサポートしていません。



## 手順 4: Exchange Online でパブリック フォルダー メールボックスを作成する

次に、Exchange Online PowerShell で、移行後のパブリック フォルダーを含めるターゲットのパブリック フォルダー メールボックスを作成します。

1.  次のスクリプトを実行し、ターゲットのパブリック フォルダー メールボックスを作成します。このスクリプトは、以前に「*手順 3: .csv ファイルを生成する*」で `ModernPublicFoldertoMailboxMapGenerator.ps1` スクリプトを実行して生成した .csv ファイル内のメールボックスごとに、ターゲットのメールボックスを作成します。
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path` は、`ModernPublicFoldertoMailboxMapGenerator.ps1` スクリプトで生成された、フォルダーからメールボックスへのマッピング .csv ファイル (「*手順 3: .csv ファイルを生成する*」で生成されたファイル) のファイル パスです。

## 手順 5: 移行要求を開始する

この手順では、Exchange 2013 オンプレミス環境と Exchange Online で、いくつかのコマンドを実行する必要があります。

1.  パブリック フォルダー メールボックスをホストしているいずれかの Exchange 2013 サーバーから、次のスクリプトを実行します。このスクリプトは、メールが有効なパブリック フォルダーを、ローカル Active Directory から Exchange Online に同期します。このスクリプトの最新バージョンをダウンロードしてあることと、Exchange 管理シェルからこのスクリプトを実行していることを確認してください。
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential` は、Exchange Online の管理者のユーザー名とパスワードです。
    
      - `CsvSummaryFile` は、同期操作やエラーのログ ファイルの置き場所へのファイル パスです。ログは .csv 形式になります。

2.  Exchange 2013 サーバーで、MR プロキシ エンドポイント サーバーを見つけてメモしておきます。移行要求を実行する際に、この情報が必要になります。下記の手順 3b で使用するために、この情報を保存します。

3.  Exchange Online PowerShell で次のコマンドを実行すると、前の手順で返された資格情報と MRS 情報が、移行要求で使われるコマンドレット変数に渡されます。
    
    1.  Exchange 2013 オンプレミス環境で管理者アクセス許可を持つユーザーの資格情報を、変数 `$Source_Credential` に渡します。Exchange Online で実行する移行要求では、この資格情報を使って、パブリック フォルダーのコンテンツを Exchange Online にコピーするためにオンプレミスの Exchange 2013 サーバーにアクセスします。
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  上記の手順 2 でメモした、Exchange 2013 環境からの MRS プロキシ サーバーの情報を、次のように変数に渡します。
        
            $Source_RemoteServer = "<paste the value here>"

4.  Exchange Online PowerShell で、次のコマンドを実行して、パブリック フォルダー移行エンドポイントとパブリック フォルダー移行要求を作成します。
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    

    > [!NOTE]
    > 複数のメール アドレスは、コンマで区切って指定します。

    
    `folder_mapping.csv` は、「*手順 3: .csv ファイルを生成する*」で生成されたマップ ファイルです。完全なファイル パスを指定してください。何らかの理由でマップ ファイルを移動した場合は、新しい場所を使用していることを確認します。

5.  最後に Exchange Online PowerShell で次のコマンドを使用し、移行を開始します。
    
        Start-MigrationBatch PublicFolderMigration

バッチ移行は Exchange Online PowerShell で New-MigrationBatch コマンドレットを使用して作成する必要がありますが、移行の進行と完了の表示と管理は EAC で行うか Get-MigrationBatch コマンドレットを実行して行うことができます。New-MigrationBatch コマンドレットは、パブリック フォルダー メールボックスごとにメールボックス移行要求を開始するので、メールボックスの移行ページを使用してこれらの要求の状態を確認することができます。

メールボックス移行ページにアクセスするには、次のようにします。

1.  Exchange Online にログオンし、EAC を開きます。

2.  **\[受信者\]** に移動してから、**\[移行\]** を選択します。

3.  作成したばかりの移行要求を選択して、**\[詳細\]** ウィンドウの **\[詳細の表示\]** を選択します。

「*手順 6: Exchange 2013 サーバーでパブリック フォルダーをロック ダウンする* 」に進む前に、すべてのデータがコピーされており、移行中にエラーが発生していないことを確認します。バッチが**同期済み**の状態に移ったことを確認し終えたら、「*手順 2:移行の準備*」の「**オンプレミスの Exchange 2013 サーバー環境での前提条件となる手順**」の最後の手順で示されているコマンドを実行して、オンプレミスでパブリック フォルダーのスナップショットを取得します。これらのコマンドを実行し終えたら、次の手順に進むことができます。対象フォルダーの数によっては、これらのコマンドが完了するまでにしばらく時間がかかることがあるのでご注意ください。

## 手順 6: Exchange 2013 環境でパブリック フォルダーを最終的な移行用にロック ダウンする (パブリック フォルダーのダウンタイムが必要)

移行プロセスのこの時点まで、ユーザーはオンプレミスのパブリック フォルダーにアクセスできました。次の手順では、ユーザーは Exchange 2013 のパブリック フォルダーからログオフされることになり、移行プロセスで最終的な同期が完了するまでフォルダーはロックされます。この間、ユーザーはパブリック フォルダーにアクセスできません。また、メールが有効なパブリック フォルダーに送信されたメッセージはキューに格納され、パブリック フォルダーの移行が完了するまで配信されません。

以下に示すように `PublicFolderMailboxesLockedForNewConnections` コマンドを実行する前に、すべてのジョブの状態が**同期済み**であることを確認します。これを行うには `Get-PublicFolderMailboxMigrationRequest` コマンドを実行します。すべてのジョブの状態が**同期済み**であることを確認した後にのみ、この手順を続行します。

オンプレミスの環境で次のコマンドを実行すると、最終処理のために Exchange 2013 のパブリック フォルダーがロックされます。

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true


> [!NOTE]
> <CODE>-PublicFolderMailboxesLockedForNewConnections</CODE> パラメーターにアクセスできない場合、上記の「<EM>始める前に把握しておくべき情報</EM>」の指示どおりに CU のアップグレード時に Active Directory を準備しなかったことが原因である可能性があります。詳細については、「<A href="prepare-active-directory-and-domains-exchange-2013-help.md">Active Directory とドメインを準備する</A>」を参照してください。<BR>パブリック フォルダー自体を移行する<STRONG>前に</STRONG>、そのパブリック フォルダーへのアクセスを必要とするユーザーを最初に移行する必要があることにもご注意ください。



組織の複数の Exchange 2013 サーバーにパブリック フォルダー メールボックスがある場合、AD のレプリケーションが完了するまで待つ必要が生じます。完了したら、すべてのパブリック フォルダー メールボックスの `PublicFolderMailboxesLockedForNewConnections` フラグが採用されたことと、ユーザーが最近パブリック フォルダーに加えた保留中の変更が組織全体で収束したことを確認できます。これらのすべてには数時間かかることがあります。

## 手順 7:パブリック フォルダーの移行の終了処理をする (パブリック フォルダーのダウンタイムが必要)

パブリック フォルダーの移行を完了する前に、オンプレミスの Exchange 環境で他のパブリック フォルダー メールボックスの移動やパブリック フォルダーの移動が行われていないことを確認する必要があります。これを行うには、`Get-MoveRequest` および `Get-PublicFolderMoveRequest` コマンドレットを使用して、既存のパブリック フォルダーの移動をリストします。進行中の移動がある場合、または**完了**状態の移動がある場合は、それらを削除します。

次に、パブリック フォルダーの移行を完了するために、Exchange Online PowerShell で次のコマンドを実行します。

    Complete-MigrationBatch PublicFolderMigration

このコマンドを実行すると、Exchange は、オンプレミスの Exchange 組織と Exchange Online との間の最終的な同期を行います。この期間、移行バッチの状態は**同期から**に変更**完了**、し、最後に**完了**します。最終的な同期が成功した場合は、オンラインの Exchange のパブリック フォルダーはロックできません。

一般的に、移行バッチの状態が**同期済み**から**完了処理中**に変わるまでに数時間かかり、この時点で最終的な同期が開始されます。

## 手順 8:Exchange Online のパブリック フォルダーをテストしてロックを解除する

パブリック フォルダーの移行を完了した後、次の手順を実行して、移行が成功したかテストし、完了したことを正式に確認します。この最後のタスクにより、移行したパブリック フォルダー階層をテストしてから、Exchange Online のパブリック フォルダーを使用するように組織を完全に切り替えることができるようになります。

1.  Exchange Online PowerShell で、次のようにテスト ユーザー メールボックスを割り当てて、移行したばかりのパブリック フォルダー メールボックスのいずれかが既定のパブリック フォルダー メールボックスとして使用されるようにします。
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    パブリック フォルダーの作成に必要なアクセス許可が、テスト ユーザーにあることを確認します。

2.  前の手順で指定し、次のパブリック フォルダーのテストを実行し、テスト ユーザーと Outlook にログオンします。変更を反映するための 15 ~ 30 分かかる場合があることを注意してください。Outlook では、変更の内容を後に、求めるメッセージが何回かを再起動します。
    
    1.  階層の表示
    
    2.  アクセス許可のチェック
    
    3.  パブリック フォルダーの作成と削除
    
    4.  パブリック フォルダーに対する内容の追加と削除
    
    すべての問題に実行し、完全にオンラインの Exchange 組織のパブリック フォルダーを切り替える準備ができていないことを確認すると場合、は、 [Exchange 2013 から Exchange Online へのパブリック フォルダーの移行をロールバックする](roll-back-a-public-folder-migration-from-exchange-2013-to-exchange-online-exchange-2013-help.md)を参照してください。

3.  次のコマンドを実行 Exchange オンライン Exchange パブリック フォルダーのロックを解除する PowerShell オンライン。コマンドを実行した後、変更を有効に約 15 ~ 30 分がかかる場合があります。Outlook が変更の内容になると、プログラムを何度か再起動するのには、ユーザーが表示こと可能性があります。
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 手順 9:オンプレミスでの移行の終了処理を行う

パブリック フォルダーのメールが有効な設置に e メールを有効にするには、次の手順を実行します。

1.  オンプレミスの環境で、次のスクリプトを実行し、メールが有効なパブリック フォルダーに対するすべてのメールが Exchange Online に正しくルーティングされることを確認します。このスクリプトは、Exchange Online の対応するフォルダーを指す `ExternalEmailAddress` を使用して、メールが有効なパブリック フォルダーにスタンプを適用します。
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  テストが成功した場合は、オンプレミスの環境で次のコマンドを実行して、パブリック フォルダーの移行が完了したことを示します。
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## 設定が適用されたことを確認する方法

「手順 2: 移行の準備」で、オンプレミスのパブリック フォルダーの構造、統計情報、アクセス許可に関するスナップショットを取得しました。次のステップでは、Exchange Online への移行後に同様のスナップショットを取得して、パブリック フォルダーの移行が成功したことを確認します。両ファイルのデータを比較して、移行が成功したことを確認します。

1.  新しいフォルダー構造のスナップショットを取得するには、Exchange Online PowerShell で次のコマンドを実行します。
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  アイテム数、サイズ、所有者などのパブリック フォルダーの統計情報のスナップショットを取得するには、Exchange Online PowerShell で次のコマンドを実行します。
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  アクセス許可のスナップショットを取得するには、Exchange Online PowerShell で次のコマンドを実行します。
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  メールが有効なパブリック フォルダーのスナップショットを取得するには、Exchange Online PowerShell で次のコマンドを実行します。
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## 既知の問題

組織内に発生する一般的なパブリック フォルダー移行の問題を次に示します。

  - Exchange Online 内の一意のパブリック フォルダーのメールボックスの数が 100 以上である場合にオンラインの Exchange パブリック フォルダーの移行をサポートしていません。

  - ルート パブリック フォルダーや EFORMS REGISTRY フォルダーに対するアクセス権が Exchange Online に移行されず、Exchange Online で手動で適用する必要が生じます。適用するには、Exchange Online PowerShell で次のコマンドを実行します。このコマンドは、オンプレミスでは存在し Exchange Online では存在しないアクセス許可エントリごとに 1 度ずつ実行します。
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - 一部のパブリック フォルダーのメールボックスがパブリック フォルダー階層を処理していない場合、いくつかのパブリック フォルダーの移行は失敗します。これは、1 つまたは複数のメールボックス上の`IsExcludedFromServingHierarchy`パラメーターを`$true`に設定されていることを意味します。これを回避するには、階層構造を提供する Exchange Online のすべてのメールボックスを設定します。

  - **送信者**と**代理人として送信する**のアクセス許可が Exchange Online に移行されません。移行の際にこの問題が発生する場合は、オンプレミスの環境で次のコマンドを使用し、だれがこれらのアクセス許可を持っているかをメモします。
    
    オンプレミスで送信者アクセス許可を持つパブリック フォルダーを調べるには、次のようにします。
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    オンプレミスで代理人として送信するアクセス許可を持つパブリック フォルダーを調べるには、次のようにします。
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    Exchange Online でメールが有効なパブリック フォルダーに送信者アクセス許可を追加するには、Exchange Online PowerShell で次のように入力します。
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **例**:
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    Exchange Online でメールが有効なパブリック フォルダーに代理人として送信するアクセス許可を追加するには、Exchange Online PowerShell で次のように入力します。
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **例**:
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" フォルダーの下に 10,000 を超える数のフォルダーがあると、移行が失敗することがあります。したがって、"\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" フォルダーをチェックして、10,000 を超える数のフォルダーが直下にないか (直接の子) どうかを確認してください。次のコマンドを使用すると、現在の場所にあるパブリック フォルダーの数を確認できます。
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    Exchange Online は、10,000 個を超えるサブフォルダーをサポートしていないために、10,000 個を超えるフォルダーの移行が失敗します。このような構成のブロックを解除するためのスクリプトを開発中です。その間は、パブリック フォルダーの移行はお待ちいただくことをお勧めします。

  - 移行ジョブが進行しない、または停止してしまう。これは、並列で実行されているジョブの数が多すぎて、ジョブが断続的なエラーで失敗している場合に発生することがあります。`MaxConcurrentMigrations` と `MaxConcurrentIncrementalSyncs` を小さい数値に変更することによって、同時実行ジョブの数を減らすことができます。これらの値を設定するには、次の例を使用します。
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - 移行ジョブが次のエラーで失敗する。"エラー:収集フォルダーの収集。"このエラーが発生した場合、バッチを停止してから再起動すると、解決します。

  - 移行ジョブが失敗し、生成、"次のエラーにより要求が検疫された: 指定されたキーがディクショナリ内に存在しない"エラー メッセージ。これは、移行ジョブをコピーできませんフォルダーに破損している項目がある場合に発生します。この問題を回避するには。
    
    1.  移行バッチを停止します。
    
    2.  破損した項目を含むフォルダーを特定します。移行レポートに、エラーが発生したときにコピー中だったフォルダーへの参照が含まれています。
    
    3.  オンプレミス環境で、影響のあったフォルダーをプライマリ パブリック フォルダーのメールボックスに移動します。`New-PublicFolderMoveRequest` コマンドレットを使用してフォルダーを移動できます。
    
    4.  フォルダーの移動を完了するまで待機します。それが完了したら、移動要求を削除します。移行バッチを再開します。

## Exchange オンプレミス環境からパブリック フォルダー メールボックスを削除する

移行の完了後に、Exchange Online のパブリック フォルダーが想定どおりに動作しており、想定しているすべてのデータが含まれていることを確認したら、オンプレミスのパブリック フォルダー メールボックスを削除できます。

この手順ではないこと元に戻すことは、パブリック フォルダーのメールボックスを削除した後は復元できませんので注意します。したがって、だけでなく、移行の成功を確認するには、監視することも、オンラインの Exchange パブリック フォルダー設置型のパブリック フォルダーのメールボックスを削除する前に、いくつかの週を強くお勧めします。

