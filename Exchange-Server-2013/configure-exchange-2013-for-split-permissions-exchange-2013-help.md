---
title: 'Exchange 2013 の分割型アクセス許可を構成する: Exchange 2013 Help'
TOCTitle: Exchange 2013 の分割型アクセス許可を構成する
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 49896355
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 の分割型アクセス許可を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

分割型アクセス許可を使用すると、Active Directory 管理者や Microsoft Exchange Server 2013 管理者などの異なる 2 つのグループが、それらのグループのサービス、オブジェクト、属性をそれぞれで管理できるようになります。Active Directory 管理者は、Active Directory フォレストにアクセスするためのアクセス許可を提供するセキュリティ プリンシパル (ユーザーなど) を管理し、Exchange 管理者は、Active Directory オブジェクトの Exchange 関連属性と Exchange 固有のオブジェクトの作成および管理を管理します。

Microsoft Exchange Server 2013 では、次の種類の分割型アクセス許可モデルが提供されています。

  - **RBAC 分割型アクセス許可**    Active Directory ドメイン パーティション内にセキュリティ プリンシパルを作成するためのアクセス許可は、役割ベースのアクセス制御 (RBAC) によって制御されます。セキュリティ プリンシパルを作成できるのは、適切な役割グループのメンバーのみです。

  - **Active Directory の分割型アクセス許可**   Active Directory ドメイン パーティション内にセキュリティ プリンシパルを作成するアクセス許可が、すべての Exchange ユーザー、サービス、またはサーバーから完全に削除されています。RBAC でセキュリティ プリンシパルを作成するオプションは用意されていません。Active Directory でセキュリティ プリンシパルを作成する場合は、Active Directory 管理ツールを使用する必要があります。
    

    > [!NOTE]
    > Active Directory 分割型アクセス許可は、Microsoft Exchange Server 2010 Service Pack 1 (SP1) 以降、Exchange 2013、または Exchange の両方のバージョンを実行している組織で使用できます。



組織の構造およびニーズに合わせて、モデルを選択してください。構成したいモデルに合わせて手順を選択してください。RBAC 分割型アクセス許可モデルを使用することをお勧めします。RBAC 分割型アクセス許可モデルは、Active Directory 分割型アクセス許可と同じ管理の分割を提供すると同時に、高い柔軟性を備えています。

共有アクセス許可と分割型アクセス許可の詳細については、「[分割型アクセス許可について](understanding-split-permissions-exchange-2013-help.md)」を参照してください。

管理役割グループ、管理役割、正規および委任の管理役割の割り当ての詳細については、以下のトピックを参照してください。

  - [役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)

  - [管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)

  - [管理の役割について](understanding-management-roles-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

アクセス許可に関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「Active Directory 分割型アクセス許可」。

  - これらの手順を実行するには、Windows PowerShell、Windows コマンド シェル、またはその両方を使用する必要があります。詳細については、各手順を参照してください。

  - 組織内に Exchange 2010 サーバーがある場合、選択したアクセス許可モデルがそれらのサーバーにも適用されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## RBAC 分割型アクセス許可に切り替える

RBAC 分割型アクセス許可のために Exchange 2013 組織を構成することができます。完了すると、Active Directory 管理者のみが Active Directory セキュリティ プリンシパルを作成できるようになります。したがって、Exchange 管理者は次のコマンドレットを使用できなくなります。

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Exchange 管理者は、既存の Active Directory セキュリティ プリンシパルの Exchange 属性しか管理できなくなります。ただし、トランスポート ルールや配布グループなどの Exchange 固有のオブジェクトの作成および管理を行うことはできます。詳細については、[分割型アクセス許可について](understanding-split-permissions-exchange-2013-help.md) の「RBAC 分割型アクセス許可」を参照してください。

分割型アクセス許可のために Exchange 2013 を構成するには、Active Directory 管理者であるメンバーを含む役割グループに、"Mail Recipient Creation/メール受信者の作成" 役割および "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割を割り当てる必要があります。次に、これらの役割と Exchange 管理者を含む役割グループまたはユニバーサル セキュリティ グループ (USG) との間の割り当てを削除する必要があります。

RBAC 分割型アクセス許可を構成するには、次の操作を行います。

1.  現在、組織を Active Directory 分割型アクセス許可のために構成している場合、Windows コマンド シェル プロンプトから次の操作を実行します。
    
    1.  Exchange 2013 インストール メディアから次のコマンドを実行して、Active Directory 分割型アクセス許可を無効にします。
        
            setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
    
    2.  組織内の Exchange 2013 サーバーを再起動するか、Active Directory アクセス トークンがすべての Exchange 2013 サーバーにレプリケートされるのを待ちます。
        

        > [!NOTE]
        > 組織内に Exchange 2010 サーバーがある場合、それらのサーバーを再起動する必要もあります。



2.  Exchange 管理シェルから、次の操作を実行します。
    
    1.  Active Directory 管理者の役割グループを作成します。役割グループを作成する以外に、コマンドにより、新しい役割グループと、"Mail Recipient Creation/メール受信者の作成" 役割および "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割の間に正規の役割の割り当てが作成されます。
        
            New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        

        > [!NOTE]
        > この役割グループのメンバーが役割の割り当てを作成できるようにする場合は、"Role Management/役割の管理" 役割を含めます。ここではこの役割を追加する必要はありません。ただし、"Mail Recipient Creation/メール受信者の作成" 役割または "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割のいずれかを他の役割担当者に割り当てる場合は、この新しい役割グループに "Role Management/役割の管理" 役割を割り当てる必要があります。実行する手順は、これらの役割を委任可能な唯一の役割グループとして "Active Directory Administrators/Active Directory 管理者" 役割グループを構成します。

    
    2.  以下のコマンドを使用して、新しい役割グループと、"Mail Recipient Creation/メールの受信者の作成" 役割および "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割の間に委任の役割の割り当てを作成します。
        
            New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
            New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
    
    3.  以下のコマンドを使用して、新しい役割グループにメンバーを追加します。
        
            Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
    
    4.  役割グループのメンバーのみがメンバーを追加または削除することができるように、新しい役割グループの代理人の一覧を置き換えます。
        
            Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        

        > [!IMPORTANT]
        > 組織の管理 役割グループのメンバー、あるいは、直接、または別の役割グループや USG を介して "Role Management/役割管理" 役割に割り当てられている人間は、この代理人セキュリティ チェックをバイパスできます。すべての Exchange 管理者が新しい役割グループに自分自身を追加するのを防止する場合は、"Role Management/役割管理" と任意の Exchange 管理者の間の役割の割り当てを削除し、この役割の割り当てを別の役割グループに割り当てる必要があります。

    
    5.  以下のコマンドを使用して、"Mail Recipient Creation/メール受信者の作成" 役割へのすべての正規および委任の役割の割り当てを検索します。コマンドは、**Name**、**Role**、および **RoleAssigneeName** プロパティのみを表示します。
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    6.  以下のコマンドを使用して、新しい役割グループやその他の役割グループ、USG、または保持する必要がある直接的な役割に関連付けられていない "Mail Recipient Creation/メール受信者の作成" 役割へのすべての正規および委任の役割の割り当てを削除します。
        
            Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        

        > [!NOTE]
        > "Active Directory Administrators/Active Directory 管理者" 役割グループ以外のすべての役割担当者に対する "Mail Recipient Creation/メール受信者の作成" 役割への正規および委任の役割の割り当てすべて削除する場合は、次のコマンドを使用します。<EM>WhatIf</EM> スイッチを使用すると、どの役割割り当てを削除するかを確認できます。役割割り当てを削除するには、<EM>WhatIf</EM> スイッチを削除して再度コマンドを実行します。

        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
    
    7.  以下のコマンドを使用して、"Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割へのすべての正規および委任の役割の割り当てを検索します。コマンドは、**Name**、**Role**、および **RoleAssigneeName** プロパティのみを表示します。
        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    8.  以下のコマンドを使用して、新しい役割グループやその他の役割グループ、USG、または保持する必要がある直接的な役割に関連付けられていない "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割へのすべての正規および委任の役割の割り当てを削除します。
        
            Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        

        > [!NOTE]
        > この例で示すように、"Active Directory Administrators/Active Directory 管理者" 役割グループ以外のすべての役割担当者に対する "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割への正規および委任の役割の割り当てをすべて削除するには、前述の注で説明したのと同じコマンドを使用します。

        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [New-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/ja-jp/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351205\(v=exchg.150\))

## Active Directory 分割型アクセス許可に切り替える

Active Directory 分割型アクセス許可のために Exchange 2013 組織を構成することができます。Active Directory 分割型アクセス許可は、Exchange 管理者とサーバーに、Active Directory でのセキュリティ プリンシパルの作成、またはこれらのオブジェクトの Exchange 以外の属性の変更を許可するアクセス許可を完全に削除します。完了すると、Active Directory 管理者のみが Active Directory セキュリティ プリンシパルを作成できるようになります。したがって、Exchange 管理者は次のコマンドレットを使用できなくなります。

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

  - **Update-DistributionGroupMember**

Exchange 管理者とサーバーは、既存の Active Directory セキュリティ プリンシパルの Exchange 属性しか管理できなくなります。ただし、トランスポート ルールやユニファイド メッセージング ダイヤル プランなどの Exchange 固有のオブジェクトの作成および管理を行うことはできます。


> [!NOTE]
> Active Directory 分割型アクセス許可を有効にすると、Exchange 管理者とサーバーは Active Directory でセキュリティ プリンシパルを作成できなくなり、配布グループ メンバーシップを管理することもできなくなります。これらのタスクを実行するには、必要な Active Directory アクセス許可を付与されたうえで、Active Directory 管理ツールを使用する必要があります。この変更を行う場合は事前に、この変更によって、自分の管理プロセスや、Exchange 2013 と RBAC アクセス許可モデルに統合されるサードパーティのアプリケーションが受ける影響を把握しておく必要があります。<BR>詳細については、「<A href="understanding-split-permissions-exchange-2013-help.md">分割型アクセス許可について</A>」の「Active Directory 分割型アクセス許可」を参照してください。



共有アクセス許可または RBAC 分割型アクセス許可から Active Directory 分割型アクセス許可に切り替えるには、次の操作を実行します。

1.  Windows コマンド シェルで、Exchange 2013 インストール メディアから次のコマンドを実行して Active Directory 分割型アクセス許可を有効にします。
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true

2.  組織内に複数の Active Directory ドメインがある場合、Exchange サーバーまたはオブジェクトを含むそれぞれの子ドメインで `setup.exe /PrepareDomain` を実行するか、すべてのドメインの Active Directory サーバーがあるサイトから `setup.exe /PrepareAllDomains` を実行します。

3.  組織内の Exchange 2013 サーバーを再起動するか、Active Directory アクセス トークンがすべてのExchange 2013 サーバーにレプリケートされるのを待ちます。
    

    > [!NOTE]
    > 組織内に Exchange 2010 サーバーがある場合、それらのサーバーを再起動する必要もあります。


