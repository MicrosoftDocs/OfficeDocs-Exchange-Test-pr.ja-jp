---
title: '組織の管理: Exchange 2013 Help'
TOCTitle: 組織の管理
ms:assetid: 0bfd21c1-86ac-4369-86b7-aeba386741c8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335087(v=EXCHG.150)
ms:contentKeyID: 49895232
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の管理

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

組織の管理 管理役割グループは、Microsoft Exchange Server 2013 の役割ベースのアクセス制御 (RBAC) というアクセス許可モデルを構成するいくつかの組み込みの役割グループの 1 つです。役割グループには、指定された一連のタスクの実行に必要なアクセス許可を含む 1 つ以上の管理役割が割り当てられます。役割グループのメンバーには、役割グループに割り当てられた管理役割に対するアクセス権が付与されます。役割グループの詳細については、「[管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)」を参照してください。

組織の管理 役割グループのメンバーである管理者は、Exchange 2013 組織全体に対する管理アクセス許可を持ち、一部の例外を除き、任意の Exchange 2013 オブジェクトに対してほぼすべてのタスクを実行できます。既定では、この役割グループのメンバーは、メールボックスの検索および対象範囲外の最上位の管理役割の管理はできません。詳細については、後の「委任専用の役割の割り当て」を参照してください。


> [!IMPORTANT]
> 組織の管理 役割グループは極めて強力な役割であるため、Exchange 組織全体に影響を与える可能性がある組織レベルの管理タスクを実行するユーザーまたはユニバーサル セキュリティ グループ (USG) のみ、この役割グループのメンバーにする必要があります。



この役割グループは、Exchange Server 2007 での Exchange 組織管理者の役割と同等です。

RBAC の詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

## 役割グループ メンバーシップ

既定では、組織で Exchange 2013 のインストールに使用されるアカウントが組織の管理役割グループのメンバーとして追加されます。このアカウントは、必要に応じて他のメンバーを役割グループに追加できます。

この役割グループに対してメンバーを追加または削除する場合は、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。

既定では、"Organization Management" 役割グループのメンバーのみ、この役割グループに対してメンバーを追加または削除できます。役割グループの委任をさらに追加する方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループの委任の追加または削除」を参照してください。

次のコマンドを使用して、この役割グループのメンバーであるユーザーまたは USG の一覧を表示できます。

    Get-RoleGroupMember "Organization Management"

役割グループのメンバーの詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

## 役割グループのカスタマイズ

この役割グループには、既定で管理役割が割り当てられます。含まれている役割の一覧については、「この役割グループに割り当てられている管理役割」をご覧ください。組織のニーズに合わせて、この役割グループに対して役割の割り当てを追加または削除できます。

Exchange 2013 で提供される役割グループは、よりきめ細かなタスクに合うように設計されています。役割を役割グループに割り当てることで、その役割グループのメンバーがその役割に関連付けられているタスクを実行できるようにできます。たとえば、"Journaling /ジャーナリング" 役割では、ジャーナリング エージェントとジャーナリング ルールを管理できます。役割グループに役割を割り当てる方法について詳しくは、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」をご覧ください。

この役割グループに割り当てられる役割には、既定の管理スコープが与えられます。管理スコープは、役割グループのメンバーが表示または変更できる Exchange オブジェクトを決定します。役割と役割グループ間の割り当てに関連付けられているスコープは、変更できます。たとえば、役割グループのメンバーのみが特定の組織単位または特定の場所の受信者を変更できるようにする場合に、この操作を行うことができます。管理のスコープについて詳しくは、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」をご覧ください。

この役割グループのカスタマイズ方法について詳しくは、次のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)

役割グループを作成し、この役割グループに割り当てられている役割の一部を新しい役割グループに割り当てる場合は、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループの作成」を参照してください。

この役割をカスタマイズするいくつかの方法を次に示します。

  - **アクセス許可の所有者**   組織内のアクセス許可が Exchange 管理者以外の特定のグループによって制御されている場合、役割グループを作成して、その新しい役割グループに "Role Management/役割管理" 役割の正規と委任の役割割り当てを移動できます。こうすることにより、組織の管理役割グループのメンバーが RBAC アクセス許可を管理できないようにできます。

  - **Active Directory の分割型アクセス許可**   ユーザー アカウントなどの組織内のセキュリティ プリンシパルの作成が、Exchange 管理者以外の特定のグループによって制御されている場合、役割グループを作成して、その新しい役割グループに、"Mail Recipient Creation/メール受信者の作成" 役割および "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割の正規と委任の役割割り当てを移動できます。これを行うと、組織の管理 役割グループのメンバーが Active Directory オブジェクトを作成できなくなります。ただしメンバーは、新しい Active Directory オブジェクトのメールを引き続き有効にすることができます。分割型アクセス許可の詳細については、「[分割型アクセス許可について](understanding-split-permissions-exchange-2013-help.md)」を参照してください。

## カスタマイズの制限

この役割グループに対しては、次の制限付きで、任意の役割を追加または削除できます。

  - この役割グループから委任役割割り当てを削除する前に、すべての役割に、役割グループまたは USG に対する少なくとも 1 つの委任役割割り当てがある必要があります。

  - この役割グループから正規の役割割り当てを削除する前に、"Role Management/役割管理" 役割に、役割グループまたは USG に対する少なくとも 1 つの正規の役割割り当てがある必要があります。

これらの制限は、システムから自分自身を誤ってロックアウトしないようにすることを目的としています。すべての役割と 1 つ以上の役割グループまたは USG 間に少なくとも 1 つの委任役割割り当てを存在するように要求することで、常に役割を役割担当者に割り当てられるようになります。"Role Management/役割管理" 役割と 1 つ以上の役割グループまたは USG 間に少なくとも 1 つの正規の役割割り当てが存在するように要求することで、常に役割グループと役割の割り当てを構成できるようになります。


> [!IMPORTANT]
> これらの制限により、役割グループまたは USG を委任または正規の役割割り当ての対象にすることが必要になります。最後の割り当てがユーザーに対するものである場合、"Role Management/役割管理" 役割の委任役割割り当てまたは正規の割り当てを削除することはできません。



## 委任専用の役割の割り当て

"Mailbox Search/メールボックス検索" と "Unscoped Role Management/対象範囲外の役割の管理" のような 組織の管理 役割グループと管理役割間の役割割り当ての一部は、役割割り当てのみが委任されます。これらの役割により、メールボックスの内容など機密情報または個人情報へのアクセスが許可され、強力な対象範囲外の管理役割の作成が可能になります。

委任専用の役割割り当てを使用すると、組織の管理役割グループのメンバーのみ、関連する役割を他の役割グループ、管理役割割り当てポリシー、ユーザー、または USG に割り当てられるようになります。組織の管理役割グループのメンバーには、既定では、その役割が提供するアクセス許可が付与されません。これにより、個人情報の誤った公開や特権の誤った昇格を避けられるようになります。

ただし、組織の管理 役割グループのメンバーは、自身にあらゆる役割を割り当てることが可能であり、実質上あらゆるタスクを実行できるようにすることが可能です。たとえば、組織の管理 役割グループのメンバーは、組織の管理 役割グループに "Mailbox Search/メールボックス検索" 役割を割り当てることができます。この役割の割り当てを行うと、組織の管理役割グループのメンバーは、"Mailbox Search/メールボックス検索" 役割によって有効にされたタスクを実行できます。

委任役割割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

## 追加のアクセス許可

組織の管理役割グループのメンバーに付与されるアクセス許可は、主にその役割グループに割り当てられた管理役割によって決まります。ただし、実行する必要があるタスクには、管理役割の対象に含まれていないタスクが存在します。一部のタスクは Exchange 管理ツール外で行われるため、RBAC アクセス許可モデルは適用されません。これらのタスクについては、組織の管理役割グループを特定の Active Directory オブジェクトのアクセス制御リスト (ACL) に追加することで、アクセス許可を提供します。

次のタスクに対するアクセス許可の付与は、Active Directory役割グループに割り当てられた管理役割でなく、組織の管理 オブジェクトの ACL によって行われます。

  - Setup.exe による DomainPrep と ForestPrep の実行

  - 組織内の追加のサーバーの展開

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
<th>受信者の読み取り範囲</th>
<th>受信者の書き込み範囲</th>
<th>構成の読み取り範囲</th>
<th>構成の書き込み範囲</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">&quot;Active Directory Permissions/Active Directory アクセス許可&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="address-lists-role-exchange-2013-help.md">&quot;Address Lists/アドレス一覧&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="audit-logs-role-exchange-2013-help.md">&quot;Audit Logs/監査ログ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">&quot;Cmdlet Extension Agents/コマンドレット拡張エージェント&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">&quot;Data Loss Prevention/データ損失防止&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">&quot;Database Availability Groups/データベース可用性グループ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="database-copies-role-exchange-2013-help.md">&quot;Database Copies/データベース コピー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="databases-role-exchange-2013-help.md">&quot;Databases/データベース&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">&quot;Disaster Recovery/障害回復&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="distribution-groups-role-exchange-2013-help.md">&quot;Distribution Groups/配布グループ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">&quot;Edge Subscriptions/エッジ サブスクリプション&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">&quot;E-Mail Address Policies/電子メール アドレス ポリシー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">&quot;Exchange Connectors/Exchange コネクタ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">&quot;Exchange Server Certificates/Exchange Server 証明書&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange Servers 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">&quot;Exchange Virtual Directories/Exchange 仮想ディレクトリ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="federated-sharing-role-exchange-2013-help.md">&quot;Federated Sharing/フェデレーションの共有&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Information Rights Management 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="journaling-role-exchange-2013-help.md">&quot;Journaling/ジャーナリング&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="legal-hold-role-exchange-2013-help.md">&quot;Legal Hold/法的情報保留&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="legalholdapplication-role-exchange-2013-help.md">LegalHoldApplication 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">&quot;Mail Enabled Public Folders/メールが有効なパブリック フォルダー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">&quot;メール受信者の作成&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-recipients-role-exchange-2013-help.md">&quot;Mail Recipient/メール受信者&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-tips-role-exchange-2013-help.md">&quot;Mail Tips/メール ヒント&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">&quot;Mailbox Import Export/メールボックスのインポートとエクスポート&quot; 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mailbox-search-role-exchange-2013-help.md">&quot;Mailbox Search/メールボックス検索&quot; 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="message-tracking-role-exchange-2013-help.md">&quot;Message Tracking/メッセージ追跡&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="migration-role-exchange-2013-help.md">&quot;Migration/移行&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-role-exchange-2013-help.md">&quot;Monitoring/監視&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">&quot;Move Mailboxes/メールボックスの移動&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-client-access-role-exchange-2013-help.md">&quot;Organization Client Access/組織クライアント アクセス&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="organization-configuration-role-exchange-2013-help.md">&quot;Organization Configuration/組織の構成&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">&quot;Organization Transport Settings/組織トランスポート設定&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">&quot;POP3 and IMAP4 Protocols/POP3 および IMAP4 プロトコル&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="public-folders-role-exchange-2013-help.md">&quot;Public Folders/パブリック フォルダー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="receive-connectors-role-exchange-2013-help.md">&quot;Receive Connectors/受信コネクタ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="recipient-policies-role-exchange-2013-help.md">&quot;Recipient Policies/受信者ポリシー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">&quot;Remote and Accepted Domains/リモートおよび承認済みドメイン&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="reset-password-role-exchange-2013-help.md">&quot;Reset Password/パスワードのリセット&quot; 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="retention-management-role-exchange-2013-help.md">&quot;Retention Management/保有管理&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="role-management-role-exchange-2013-help.md">&quot;Role Management/役割管理&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">&quot;Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="send-connectors-role-exchange-2013-help.md">&quot;Send Connectors/送信コネクタ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">&quot;Support Diagnostics/サポート診断&quot; 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-agents-role-exchange-2013-help.md">&quot;Transport Agents/トランスポート エージェント&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">&quot;Transport Hygiene/トランスポート検疫&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-queues-role-exchange-2013-help.md">&quot;Transport Queues/トランスポート キュー&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-rules-role-exchange-2013-help.md">&quot;Transport Rules/トランスポート ルール&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">&quot;UM Mailboxes/UM メールボックス&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="um-prompts-role-exchange-2013-help.md">&quot;UM Prompts/UM プロンプト&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">&quot;Unscoped Role Management/スコープ外役割管理&quot; 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="unified-messaging-role-exchange-2013-help.md">ユニファイド メッセージングの役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="user-options-role-exchange-2013-help.md">&quot;User Options/ユーザー オプション&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">&quot;View-Only Audit Logs/表示専用監査ログ&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">&quot;View-Only Configuration/表示専用構成&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">&quot;View-Only Recipients/表示専用受信者&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement 役割</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">&quot;My Custom Apps/自分のカスタム アプリ&quot; 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">&quot;My Marketplace Apps/マイ マーケットプレイス アプリ&quot; 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail 役割</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

