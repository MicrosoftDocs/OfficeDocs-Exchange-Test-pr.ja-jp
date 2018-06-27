---
title: '高可用性とサイト復元のアクセス許可: Exchange 2013 Help'
TOCTitle: 高可用性とサイト復元のアクセス許可
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 48269591
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 高可用性とサイト復元のアクセス許可

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-11-12_

高可用性を構成するのに必要なアクセス許可は、実行する手順、または実行するコマンドレットによって異なります。高可用性の詳細については、「[高可用性とサイトの復元](high-availability-and-site-resilience-exchange-2013-help.md)」を参照してください。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。

## データベース可用性グループのアクセス許可

データベース可用性グループ (DAG) の追加、削除、および設定の構成を実行するには、次の表の機能を使用できます。

"View-Only Management (閲覧限定の管理)" 役割グループが割り当てられているユーザーは、次の表にある機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


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
<td><p>データベース可用性グループのメンバーシップ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">&quot;Database Availability Groups/データベース可用性グループ&quot; 役割</a></p></td>
</tr>
<tr class="even">
<td><p>データベース可用性グループのプロパティ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">&quot;Database Availability Groups/データベース可用性グループ&quot; 役割</a></p></td>
</tr>
<tr class="odd">
<td><p>データベース可用性グループ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">&quot;Database Availability Groups/データベース可用性グループ&quot; 役割</a></p></td>
</tr>
<tr class="even">
<td><p>データベース可用性ネットワーク</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">&quot;Database Availability Groups/データベース可用性グループ&quot; 役割</a></p></td>
</tr>
</tbody>
</table>


## メールボックス データベース コピーのアクセス許可

メールボックス データベース コピーの追加、削除、更新、およびアクティブ化を実行するには、次の表の機能を使用できます。


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
<td><p>データベースの切り替え</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="databases-role-exchange-2013-help.md">&quot;Databases/データベース&quot; 役割</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックス データベース コピー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">&quot;Database Copies/データベース コピー&quot; 役割</a></p></td>
</tr>
<tr class="odd">
<td><p>サーバーの切り替え</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="databases-role-exchange-2013-help.md">&quot;Databases/データベース&quot; 役割</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックス データベース コピーの更新</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">&quot;Database Copies/データベース コピー&quot; 役割</a></p></td>
</tr>
</tbody>
</table>

