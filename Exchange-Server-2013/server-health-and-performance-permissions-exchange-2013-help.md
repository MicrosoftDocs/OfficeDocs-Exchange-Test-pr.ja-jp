---
title: 'サーバーの状態とパフォーマンスのアクセス許可: Exchange 2013 Help'
TOCTitle: サーバーの状態とパフォーマンスのアクセス許可
ms:assetid: 00b23fd3-6679-4b06-a3d4-51df3112b9cd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150479(v=EXCHG.150)
ms:contentKeyID: 48269118
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# サーバーの状態とパフォーマンスのアクセス許可

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

Microsoft Exchange Server 2013 の各種コンポーネントの構成作業を実行するために必要なアクセス許可は、実行している処理または実行するコマンドレットによって異なります。各機能の詳細については、このトピックの各セクションを参照してください。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。


> [!NOTE]
> 一部の機能では、管理するサーバーのローカル管理者アクセス許可を持っている必要がある場合があります。これらの機能を管理するには、このサーバーでローカルの Administrators グループのメンバーである必要があります。



## Exchange ワークロード管理のアクセス許可

次の表は、Exchange 2013 組織の正常性とパフォーマンスを管理するタスクの実行に必要なアクセス許可を示します。詳細については、「[Exchange ワークロード管理](exchange-workload-management-exchange-2013-help.md)」を参照してください。

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
<td><p>ユーザー調整</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ワークロード調整</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange イベント ログのアクセス許可

次の表は、Exchange イベント ログ設定を管理する作業の実行に必要なアクセス許可を示します。

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
<td><p>Exchange イベント ログ管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
</tbody>
</table>

