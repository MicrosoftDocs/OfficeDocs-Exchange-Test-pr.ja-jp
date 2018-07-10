---
title: '通常または排他スコープを作成する: Exchange 2013 Help'
TOCTitle: 通常または排他スコープを作成する
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 49896437
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通常または排他スコープを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

管理役割スコープでユーザーが使用できるオブジェクトを決定すると、割り当てられたコマンドレットとパラメーターを使用してオブジェクトを変更できます。管理スコープを追加することで、ユーザーが組織内の特定のサーバー、データベース、受信者、およびその他のオブジェクトを管理できると同時に、その他のオブジェクトへの変更が制限されるように、管理役割の割り当てを構成することができます。


> [!IMPORTANT]
> 通常または排他的スコープを作成すると、割り当てる管理役割で定義された書き込みスコープが無効になります。管理役割で構成された読み取りスコープは、無効にすることはできません。



カスタム管理スコープを作成して、管理役割の割り当てを追加または変更することができます。事前に作成された管理スコープまたは組織単位 (OU) 管理スコープで管理役割割り当てを作成する場合は、「[ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)」を参照してください。

Microsoft Exchange Server 2013 での管理役割スコープおよび割り当ての詳細については、以下のトピックを参照してください。

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

スコープに関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理スコープ」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:カスタム スコープを作成する

カスタム スコープを作成するには、次のいずれかのスコープの種類を選択します。

## 受信者フィルター スコープ

受信者フィルター ベースのスコープは、*RecipientRestrictionFilter* パラメーターを **New-ManagementScope** コマンドレットで使用して作成します。フィルター処理する受信者プロパティのほかに、受信者フィルターを作成すると、フィルター クエリーを実行する OU を指定できます。ベース OU を指定すると、役割の書き込みスコープがさらに制限されます。

管理スコープ フィルターの詳細については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

次の構文を使用して、ベース OU を指定したドメイン制限フィルター スコープを作成します。

    New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]

この例では、contoso.com/Sales OU 内のすべてのメールボックスを取り込むスコープを作成します。

    New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"


> [!NOTE]
> フィルターを特定の OU 内だけでなく、管理役割の暗黙的な読み取りスコープ全体に適用する場合は、<EM>RecipientRoot</EM> パラメーターを省略できます。



構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## サーバー フィルターの構成スコープ

サーバー フィルター ベースの構成スコープは、*ServerRestrictionFilter* パラメーターを **New-ManagementScope** コマンドレットで使用して作成します。サーバー フィルターを使用すると、指定するフィルターに一致するサーバーのみに適用されるスコープを作成できます。

管理スコープ フィルターの詳細情報およびフィルター可能なサーバー プロパティの一覧については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

サーバー フィルター スコープを作成するには、次の構文を使用します。

    New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>

この例では、すべてのサーバーを 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' AD (Active Directory) サイト内に含めるスコープを作成します。

    New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## サーバー リストの構成スコープ

サーバー リスト ベースの構成スコープは、*ServerList* パラメーターを **New-ManagementScope** コマンドレットで使用して作成します。サーバー リスト スコープを使用すると、リストで指定するサーバーのみに適用されるスコープを作成できます。

サーバー リスト スコープを作成するには、次の構文を使用します。

    New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>

この例では、MBX1、MBX3、および MBX5 のみに適用されるスコープを作成します。

    New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5

構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## データベース フィルターの構成スコープ

データベース フィルター ベースの構成スコープは、**New-ManagementScope** コマンドレットで *DatabaseRestrictionFilter* パラメーターを使用して作成します。データベース フィルターを使用すると、指定したフィルターと一致するデータベースのみに適用されるスコープを作成できます。


> [!IMPORTANT]
> データベース スコープに関連付けられている役割割り当ては、Microsoft Exchange Server 2010 Service Pack&nbsp;1 (SP1) 以降または Exchange 2013 を実行しているサーバーに接続しているユーザーのみに適用されます。データベース スコープに関連付けられている役割割り当てが割り当てられているユーザーが Exchange 2010 SP1 以前のサーバーに接続している場合、この役割割り当てはユーザーに適用されず、役割割り当てによって提供されるアクセス許可がユーザーに与えられることはありません。



管理スコープ フィルターの詳細情報およびフィルター可能なデータベース プロパティの一覧については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

データベース制限フィルターを作成するには、次の構文を使用します。

    New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>

この例では、データベースの **Name** プロパティに "Executive" という文字列が含まれる全データベースを含むスコープを作成します。

    New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }

構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## データベース リストの構成スコープ

データベース リスト ベースの構成スコープは、**New-ManagementScope** コマンドレットで *DatabaseList* パラメーターを使用して作成します。データベース リスト スコープを使用すると、リストで指定するデータベースのみに適用されるスコープを作成できます。


> [!IMPORTANT]
> データベース スコープに関連付けられている役割割り当ては、Microsoft Exchange Server 2010 Service Pack&nbsp;1 (SP1) 以降または Exchange 2013 を実行しているサーバーに接続しているユーザーのみに適用されます。データベース スコープに関連付けられている役割割り当てが割り当てられているユーザーが Exchange 2010 SP1 以前のサーバーに接続している場合、この役割割り当てはユーザーに適用されず、役割割り当てによって提供されるアクセス許可がユーザーに与えられることはありません。



データベース リスト スコープを作成するには、次の構文を使用します。

    New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>

この例では、"Database 1"、"Database 2"、および "Database 3" のみに適用されるスコープを作成します。

    New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"

構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## 排他的スコープ

**New-ManagementScope** コマンドレットで作成するスコープは、排他的スコープとして指定できます。排他的スコープを作成するには、前述の受信者フィルター ベースのスコープ、サーバー フィルター ベースのスコープ、サーバー リスト ベースのスコープ、データベース フィルター ベースのスコープ、またはデータベース リスト ベースのスコープの作成のセクションのうちのいずれかと同じコマンドを使用した後、コマンドに *Exclusive* スイッチを追加します。


> [!NOTE]
> 排他的な管理スコープを作成した場合、変更対象のオブジェクトを含んだ排他的スコープが割り当てられている役割割り当てに限り、そのオブジェクトにアクセスできます。排他的スコープのある役割を割り当てられた管理者のみが、これらの排他的または保護オブジェクトにアクセスできます。



この例では、Executives 部門のユーザーに一致する排他的な受信者フィルター ベース スコープを作成します。

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive

既定では、排他的スコープを作成すると、排他的スコープを作成したこと、および既存の排他的でない役割割り当てに対する排他的スコープの影響を認識していることの確認を求められます。警告を表示しないようにするには、*Force* スイッチを使用します。この例では、前の例と同じですが、警告のないスコープを作成します。

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force

構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## 手順 2:管理役割割り当てを追加または変更する

スコープを作成したら、そのスコープを新しいまたは既存の管理役割割り当てに追加する必要があります。

管理スコープを作成して、作成する新しい管理役割割り当てに追加する場合は、次のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

管理役割スコープを作成して、既存の役割管理割り当てに追加する場合は、次のトピックを参照してください。

  - [役割の割り当てポリシーの管理](manage-role-assignment-policies-exchange-2013-help.md)

  - [役割の割り当てを変更する](change-a-role-assignment-exchange-2013-help.md)

