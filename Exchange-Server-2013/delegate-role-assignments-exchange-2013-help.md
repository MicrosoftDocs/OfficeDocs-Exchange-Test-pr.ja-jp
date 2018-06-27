---
title: '役割割り当てを委任する: Exchange 2013 Help'
TOCTitle: 役割割り当てを委任する
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 49896540
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割割り当てを委任する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-02_

管理役割の委任によって、役割の被割り当て者が、指定された管理役割を他の管理役割グループ、管理役割割り当てポリシー、ユーザー、またはユニバーサル セキュリティ グループ (USG) に割り当てることができます。 既定では、組織管理の管理役割グループのメンバーだけが、役割割り当てを委任することができます。新しい Microsoft Exchange Server 2013 が展開されると、Exchange 2013 をインストールしたユーザー アカウントだけが組織管理の役割グループのメンバーになれます。

委任役割割り当てを役割グループに割り当てると、役割グループのメンバーはすべて、関連する管理役割を他の役割の被割り当て者に委任できます。


> [!IMPORTANT]
> 役割割り当ての委任によって、役割の被割り当て者に対し、役割によって付与されるアクセス許可が与えられることはなく、役割を他に割り当てる機能だけが与えられます。 役割によって付与されるアクセス許可を役割の被割り当て者に与えたい場合は、正規の役割割り当てを作成する必要があります。 正規の役割割り当てを作成するには、次のトピックを参照してください。<BR><A href="manage-role-groups-exchange-2013-help.md">役割グループの管理</A><BR><A href="manage-role-assignment-policies-exchange-2013-help.md">役割の割り当てポリシーの管理</A><BR><A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">ユーザーまたは USG に役割を追加する</A>




> [!NOTE]
> このトピックでは、管理役割割り当ての委任について説明します。推奨の委任方法である、役割グループのメンバーの追加、削除の委任については、「<A href="manage-role-groups-exchange-2013-help.md">役割グループの管理</A>」を参照してください。



正規の役割割り当ておよび管理委任割り当ての委任の詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

アクセス許可の管理に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - この手順の予想所要時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割の割り当て」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して管理の役割を委任する

同じ定義済みスコープ、受信者フィルターまたはサーバー フィルター べースのスコープ、サーバー一覧ベースのスコープ、正規スコープまたは排他的スコープの作成に使用可能な組織単位 (OU) のスコープを使用して、委任役割割り当てを作成できます。 正規の役割割り当ての作成と、役割割り当ての委任の違いは、コマンドへの*Delegating* スイッチの追加だけです。 役割割り当ての作成方法の詳細については、次のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)


> [!NOTE]
> 管理役割割り当てポリシーに委任役割割り当てを作成することはできません。



この例では、委任役割割り当てを作成して、上級管理の役割グループのメンバーが、"Mail Recipients/メール受信者" の役割を Exchange 組織内の役割の被割り当て者すべてに対して割り当てられるようにしています。

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating

この例では、委任役割割り当てを作成して、"legal hold management/上級管理" 役割グループのメンバーが、メール受信者の役割を "contoso.com"ドメイン内の "Sales/Users" という OU 内のユーザーに対してのみ割り当てられるようにしています。

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

