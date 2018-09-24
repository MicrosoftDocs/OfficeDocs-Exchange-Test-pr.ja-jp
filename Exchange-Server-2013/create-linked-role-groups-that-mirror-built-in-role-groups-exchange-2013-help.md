---
title: '組み込みの役割グループをミラーするリンクされた役割グループを作成する: Exchange 2013 Help'
TOCTitle: 組み込みの役割グループをミラーするリンクされた役割グループを作成する
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 49896348
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組み込みの役割グループをミラーするリンクされた役割グループを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

Microsoft Exchange Server 2013 のリンクされた管理役割グループを使用すると、Exchange 2013 リソース フォレスト内の役割グループを、外部ユーザー フォレスト内のユニバーサル セキュリティ グループ (USG) にリンクできます。これは、ユーザー フォレストのアカウントを持つ管理者が、リソース フォレスト内の Exchange を実行しているサーバーを管理する必要がある場合に有用です。 リンクされた役割グループの詳細については、「[管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)」を参照してください。

既定では、Exchange 2013 には、さまざまな機能とジョブ機能を管理するためのアクセス許可を提供する組み込みの役割グループのメンバーが数多く備えられています。 各役割グループは、各機能とジョブ機能に特定のアクセス許可を提供するようにカスタマイズされます。 ただし、これらの役割グループを外部フォレスト内の USG にリンクすることはできません。 これらの役割グループには、ローカル リソース フォレストからのユーザーと USG しか含めることができません。 しかし幸いなことに、リンクされた役割グループを使用してこれらの組み込みの役割グループを複製することができます。

各組み込みの役割グループは、リンクされた役割グループとして作成し直すことができます。 各役割グループに割り当てられている管理役割と管理スコープはすべて、リンクされた新しい役割グループに追加されます。 管理役割とスコープの詳細については、以下のトピックを参照してください。

  - [管理の役割について](understanding-management-roles-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

役割グループに関連する他の管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割グループ」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - リンクされた役割グループを構成するには、リンクされた役割グループが存在するリソース Active Directory フォレストと、ユーザーまたは USG が存在する外部 Active Directory フォレストとの間に一方向の信頼が必要になる。 リソース フォレストは外部フォレストを信頼する必要があります。

  - 外部 Active Directory フォレストに関する以下の情報を把握している必要があります。
    
      - **資格情報**   外部 Active Directory フォレストにアクセスできるユーザー名とパスワードを有する必要があります。 この情報は、**New-RoleGroup** コマンドレットの *LinkedCredential* パラメーターで使用されます。 この情報は、**Get-Credential** コマンドレットを実行することによって取得されます。ユーザー名の形式は、*ドメイン*\\*ユーザー名*です。
    
      - **ドメイン コントローラー**   外部 Active Directory フォレスト内の Active Directory ドメイン コントローラーの完全修飾ドメイン名 (FQDN) を有する必要があります。 この情報は、**New-RoleGroup** コマンドレットの *LinkedDomainController* パラメーターで使用されます。
    
      - **外部 USG**   リンクされた役割グループに関連付けるメンバーを含む外部 Active Directory フォレスト内の USG の完全名を有する必要があります。 この情報は、**New-RoleGroup** コマンドレットの *LinkedForeignGroup* パラメーターで使用されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して組み込みの役割グループを複製するリンクされた役割グループを作成する

以下の各セクションでは、各役割グループをリンクされた役割グループとして作成し直す方法を示します。 各セクションの手順を実行すると、すべての組み込みの役割グループをリンクされた役割グループとして作成し直すことができます。

## リンクされた "Organization Management/組織の管理" 役割グループを作成する

組織の管理 役割グループをリンクされた役割グループとして作成し直すには、他の組み込みの役割グループを作成し直す手順とは異なる手順を実行します。 これは、組織の管理 役割グループには、この役割グループとすべての管理役割との間に委任の役割割り当てがあるためです。 委任の役割の割り当てを作成し直すには、さらに別の手順が必要になります。

1.  外部フォレスト内で 組織の管理 役割グループにリンクされる USG を作成します。

2.  変数に外部 Active Directory フォレストの資格情報を格納します。
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

3.  組織の管理 役割グループに割り当てられたすべての役割を変数に格納します。
    
        $OrgMgmt  = Get-RoleGroup "Organization Management"

4.  組織の管理 のリンクされた役割グループを作成し、組み込みの 組織の管理 役割グループに割り当てられた役割を追加します。
    
    ```powershell
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    ```

5.  新しい組織の管理 のリンクされた役割グループと My\* エンドユーザー役割の間のすべての正規の割り当てを削除します。
    
    ```powershell
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    ```

6.  新しい組織の管理 のリンクされた役割グループとすべての管理役割の間の委任の役割の割り当てを追加します。
    
    ```powershell
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating
    ```

この例では、以下の値が各パラメーターに使用されていることを想定しています。

  - **LinkedForeignGroup**   `Organization Management Administrators`

  - **LinkedDomainController**   `DC01.users.contoso.com`

この例では、上記の値を使用して 組織の管理 役割グループをリンクされた役割グループとして作成し直します。

```powershell
$ForeignCredential = Get-Credential
```
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

## 他のすべてのリンクされた役割グループを作成する

組み込みの役割グループ (組織の管理役割グループ以外) をリンクされた役割グループとして作成し直すには、グループごとに以下の手順を実行します。

1.  各新しい役割グループにリンクされる各役割グループの外部フォレスト内で USG を作成します。

2.  変数に外部 Active Directory フォレストの資格情報を格納します。 これは 1 度実行するだけで十分です。
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

3.  以下のコマンドレットを使用して役割グループ一覧を取得します。
    
    ```powershell
    Get-RoleGroup
    ```

4.  組織の管理 役割グループ以外の各役割グループに対して、次の操作を実行します。
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to re-create>
    New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    ```

5.  リンクされた役割グループとして作成し直す必要がある組み込みの役割グループごとに、上記の手順を繰り返します。

この例では、以下の値が各パラメーターに使用されていることを想定しています。

  - **LinkedDomainController**   `DC01.users.contoso.com`

  - **リンクされた役割グループとして作成し直す組み込みの役割グループ**   `Recipient Management, Server Management`

  - **受信管理のリンクされた役割グループの外部グループ**   `Recipient Management Administrators`

  - **送信管理のリンクされた役割グループの外部グループ**   `Server Management Administrators`

上記の値を使用して、この例では、Recipient Management と "Server Management/サーバーの管理" 役割グループをリンクされた役割グループとして作成し直します。

```powershell
$ForeignCredential = Get-Credential
```
```powershell
Get-RoleGroup
```
```powershell
$RoleGroup = Get-RoleGroup "Recipient Management"
New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
$RoleGroup = Get-RoleGroup "Server Management"
New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
```

## その他のタスク

リンクされた役割グループを作成した後で、次の操作も実行できます。

外部フォレスト内の Active Directory ユーザーとコンピューターを使用する外部 USG を追加します。

組み込みの役割グループのメンバーを削除します。詳細については、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。

新しいリンクされた役割グループで役割のスコープを追加、削除、または変更します。詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

追加のリンクされた役割グループを作成します。詳細については、「[リンクされた役割グループの管理](manage-linked-role-groups-exchange-2013-help.md)」を参照してください。

