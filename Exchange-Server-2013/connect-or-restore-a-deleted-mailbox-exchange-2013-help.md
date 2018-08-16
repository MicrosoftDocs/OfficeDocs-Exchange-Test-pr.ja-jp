---
title: '削除されたメールボックスの接続または復元: Exchange 2013 Help'
TOCTitle: 削除されたメールボックスの接続または復元
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50555842
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 削除されたメールボックスの接続または復元

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-05-04_

EAC またはシェルを使用して、削除済みメールボックスを Active Directory ユーザー アカウントに接続できます。メールボックスを削除すると、Exchange はそのメールボックスをメールボックス データベースに保持し、メールボックスを無効な状態に切り替えます。関連付けられた Active Directory ユーザー アカウントも削除されます。メールボックスは削除済みメールボックスの保持期間 (既定では 30 日) が経過するまで保持され、その後に、メールボックス データベースから完全に削除 (つまり*消去*) されます。

削除済みメールボックスが Exchange メールボックス データベースから完全に削除されるまでは、EAC またはシェルを使用して、削除済みメールボックスを Active Directory ユーザー アカウントに接続できます。シェルを使用して、削除済みメールボックスの内容を既存のメールボックスに復元することもできます。

切断されたメールボックスおよびその他の関連する管理タスクの実行方法の詳細については、次のトピックを参照してください。

  - [未接続のメールボックス](disconnected-mailboxes-exchange-2013-help.md)

  - [メールボックスの無効化または削除](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [無効にされたメールボックスを接続する](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [メールボックスの完全削除](permanently-delete-a-mailbox-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - 削除済みメールボックスを接続する新しいユーザー アカウントを Active Directory 内に作成します。または、シェルで **Get-User** コマンドレットを使用して、削除済みメールボックスを接続する Active Directory ユーザー アカウントが存在し、かつ別のメールボックスにまだ関連付けられていないことを確認します。削除済みメールボックスをユーザー アカウントに接続するには、アカウントが存在している必要があり、かつ *RecipientType* プロパティの値が、アカウントのメールボックスがまだ有効ではないことを示す `User` である必要があります。
    
    社内 Exchange 組織の場合は、この情報を \[Active Directory ユーザーとコンピューター\] で確認することもできます。
    

    > [!IMPORTANT]
    > 削除済みのリンクされたメールボックス、リソース メールボックス、または共有メールボックスを接続する場合は、メールボックスを接続する Active Directory ユーザー アカウントが無効である必要があります。



  - ユーザー アカウントを接続する削除済みメールボックスがメールボックス データベースに存在し、回復可能な削除によって削除されたメールボックスではないことを確認するには、次のコマンドを実行します。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    削除済みメールボックスがメールボックス データベースに存在し、*DisconnectReason* プロパティの値が `Disabled` である必要があります。メールボックスがデータベースから消去されている場合、コマンドは結果を返しません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

  - 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## 必要な作業

## 削除済みメールボックスを接続する

削除済みメールボックスを接続する際には、メールが有効ではない (つまり、既存のメールボックスを持たない) ユーザー アカウントにメールボックスを関連付けます。削除済みメールボックスをメールボックスを持つユーザー アカウントに接続するには、削除済みメールボックスを復元する必要があります。詳細については、後の「削除済みメールボックスを復元する」を参照してください。

## EAC を使用して削除済みメールボックスを接続する

次の手順では、削除済みユーザー メールボックスをユーザー アカウントに接続する方法を示します。この手順を使用して、削除されているリンクされたメールボックス、リソース メールボックス、および共有メールボックスをユーザー アカウントに接続することもできます。

1.  EAC で、**\[受信者\]** \> <strong>\[メールボックス\]</strong>に移動します。

2.  **\[その他\]** ![\[その他のオプション\] アイコン](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "[その他のオプション] アイコン") をクリックし、**\[メールボックスの接続\]** をクリックします。
    
    Exchange 組織内の選択した Exchange サーバー上にある、切断されたメールボックスの一覧が表示されます。
    

    > [!NOTE]
    > この切断されたメールボックスの一覧には、無効にされたメールボックス、削除されたメールボックス、および回復可能な削除によって削除されたメールボックスが含まれます。



3.  ユーザーを接続する削除済みメールボックスをクリックし、**\[接続\]** をクリックします。

4.  そのメールボックスを接続するかどうかを確認するウィンドウで、**\[はい\]** をクリックします。
    
    メールが有効ではないユーザー アカウントの一覧が表示されます。

5.  削除済みメールボックスを接続するユーザーをクリックし、**\[OK\]** をクリックします。
    
    Exchange により、削除済みメールボックスが選択したユーザー アカウントに接続されます。

## シェルを使用した削除済みメールボックスへの接続

シェルで **Connect-Mailbox** コマンドレットを使用して、メールが有効ではないユーザー アカウントに削除済みメールボックスを接続します。接続するメールボックスの種類を指定する必要があります。次の例では、ユーザー メールボックス、リンクされたメールボックス、会議室メールボックス、備品用メールボックス、および共有メールボックスを再接続するための構文を示します。すべての例では、オプションの *Alias* パラメーターを使用して電子メール エイリアスを指定します。電子メール エイリアスは、電子メール アドレスの @ 記号の左に表示される部分です。*Alias* パラメーターを含めない場合は、*User* パラメーターまたは *LinkedMasterAccount* パラメーターで指定した値を使用して、再接続したメールボックスの電子メール アドレスのエイリアスが作成されます。


> [!NOTE]
> 前述したように、リンクされたメールボックス、リソース メールボックス、または共有メールボックスを接続する場合は、メールボックスをリンクする Active Directory ユーザー アカウントが無効である必要があります。



この例では、ユーザー メールボックスを接続しています。*Identity* パラメーターでは、MBXDB01 という名前のメールボックス データベースに保持された、削除済みメールボックスの表示名を指定します。*User* パラメーターでは、メールボックスを接続する Active Directory ユーザー アカウントを指定します。

    Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw


> [!NOTE]
> <CODE>LegacyDN</CODE> プロパティまたは <CODE>MailboxGuid</CODE> プロパティの値を使用して、削除済みメールボックスを識別することもできます。



この例では、リンクされたメールボックスを接続しています。*Identity* パラメーターでは、MBXDB02 という名前のメールボックス データベースの削除済みメールボックスを指定します。*LinkedMasterAccount* パラメーターでは、メールボックスを接続するアカウント フォレスト内の Active Directory ユーザー アカウントを指定します。*LinkedDomainController* パラメーターでは、アカウント フォレスト内のドメイン コント ローラーを指定します。

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

この例では、会議室メールボックスを接続しています。

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

この例では、備品メールボックスを接続しています。

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

この例では、共有メールボックスを接続しています。

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared


> [!NOTE]
> <CODE>LegacyDN</CODE> または <CODE>MailboxGuid</CODE> の値を使用して、削除済みメールボックスを識別することもできます。



構文およびパラメーターの詳細については、「[Connect-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997878\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

削除済みメールボックスがユーザー アカウントに正常に接続されたことを確認するには、次のいずれかを実行します。

  - EAC で、**\[受信者\]** をクリックし、接続したメールボックスの種類の適切なページに移動し、**\[最新の情報に更新\]** ![\[最新の情報に更新\] アイコン](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "[最新の情報に更新] アイコン") をクリックし、メールボックスが一覧に表示されていることを確認します。

  - \[Active Directory ユーザーとコンピューター\] で、メールボックスに接続したユーザー アカウントを右クリックし、**\[プロパティ\]** をクリックします。**\[全般\]** タブで、接続したメールボックスの電子メール アドレスが **\[電子メール\]** ボックスに読み込まれていることに注意してください。

  - シェルで、次のコマンドを実行します。
    
        Get-User <identity>
    
    *RecipientType* プロパティの **UserMailbox** 値は、ユーザー アカウントとメールボックスが接続されていることを示します。**Get-Mailbox \<identity\>** コマンドを実行して、メールボックスが接続されたことを確認することもできます。

## 削除済みメールボックスを復元する

シェルで **New-MailboxRestoreRequest** コマンドレットを使用して、削除済みメールボックスを既存のメールボックスに復元できます。削除済みメールボックスを復元すると、その内容が既存のメールボックス (*ターゲット メールボックス*と呼ばれる) にコピーされます。削除済みメールボックスを復元した後には、そのメールボックスが管理者によって完全に削除されるか、またはメールボックスの保持期間が経過した後に消去されるまで、メールボックスがメールボックス データベースに保持されたままになります。

メールボックスの復元要求が正常に完了した後には、削除されるまで、既定ではメールボックスが 30 日間保持されます。**Remove-StoreMailbox** コマンドレットを使用すると、より早い時点でメールボックスを削除できます。


> [!NOTE]
> EAC を使用して削除済みメールボックスを復元することはできません。



## シェルを使用して削除済みメールボックスを復元する

メールボックス復元要求を作成するには、削除済みメールボックスの表示名、従来の識別名 (DN)、またはメールボックス GUID を使用する必要があります。復元する削除済みメールボックスの `DisplayName` プロパティ、`MailboxGuid` プロパティ、および `LegacyDN` プロパティの値を表示するには、**Get-MailboxStatistics** コマンドレットを使用します。たとえば、次のコマンドを実行すると、組織内のすべての無効なメールボックスおよび削除済みメールボックスに関するこの情報が返されます。

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

この例では、*SourceStoreMailbox* パラメーターによって識別される、MBXDB01 メールボックス データベースにある削除済みメールボックスを、メールボックス Debra Garcia に復元します。従来の DN 値が同じではない別のメールボックスに復元元メールボックスを復元できるように、*AllowLegacyDNMismatch* パラメーターを使用します。

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

この例では、Pilar Pinilla の削除済みアーカイブ メールボックスを Pilar Pinilla の現在のアーカイブ メールボックスに復元します。プライマリ メールボックスと、その対応するアーカイブ メールボックスの従来の DN は同じであるため、*AllowLegacyDNMismatch* パラメーターは必要ありません。

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

構文およびパラメーターの詳細については、「[New-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829875\(v=exchg.150\))」を参照してください。

## シェルを使用して削除済みのパブリック フォルダー メールボックスを復元する

復元するパブリック フォルダー メールボックスが物理的に削除されていて、そのメールボックスが削除済みアイテムの保存期間制限内にある場合 (「[削除済みアイテムの保存期間と回復可能なアイテムのクォータを構成する](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)」をご覧ください)、`Connect-Mailbox` コマンドレット、その後 `Update-StoreMailboxState` コマンドレットを使用できます。構文およびパラメーターの詳細については、「[Connect-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997878\(v=exchg.150\))」と「[Update-StoreMailboxState](https://technet.microsoft.com/ja-jp/library/jj860462\(v=exchg.150\))」を参照してください。

削除されたパブリック フォルダー メールボックスの GUID、およびそのパブリック フォルダー メールボックスが含まれていたメールボックス データベースの GUID または名前が必要になります。この情報がない場合は、次の手順を実行できます。

1.  次のコマンドレットを実行して Active Directory フォレストとドメイン コント ローラーの完全修飾ドメイン名 (FQDN) を取得します。
    
        Get-OrganizationConfig | fl OriginatingServer

2.  手順 1 で返される情報を使用して、パブリック フォルダー メールボックスの GUID と、削除されたパブリック フォルダー メールボックスが含まれていたメールボックス データベースの GUID または名前を、Active Directory の削除済みオブジェクト コンテナーで検索します。
    

    > [!TIP]
    > 削除済みオブジェクトの検索は、カスタム スクリプトを使用しても、Ldp ユーティリテイを使用しても行えます。このユーティリティは、Powershell プロンプトに <STRONG>ldp.exe</STRONG> と入力して開くことができます。



削除されたパブリック フォルダー メールボックスの GUID、およびそのパブリック フォルダー メールボックスが含まれていたメールボックス データベースの名前または GUID がわかっている場合には、以下のコマンドを実行してパブリック フォルダー メールボックスを復元します。

1.  次のコマンドを実行して新しい Active Directory オブジェクトを作成します (適切な資格情報の入力が求められる場合があります)。
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    ここで `<mailUserName>`、`<emailAddress>`、`<mailUserName>` はユーザー選択の値です。次の手順では、同じ `<mailUserName>` 値を使用します。

2.  削除されたパブリック フォルダー メールボックスを、次のコマンドを実行して作成した Active Directory オブジェクトに接続します。
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    

    > [!NOTE]
    > <CODE>Identity</CODE> パラメーターには、Active Directory ユーザー オブジェクトと接続する Exchange データベースのメールボックス オブジェクトを指定します。上記の例では、パブリック フォルダー メールボックスの GUID を指定しますが、表示名の値または LegacyExchangeDN 値を使用することもできます。



3.  次の例を基にして、パブリック フォルダー メールボックスで `Update-StoreMailboxState` を実行します。
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    手順 2 に示されていたように、`Identity` パラメーターはパブリック フォルダー メールボックスの GUID、表示名、または LegacyExchangeDN の値を受け付けます。

## 正常な動作を確認する方法

削除されたパブリック フォルダー メールボックスが正常に復元されたことを確認するには、**Get-PublicFolder -GetChildren -\<public folder mailbox GUID\>** コマンドレットを実行します。復元が成功した場合、このコマンドレットは動作します。

詳細については、次のトピックを参照してください。

  - [Connect-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/ja-jp/library/jj860462\(v=exchg.150\))

