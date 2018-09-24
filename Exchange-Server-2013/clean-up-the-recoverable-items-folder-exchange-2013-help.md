---
title: '回復可能なアイテム フォルダーのクリーンアップ: Exchange 2013 Help'
TOCTitle: 回復可能なアイテム フォルダーのクリーンアップ
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50555809
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- メッセージ流出
- メッセージ流出クリーンアップ
- 分類されたメッセージ流出
- 分類されたメッセージ流出クリーンアップ
- 分類された流出
- 分類された流出のクリーンアップ
- 検索と破棄
ms.translationtype: HT
---

# 回復可能なアイテム フォルダーのクリーンアップ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-09-30_

回復可能なアイテム フォルダー (以前のバージョンの Exchange では*収集*と呼ばれていました) により、誤りによる削除または悪意による削除から保護するとともに、訴訟または調査の前または最中に通常行われる検索作業がしやすくなります。回復可能なアイテム フォルダーの詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」を参照してください。

メールボックスの回復可能なアイテム フォルダーのクリーンアップ方法は、メールボックスがインプレース保持や訴訟ホールドの対象かどうか、または単一アイテムの回復が有効かどうかによって異なります。

  - メールボックスがインプレース保持や訴訟ホールドの対象でない場合、または単一アイテムの回復が有効でない場合は、回復可能なアイテム フォルダーからアイテムを削除できます。削除が行われた後は、単一アイテムの回復を使用してアイテムを回復することはできません。

  - メールボックスがインプレース保持や訴訟ホールドの対象であるか、または単一アイテムの回復が有効になっている場合は、保持やホールドが解除されるかまたは単一アイテムの回復が無効になるまでメールボックスのデータを保存することが重要です。この場合、回復可能なアイテム フォルダーをクリーンアップするには、より詳細な手順の実行が必要です。

インプレース保持と訴訟ホールドの詳細については、「[インプレース保持と訴訟ホールド](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-and-litigation-holds)」を参照してください。単一アイテムの回復の詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」の「Single Item Recovery」を参照してください。

回復可能なアイテム フォルダーの詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - この手順の予想所要時間:30 分。これは、回復可能なアイテム フォルダーのサイズによって異なる場合があります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メールボックス内容の削除」。

  - 回復可能なアイテム フォルダーを誤ってクリーンアップしてしまうとデータの損失に繋がるため、回復可能なアイテム フォルダーと、そのコンテンツを削除することによる影響を理解することは重要です。この手順を実行する前に、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」の情報を確認することをお勧めします。

  - Exchange 管理センター (EAC) を使用して、これらの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## シェルを使用して、保留になっていないメールボックスまたは単一アイテムの回復が有効になっていないメールボックスの回復可能なアイテム フォルダーからアイテムを削除する

この例では Gurinder Singh の回復可能なアイテム フォルダーからアイテムを完全に削除し、また検出検索メールボックス (Exchange セットアップで作成した検出メールボックス) の GurinderSingh-RecoverableItems フォルダーにアイテムをコピーします。

```powershell
Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
```


> [!NOTE]
> 別のメールボックスにコピーせずにメールボックスからアイテムを削除するには、前述のコマンドを <EM>TargetMailbox</EM> および <EM>TargetFolder</EM> パラメーターなしで実行します。



構文およびパラメーターの詳細については、「[Search-Mailbox](https://technet.microsoft.com/ja-jp/library/dd298173\(v=exchg.150\))」を参照してください。

## シェルを使用して、保留になっているメールボックスまたは単一アイテムの回復が有効になっているメールボックスの回復可能なアイテム フォルダーをクリーンアップする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メールボックス内容の削除」。

メールボックスが、その回復可能なアイテムのクォータに達する場合は、フォルダーからアイテムを削除せずにクォータを増やすことをお勧めします。回復可能なアイテムの警告クォータに関連するアプリケーション ログのイベントを監視して、必要な作業 (たとえば、クォータの増加または警告クォータに達するメールボックスの \[回復可能なアイテム\] フォルダーの増大に関する調査) を実行することもできます。

格納域の制約または類似の問題により、回復可能なアイテムのクォータを増やすことができない場合で、インプレース保持/訴訟ホールドの対象となっているメールボックスまたは単一アイテムの回復が有効になっているメールボックスの回復可能なアイテム フォルダーからメッセージを削除する必要がある場合、最初にユーザーの回復可能なアイテム フォルダーから別のメールボックスにデータをコピーすることをお勧めします。1 つのボリュームの格納域の制約によりアイテムを削除する場合、適切な格納域を有するボリュームに配置されたメールボックスにアイテムをコピーできます。

この手順は、Gurinder Singh の回復可能なアイテム フォルダーから、検出検索メールボックスの GurinderSingh-RecoverableItems フォルダーへとアイテムをコピーします。回復可能なアイテム フォルダーからアイテムをコピーおよび削除する前に、アイテムが回復可能なアイテム フォルダーから削除されないことを確認するために、最初にいくつかの手順を実行する必要があります。アイテムを検出またはバックアップ メールボックスにコピーしてフォルダーをクリーンアップした後は、メールボックスを以前の設定に戻すことができます。

1.  以下のクォータ設定を取得します。値をメモして、回復可能なアイテム フォルダーをクリーンアップした後に、これらの設定を戻せるようにします。
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    

    > [!NOTE]
    > <EM>UseDatabaseQuotaDefaults</EM> パラメーターが <CODE>$true</CODE> に設定されている場合、以前のクォータ設定は適用されません。メールボックス データベース上に構成された対応するクォータ設定が適用され、個人のメールボックス設定にも適用されます。

    
    ```powershell
    Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults
    ```

2.  メールボックスのメールボックス アクセス設定を取得します。後で使用するために、これらの設定を忘れずにメモします。
    
    ```powershell
    Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled
    ```

3.  回復可能なアイテム フォルダーの現在のサイズを取得します。サイズをメモして、手順 6 でクォータを増やすことができるようにします。
    
    ```powershell
    Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize
    ```

4.  現在の管理フォルダー アシスタントのワーク サイクル構成を取得します。後で使用するために、設定を忘れずにメモします。
    
    ```powershell
    Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle
    ```

5.  メールボックスへのクライアント アクセスを無効にし、この手順の実行中にメールボックス データに対して変更が行われないようにします。
    
    ```powershell
    Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false
    ```

6.  回復可能なアイテム フォルダーからアイテムが削除されないことを確認するために、回復可能なアイテムのクォータを増やし、回復可能なアイテムの警告クォータを増やし、削除されたアイテムの保持期間をユーザーの回復可能なアイテム フォルダーの現在のサイズよりも大きく設定します。これは、インプレース保持または訴訟ホールドの対象となっているメールボックスのメッセージを保持するのに特に重要です。これらの設定を現在のサイズの 2 倍に増やすことをお勧めします。
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false
    ```

7.  メールボックス サーバーの管理フォルダー アシスタントを無効にする。
    
    ```powershell
    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
    ```
    

    > [!IMPORTANT]
    > メールボックスがデータベース可用性グループ (DAG) のメールボックス データベースに存在する場合、データベースのコピーをホストする各 DAG メンバー上で管理フォルダー アシスタントを無効にする必要があります。これにより、データベースが別のサーバーにフェールオーバーした場合に、サーバー上の管理フォルダー アシスタントがメールボックスのデータを削除するのを防止します。



8.  単一アイテムの回復を無効にし、訴訟ホールドからメールボックスを削除します。
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
    ```
    

    > [!IMPORTANT]
    > このコマンドを実行した後、単一アイテムの回復または訴訟ホールドを無効にするのに最大 1 時間かかる可能性があります。それ以上に時間が経過した場合にのみ、次の手順を実行することをお勧めします。



9.  アイテムを回復可能なアイテム フォルダーから検出検索メールボックスのフォルダーにコピーして、ソース メールボックスからコンテンツを削除します。
    
    ```powershell
    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    ```
    
    指定した条件に一致するメッセージのみを削除する必要がある場合は、*SearchQuery* パラメーターを使用して条件を指定します。この例では、<strong>件名</strong>フィールドに「Your bank statement」という文字列が含まれるメッセージを削除します。
    
    ```powershell
    Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    ```
    

    > [!NOTE]
    > 検出検索メールボックスにアイテムをコピーする必要はありません。任意のメールボックスにメッセージをコピーできます。ただし、機密性の高いメールボックス データへのアクセスを防止するために、承認されたレコード マネージャーにのみアクセスが制限されたメールボックスにメッセージをコピーすることをお勧めします。既定値では、既定の検出検索メールボックスへのアクセスは、"Discovery Management/検出の管理" 役割グループのメンバーに制限されています。詳細については、「<A href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">インプレース電子情報開示 (eDiscovery)</A>」を参照してください。



10. メールボックスが訴訟ホールドの対象だった場合または以前に単一アイテムの回復が有効だった場合は、それらの機能を再度有効にします。
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
    ```
    

    > [!IMPORTANT]
    > このコマンドを実行した後、単一アイテムの回復または訴訟ホールドを有効にするのに最大 1 時間かかる可能性があります。それ以上に時間が経過した場合にのみ、管理フォルダー アシスタントを有効にしてクライアント アクセスを許可することをお勧めします (手順 11 および 12)。



11. 以下のクォータを、手順 1 でメモした値に戻します。
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    この例では、メールボックスは訴訟ホールドから削除され、削除されたアイテム保持期間は既定値の 14 日間にリセットされ、回復可能なアイテムのクォータはメールボックス データベースと同じ値を使用するよう構成されます。手順 1 でメモした値が異なる場合は、前述のパラメーターを使用してそれぞれの値を指定し、*UseDatabaseQuotaDefaults* パラメーターを `$false` に設定する必要があります。*RetainDeletedItemsForand UseDatabaseRetentionDefaults* パラメーターを以前に異なる値に設定していた場合は、それらも手順 1 でメモした値に戻す必要があります。
    
    ```powershell
    Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true
    ```

12. ワーク サイクルの設定を手順 4 でメモした値に戻すことで、管理フォルダー アシスタントを有効にします。この例ではワーク サイクルを 1 日に設定します。
    
    ```powershell
    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1
    ```

13. クライアント アクセスを有効にします。
    
    ```powershell
    Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true
    ```

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/ja-jp/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/ja-jp/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/ja-jp/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/ja-jp/library/dd298173\(v=exchg.150\))

## 正常な動作を確認する方法

メールボックスの回復可能なアイテム フォルダーが正常にクリーンアップされたことを確認するには、[Get-MailboxFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa996762\(v=exchg.150\)) コマンドレットを使用して回復可能なアイテム フォルダーのサイズを確認します。

この例では、回復可能なアイテム フォルダーとそのサブフォルダーのサイズ、およびフォルダー/各サブフォルダー内のアイテム数を取得します。

```powershell
Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto
```

