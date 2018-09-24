---
title: 'バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Office 365 グループに移行する'
TOCTitle: バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Office 365 グループに移行する
ms:assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt843873(v=EXCHG.150)
ms:contentKeyID: 74468741
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# バッチ移行を使用して、Exchange 2013 のパブリック フォルダーを Office 365 グループに移行する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2018-03-26_

**概要:**  Exchange 2013 のパブリック フォルダーを Office 365 グループに移動する方法

*バッチ移行*というプロセスを通じて、Exchange 2013 のパブリック フォルダーの一部またはすべてを、Office 365 グループに移動することができます。Office 365 グループは、パブリック フォルダーよりも優れた利点を提供する Microsoft の新しいコラボレーション製品です。パブリック フォルダーと Office 365 グループの相違点の概要と、組織が Office 365 グループに切り替えることのメリットとデメリットの根拠については、「[パブリック フォルダーを Office 365 グループに移行する](https://docs.microsoft.com/ja-jp/exchange/collaboration-exo/public-folders/migrate-your-public-folders-to-office-365-groups)」を参照してください。

この記事では、Exchange 2013 のパブリック フォルダーを実際にバッチ移行するためのステップごとの手順を示します。

## 始める前に把握しておくべき情報

移行の準備を始める前に、次の条件がすべて満たされていることを確認してください。

  - Exchange 2013 サーバーで、**Exchange 2013 CU15** 以降が稼働している必要があります。

  - Exchange Online で組織の管理役割グループのメンバーになっている必要があります。この役割グループは、Office 365 または Exchange Online にサブスクライブした場合に割り当てられるアクセス許可とは異なるものです。組織の管理役割グループを有効にする方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 で、組織の管理役割グループまたはサーバーの管理 RBAC 役割グループのメンバーになっている必要があります。詳細については、「[役割グループにメンバーを追加する](https://go.microsoft.com/fwlink/?linkid=299212)」を参照してください。

  - パブリック フォルダーを Office 365 グループに移行する前に、移行後に Office 365 グループにアクセスする必要があるユーザーのために、まずそれらのユーザーのメールボックスを Office 365 に移動することをお勧めします。詳細については、「[複数のメール アカウントを Office 365 に移行する方法](https://support.office.com/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842)」を参照してください。

  - 1 つ以上の Exchange サーバー (パブリック フォルダー メールボックスのホストも行っているサーバーであること) で MRS プロキシを有効にする必要があります。詳細については、「[MRS プロキシ エンドポイントのリモート移動を有効にする](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) または Exchange 管理コンソール (EMC) を使用して、この手順を実行することはできません。Exchange 2013 サーバーでは、Exchange 管理シェルを使用する必要があります。Exchange Online の場合、Exchange Online の PowerShell を使用する必要があります。詳細については、「[リモート PowerShell による Exchange Online への接続](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx)」を参照してください。

  - 現時点で、Office 365 グループに移行できるのは、カレンダーとメールのパブリック フォルダーだけです。他の種類のパブリック フォルダーの移行はサポートされていません。また、移行前に Office 365 のターゲット グループを作成しておく必要があります。

  - バッチ移行プロセスでは、Office 365 グループへ移行するパブリック フォルダーからメッセージとカレンダーのアイテムだけがコピーされます。ポリシー、ルール、アクセス許可など、パブリック フォルダーのその他のエンティティは、Office 365 グループでサポートされていないためコピーされません。

  - Office 365 グループには、50 GB のメールボックスが付属しています。移行するパブリック フォルダーのデータの合計が 50 GB 未満になるようにしてください。また、移行後にユーザーが将来的に新しいコンテンツを追加するための記憶領域を確保してください。移行するパブリック フォルダーのサイズは、合計で 25 GB 以下にすることをお勧めします。

  - これは、「オール オア ナッシング」の移行ではありません。移行したい特定のパブリック フォルダーを選択することができ、選択されたパブリック フォルダーのみが移行されます。移行対象のパブリック フォルダーにサブフォルダーがある場合、そのサブフォルダーは移行に自動的には含められません。移行する場合は、そのサブフォルダーを明示的に含める必要があります。

  - パブリック フォルダーがこの移行から影響を受けることは一切ありません。ただし、ロックダウン スクリプトを使用して、移行されたパブリック フォルダーを読み取り専用にすると、ユーザーはパブリック フォルダーの代わりに Office 365 グループを使用しなければならなくなります。 

  - 一部の手順ではダウンタイムが必要になるため、この手順を始める前に、この記事全体に目を通してください。

## 手順 1: スクリプトを取得する

Office 365 グループへのバッチ移行では、この記事で後述するように、移行のさまざまな時点で多数のスクリプトを実行する必要があります。[このサイト](https://www.microsoft.com/en-us/download/details.aspx?id=55985)から、スクリプトとサポート ファイルをダウンロードしてください。すべてのスクリプトとファイルをダウンロードしたら、`c:\PFtoGroups\Scripts` など同一の場所に保存してください。

続行する前に、次のすべてのスクリプトとファイルをダウンロードし、保存したことを確認してください。


> [!NOTE]
> 必ずすべてのスクリプトとファイルを同一の場所に保存してください。



  - **AddMembersToGroups.ps1:**  このスクリプトは、元のパブリック フォルダーのアクセス許可エントリに基づいて、Office 365 グループにメンバーおよび所有者を追加します。

  - **AddMembersToGroups.strings.psd1:**  このサポート ファイルはスクリプト `AddMembersToGroups.ps1` が使用します。

  - **LockAndSavePublicFolderProperties.ps1:**  このスクリプトは、パブリック フォルダーを読み取り専用にして変更されないようにし、メール関連のパブリック フォルダーのプロパティ (そのパブリック フォルダーでメールが有効な場合) をターゲット グループに移動します。これにより、パブリック フォルダーからターゲット グループにメールが転送されます。また、このスクリプトは、アクセス許可エントリとメール プロパティを変更前にバックアップします。

  - **LockAndSavePublicFolderProperties.strings.psd1:**  このサポート ファイルはスクリプト `LockAndSavePublicFolderProperties.ps1` が使用します。

  - **UnlockAndRestorePublicFolderProperties.ps1:**  このスクリプトは、`LockandSavePublicFolderProperties.ps1` で作成されたバックアップ ファイルを使用して、パブリック フォルダーのアクセス権とメール プロパティを復元します。

  - **UnlockAndRestorePublicFolderProperties.strings.psd1:**  このサポート ファイルはスクリプト `UnlockAndRestorePublicFolderProperties.ps1` が使用します。

  - **WriteLog.ps1:**  このスクリプトは、上述の 3 つのスクリプトでログを書き込めるようにします。

  - **RetryScriptBlock.ps1:**  このスクリプトは、一時的なエラーが発生した場合に、`AddMembersToGroups`、`LockAndSavePublicFolderProperties`、`UnlockAndRestorePublicFolderProperties` スクリプトが特定の動作を再試行できるようにします。

`AddMembersToGroups.ps1`、`LockAndSavePublicFolderProperties.ps1`、`UnlockAndRestorePublicFolderProperties.ps1`、およびこれらのスクリプトが環境内で実行するタスクの詳細については、この記事の後半の「移行スクリプト」を参照してください。

## 手順 2: 移行の準備をする

組織がこの移行の準備をするには、次の手順が必要です。

1.  Office 365 グループに移行したいパブリック フォルダー (メールとカレンダーの種類) の一覧をまとめます。

2.  移行対象の各パブリック フォルダーに対応するターゲット グループの一覧を作成します。各パブリック フォルダー用に Office 365 に新しいグループを作成するか、既存のグループを使用します。新しいグループを作成する場合は、「[Office 365 グループの概要](https://go.microsoft.com/fwlink/p/?linkid=858521)」を参照し、グループの必須設定を確認してください。移行するパブリック フォルダーの既定の権限が **Author** 以上である場合は、Office 365 で対応するグループを、プライバシー設定を **Public** にして作成する必要があります。ただし、ユーザーが Outlook の**グループ** ノードの下にパブリック グループを表示するには、そのパブリック グループに参加する必要があります。

3.  名前にバックスラッシュ (**\\**) を含むパブリック フォルダーは、名前を変更してください。そうしないと、パブリック フォルダーが正しく移行されないことがあります。

4.  Office 365 テナントに対して移行機能 **PAW** を有効にする必要があります。有効になっていることを確認するには、Exchange Online PowerShell で次のコマンドを実行します。
    
    ```powershell
    Get-MigrationConfig
    ```
    
    **Features** の下の出力に **PAW** がある場合は、この機能が有効になっており、「*手順 3: .csv ファイルを作成する*」に進むことができます。
    
    テナントに対して PAW がまだ有効になっていない場合、既存の移行バッチ (パブリック フォルダーのバッチかユーザーのバッチ) が存在することが原因である可能性があります。これらのバッチの状態は、Completed (完了) を含めていずれの状態の可能性もあります。移行バッチが存在する場合、既存の移行バッチを完了させて削除し、`Get-MigrationBatch` の実行時にレコードが返されなくなるようにしてください。既存のバッチをすべて削除すると、PAW は自動的に有効になるはずです。なお、変更が `Get-MigrationConfig` に即時に反映されない場合がありますが、それで正常です。この手順が完了したら、引き続き新しいユーザー移行のバッチを作成できます。

## 手順 3: .csv ファイルを作成する

移行スクリプトのいずれかの入力を実行するための .csv ファイルを作成します。

.csv ファイルには、次の列が含まれている必要があります。

  - **FolderPath:**  移行するパブリック フォルダーのパスです。

  - **TargetGroupMailbox:**  Office 365 のターゲット グループの SMTP アドレスです。次のコマンドを実行して、プライマリ SMTP アドレスを確認できます。
    
    ```powershell
    Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress
    ```

.csv ファイルの例:

  ```powershell
  "FolderPath","TargetGroupMailbox"
  "\Sales","sales@contoso.onmicrosoft.com"
  "\Sales\EMEA","emeasales@contoso.onmicrosoft.com"
  ```

なお、メール フォルダーとカレンダー フォルダーは、Office 365 の 1 つのグループにマージすることができます。ただし、一度の移行バッチ内で複数のパブリック フォルダーを 1 つのグループにマージする、その他のシナリオはサポートされていません。同じ Office 365 グループに複数のパブリック フォルダーをマップする必要がある場合は、連続して実行する必要がある異なる移行バッチを 1 つずつ実行することで達成することができます。移行バッチごとに最大で 500 のエントリを持つことができます。

1 つのパブリック フォルダーは、1 つの移行バッチで 1 つのグループにしか移行できません。

## 手順 4: 移行要求を開始する

この手順では、Exchange 環境から情報を収集し、その情報を Exchange Online の PowerShell で使用して移行バッチを作成します。その後、移行を開始します。

1.  Exchange 2013 サーバーで、MRS プロキシ エンドポイント サーバーを見つけてメモしておきます。後で移行要求を実行する際に、この情報が必要になります。

2.  Exchange Online の PowerShell で、上記の手順 1 で返された情報を使用して、次の各コマンドを実行します。これらのコマンドの各変数は、手順 1 からの値になります。
    
    1.  Exchange 2013 環境で管理者アクセス許可を持つユーザーの資格情報を、変数 `$Source_Credential` に渡します。最終的に Exchange Online で移行要求を実行する際に、内容を Exchange Online にコピーするために、この資格情報を使って Exchange 2013 サーバーにアクセスします。
        
          ```powershell
          $Source_Credential = Get-Credential
          <source_domain>\<PublicFolder_Administrator_Account>
          ```
    
    2.  上記の手順 1 でメモした、Exchange 2013 環境からの MRS プロキシ サーバーの情報を使って、その値を変数 `$Source_RemoteServer` に渡します。
        
        ```powershell
        $Source_RemoteServer = "<MRS proxy endpoint>"
        ```

3.  Exchange Online の PowerShell で、次のコマンドを実行して移行エンドポイントを作成します。
    
      ```powershell
      $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
      ```

4.  次のコマンドを実行して、パブリック フォルダーから Office 365 グループへの新しい移行バッチを作成します。コマンドは次のとおりです。
    
      - **CSVData** は、上記の「*手順 3: .csv ファイルを作成する*」で作成された .csv ファイルです。このファイルへの完全なパスを必ず指定してください。何らかの理由でファイルを移動した場合は、新しい場所を必ず確認して使用します。
    
      - **NotificationEmails** は、移行のステータスと進行状況に関する通知を受け取るメール アドレスを設定するために使用できるオプションのパラメーターです。
    
      - **AutoStart** はオプションのパラメーターで、使用すると、移行バッチは作成後すぐに開始されます。
    
      - **PublicFolderToUnifiedGroup** は、パブリック フォルダーから Office 365 グループへの移行バッチであることを示すパラメーターです。
    
    <!-- end list -->
    
      ```powershell
      New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
      ```

5.  Exchange Online の PowerShell で次のコマンドを実行することにより、移行を開始します。このステップが必要になるのは上記の手順 4 でバッチ作成時に `-AutoStart` パラメーターが使用されなかった場合のみであることに注意してください。
    
    ```powershell
    Start-MigrationBatch PublicFolderToGroupMigration
    ```

バッチ移行は Exchange Online の PowerShell の `New-MigrationBatch` コマンドレットを使用して作成する必要がありますが、移行の進行状況を Exchange 管理センター で表示および管理できます。移行の進行状況は [Get-MigrationBatch](https://technet.microsoft.com/ja-jp/library/jj219164\(v=exchg.150\)) および [Get-MigrationUser](https://technet.microsoft.com/ja-jp/library/jj218702\(v=exchg.150\)) コマンドレットを実行して表示することもできます。`New-MigrationBatch` コマンドレットは、Office 365 グループ メールボックスごとの移行ユーザーを開始し、メールボックス移行ページを使用してこれらの要求のステータスを表示できます。

メールボックス移行ページを表示するには、次の手順を実行します。

1.  Exchange Online で Exchange 管理センター を開きます。

2.  <strong>受信者</strong> に移動してから、<strong>移行</strong> を選択します。

3.  作成したばかりの移行要求を選択して、<strong>詳細</strong> ウィンドウの <strong>詳細の表示</strong> を選択します。

バッチのステータスが <strong>完了</strong> である場合、「*手順 5: パブリック フォルダーから Office 365 グループにメンバーを追加する*」に進むことができます。

## 手順 5: パブリック フォルダーから Office 365 グループにメンバーを追加する

必要に応じて、Office 365 のターゲット グループにメンバーを手動で追加できます。ただし、パブリック フォルダーのアクセス許可エントリに基づいてグループにメンバーを追加する場合は、次のコマンドに示すように、Exchange 2013 サーバーのスクリプト `AddMembersToGroups.ps1` を実行してこの追加を行う必要があります。Office 365 グループのメンバーとして追加するために、ユーザーのメールボックスを Exchange Online に同期する必要があります。Office 365 のグループのメンバーとしてどのパブリック フォルダーのアクセス許可が追加対象であるかを確認するには、この記事で後述する「移行スクリプト」を参照してください。

コマンドは次のとおりです。

  - **MappingCsv** は、上記の「*手順 3: .csv ファイルを作成する*」で作成された .csv ファイルです。このファイルへの完全なパスを必ず指定してください。何らかの理由でファイルを移動した場合は、新しい場所を必ず確認して使用します。

  - **BackupDir** は移行ログ ファイルを格納するディレクトリです。

  - **ArePublicFoldersOnPremises** はパブリック フォルダーがオンプレミスにあるのか、Exchange Online にあるのかを示すパラメーターです。

  - **Credential** は、Exchange Online のユーザー名とパスワードです。

<!-- end list -->

  ```powershell
  .\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
  ```

ユーザーが Office 365 のグループに追加されると、グループの使用を開始できます。

## 手順 6: パブリック フォルダーをロックする (パブリック フォルダーのダウンタイムが必要)

パブリック フォルダー内のデータの大部分が Office 365 グループに移行されたら、Exchange 2013 サーバー上のスクリプトの `LockAndSavePublicFolderProperties.ps1` を実行してパブリック フォルダーを読み取り専用にすることができます。この手順により、移行が完了する前に新しいデータがパブリック フォルダーに追加されるのを防ぐことができます。


> [!NOTE]
> 移行対象の各パブリック フォルダーの中にメールが有効なパブリック フォルダー (MEPF) がある場合、この手順により SMTP アドレスなどの、MEPF のプロパティの一部が Office 365 の対応するグループにコピーされ、その後でパブリック フォルダーのメールが無効になります。このスクリプトの実行後、MEPF の移行ではメールが無効になるため、電子メールは対応するグループで受信される代わりに MEPF への送信が開始されます。詳細については、この記事で後述する「移行スクリプト」を参照してください。



コマンドは次のとおりです。

  - **MappingCsv** は、上記の「*手順 3: .csv ファイルを作成する*」で作成された .csv ファイルです。このファイルへの完全なパスを必ず指定してください。何らかの理由でファイルを移動した場合は、新しい場所を必ず確認して使用します。

  - **BackupDir** は、アクセス許可エントリ、MEPF プロパティ、および移行ログ ファイルのバックアップ ファイルが格納されるディレクトリです。このバックアップは、パブリック フォルダーにロールバックする必要がある場合に役立ちます。

  - **ArePublicFoldersOnPremises** はパブリック フォルダーがオンプレミスにあるのか、Exchange Online にあるのかを示すパラメーターです。

  - **Credential** は、Exchange Online のユーザー名とパスワードです。

<!-- end list -->

  ```powershell
  .\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
  ```

## 手順 7: パブリック フォルダーの Office 365 グループへの移行を完了する

パブリック フォルダーを読み取り専用にしたら、もう一度移行を実行する必要があります。これは、データの最後の増分コピーに必要です。移行を再度実行する前に、既存のバッチを削除する必要があります。これを行うには、次のコマンドを実行します。

```powershell
Remove-MigrationBatch <name of migration batch>
```

次に、以下のコマンドを実行して、同じ .csv ファイルで新しいバッチを作成します。コマンドは次のとおりです。

  - **CsvData** は、上記の「*手順 3: .csv ファイルを作成する*」で作成された .csv ファイルです。このファイルへの完全なパスを指定してください。何らかの理由でファイルを移動した場合は、新しい場所を確認して使用します。

  - **NotificationEmails** は、移行のステータスと進行状況に関する通知を受け取るメール アドレスを設定するために使用できるオプションのパラメーターです。

  - **AutoStart** はオプションのパラメーターで、使用すると、移行バッチは作成後すぐに開始されます。

<!-- end list -->

  ```powershell
  New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
  ```

新しいバッチが作成されたら、Exchange Online の PowerShell で次のコマンドを実行することにより、移行を開始します。なお、この手順は上記のコマンドで `-AutoStart` パラメーターを使用しなかった場合にのみ必要です。

```powershell
Start-MigrationBatch PublicFolderToGroupMigration
```

この手順を完了したら (バッチステータスが**完了**になる)、すべてのデータが Office 365 グループにコピーされていることを確認します。その時点で、グループのデータ状況に問題がなければ、移行されたパブリック フォルダーを Exchange 2013 環境から削除することができます。


> [!IMPORTANT]
> 移行をロールバックしてパブリック フォルダーに戻す手順が用意されていますが、元のパブリック フォルダーが削除された後は実行できません。詳細については、「Office 365 グループからパブリック フォルダーにロールバックする方法」を参照してください。



## 既知の問題

次の既知の問題が、一般的なパブリック フォルダーから Office 365 グループへの移行中に発生する可能性があります。

  - メールが有効なパブリック フォルダーから Office 365 グループに SMTP アドレスを移動するスクリプトは、Exchange Online でアドレスをセカンダリ メール アドレスとしてのみ追加します。このため、環境内に Exchange Online Protection (EOP) または一元化されたメール フローの設定がある場合、移行後のグループ (セカンダリ メール アドレス) にメールを送信する際に問題が発生します。

  - .csv マッピング ファイルに無効なパブリック フォルダーのパスのエントリがある場合、移行バッチはエラーをスローせずに**完了**として表示され、それ以降のデータはコピーされません。

## 移行スクリプト

参考までに、このセクションでは、3 つの移行スクリプトとそれらのスクリプトが Exchange 環境で実行するタスクについて詳細に説明します。すべてのスクリプトとサポート ファイルは、[このサイト](https://www.microsoft.com/en-us/download/details.aspx?id=55985)からダウンロードできます。

## AddMembersToGroups.ps1

このスクリプトは、移行されるパブリック フォルダーのアクセス許可を読み取り、次のようにメンバーおよび所有者を Office 365 グループに追加します。

  - 次のアクセス許可ロールを持つユーザーは、Office 365 のグループにメンバーとして追加されます。 **アクセス許可ロール:**  所有者, 発行編集者, 編集者, 発行作成者, 作成者

  - 上記に加えて、以下の最小アクセス権を持つユーザーも Office 365 のグループにメンバーとして追加されます。 **アクセス権:**  ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems

  - アクセス権が「所有者」のユーザーは、所有者としてグループに追加され、その他の有効アクセス権を持つユーザーはメンバーとして追加されます。

  - セキュリティ グループを Office 365 のグループにメンバーとして追加することはできません。したがって、セキュリティ グループは展開され、個々のユーザーがセキュリティ グループのアクセス権に基づいてグループにメンバーまたは所有者として追加されます。

  - パブリック フォルダーに対するアクセス権を持つセキュリティ グループのユーザーが、同じパブリック フォルダーに対する明示的なアクセス許可を持っている場合は、明示的なアクセス許可が優先されます。 たとえば、「SG1」というセキュリティ グループに User1 と User2 のメンバーが含まれているとします。パブリック フォルダー「PF1」のアクセス許可のエントリは次のとおりです。
    
    SG1: PF1 の作成者
    
    User1: PF1 の所有者
    
    この場合、User 1 が Office 365 のグループに所有者として追加されます。

  - 移行するパブリック フォルダーの既定のアクセス許可が「作成者」以上の場合、スクリプトは対応するグループのプライバシー設定を「公開」に設定するように提案します。

このスクリプトは、パブリック フォルダーのロックダウン後でも、パラメーター `ArePublicFoldersLocked` を ` $true` に設定して実行できます。この場合、スクリプトは、ロックダウン中に作成されたバックアップ ファイルからアクセス許可を読み取ります。

## LockAndSavePublicFolderProperties.ps1

このスクリプトを実行すると、移行されるパブリック フォルダーが読み取り専用になります。メールが有効なパブリック フォルダーが移行されると、まずメールが無効になり、それらの SMTP アドレスが Office 365 のそれぞれのグループに追加されます。次に、アクセス許可エントリが変更されて読み取り専用になります。メールが有効なパブリック フォルダーのメール プロパティのバックアップとすべてのパブリック フォルダーのアクセス許可エントリは、何らかの変更がなされる前にコピーされます。

移行バッチが複数ある場合は、マッピング .csv ファイルごとに個別のバックアップ ディレクトリを使用する必要があります。

それぞれのメールが有効なパブリック フォルダーと Office 365 グループと共に、次のメール プロパティが格納されます。

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - SendAs Trustee list

上記のメール プロパティは、ロールバック プロセスで使用できる .csv ファイルに保存されます (パブリック フォルダーの使用に戻したい場合、詳細は「Office 365 グループからパブリック フォルダーにロールバックする方法」を参照してください)。メールが有効なパブリック フォルダーのプロパティのスナップショットも、PfMailProperties.csv というファイルに格納されます。このファイルはロールバック プロセスでは必要ありませんが、参照用に使用できます。

次のメール プロパティは、ロック ダウンの一環としてターゲット グループに移行されます。

  - PrimarySMTPAddress

  - EmailAddresses

  - SendAs Trustee list

  - GrantSendOnBehalfTo

スクリプトにより、メールが有効なパブリック フォルダーの移行の PrimarySMTPAddress と EmailAddresses が、Office 365 の対応するグループのセカンダリ SMTP アドレスとして追加されます。また、メールが有効なパブリック フォルダーのユーザーの SendAs と SendOnBehalfTo アクセス許可には、対応するターゲット グループで同等のアクセス許可が付与されます。

**許可されるアクセス権**

パブリック フォルダーがすべてのユーザーに対して読み取り専用になるようにするため、ユーザーには次のアクセス権だけが許可されます。これらは **ListOfAccessRightsAllowed** に格納されます。

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

アクセス許可エントリは次のように変更されます。

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>ロック ダウン前</th>
    <th>ロック ダウン後</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>なし</p></td>
    <td><p>なし</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>共同作成者</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>レビュー担当者</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>作成者</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>編集者</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>所有者</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  読み取りのアクセス許可を持たないユーザーのアクセス権は、そのまま変更されず、引き続き読み取り権限から拒否されます。

3.  カスタムのロールを持つユーザーの場合、**ListOfAccessRightsAllowed** に含まれないすべてのアクセス権は削除されます。ユーザーがフィルター処理後の許可リストからのアクセス権をいずれも持たない場合、これらのユーザーのアクセス権は「なし」に設定されます。

フォルダーのメールが無効になるときとその SMTP アドレスが Office 365 グループに追加されるときの間に、メールが有効なパブリック フォルダーへのメール送信に中断が生じる場合があります。

## UnlockAndRestorePublicFolderProperties.ps1

このスクリプトは、パブリック フォルダーのロック ダウン中に取得されたバックアップ ファイルに基づいて、アクセス許可をパブリック フォルダーに再度割り当てて戻します。また、このスクリプトは、Office 365 のそれぞれのグループからフォルダーの SMTP アドレスを削除した後で、メールが無効になったパブリック フォルダーのメールを有効にします。この処理中にわずかなダウンタイムが発生する可能性があります。

## Office 365 グループからパブリック フォルダーにロールバックする方法

方針を変更し、Office 365 グループを使用した後でパブリック フォルダーの使用に戻る場合、下記のコマンドは環境を移行前の状態に復元します。バックアップ ファイルが存在し、移行後のパブリック フォルダーを削除していない限り、ロールバックを実行できます。

Exchange 2013 サーバーで次のコマンドを実行します。コマンドは次のとおりです。

  - **BackupDir** は、アクセス許可エントリ、MEPF プロパティ、および移行ログ ファイルのバックアップ ファイルが格納されるディレクトリです。「*手順 6: カットオーバーするパブリック フォルダーをロックする (パブリック フォルダーのダウンタイムが必要)*」で指定したのと同じ場所を使用してください。

  - **ArePublicFoldersOnPremises** はパブリック フォルダーがオンプレミスにあるのか、Exchange Online にあるのかを示すパラメーターです。

  - **Credential** は、Exchange Online のユーザー名とパスワードです。

<!-- end list -->

  ```powershell
  .\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
  ```

Office 365 グループに追加されたアイテムやグループ内で実行された編集操作はパブリック フォルダーにコピーされないことに注意してください。したがって、パブリック フォルダーがグループだった間に追加された新しいデータがある場合、データの損失が生じることになります。

また、パブリック フォルダーのサブセットを復元することはできないことにも注意してください。つまり、移行されたすべてのパブリック フォルダーを復元する必要があります。

ロールバック プロセスの一部として Office 365 内の対応するグループは削除されません。それらのグループは手動で消去つまり削除する必要があります。

