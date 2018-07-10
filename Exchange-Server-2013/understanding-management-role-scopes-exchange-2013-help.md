---
title: '管理役割スコープについて: Exchange 2013 Help'
TOCTitle: 管理役割スコープについて
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 49895296
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理役割スコープについて

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

*管理役割スコープ*を使用すると、管理役割が作成されたときに管理役割の割り当てに影響を及ぼす一定の範囲を定義できます。スコープを適用する場合、役割が割り当てられた役割担当者は、そのスコープの中に含まれているオブジェクトのみを変更できます。役割担当者は管理役割グループ、管理役割、管理役割割り当てポリシー、ユーザー、またはユニバーサル セキュリティ グループ (USG) のいずれかです。管理役割の詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> ここでは、RBAC の高度な機能について説明します。基本的な Exchange 2013 アクセス許可を管理する場合 (Exchange 管理センター (EAC) を使用して役割グループ間のメンバーの追加と削除、役割グループの作成と変更、役割割り当てポリシーの作成と変更を行う場合など) は、「<A href="permissions-exchange-2013-help.md">アクセス許可</A>」を参照してください。



すべての管理役割には、組み込みの役割とカスタムの役割のいずれであっても、管理スコープがあります。管理スコープは以下のいずれかです。

  - **通常**   *通常スコープ*は排他的ではありません。これは Active Directory で、管理役割が割り当てられたユーザーによってオブジェクトを表示または変更できる範囲を指定します。一般に、管理役割とは作成または変更が可能な内容を示し、管理役割スコープは作成または変更を実行できる場所を示します。正規のスコープは、暗黙的スコープまたは明示的スコープのどちらでも可能です。詳細はこのトピックで後述します。

  - **排他的**   *排他的スコープ*の動作は、通常スコープとほぼ同じです。重要な違いは、排他的スコープに関連付けられた役割がユーザーに割り当てられていない場合、排他的スコープ内に含まれるオブジェクトに対してそれらのユーザーのアクセスを拒否できることです。排他的スコープはすべて明示的スコープです。これらについては、後で説明します。
    
    排他的スコープの詳細については、「[排他スコープについて](understanding-exclusive-scopes-exchange-2013-help.md)」を参照してください。

スコープは、管理役割から継承するか、管理役割割り当てで定義済みの相対スコープとして指定するか、カスタム フィルターを使用して作成して管理役割割り当てに追加することができます。管理役割から継承される管理スコープは*暗黙的スコープ*と呼ばれ、定義済みおよびカスタムのスコープは*明示的スコープ*と呼ばれます。以下のセクションでは、各種スコープについて説明します。

  - 暗黙的スコープ

  - 明示的スコープ

  - 定義済み相対スコープ

  - カスタム スコープ
    
      - 受信者フィルター スコープ
    
      - 構成スコープ

各役割には、次の種類のスコープを設定できます。

  - **受信者の読み取りスコープ**   暗黙的受信者読み取りスコープは、Active Directory からの読み取りを許可する、ユーザーによって管理役割が割り当てられた受信者オブジェクトを指定します。

  - **受信者の書き込みスコープ**   暗黙的受信者書き込みスコープは、Active Directory での変更を許可する、ユーザーによって管理役割が割り当てられた受信者オブジェクトを指定します。

  - **構成の読み取りスコープ**   暗黙的構成読み取りスコープは、Active Directory からの読み取りを許可する、ユーザーによって管理役割が割り当てられた構成オブジェクトを指定します。

  - **構成の書き込みスコープ**   暗黙的構成書き込みスコープは、Active Directory での変更を許可する、ユーザーによって管理役割が割り当てられた組織、データベース、およびサーバー オブジェクトを指定します。

受信者オブジェクトには、メールボックス、配布グループ、メールが有効なユーザー、およびその他のオブジェクトが含まれます。構成オブジェクトには、Microsoft Exchange Server 2013 を実行しているサーバーと、Exchange を実行しているサーバーにあるデータベースが含まれます。各種スコープは、暗黙的スコープまたは明示的スコープのいずれかです。

## 暗黙的スコープ

暗黙的スコープは、管理役割の種類に適用される既定のスコープです。暗黙的スコープが管理役割の種類に関連付けられているため、同じ役割の種類の親および子の管理役割もすべて暗黙的スコープが設定されます。暗黙的スコープは、組み込み管理役割とカスタム管理役割の両方に適用されます。管理役割と管理役割の種類については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

以下の表は、管理役割で定義できる暗黙的スコープのすべてを示します。

### 管理役割で定義された暗黙的スコープ

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>暗黙的スコープ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code> が役割の受信者書き込みスコープ内にある場合、役割は Exchange 組織全体にわたって受信者オブジェクトを作成または変更できます。</p>
<p><code>Organization</code> が役割の受信者読み取りスコープ内にある場合、役割は Exchange 組織全体にわたって受信者オブジェクトを表示できます。</p>
<p>このスコープは、受信者の読み取りおよび書き込みスコープでのみ使用されます。</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code> が役割の受信者書き込みスコープ内にある場合、役割は現行ユーザーのグローバル アドレス一覧 (GAL) 内にある受信者のプロパティを表示できます。</p>
<p><code>MyGAL</code> が役割の受信者読み取りスコープ内にある場合、役割は現行 GAL 内にある受信者のプロパティを表示できます。</p>
<p>このスコープは、受信者読み取りスコープでのみ使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p><code>Self</code> が役割の受信者書き込みスコープ内にある場合、役割は現行ユーザーのメールボックスのプロパティのみを変更できます。</p>
<p><code>Self</code> が役割の受信者読み取りスコープ内にある場合、役割は現行ユーザーのメールボックスのプロパティのみを表示できます。</p>
<p>このスコープは、受信者の読み取りおよび書き込みスコープでのみ使用されます。</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyDistributionGroups</code> が役割の受信者書き込みスコープ内にある場合、役割は現行ユーザーが所有する配布リスト オブジェクトを作成または変更できます。</p>
<p><code>MyDistributionGroups</code> が役割の受信者読み取りスコープ内にある場合、役割は現行ユーザーが所有する配布リスト オブジェクトを表示できます。</p>
<p>このスコープは、受信者の読み取りおよび書き込みスコープでのみ使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code> が役割の構成書き込みスコープ内にある場合、役割は Exchange 組織全体にわたってサーバーまたはデータベース構成オブジェクトを作成または変更できます。</p>
<p><code>OrganizationConfig</code> が役割の構成読み取りスコープ内にある場合、役割は Exchange 組織全体にわたってサーバーまたはデータベース構成オブジェクトを変更できます。</p>
<p>このスコープは、構成読み取りおよび書き込みスコープでのみ使用されます。</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p><code>None</code> がスコープ内にある場合、役割はそのスコープを使用できません。たとえば、受信者書き込みスコープ内に <code>None</code> がある役割は Exchange 組織内の受信者オブジェクトを変更できません。</p></td>
</tr>
</tbody>
</table>


役割が役割担当者に割り当てられ、定義済みまたはカスタムのスコープが指定されていない場合は、ユーザーが表示または変更できる受信者または組織オブジェクトを制御するために、役割で定義された暗黙的スコープが使用されます。

役割の暗黙的書き込みスコープは、常に暗黙的読み取りスコープ以下です。つまり、役割はスコープによって表示できないオブジェクトを変更することはできません。

管理役割で定義された暗黙的スコープを変更することはできません。ただし、管理役割で暗黙的書き込みスコープと構成スコープを上書きすることはできます。定義済みの相対スコープまたはカスタム スコープが役割割り当てで使用される場合、役割の暗黙的書き込みスコープが上書きされ、新しいスコープが優先されます。役割の暗黙的読み取りスコープは、上書きできず、常に適用されます。詳細については、「定義済み相対スコープ」および「カスタム スコープ」を参照してください。

以下の表を展開すると、すべての組み込み管理役割とそれらの暗黙的スコープのリストが表示されます。各組み込みの役割の詳細については、「[組み込みの管理役割](built-in-management-roles-exchange-2013-help.md)」を参照してください。

## 組み込み管理役割の暗黙的スコープ


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割</th>
<th>受信者の読み取りスコープ</th>
<th>受信者の書き込みスコープ</th>
<th>構成の読み取りスコープ</th>
<th>構成の書き込みスコープ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## 明示的スコープ

明示的スコープは、管理役割がどのオブジェクトを変更できるかをユーザー自身で設定して制御するスコープです。暗黙的スコープは管理役割で定義されますが、明示的スコープが管理役割割り当てで定義されます。つまり、最優先の明示的スコープの使用を選択しなければ、管理役割全体に暗黙的スコープを定常的に適用できます。管理役割の割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

明示的スコープは、管理役割の暗黙的書き込みスコープと構成スコープを上書きします。明示的スコープは、管理役割の暗黙的読み取りスコープを上書きしません。暗黙的読み取りスコープは、管理役割が読み取ることができるオブジェクトの定義を継続します。

明示的スコープは、管理役割の暗黙的書き込みスコープがビジネス要件を満たしていない場合に役立ちます。新しいスコープが暗黙的読み取りスコープの範囲を超えない限り、必要とするほとんどすべてを含むために明示的スコープを追加できます。管理役割の一部であるコマンドレットは、オブジェクトを作成または変更するためにコマンドレットのオブジェクトを含むオブジェクトまたはコンテナーに関する情報を読み取ることができる必要があります。たとえば、管理役割の暗黙的読み取りスコープが `Self` に設定される場合、明示的書き込みスコープが暗黙的読み取りスコープの範囲を超えるので、`Organization` の明示的書き込みスコープを追加できません。

詳細については、以下のセクションを参照してください。

  - 定義済み相対スコープ

  - カスタム スコープ

## 定義済み相対スコープ

Exchange 2013 では、管理役割の範囲を変更するために使用できる複数の定義済み相対書き込みスコープを提供します。定義済み相対スコープを使用すると、カスタム スコープを手動で作成しなくても、簡単にビジネス要件を細部まで一致させることができます。これらが相対スコープと呼ばれるのは、関連役割割り当てが割り当てられた役割担当者を基準とした、相対指定のスコープであるためです。たとえば、`Self` 定義済み相対スコープは、その書き込みスコープを現行ユーザーのみに制限します。`MyDistributionGroups` 定義済み相対スコープは、書き込みスコープを現行ユーザーの所有配布グループのみに制限します。定義済み相対スコープは、受信者オブジェクトの範囲設定にのみ使用できます。定義済み相対スコープは、構成オブジェクトの範囲設定には使用できません。次の表は、使用できる定義済み相対スコープの一覧を示します。

### 定義済み相対スコープ

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>暗黙的スコープ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code> が役割の受信者書き込みスコープ内にある場合、役割は Exchange 組織全体にわたって受信者オブジェクトを作成または変更できます。</p>
<p><code>Organization</code> が役割の受信者読み取りスコープ内にある場合、役割は Exchange 組織全体にわたって受信者オブジェクトを表示できます。</p>
<p>このスコープは、受信者の読み取りおよび書き込みスコープでのみ使用されます。</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p><code>Self</code> が役割の受信者書き込みスコープ内にある場合、役割は現行ユーザーのメールボックスのプロパティのみを変更できます。</p>
<p><code>Self</code> が役割の受信者読み取りスコープ内にある場合、役割は現行ユーザーのメールボックスのプロパティのみを表示できます。</p>
<p>このスコープは、受信者の読み取りおよび書き込みスコープでのみ使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyDistributionGroups</code> が役割の受信者書き込みスコープ内にある場合、役割は現行ユーザーが所有する配布リスト オブジェクトを作成または変更できます。</p>
<p><code>MyDistributionGroups</code> が役割の受信者読み取りスコープ内にある場合、役割は現行ユーザーが所有する配布リスト オブジェクトを表示できます。</p>
<p>このスコープは、受信者の読み取りおよび書き込みスコープでのみ使用されます。</p></td>
</tr>
</tbody>
</table>


定義済み相対スコープは、新しい管理役割割当てを作成するときに適用されます。**New-ManagementRoleAssignment** コマンドレットを使用して役割割り当てを作成するときに、*RecipientRelativeWriteScope* パラメーターを使用して定義済み相対スコープを指定できます。新しい役割割り当てが作成されると、新しい定義済み役割が管理役割の暗黙的書き込みスコープを上書きします。定義済み相対スコープを持つ役割割り当てを作成する場合に、カスタム受信者スコープを指定することはできません。ただし、必要な場合は、カスタム構成スコープを指定できます。

定義済み相対スコープと共に管理役割割り当てを追加する方法については、「[ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)」を参照してください。

## カスタム スコープ

カスタム スコープは、暗黙的書き込みスコープと定義済み相対スコープのどちらもビジネス要件に対応できない場合に必要です。カスタム スコープでは、管理役割を適用するスコープを詳細レベルで定義できます。たとえば、特定の組織単位 (OU)、特定の種類の受信者、またはその両方を対象にする場合があります。または、単に管理者のグループでメールボックス データベースの特定セットを管理できるようにする場合があります。

定義済み相対スコープと同様に、カスタム スコープは管理役割で定義された暗黙的書き込みおよび組織構成スコープを上書きします。管理役割の暗黙的読み取りスコープは続いて適用され、結果のカスタム スコープは暗黙的読み取りスコープの範囲を超えることができません。次の 3 種類のカスタム スコープを作成できます。

  - **OU スコープ**   OU スコープは、最も単純なカスタム スコープであり、**New-ManagementRoleAssignment** コマンドレットで *RecipientOrganizationalUnitScope* パラメーターを使用して作成されます。役割の割り当て時に OU スコープを指定することによって、役割が割り当てられた役割担当者はその OU 内の受信者オブジェクトのみを変更できます。OU スコープと共に管理役割割り当てを追加する方法については、「[ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)」を参照してください。

  - **受信者フィルター スコープ**   受信者フィルター スコープは、フィルターを使用することによって、受信者の種類または部門、マネージャー、場所などその他の受信者プロパティに基づいて特定の受信者を対象にします。詳細については、「受信者フィルター スコープ」を参照してください。

  - **構成スコープ**   構成スコープは、フィルターまたはリストを使用することによって、Active Directory サイトまたはサーバー役割など、サーバーに定義できるサーバー リストまたはフィルター可能プロパティに基づいて、特定のサーバーを対象にします。データベース一覧やフィルター可能データベース プロパティに従って特定のデータベースを指定するとき、構成スコープではデータベース スコープも使用できます。詳細については、「構成スコープ」を参照してください。

単純かつ広範または複雑かつ詳細な受信者および構成カスタム スコープは、**New-ManagementScope** コマンドレットを使用して作成できます。受信者スコープまたは構成スコープのいずれかを作成すると、それぞれのスコープに一致する受信者、サーバー、またはデータベースのオブジェクトのみが返されます。これらのスコープが **New-ManagementRoleAssignment** または **Set-ManagementRoleAssignment** コマンドレットを使用して役割割り当てに適用されると、役割が割り当てられた役割担当者がスコープに一致するオブジェクトのみを変更できます。カスタム スコープが作成された後は、スコープの種類を変更できません。受信者スコープは常に受信者スコープであり、構成スコープは常に構成スコープです。

既定では、カスタム スコープによって、定義するスコープに一致したオブジェクトのセットに役割担当者がアクセスすることができます。ただし、フィルターは同一または同等のスコープも割り当てられていない他の役割担当者へのアクセスをアクティブに除外しません。カスタム スコープは、それらのスコープへのリストまたはフィルターが同一オブジェクトに一致する場合、同一オブジェクトにアクセスできます。上級管理者など、この操作が不要なオブジェクトがあります。これらのオブジェクトに対して、排他的スコープを定義できます。排他的スコープは、通常スコープと同じ方法でフィルターまたはリストを使用しますが、通常スコープと異なり、同一または同等の排他的スコープに含まれない人物によるスコープ内のオブジェクトへのアクセスを拒否します。排他的スコープの詳細については、「[排他スコープについて](understanding-exclusive-scopes-exchange-2013-help.md)」を参照してください。

## 受信者フィルター スコープ

受信者フィルター スコープを使用すると、フィルター ステートメントで指定する値に対して受信者オブジェクトの 1 つまたは複数のプロパティを評価することによって、役割担当者が管理できる受信者オブジェクトを制御できます。受信者スコープに含まれる受信者はメールボックス、メールが有効なユーザー、配布グループ、およびメール連絡先です。その役割の割り当てが割り当てられた役割担当者が管理するのは、指定するフィルターに一致する受信者のみです。フィルター ステートメントの例は、`{ Name -Eq "David" }` です。ここで、**Name** は評価中の受信者オブジェクトのプロパティであり、**David** はプロパティに対して評価する値です。**-Eq** 比較演算子は、プロパティに格納された値がフィルターに true として指定された値と同等でなくてはなりません。フィルターが true の場合、その受信者はスコープに含まれています。

受信者フィルター スコープを作成するには、*RecipientRestrictionFilter* パラメーターを **New-ManagementScope** コマンドレットで使用する受信者フィルターを指定します。既定では、**New-ManagementScope** コマンドレットが正規のスコープを作成します。排他的スコープを作成する場合は、*Exclusive* スイッチを *RecipientRestrictionFilter* パラメーターと共に指定します。

受信者制限フィルターを作成する場合、Exchange は、既定で組織内の受信者オブジェクトごとに指定したフィルターを評価します。スコープが評価する受信者を制限する場合は、*RecipientRoot* パラメーターと共に *RecipientRestrictionFilter* パラメーターを使用できます。*RecipientRoot* パラメーターには、OU を指定できます。*RecipientRoot* パラメーターを使用する場合、Exchange は、入力したフィルターに対して指定の OU に含まれる受信者のみを評価します。

受信者フィルター スコープを役割の割り当てに追加する場合、新しい役割の割り当てを作成していれば **New-ManagementRoleAssignment** コマンドレットで、既存の役割の割り当てを更新していれば **Set-ManagementRoleAssignment** コマンドレットで、*CustomRecipientWriteScope* パラメーター内の受信者スコープの名前を指定します。各ロールの割り当てには、定義済みの相対的なスコープなど、1 つの受信者スコープを指定できます。受信者スコープの追加先となった同じ役割の割当てに対して、1 つの構成スコープを追加できます。

フィルター構文の詳細と、受信者に対するフィルター可能な受信者プロパティの全リストについては、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

## 構成スコープ

次の 2 種類の構成のスコープが Exchange 2013 で提供されます。

  - **サーバー スコープ**   サーバー スコープには、サーバー フィルター スコープとサーバー リスト スコープという 2 つの種類があります。受信コネクタ、トランスポート キュー、サーバー証明書、仮想ディレクトリなどのサーバー構成は、サーバー スコープにサーバー オブジェクトが含まれる場合に管理できます。
    
      - **サーバー フィルター スコープ**   サーバー フィルター スコープを使用すると、フィルター ステートメントで指定する値に対してサーバー オブジェクトの 1 つまたは複数のプロパティを評価することによって、役割担当者が管理できるサーバー オブジェクトを制御できます。サーバー フィルター スコープを作成するには、*ServerRestrictionFilter* パラメーターを **New-ManagementScope** コマンドレットで使用します。
    
      - **サーバー リスト スコープ**   サーバー リスト スコープを使用すると、役割担当者がアクセスできるサーバーのリストを定義することによって、役割担当者が管理できるサーバー オブジェクトを制御できます。サーバー リスト スコープを作成するには、*ServerList* パラメーターを **New-ManagementScope** コマンドレットで使用します。

  - **データベース スコープ**   データベース スコープには、データベース フィルター スコープとデータベース リスト スコープという 2 つの種類があります。データベース オブジェクトがデータベース スコープに含まれる場合に管理できるデータベース構成には、データベースのクォータ制限、データベース保守、パブリック フォルダー レプリケーション、データベースのマウント有無などがあります。データベース構成以外に、データベース スコープ内にどのデータベース受信者を作成できるかも、データベース スコープで制御できます。所属組織で Exchange 2010 SP1 より前のサーバーを使用している場合、このトピックの後半の データベース スコープと Exchange の以前のバージョン セクションを参照してください。
    
      - **データベース フィルター スコープ**   データベース フィルター スコープを使用すると、フィルター ステートメントで指定する値に対してデータベース オブジェクトの 1 つまたは複数のプロパティを評価することによって、役割担当者が管理できるデータベース オブジェクトを制御できます。データベース フィルター スコープを作成するには、*DatabaseRestrictionFilter* パラメーターを **New-ManagementScope** コマンドレットで使用します。
    
      - **データベース リスト スコープ**   データベース リスト スコープを使用すると、役割担当者がアクセスできるデータベースのリストを定義することによって、役割担当者が管理できるデータベース オブジェクトを制御できます。データベース リスト スコープを作成するには、*DatabaseList* パラメーターを **New-ManagementScope** コマンドレットで使用します。

フィルター構文の詳細と、フィルター可能なサーバーおよびデータベース プロパティの全リストについては、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

サーバーおよびデータベース リストを定義するには、それぞれのスコープの対象にする各サーバーおよびデータベースを指定します。複数のサーバーまたはデータベースは、サーバーとデータベースの名前をコンマで区切ることによって、それぞれのスコープに指定できます。

サーバーまたはデータベース構成スコープを役割の割り当てに追加する場合、新しい役割の割り当てを作成しているならば **New-ManagementRoleAssignment** コマンドレットで、既存の役割の割り当てを更新しているならば **Set-ManagementRoleAssignment** コマンドレットで、*CustomConfigWriteScope* パラメーター内のサーバーまたはデータベース構成スコープの名前を指定します。各ロールの割り当てには、1 つの構成スコープのみを指定できます。

役割担当者が管理できるデータベースを制御することに加えて、データベース スコープを使用すると、役割担当者がメールボックスを作成できるデータベースを制御することもできます。これは、役割担当者が管理できる受信者の管理とは別です。役割担当者に新しいメールボックスを作成するか、既存ユーザーのメールを有効にするか、またはメールボックスを移動するアクセス許可がある場合、メールボックスを作成するデータベースまたはメールボックスの移動先のデータベースをデータベース スコープで制御することによって、アクセス許可を詳細に設定することができます。役割担当者が管理できる受信者を制御することは、*CustomRecipientWriteScope* パラメーターを **New-ManagementRoleAssignment** または **Set-ManagementRoleAssignment** コマンドレットで指定した受信者スコープで行われます。メールボックスを作成できるデータベースまたはメールボックスの移動先データベースを制御することは、*CustomConfigurationWriteScope* パラメーターを同じコマンドレットで指定したデータベース スコープで管理されます。


> [!NOTE]
> メールボックスの自動配布は、データベース スコープを使用して制御できます。



Exchange 機能では、サーバー スコープとデータベース スコープのどちらか、またはその両方の管理が必要な場合があります。サーバー スコープおよびデータベース スコープの両方が管理対象となる機能の場合、2 つの役割割り当てを作成して、機能の管理のためにアクセス許可を持つ必要がある役割担当者に割り当てる必要があります。役割割り当てのうち、1 つはサーバー スコープと関連付け、もう 1 つはデータベース スコープと関連付けます。

コマンドレットは、一目でわかる構成スコープを使用する場合もあります。次の表は、コマンドレットのリストと、利用を制御するために使用できる構成スコープを示します。受信者機能領域に含まれるコマンドレットの場合、構成スコープを使用すると、受信者を作成できるデータベースを制御できます。管理できる受信者は制御しません。**\[必要なスコープ\]** 列は、以下の項目で構成できます。

  - **データベース**   コマンドレットを実行するには、管理対象のデータベースを含むデータベース スコープによって役割担当者を役割の割り当てに割り当てるか、役割の暗黙的構成書き込みスコープに管理対象のデータベースを指定する必要があります。

  - **サーバー**   コマンドレットを実行するには、管理対象のサーバーを含むサーバー スコープによって役割担当者を役割の割り当てに割り当てるか、役割の暗黙的構成書き込みスコープに管理対象のサーバーを指定する必要があります。

  - **サーバーまたはデータベース**   コマンドレットを実行するには、データベース スコープに管理しているデータベースが含まれるか、サーバー スコープにデータベースが置かれたサーバーが含まれる役割の割り当てに役割担当者を割り当てる必要があります。または、役割の暗黙的構成書き込みスコープは、管理対象のデータベースを含むか、データベースが置かれたサーバーを含む必要があり、役割の割り当てにはカスタム書き込みスコープを設定できません。

  - **サーバーおよびデータベース**   このコマンドレットを実行するには、役割担当者を 2 つの役割割り当てに割り当てる必要があります。最初の役割割り当てには、管理対象のデータベースを含むデータベース スコープを指定する必要があります。2 番目の役割割り当てには、データベースが置かれたサーバーを含むサーバー スコープを指定する必要があります。役割割り当ては、カスタム構成スコープを定義することができるか、暗黙的構成書き込みスコープを役割から継承できます。役割から暗黙的書き込みスコープを継承するには、役割割り当てはカスタムの書き込みスコープを指定できません。

### 機能領域と適用可能なデータベース スコープおよびサーバー スコープ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>機能領域</th>
<th>コマンドレット</th>
<th>必要なスコープ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>データベース</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>データベース</p></td>
</tr>
<tr class="even">
<td><p>データベース</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>データベース</p></td>
</tr>
<tr class="odd">
<td><p>データベース</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>サーバーおよびデータベース</p></td>
</tr>
<tr class="even">
<td><p>データベース</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>サーバーまたはデータベース</p></td>
</tr>
<tr class="odd">
<td><p>データベース</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>データベース</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>サーバー</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>サーバーまたはデータベース</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>サーバーまたはデータベース</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>サーバーまたはデータベース</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>サーバーまたはデータベース</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>サーバーまたはデータベース</p></td>
</tr>
<tr class="odd">
<td><p>受信者</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>データベース</p></td>
</tr>
<tr class="even">
<td><p>受信者</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>データベース</p></td>
</tr>
<tr class="odd">
<td><p>受信者</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>データベース</p></td>
</tr>
<tr class="even">
<td><p>受信者</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>データベース</p></td>
</tr>
<tr class="odd">
<td><p>トラブルシューティング</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>データベース</p></td>
</tr>
</tbody>
</table>


## データベース スコープと Exchange の以前のバージョン

データベース スコープを最初に導入したのは Microsoft Exchange 2010 Service Pack 1 (SP1) でしたが、Exchange 2013 でも引き続きサポートしています。Exchange 2010 SP1 より前のバージョンの Exchange でサポートしているのは、受信者スコープとサーバー構成スコープだけです。新しいデータベース スコープを Exchange 2010 SP1 以降のサーバーで作成すると、次の警告が表示されます。

    WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.

データベース スコープを作成しても、適用されるのは Exchange 2010 SP1 以降を実行しているサーバーに接続するユーザーのみです。Exchange 2010 SP1 より前のサーバーに接続するユーザーには、適用されたデータベース スコープに関連付けた役割割り当てがありません。つまり、これらの役割割り当てで指定するアクセス許可は、ユーザーが Exchange 2010 SP1 より前のサーバーに接続するときには与えられません。データベース スコープは、Exchange 2010 SP1 より前のサーバーで作成、削除、変更、または表示することはできません。

データベース スコープには、Exchange 組織に任意のデータベースを指定できます。これには Exchange Server 2007、Exchange 2010、そして Exchange 2013 サーバーが含まれます。これにより、Exchange バージョンに関係なく、そのユーザーが管理できるデータベースを制御できるようになります。他のデータベース スコープと同様に、Exchange 2007 と Exchange 2010 のデータベースが含まれるデータベース スコープに関連付けられた役割割り当ては、ユーザーが Exchange 2010 SP1 以降のサーバーに接続するときだけに適用されます。

Exchange 2010 SP1 より前のサーバーに接続するユーザーは、データベース スコープに関連付けられた役割割り当ての表示と変更ができます。これには、データベース スコープに現在関連付けられている場合、サーバー スコープへの既存の役割割り当てで構成スコープを変更することが含まれます。ただし、役割割り当ての構成スコープをサーバー スコープに変更した後、ユーザーがデータベース スコープに戻す場合、またはユーザーが構成スコープを別のデータベース スコープに変更する場合、ユーザーは Exchange 2010 SP1 以降のサーバーに接続している間に変更する必要があります。Exchange 2010 SP1 より前のサーバーに接続している場合、ユーザーがサーバー スコープを指定できるのは、役割割り当ての構成スコープの変更時だけです。

