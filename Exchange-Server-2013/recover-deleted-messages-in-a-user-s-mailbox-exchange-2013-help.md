---
title: 'ユーザーのメールボックス内の削除済みメッセージを復元する: Exchange Online Help'
TOCTitle: ユーザーのメールボックス内の削除済みメッセージを復元する
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50555836
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのメールボックス内の削除済みメッセージを復元する

 

_**適用先:** Exchange Online, Exchange Server 2013_

(このトピックは、Exchange 管理者を対象としたものです。)

管理者はユーザーのメールボックス内の削除済みの電子メール メッセージを検索して回復できます。これには、ユーザーにより完全に削除 (消去) されたアイテム (回復には Outlook または Outlook Web App の \[削除済みアイテムを復元\] 機能を使用する) や、ユーザーのメールボックスに割り当てられているアイテム保持ポリシーなどの自動化されたプロセスによって削除されたアイテムが含まれます。このような場合、削除されたアイテムをユーザーが回復することはできません。しかし、管理者は、アイテムの削除済みアイテム保持期間を過ぎていなければ、削除されたメッセージを回復できます。


> [!NOTE]
> この手順は、削除済みアイテム (単一アイテムの回復または訴訟ホールドが有効になっている場合に Recoverable Items\Purges フォルダーに移動されています) を検索して回復するために使用するほか、メールボックスの他のフォルダーに存在するアイテムを検索し、送信元メールボックスからアイテムを削除する (<EM>検索と破損</EM>とも呼ばれます) ためにも使用できます。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 ～ 30 分。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - 回復するアイテムが削除される前に、メールボックスに対して単一アイテムの回復を有効にする必要があります。Exchange Online では、新しいメールボックスの作成時に単一アイテムの回復が既定で有効になります。Exchange 2013 では、メールボックスの作成時には単一アイテムの回復は無効になっています。詳細については、「[メールボックスの単一アイテムの回復を有効または無効にする](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md)」を参照してください。

  - アイテムを検索して回復するには、次の情報が必要です。
    
      - **移動元のメールボックス**   これは、検索対象となるメールボックスです。
    
      - **移動先のメールボックス**   これは、メッセージが回復される探索メールボックスです。Exchange セットアップでは、既定の探索メールボックスが作成されます。Exchange Online でも、探索メールボックスは既定で作成されます。必要に応じて、追加の探索メールボックスを作成できます。詳細については、「[探索メールボックスの作成](create-a-discovery-mailbox-exchange-2013-help.md)」を参照してください。
        

        > [!NOTE]
        > <STRONG>Search-Mailbox</STRONG> コマンドレットを使用する場合、探索メールボックス以外の移動先のメールボックスも指定できます。ただし、移動元のメールボックスと移動先のメールボックスに同じメールボックスを指定することはできません。

    
      - **検索条件**   条件には、送信者または受信者、またはメッセージ内のキーワード (単語または語句) が含まれます。

  - このトピックでは、PowerShell を使用してユーザーのメールボックス内の削除済みアイテムを復元することについて説明します。削除済みアイテムについては、GUI ベースのインプレース電子情報開示ツールを使用することにより、それらを検索して PST ファイルにエクスポートすることもできます。ユーザーは、その PST ファイルを使用することにより、削除済みメッセージを自分のメールボックスに復元します。詳しい手順については、「[ユーザーのメールボックスの削除済みアイテムの復元 - 管理ヘルプ](https://go.microsoft.com/fwlink/p/?linkid=722928)」をご覧ください。

## (オプション) 手順 1: リモート PowerShell を使用した Exchange Online への接続

Exchange Online 組織または Office 365 組織がある場合はこの手順のみを実行する必要があります。Exchange 2013 組織がある場合は、次の手順に進み、Exchange 管理シェル でコマンドを実行します。

1.  ローカル コンピューターで、Windows PowerShell を開き、次のコマンドを実行します。
    
        $UserCredential = Get-Credential
    
    **\[Windows PowerShell 資格情報の要求\]** ダイアログ ボックスで、Office 365 のグローバル管理者アカウントのユーザー名とパスワードを入力し、**\[OK\]** をクリックします。

2.  次のコマンドを実行します。
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  次のコマンドを実行します。
    
        Import-PSSession $Session

4.  Exchange Online 組織に接続されたことを検証するために、次のコマンドを実行して、組織内のすべてのメールボックスのリストを取得します。
    
        Get-Mailbox

詳細については、または Exchange Online 組織への接続に関する問題がある場合は、「[リモート PowerShell による Exchange への接続](https://go.microsoft.com/fwlink/p/?linkid=517283)」を参照してください。

## 手順 2:見つからないアイテムを検索し、回復する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「インプレース電子情報開示」。


> [!NOTE]
> Exchange 管理センター (EAC) のインプレース電子情報開示を使用して、見つからないアイテムを検索することができます。ただし、EAC を使用する場合は、回復可能なアイテム フォルダーに対して検索を限定できません。削除されていない場合であっても、検索パラメーターと一致するメッセージが返されます。指定した探索メールボックスにメッセージを回復した後には、残っているメッセージをユーザーのメールボックスに回復するか、または .pst ファイルにエクスポートする前に、検索結果を確認し、不要なメッセージを削除する必要があります。<BR>EAC を使用してインプレース電子情報開示検索を実行する方法の詳細については、「<A href="create-an-in-place-ediscovery-search-exchange-2013-help.md">インプレース電子情報開示検索を作成する</A>」を参照してください。



回復処理の最初の手順は、移動元のメールボックス内のメッセージを検索することです。ユーザー メールボックスを検索し、メッセージを探索メールボックスにコピーするには、以下のいずれかの方法を使用します。

この例では、April Stewart のメールボックスで、次の条件に一致するメッセージを検索します。

  - 送信者:Ken Kwok

  - キーワード: シアトル

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full


> [!NOTE]
> <STRONG>Search-Mailbox</STRONG> コマンドレットを使用する場合、<EM>SearchQuery</EM> パラメーターを使用してキーワード クエリ言語 (KQL) によって書式設定されたクエリを指定することで、検索を絞り込むことができます。<EM>SearchDumpsterOnly</EM> スイッチを使用して、回復可能なアイテム フォルダーのアイテムのみを検索することもできます。



構文およびパラメーターの詳細については、「[Search-Mailbox](https://technet.microsoft.com/ja-jp/library/dd298173\(v=exchg.150\))」を参照してください。

**正常な動作を確認する方法**

回復するメッセージが正常に検索されたことを確認するには、ターゲット メールボックスとして選択した探索メールボックスにログオンし、検索結果を確認します。

## 手順 3: 回復されたアイテムを復元する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「インプレース電子情報開示」。


> [!NOTE]
> EAC を使用して回復されたアイテムを復元することはできません。



メッセージが探索メールボックスに回復された後、**Search-Mailbox** コマンドレットを使用してユーザーのメールボックスにメッセージを復元できます。Exchange 2013 の場合、**New-MailboxExportRequest** コマンドレットと **New-MailboxImportRequest** コマンドレットを使用して, .pst ファイルにメッセージをエクスポートしたり, .pst ファイルからメッセージをインポートしたりすることもできます。

## シェルを使用してメッセージを復元する

この例では、メッセージを April Stewart のメールボックスに復元し、探索検索メールボックスから削除します。

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

構文およびパラメーターの詳細については、「[Search-Mailbox](https://technet.microsoft.com/ja-jp/library/dd298173\(v=exchg.150\))」を参照してください。

**正常な動作を確認する方法**

メッセージがユーザーのメールボックスに正常に回復されたことを確認するには、上記のコマンドで指定したターゲット フォルダーのメッセージを確認するようにユーザーに依頼します。

## (Exchange 2013) シェルを使用してメッセージを .pst ファイルにエクスポートしたり, .pst ファイルからインポートしたりする

Exchange 2013 では、メールボックスの内容を .pst ファイルにエクスポートしたり, .pst ファイルからメールボックスにインポートしたりできます。メールボックスのインポートとエクスポートの詳細については、「[メールボックスのインポート要求とエクスポート要求](mailbox-import-and-export-requests-exchange-2013-help.md)」を参照してください。この作業を Exchange Online で実行することはできません。

この例では、次の設定を使用して探索検索メールボックスのフォルダー April Stewart Recovery から .pst ファイルにメッセージをエクスポートします。

  - **メールボックス**   探索検索メールボックス

  - **ソース フォルダー**   April Stewart Recovery

  - **ContentFilter**   April travel plans

  - **PST ファイルのパス**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

構文およびパラメーターの詳細については、「[New-MailboxExportRequest](https://technet.microsoft.com/ja-jp/library/ff607299\(v=exchg.150\))」を参照してください。

この例では、次の設定を使用して .pst ファイルから April Stewart のメールボックスのフォルダー Recovered By Helpdesk にメッセージをインポートします。

  - **メールボックス**   April Stewart

  - **ターゲット フォルダー**   Recovered By Helpdesk

  - **PST ファイルのパス**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

構文およびパラメーターの詳細については、「[New-MailboxImportRequest](https://technet.microsoft.com/ja-jp/library/ff607310\(v=exchg.150\))」を参照してください。

**正常な動作を確認する方法**

メッセージが .pst ファイルに正常にエクスポートされたことを確認するには、Outlook を使用して .pst ファイルを開き、その内容を調べます。メッセージが .pst ファイルから正常にインポートされたことを確認するには、上記のコマンドで指定したターゲット フォルダーの内容を調べるようにユーザーに依頼します。

## 詳細情報

  - 削除済みアイテムを回復する機能は、*単一アイテムの回復*によって有効にされます。この機能により、ユーザーまたはアイテム保持ポリシーによって削除されたメッセージの削除済みアイテムの保存期間が経過していない限り、管理者はそのメッセージを回復することができます。単一アイテムの回復の詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」を参照してください。

  - 既定では、Exchange Online メールボックスは削除済みアイテムを 14 日間保持するように構成されています。この設定は最大 30 日にまで変更できます。Exchange 2013 の場合、メールボックス データベースが削除済みアイテムを 14 日間保持するよう既定で構成されています。メールボックスまたはメールボックス データベースの削除済みアイテム保存期間の設定を構成することができます。詳細については、以下を参照してください。
    
      - [Exchange Online メールボックスの完全に削除したアイテムの保持期間を変更する](https://technet.microsoft.com/ja-jp/library/dn163584\(v=exchg.150\))
    
      - [削除済みアイテムの保存期間と回復可能なアイテムのクォータを構成する](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - 前述のように、削除済みアイテムについては、インプレース電子情報開示ツールを使用することにより、それらを検索して PST ファイルにエクスポートすることもできます。ユーザーは、その PST ファイルを使用することにより、削除済みメッセージを自分のメールボックスに復元します。詳しい手順については、「[ユーザーのメールボックスの削除済みアイテムの復元 - 管理ヘルプ](https://go.microsoft.com/fwlink/p/?linkid=722928)」をご覧ください。

  - 削除済みアイテムが完全には削除されておらず、そのアイテムの削除済みアイテム保持期間を過ぎていなければ、ユーザーは削除済みのそのアイテムを回復できます。ユーザーが \[回復可能なアイテム\] フォルダーから削除済みアイテムを回復する必要がある場合は、以下のトピックを参照するように伝えてください。
    
      - [Outlook 2010 で削除済みのアイテムを復元する](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Windows 版 Outlook で削除済みのアイテムを復元する](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [Outlook Web App で削除されたアイテムまたは電子メールを復元する](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - このトピックでは、**Search-Mailbox** コマンドレットを使用して見つからないアイテムを検索し回復する方法を示します。このコマンドレットを使用する場合は、一度に 1 つのメールボックスしか検索できません。複数のメールボックスを同時に検索する場合は、Exchange 管理センター (EAC) の [インプレース電子情報開示 (eDiscovery)](in-place-ediscovery-exchange-2013-help.md) または Windows PowerShell の [New-MailboxSearch](https://technet.microsoft.com/ja-jp/library/dd298064\(v=exchg.150\)) コマンドレットを使用できます。

  - 削除済みのアイテムを検索し回復すること以外にも、これと同様の手順でユーザーのメールボックス内のアイテムを検索し、アイテムがあるメールボックスからそれらのアイテムを削除することもできます。詳細については、「[メッセージを検索して削除する - 管理者向けヘルプ](search-for-and-delete-messages-admin-help-exchange-2013-help.md)」を参照してください。

