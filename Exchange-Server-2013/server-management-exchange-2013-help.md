---
title: 'サーバー管理: Exchange 2013 Help'
TOCTitle: サーバー管理
ms:assetid: 30cbc4de-adb3-42e8-922f-7661095bdb8c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876866(v=EXCHG.150)
ms:contentKeyID: 49896187
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# サーバー管理

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

サーバー管理 管理役割グループは、Microsoft Exchange Server 2013 の役割ベースのアクセス制御 (RBAC) というアクセス許可モデルを構成するいくつかの組み込みの役割グループの 1 つです。役割グループには、指定された一連のタスクの実行に必要なアクセス許可を含む 1 つ以上の管理役割が割り当てられます。役割グループのメンバーには、役割グループに割り当てられた管理役割に対するアクセス権が付与されます。役割グループの詳細については、「[管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)」を参照してください。

この役割グループのメンバーである管理者は、データベース コピー、証明書、トランスポート キューと送信コネクタ、仮想ディレクトリ、クライアント アクセス プロトコルなど、トランスポート クライアント アクセスとメールボックスの各機能にサーバー固有の構成を構成できます。

この役割グループは、Microsoft Exchange の Exchange Server 2007 サーバー管理者の役割に似ています。物理サーバーの構成を管理するためのアクセスが許可されます。ただし、Exchange が実行されているローカル サーバーへのアクセス許可のみが付与された、Exchange 2007 の Exchange 2007 "Server Administrators/サーバー管理者" 役割とは異なり、"Server Management/サーバーの管理" 役割グループでは表示および構成のために組織内のすべての Exchange Server 2010 サーバーにアクセスできます。

管理者に組織内の特定サーバーの管理のみを許可する場合は、この役割グループに適用される管理スコープを変更できます。または、"Server Management/サーバーの管理" 役割グループに基づいて役割グループを作成し、新しい役割グループの管理スコープをカスタマイズできます。詳細については、このトピックの後半の「役割グループのカスタマイズ」を参照してください。

RBAC の詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

## 役割グループ メンバーシップ

この役割グループに対してメンバーを追加または削除する場合は、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。

既定では、"Organization Management" 役割グループのメンバーのみ、この役割グループに対してメンバーを追加または削除できます。役割グループの委任をさらに追加する方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループの委任の追加または削除」を参照してください。

次のコマンドを使用して、この役割グループのメンバーであるユーザーまたはユニバーサル セキュリティ グループ (USG) の一覧を表示できます。

    Get-RoleGroupMember "Server Management"

役割グループのメンバーの詳細については、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」の「[View the members of a role group](manage-role-group-members-exchange-2013-help.md)」を参照してください。

## 役割グループのカスタマイズ

この役割グループには、既定で管理役割が割り当てられます。含まれている役割の一覧については、「この役割グループに割り当てられている管理役割」をご覧ください。組織のニーズに合わせて、この役割グループに対して役割の割り当てを追加または削除できます。

Exchange 2013 で提供される役割グループは、よりきめ細かなタスクに合うように設計されています。役割を役割グループに割り当てることで、その役割グループのメンバーがその役割に関連付けられているタスクを実行できるようにできます。たとえば、"Journaling /ジャーナリング" 役割では、ジャーナリング エージェントとジャーナリング ルールを管理できます。役割グループに役割を割り当てる方法について詳しくは、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」をご覧ください。

この役割グループに割り当てられる役割には、既定の管理スコープが与えられます。管理スコープは、役割グループのメンバーが表示または変更できる Exchange オブジェクトを決定します。役割と役割グループ間の割り当てに関連付けられているスコープは、変更できます。たとえば、役割グループのメンバーのみが特定の組織単位または特定の場所の受信者を変更できるようにする場合に、この操作を行うことができます。管理のスコープについて詳しくは、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」をご覧ください。

この役割グループのカスタマイズ方法について詳しくは、次のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)

役割グループを作成し、この役割グループに割り当てられている役割の一部を新しい役割グループに割り当てる場合は、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループの作成」を参照してください。

## この役割グループに割り当てられている管理役割

次の表は、この役割グループに割り当てられるすべての管理役割、および各役割の割り当ての次の属性の一覧です。

  - **正規割り当て**   役割グループのメンバーが、関連付けられている管理役割によって利用可能にされた管理役割エントリにアクセスできるようにします。

  - **委任割り当て**   役割グループのメンバーが、特定の役割を他の役割グループ、役割割り当てポリシー、ユーザー、または USG に割り当てられるようにします。

  - **受信者の読み取りスコープ**   Active Directory から読み取りできる役割グループの受信者オブジェクト メンバーを決定します。

  - **受信者の書き込みスコープ**   Active Directory で変更できる役割グループの受信者オブジェクト メンバーを決定します。

  - **構成の読み取りスコープ**   Active Directory から読み取りできる役割グループの構成オブジェクトとサーバー オブジェクトのメンバーを決定します。

  - **構成の書き込みスコープ**   Active Directory で変更できる役割グループの構成オブジェクトとサーバー オブジェクトのメンバーを決定します。

役割の割り当てと管理スコープについて詳しくは、次のトピックを参照してください。

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

### この役割グループに割り当てられている管理役割

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割</th>
<th>正規の割り当て</th>
<th>委任の割り当て</th>
<th>受信者の読み取りスコープ</th>
<th>受信者の書き込みスコープ</th>
<th>構成の読み取りスコープ</th>
<th>構成の書き込みスコープ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="database-copies-role-exchange-2013-help.md">&quot;Database Copies/データベース コピー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="databases-role-exchange-2013-help.md">&quot;Databases/データベース&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">&quot;Exchange Connectors/Exchange コネクタ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">&quot;Exchange Server Certificates/Exchange Server 証明書&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange Servers 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">&quot;Exchange Virtual Directories/Exchange 仮想ディレクトリ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-role-exchange-2013-help.md">&quot;Monitoring/監視&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">&quot;POP3 and IMAP4 Protocols/POP3 および IMAP4 プロトコル&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="receive-connectors-role-exchange-2013-help.md">&quot;Receive Connectors/受信コネクタ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-queues-role-exchange-2013-help.md">&quot;Transport Queues/トランスポート キュー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

