---
title: 'Exchange 2013 の共有アクセス許可を構成する: Exchange 2013 Help'
TOCTitle: Exchange 2013 の共有アクセス許可を構成する
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 49896335
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 の共有アクセス許可を構成する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-07_

共有アクセス許可を付与されたユーザーは、Microsoft Exchange Server 2013 管理者として Active Directory セキュリティ プリンシパル (たとえばユーザー) を作成し、Exchange 受信者として構成することができます。分割型アクセス許可の場合は、Exchange 管理者と Active Directory 管理者から成るグループどうしの間で管理タスクを分割するのに対し、共有アクセス許可の場合はタスクを分割しません。

共有アクセス許可と分割型アクセス許可の詳細については、「[分割型アクセス許可について](understanding-split-permissions-exchange-2013-help.md)」を参照してください。

以前に組織を分割型アクセス許可に設定したことがある場合、Exchange 2013 組織を共有アクセス許可に設定することができます。共有型アクセス許可に切り替える手順は、現在、役割ベースのアクセス制御 (RBAC) 分割型アクセス許可を使用しているか、または Active Directory 分割型アクセス許可を使用しているかによって異なります。現在の構成に合った手順を選択してください。以下に該当する場合は、組織は Active Directory 分割型アクセス許可を使用しています。

  - Microsoft Exchange Protected Group 組織単位 (OU) が存在します。

  - Exchange Windows Permissions セキュリティ グループは、Microsoft Exchange Protected Groups OU 内にあります。

  - Exchange Trusted Subsystem セキュリティ グループは、Exchange Windows Permissions セキュリティ グループのメンバーです。

  - "Mail Recipient Creation/メール受信者の作成" 役割、または "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割への正規の管理役割の割り当てはありません。

以前に組織を分割型アクセス許可に設定したことがなければ、この手順を実行する必要はありません。Exchange 2013 は既定で共有アクセス許可の構成になります。

管理役割グループ、管理役割、正規および委任の管理役割の割り当ての詳細については、以下のトピックを参照してください。

  - [役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)

  - [管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)

  - [管理の役割について](understanding-management-roles-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

アクセス許可に関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - これらの手順を実行するには、Windows PowerShell、Windows コマンド シェル、またはこの両方を使用する必要があります。詳細については、各手順を参照してください。

  - Exchange 2013 組織は現在、RBAC または Active Directory 分割型アクセス許可の構成になっている必要があります。

  - 組織内に Microsoft Exchange Server 2010 サーバーがある場合、選択したアクセス許可モデルはこれらのサーバーにも適用されます。

  - メール受信者の役割が割り当てられた役割グループ (組織の管理 管理役割グループなど) に、"Mail Recipient Creation/メール受信者の作成" 管理役割および "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 管理役割を委任するには、権限が必要です。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## RBAC 分割型アクセス許可から共有アクセス許可に切り替える

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割グループ」。

RBAC 分割型アクセス許可から Exchange 2013 共有アクセス許可に切り替えるには、"Mail Recipients/メール受信者" 役割が割り当て済みで Exchange 2013 管理者がメンバーとして属す役割グループに、"Mail Recipient Creation/メール受信者の作成" 役割と "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割を割り当てる必要があります。既定の共有アクセス許可構成では、これらの各役割は 組織の管理 役割グループに含まれています。このため、この手順には 組織の管理 役割グループが含まれます。

## 共有アクセス許可を構成する

組織の管理 役割グループに共有アクセス許可を構成するには、"Mail Recipient Creation/メール受信者の作成" 役割および "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割に役割の割り当てを委任する権限のあるアカウントを使用して、以下の手順を実行します。

1.  次のコマンドを使用して、"Mail Recipient Creation/メールの受信者の作成" 役割と"Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割に対する委任の役割の割り当てを 組織の管理 役割グループに追加します。
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
    

    > [!NOTE]
    > <STRONG>New-ManagementRoleAssignment</STRONG> コマンドレットを実行して、"Mail Recipient Creation/メールの受信者の作成" 役割と"Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割に対する委任の役割の割り当てを持つ役割グループ (この手順では、"Active Directory Administrators/Active Directory 管理者" 役割グループ) を、"Role Management/役割の管理" 役割に割り当てる必要があります。"Role Management/役割の管理" 役割を委任可能な役割担当者は、その役割を "Active Directory Administrators/Active Directory 管理者" 役割グループに割り当てる必要があります。



2.  次のコマンドを使用して、"Mail Recipient Creation/メール受信者の作成" 役割に対する正規の役割の割り当てを 組織の管理 および Recipient Management 役割グループに追加します。
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"

3.  次のコマンドを使用して、"Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割に対する正規の役割の割り当てを 組織の管理 役割グループに追加します。
    
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## Active Directory 管理者のアクセス許可を削除する (省略可能)

Active Directory 管理者に Active Directory オブジェクトを作成または管理させないようにする場合、Exchange 管理ツールを使用して、管理者に付与されている権限を必要に応じて削除することができます。Active Directory 管理者からアクセス許可を削除するには、この手順を実行します。


> [!NOTE]
> Active Directory 管理者の Active Directory オブジェクト管理権限は、Exchange 管理ツールで削除することができます。ただし、Active Directory 管理者は Active Directory 権限により許可される限り、Active Directory 管理ツールを使用して引き続き Active Directory オブジェクトを管理することもできます。ただし、Active Directory オブジェクトの Exchange 固有の属性を管理することはできません。詳細については、「<A href="understanding-split-permissions-exchange-2013-help.md">分割型アクセス許可について</A>」を参照してください。



Exchange 関連の分割型アクセス許可を Active Directory 管理者から削除するには、次の操作を実行します。

1.  次のコマンドを使用して、Active Directory 管理者がメンバーとして属す役割グループまたはユニバーサル セキュリティ グループ (USG) に "Mail Recipient Creation/メール受信者の作成" 役割を割り当てる、正規および委任の役割の割り当てを削除します。このコマンドは、例として "Active Directory Administrators/Active Directory管理者" 役割グループを使用します。*WhatIf* スイッチを使用すると、どの役割割り当てを削除するかを確認できます。役割割り当てを削除するには、*WhatIf* スイッチを削除して再度コマンドを実行します。
    
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

2.  次のコマンドを使用して、Active Directory 管理者がメンバーとして属す役割グループまたは USG に "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割を割り当てる、正規および委任の役割の割り当てを削除します。このコマンドは、例として "Active Directory Administrators/Active Directory管理者" 役割グループを使用します。*WhatIf* スイッチを使用すると、どの役割割り当てを削除するかを確認できます。役割割り当てを削除するには、*WhatIf* スイッチを削除して再度コマンドを実行します。
    
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

3.  省略可。Active Directory 管理者からすべての Exchange 権限を削除するには、管理者がメンバーとして属す役割グループまたは USG を削除する方法があります。役割グループを削除する方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」または「[Remove-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351205\(v=exchg.150\))」を参照してください。

## Active Directory 分割型アクセス許可から共有アクセス許可に切り替える

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「Active Directory 分割型アクセス許可」。

Active Directory 分割型アクセス許可から Exchange 2013 共有アクセス許可に切り替えるには、Exchange 組織内の Active Directory 分割型アクセス許可を無効にするために Exchange セットアップを再度実行して、役割グループと、"Mail Recipient Creation/メール受信者の作成" 役割および "Security Group Creation and Membership/セキュリティ グループ作成とメンバーシップ" 役割の間に、役割割り当てを作成する必要があります。既定の共有アクセス許可構成では、これらの各役割は 組織の管理 役割グループに含まれています。このため、この手順には 組織の管理 役割グループが含まれます。


> [!IMPORTANT]
> この手順の setup.com コマンドは、Active Directory を変更します。これらを変更するために必要なアクセス許可を持つアカウントを使用する必要があります。このアカウントは、<STRONG>New-ManagementRoleAssignment</STRONG> コマンドレットを使用して役割割り当てを作成するためのアクセス許可を持つアカウントと同じではない可能性があります。この手順の各ステップを正常に完了するために必要なアクセス許可を持つアカウントを使用してください。



Active Directory 分割型アクセス許可から共有アクセス許可に切り替えるには、次の操作を行います。

1.  Windows コマンド シェルで、Exchange 2013 インストール メディアから次のコマンドを実行して Active Directory 分割型アクセス許可を無効にします。
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false

2.  Exchange 管理シェルで、次のコマンドを実行して、"Mail Recipient Creation/メール受信者の作成" 役割および "Security Group Creation and Management/セキュリティ グループの作成と管理" 役割と、組織の管理 および Recipient Management 役割グループの間に正規の役割割り当てを追加します。
    
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"

3.  組織内の Exchange 2013 サーバーを再起動します。
    

    > [!NOTE]
    > 組織内に Exchange 2010 サーバーがある場合、それらのサーバーを再起動する必要もあります。



構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

