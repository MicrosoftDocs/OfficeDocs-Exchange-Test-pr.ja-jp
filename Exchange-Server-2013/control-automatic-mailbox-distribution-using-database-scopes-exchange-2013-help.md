---
title: 'データベース スコープを使用したメールボックスの自動配布の制御: Exchange 2013 Help'
TOCTitle: データベース スコープを使用したメールボックスの自動配布の制御
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 49896359
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データベース スコープを使用したメールボックスの自動配布の制御

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

メールボックスの自動配布は、データベースを明示的に指定しない場合に、新しいまたは移動したメールボックスを格納するメールボックス データベースをランダムで選択する Microsoft Exchange Server 2013 の機能です。この機能により、経験の浅い管理者またはヘルプ デスクのスタッフがメールボックスを作成する場合でも、どのメールボックス データベースにメールボックスを作成する必要があるかを知る必要がないので、彼らがメールボックスを作成するのを許可する場合に役立ちます。

データベース管理スコープを使用して、メールボックスの自動配布で選択されるメールボックス データベースを制御できます。データベース スコープを管理者に適用すると、定義したデータベース スコープに一致するデータベースだけを管理者が利用できます。メールボックスの自動配布は、現在のユーザーのコンテキストを使用するため、管理者に適用されたデータベース スコープにも制約されます。

メールボックスの自動配布、データベース スコープ、および役割の割り当ての詳細については、次のトピックを参照してください。

  - [メールボックスの自動配布](automatic-mailbox-distribution-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

スコープに関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - この手順の予想所要時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理スコープ」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:データベース スコープを作成する

この手順では、データベース スコープに含めるデータベースを決定します。また、データベースの静的な一覧を指定するか、または指定する条件に一致するデータベースのみを含むデータベース フィルターを作成するかどうかを決定します。


> [!IMPORTANT]
> データベース スコープに関連付けられている役割割り当ては、Microsoft Exchange Server 2010 Service Pack&nbsp;1 (SP1) 以降または Exchange 2013 を実行しているサーバーに接続しているユーザーのみに適用されます。データベース スコープに関連付けられている役割割り当てが割り当てられているユーザーが Exchange 2010 SP1 以前のサーバーに接続している場合、この役割割り当てはユーザーに適用されず、役割割り当てによって提供されるアクセス許可がユーザーに与えられることはありません。



## データベース リスト スコープを使用する

このスコープに含める必要があるメールボックス データベースの静的な一覧を定義する場合は、データベース リストを使用します。データベース リスト スコープを作成するには、次の構文を使用します。

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

この例では、"Database 1"、"Database 2"、および "Database 3" のみに適用されるスコープを作成します。

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## データベース フィルター スコープを使用する

指定する条件に一致するデータベースのみを含む動的なデータベース スコープを作成する場合は、データベース フィルターを使用します。これは、データベース スコープの作成後にそれを管理したくない場合で、メールボックス データベースの特定のセットを識別可能な、組織用の標準値が定義済みの場合に役立ちます。

フィルター処理可能なデータベース プロパティの一覧については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

データベース フィルター スコープを作成するには、次の構文を使用します。

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

この例では、データベースの **Name** プロパティに "ACCT" という文字列が含まれる全データベースを含むスコープを作成します。

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

構文およびパラメーターの詳細については、「[New-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd335137\(v=exchg.150\))」を参照してください。

## 手順 2:データベース スコープを管理役割の割り当てに追加する

スコープを作成したら、そのスコープを新しいまたは既存の管理役割割り当てに追加する必要があります。管理役割グループを使用して管理アクセス許可を制御することをお勧めします。したがって、この手順の例では "Accounting Administrators" という名前の役割グループを例として使用しています。役割グループを作成する方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

役割を、データベース スコープを持つ役割グループに割り当てた後は、役割グループのメンバーは、そのスコープに含まれるデータベースに対するメールボックスの作成およびメールボックスの移動のみを行うことができます。

役割グループに割り当てることができる組み込みの役割の一覧については、「[組み込みの管理役割](built-in-management-roles-exchange-2013-help.md)」を参照してください。

## 新しい役割の割り当ての追加

役割グループを作成したばかりで、それに役割を追加する必要がある場合には、この手順を使用します。

以下の構文を使用して、新しいデータベース スコープと共に、割り当てる管理役割と新しい役割グループの間に役割の割り当てを作成します。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

この例では、Accounting Databases データベース スコープを使用して、"Mail Recipient/メール受信者" と "Mail Recipient Creation Role/メール受信者の作成" 役割と "Accounting Administrators" 役割グループの間に役割の割り当てを作成します。

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## 既存の役割の割り当ての変更

新しいデータベース スコープの適用先の役割との間に、既に役割が割り当てられている既存の役割グループが存在する場合には、この手順を使用します。

この手順では、パイプライン処理を使用します。詳細については、「[パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))」を参照してください。

以下の構文を使用して、データベース スコープの割り当て先の管理役割と既存の役割グループの間の役割の割り当てを変更します。

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

この例では、"Accounting Administrators" 役割グループに割り当てられた、"Mail Recipient/メール受信者" および "Mail Recipient Creation Role/メール受信者の作成" 役割に Accounting Databases データベース スコープを追加します。

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」または「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## 手順 3:役割グループにメンバーを追加する (該当する場合)

役割グループにメンバーを追加する場合は、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> この役割グループにメンバーを追加して、ユーザーを作成可能な、またはメールボックスの移動先とするデータベースを制限する場合は、そのメンバーが追加のアクセス許可を付与可能な他の役割グループのメンバーでないことを確認します。



## 手順 4:役割グループからメンバーを削除する (該当する場合)

メールボックスを作成可能な、またはメールボックスの移動先とできるデータベースを制限する新しい役割グループにメンバーを追加した場合で、彼らが追加のアクセス許可を持つ別の役割グループのメンバーの場合は、彼らを古い役割グループから削除します。詳細については、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。

