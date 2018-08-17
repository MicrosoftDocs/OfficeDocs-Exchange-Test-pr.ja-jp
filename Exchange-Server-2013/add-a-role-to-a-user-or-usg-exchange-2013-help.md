---
title: 'ユーザーまたは USG に役割を追加する: Exchange 2013 Help'
TOCTitle: ユーザーまたは USG に役割を追加する
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 49896416
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーまたは USG に役割を追加する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

管理役割の割り当てによって、管理役割をユーザーまたはユニバーサル セキュリティ グループ (USG) に割り当てることができます。 管理者がユーザーまたは USG に役割を割り当てることにより、それらのユーザーは管理役割で定義されているコマンドレット、スクリプト、およびそれらのパラメーターに基づいてタスクを実行できるようになります。

役割を管理役割グループまたは管理役割の割り当てポリシーに割り当てる場合は、以下のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [役割の割り当てポリシーの管理](manage-role-assignment-policies-exchange-2013-help.md)

役割グループにメンバーを追加する場合や、役割の割り当てポリシーをエンド ユーザーに割り当てる場合は、以下のトピックを参照してください。

  - [役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)

  - [メールボックスの割り当てポリシーを変更する](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割の割り当て」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - ユーザーと USG に役割を直接割り当てることもできますが、管理者とエンド ユーザーにアクセス許可を付与するために推奨される方法は、管理役割グループと管理役割の割り当てポリシーを使用することです。 役割グループと割り当てポリシーを使用する場合は、アクセス許可モデルを簡素化できます。

  - 役割の割り当ては追加可能です。つまり、すべての役割が評価時に一緒に合算されます。 2 つの役割が 1 人のユーザーに対して割り当てられ、このうち 1 つの役割のみにコマンドレッドが含まれている場合でも、コマンドレットはそのユーザーで使用可能です。
    
    既定では、役割の割り当てを行っても、他のユーザーに同じ役割を割り当てるアクセス許可は付与されません。 ユーザーが他のユーザーまたは USG に役割を割り当てられるようにするには、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」を参照してください。

  - スコープで割り当てを作成すると、そのスコープは役割の暗黙的な書き込みスコープを上書きします。 ただし、役割の暗黙的な読み取り範囲は引き続き適用されます。 新しいスコープは、役割の暗黙的な読み取り範囲以外のオブジェクトを返すことはできません。 詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

  - このトピックに記載したすべての手順では、役割を USG に割り当てるために *SecurityGroup* パラメーターを使用しています。 特定のユーザーに役割を割り当てる場合は、*SecurityGroup* パラメーターの代わりに *User* パラメーターを使用します。 各コマンドの他の構文はすべて同じです。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## スコープなしで役割の割り当てを作成する

スコープなしで役割の割り当てを作成することができます。 このようにすると、役割の暗黙的な読み取り、および暗黙的な書き込みスコープが適用されます。

次の構文を使用して、スコープを持たない USG に役割を割り当てます。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>

この例では、"Exchange Servers/Exchange サーバー" という役割を SeattleAdmins という USG に割り当てます。

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## 定義済みの相対スコープを持つ役割割り当てを作成する

定義済みの相対スコープがビジネス要件に適していれば、カスタム スコープを作成せずに、そのスコープを役割の割り当てに適用できます。 定義済みスコープとその説明の一覧については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

次の構文を使用して、定義済みスコープを持つ USG に役割を割り当てます。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

この例では、"Exchange Servers/Exchange サーバー" という役割を SeattleAdmins という USG に割り当て、Organization 定義済みスコープを適用します。

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## 受信者フィルター ベースのスコープを持つ役割の割り当てを作成する

受信者フィルター ベースのスコープを作成し、役割の割り当てと組み合わせて使用する場合は、*CustomRecipientWriteScope* パラメーターを使用して、USG への役割割り当てに使用するコマンドに、そのスコープを含める必要があります。 *CustomRecipientWriteScope* パラメーターを使用する場合、*RecipientOrganizationalUnitScope* パラメーターは使用できません。

役割の割り当てにスコープを追加する前に、スコープを作成しておく必要があります。 詳細については、「[通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)」を参照してください。

次の構文を使用して、受信者フィルター ベースのスコープを持つ USG に役割を割り当てます。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>

この例では、"Seattle Recipient Admins/シアトルの受信者管理者" という USG に "Mail Recipients/メール受信者" の役割を割り当て、"Seattle Recipients/シアトルの受信者" というスコープを適用します。

    New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## サーバー フィルター ベース、データベース フィルター ベース、サーバー リスト ベース、またはデータベース リスト ベースの構成スコープを持つ役割の割り当てを作成する

サーバー フィルター ベース、データベース フィルター ベース、サーバー リスト ベース、またはデータベース リスト ベースの構成スコープを作成し、役割の割り当てと組み合わせて使用する場合は、*CustomConfigWriteScope* パラメーターを使用して、USG への役割割り当てに使用するコマンドに、そのスコープを含める必要があります。

役割の割り当てにスコープを追加する前に、スコープを作成しておく必要があります。詳細については、「[通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)」を参照してください。

次の構文を使用して、構成スコープを持つ USG に役割を割り当てます。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>

この例では、"Exchange Servers/Exchange サーバー" という役割を MailboxAdmins という USG に割り当て、"Mailbox Servers/メールボックス サーバー"というスコープを適用します。

    New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"

前の例では、サーバー構成スコープとともに役割割り当てを追加する方法を示しています。 データベース構成スコープを追加するための構文は同じです。 サーバー スコープではなくデータベース スコープの名前を指定します。

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## OU スコープを持つ役割の割り当てを作成する

組織単位 (OU) に対して役割の書き込みスコープをスコープする場合、*RecipientOrganizationalUnitScope* パラメーターに OU を直接指定できます。 *RecipientOrganizationalUnitScope* パラメーターを使用する場合、*CustomRecipientWriteScope* パラメーターは使用できません。

次の構文を使用して役割を USG に割り当て、役割の書き込みスコープを特定の OU に限定できます。

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>

この例では、"Mail Recipients/メール受信者" という役割を SalesRecipientAdmins という USG に割り当て、その割り当てを contoso.com ドメイン内の "sales/users" という OU にスコープします。

    New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## 排他的な受信者スコープまたは構成スコープを持つ役割の割り当てを作成する

排他的な受信者スコープまたは構成スコープを持つ排他的な役割の割り当てを作成するには、「受信者フィルター ベースのスコープを持つ役割の割り当てを作成する」および「サーバー フィルター ベース、データベース フィルター ベース、サーバー リスト ベース、またはデータベース リスト ベースの構成スコープを持つ役割の割り当てを作成する」で記載したのと同じ手順を使用できます。 排他的スコープを持つ役割の割り当てを作成する場合の唯一の違いは、排他的な受信者スコープと排他的な構成スコープのどちらを使用しているかに応じて、次の排他的なパラメーターを使用する必要があることです。

  - **排他的な受信者の範囲**   *CustomRecipientWriteScope* パラメーターではなく *ExclusiveRecipientWriteScope* パラメーターを使用します。

  - **排他的な構成の範囲**   *CustomConfigWriteScope* パラメーターではなく *ExclusiveConfigWriteScope* パラメーターを使用します。

この手順を実行する場合、役割を割り当てられた被割り当て者は、排他的スコープの中に含まれているオブジェクトに対して操作を実行できます。 排他的スコープの詳細については、「[排他スコープについて](understanding-exclusive-scopes-exchange-2013-help.md)」を参照してください。

排他的スコープと正規のスコープの両方を持つ役割の割り当てを作成することはできません。

この例では、"Protected User Admins/保護されたユーザー管理者" という USG に "Mail Recipients/メール受信者" の役割を割り当て、"Protected Users/保護されたユーザー" という排他的スコープを適用します。

    New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

