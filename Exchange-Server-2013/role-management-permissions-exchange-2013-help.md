---
title: '役割管理のアクセス許可: Exchange 2013 Help'
TOCTitle: 役割管理のアクセス許可
ms:assetid: cb9591c4-fbb3-4199-8007-6bbfdfd5a2e9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638186(v=EXCHG.150)
ms:contentKeyID: 48270047
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割管理のアクセス許可

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

管理役割を構成するタスクの実行に必要なアクセス許可は、実行する手順、または実行するコマンドレットによって異なります。管理役割の詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。

## 役割管理のアクセス許可

次の表の機能を使用して、管理役割グループ、役割、割り当てポリシー、割り当て、管理者に適用できるアクセス許可を定義するスコープ、およびエンド ユーザーを管理できます。"View-Only Management (閲覧限定の管理)" 役割グループが割り当てられているユーザーは、次の表にある機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>必要なアクセス許可</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理役割</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>対象範囲外の管理役割</p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">&quot;Unscoped Role Management/スコープ外役割管理&quot; 役割</a> 管理役割</p></td>
</tr>
<tr class="odd">
<td><p>役割グループ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>割り当てポリシー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>役割の割り当て</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>管理スコープ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>管理役割エントリ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>従来のアクセス許可</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Active Directory の分割型アクセス許可</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>

> [!IMPORTANT]
> <EM>PrepareAD</EM> パラメーターおよび <EM>ActiveDirectorySplitPermissions</EM> パラメーターを使用して <CODE>setup.exe</CODE> コマンドを実行するには、使用するアカウントが Schema Admins グループと Enterprise Administrators グループのメンバーである必要があります。


</td>
</tr>
</tbody>
</table>

