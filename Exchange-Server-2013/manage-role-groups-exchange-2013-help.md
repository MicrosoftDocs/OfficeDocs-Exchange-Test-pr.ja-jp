---
title: '役割グループの管理: Exchange 2013 Help'
TOCTitle: 役割グループの管理
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 49896411
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割グループの管理

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-08_

このトピックでは、Microsoft Exchange Server 2013 で管理役割グループを追加、削除、コピー、および表示する方法を示します。また、役割グループに管理役割を追加、削除および一覧表示したり、役割グループの管理スコープや代理人を変更する方法も示します。Exchange 2013 の役割グループの詳細については、「[管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)」を参照してください。

役割グループに関連する追加の管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間: 5 から 10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割グループ」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 役割グループを作成します。

ユーザーのグループに割り当て可能なアクセス許可をカスタマイズする場合は、新しいカスタム管理役割グループを作成します。

## EAC を使用して役割グループを作成する

1.  Exchange 管理センター (EAC) で、<strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>役割グループの新規作成</strong> ウィンドウで、新しい役割グループの名前を指定します。

3.  その役割グループに割り当てたい役割や追加したいメンバーの選択は、すぐに行うことも、後で行うこともできます。

4.  新しい役割グループに適用したい書き込みスコープを選択します。

5.  <strong>保存</strong> をクリックして役割グループを作成します。

## シェルを使用して役割グループを作成する

例

## 正常な動作を確認する方法

役割グループが正常に作成されたことを確認するには、次の手順を実行します。

1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  役割グループ一覧に新しい役割グループが表示されることを確認し、選択します。

3.  新しい役割グループで指定したメンバー、割り当てられた役割、およびスコープが、役割グループの詳細ウィンドウに一覧表示されることを確認します。

## 役割グループをコピーする

## EAC を使用して役割グループをコピーする

アクセス許可を含む役割グループがあり、このアクセス許可をユーザーに付与したいと考えているが、その一方でこのアクセス許可に別の管理スコープを適用したい、あるいはこのアクセス許可に他のすべての役割を手動で追加せずに 1 つまたは 2 つの管理役割を削除または追加したいと考えている場合、既存の役割グループをコピーします。


> [!IMPORTANT]
> Exchange 管理シェルを使用して、役割グループに複数の管理役割スコープまたは排他的スコープを構成した場合は、役割グループをコピーする際に EAC を使用することはできません。役割グループに複数のスコープまたは排他的スコープを構成した場合は、役割グループをコピーするために後述するシェルの手順を使用する必要があります。管理役割スコープの詳細については、「<A href="understanding-management-role-scopes-exchange-2013-help.md">管理役割スコープについて</A>」を参照してください。



1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  コピーする役割グループを選択し、<strong>コピー</strong>![\[コピー\] アイコン](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "[コピー] アイコン") をクリックします。

3.  <strong>役割グループの新規作成</strong> ウィンドウで、新しい役割グループの名前を指定します。

4.  新しい役割グループにコピーされている役割を確認します。必要に応じて役割を追加または削除します。

5.  書き込みスコープを確認し、必要に応じて変更します。

6.  新しい役割グループにコピーされたメンバーを確認します。必要に応じてメンバーを追加または削除します。

7.  <strong>保存</strong> をクリックして役割グループを作成します。

## シェルを使用してスコープを持たない役割グループをコピーする

1.  以下の構文を使用して、変数にコピーする役割グループを格納します。
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  以下の構文を使用して、新しい役割グループを作成し、役割グループにメンバーを追加し、新しい役割グループを他のユーザーに委任できる人を指定します。
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>
    ```

たとえば、次のコマンドは、"Organization Management/組織管理" 役割グループをコピーし、新しい役割グループに "Limited Organization Management" という名前を付けます。メンバーに Isabelle、Carter、Lukas を追加します。Jenny と Katie によって委任できるようになります。

```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie
```

新しい役割グループを作成すると、役割の追加または削除や、役割に対する役割割り当てのスコープの変更などが可能になります。

構文およびパラメーターの詳細については、「[Get-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638115\(v=exchg.150\))」と「[New-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638181\(v=exchg.150\))」を参照してください。

## シェルを使用してカスタム スコープを持つ役割グループをコピーする

1.  以下の構文を使用して、変数にコピーする役割グループを格納します。
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  以下の構文を使用して、カスタムのスコープを持つ新しい役割グループを作成します。
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>
    ```

たとえば、次のコマンドは、"Organization Management/組織管理" 役割グループをコピーして、"Vancouver Users" 受信者の範囲と "Vancouver Servers" 構成の範囲を持つ "Vancouver Organization Management" という名前の新しい役割グループを作成します。

    
```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"
```

このトピックの「シェルを使用してスコープを持たない役割グループをコピーする」で説明した *Members* パラメーターを使用して、役割グループを作成するときにメンバーを役割グループに追加することもできます。管理のスコープの詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

新しい役割グループを作成すると、役割の追加または削除、役割に対する役割割り当てのスコープの変更、およびその他のタスクの実行が可能になります。

構文およびパラメーターの詳細については、「[Get-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638115\(v=exchg.150\))」と「[New-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638181\(v=exchg.150\))」を参照してください。

## シェルを使用して OU スコープを持つ役割グループをコピーする

1.  以下の構文を使用して、変数にコピーする役割グループを格納します。
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  以下の構文を使用して、カスタムのスコープを持つ新しい役割グループを作成します。
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>
    ```

たとえば、次のコマンドは、"Recipient Management/受信者管理" 役割グループをコピーして、Toronto Users OU のユーザーのみに管理を許可する "Toronto Recipient Management" という名前の新しい役割グループを作成します。

```powershell
$RoleGroup = Get-RoleGroup "Recipient Management"
New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"
```

このトピックの「シェルを使用してスコープを持たない役割グループをコピーする」で説明した *Members* パラメーターを使用して、役割グループを作成するときにメンバーを役割グループに追加することもできます。管理のスコープの詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

新しい役割グループを作成すると、役割の追加または削除や、役割に対する役割割り当てのスコープの変更などが可能になります。

構文およびパラメーターの詳細については、「[Get-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638115\(v=exchg.150\))」と「[New-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638181\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

役割グループが正常にコピーされたことを確認するには、次の手順を実行します。

1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  役割グループ一覧にコピーされた役割グループが表示されることを確認し、選択します。

3.  コピーされた役割グループで指定したメンバー、割り当てられた役割、およびスコープが、役割グループの詳細ウィンドウに一覧表示されることを確認します。

## 役割グループを削除する

作成した役割グループが不要になったら、削除できます。役割グループを削除すると、役割グループと管理役割間の管理役割の割り当ても削除されます。ただし、管理役割は削除されません。ユーザーが機能へのアクセスで役割グループに依存していた場合、ユーザーはその機能にアクセスできなくなります。組み込みの役割グループを削除することはできません。

## EAC を使用して役割グループを削除する

1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  削除する役割グループを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  選択した役割グループが削除するものであることを確認し、間違いがなければ警告に<strong>\[はい\]</strong> で答えます。

## シェルを使用して役割グループを削除する

例

## 役割グループを表示

役割グループの一覧または組織内に存在する特定の役割グループに関する詳細を表示することができます。

## EAC を使用して役割グループの役割一覧および役割グループの詳細を表示する

1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。組織の役割グループのすべてが一覧表示されます。

2.  役割グループを選択すると、その役割グループに構成されているメンバー、割り当てられた役割、およびスコープが表示されます。

## シェルを使用して役割グループの役割一覧および役割グループの詳細を表示する

例

## 役割グループに役割を追加する

役割グループに管理役割を追加することは、管理者または専門家ユーザーのグループにアクセス許可を与える、最適で最も簡単な方法です。役割グループのメンバーのユーザーに機能管理の機能を与えるには、機能を管理する管理役割を、役割グループに追加します。役割が追加されると、役割グループのメンバーには役割で指定されたアクセス許可が与えられます。

## EAC を使用して役割グループに管理役割を追加する


> [!IMPORTANT]
> シェルを使用して、役割グループに複数の管理役割スコープまたは排他的スコープを構成した場合は、役割グループに役割を追加する際に EAC を使用することはできません。複数のスコープまたは排他的スコープを役割グループに構成した場合は、後で説明するシェルの手順を使用して役割を役割グループに追加する必要があります。管理役割スコープの詳細については、「<A href="understanding-management-role-scopes-exchange-2013-help.md">管理役割スコープについて</A>」を参照してください。



1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  役割を追加する役割グループを選択して、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>役割</strong> セクションで役割グループに追加する役割を選択します。

4.  役割を役割グループに追加し終えたら <strong>保存</strong> をクリックします。

## シェルを使用してスコープを持たない役割割り当てを作成する

役割と役割グループの間で、スコープを持たない役割割り当てを作成できます。このようにすると、役割の暗黙的な読み取り、および暗黙的な書き込みスコープが適用されます。

次の構文を使用して、役割グループにスコープを持たない役割を割り当てます。指定しない場合、役割割り当ての名前は自動的に作成されます。

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>
```

この例では、"Seattle Compliance/Seattle 規制順守" という役割グループに対し、トランスポート ルールの管理役割を割り当てています。

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"
```

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## シェルを使用して定義済みスコープを持つ役割割り当てを作成する

定義済みスコープがビジネス要件に適合していれば、新しいスコープを作成せずに、そのスコープを役割割り当てに適用できます。定義済みスコープとその説明の一覧については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

役割割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

次の構文を使用して、定義済みスコープを持つ役割グループに役割を割り当てます。指定しない場合、役割割り当ての名前は自動的に作成されます。

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >

この例では、"Enterprise Support/エンタープライズ サポート" という役割グループにメッセージ追跡の役割を割り当て、これを "Organization/組織" という定義済みスコープに適用しています。

```powershell
New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization
``` 

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## シェルを使用して、受信者フィルター ベースのスコープを持つ役割割り当てを作成する

受信者フィルター ベースのスコープを作成済みの場合は、*CustomRecipientWriteScope* パラメーターを使用して、役割グループへの役割割り当てに使用するコマンドに、そのスコープを含める必要があります。

受信者書き込みスコープを持つ役割割り当てを作成する際に、構成書き込みスコープを含めることもできます。

役割の割り当てとスコープの詳細については、次のトピックを参照してください。

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

次の構文を使用して、受信者フィルター ベースのスコープを持つ役割グループに役割を割り当てます。指定しない場合、役割割り当ての名前は自動的に作成されます。

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>
```

この例では、"Seattle Recipient Admins/Seattle の受信者管理者" という役割グループにメッセージ追跡の役割を割り当て、これを "Seattle Recipients/Seattle の受信者" というスコープに適用しています。

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"
```

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## シェルを使用して構成スコープを持つ役割割り当てを作成する

サーバー フィルター ベース、データベース フィルター ベース、サーバー リスト ベース、またはデータベース リスト ベースの構成スコープを作成済みの場合は、*CustomConfigWriteScope* パラメーターを使用して、役割グループへの役割の割り当てに使用するコマンドに、そのスコープを含める必要があります。

構成書き込みスコープを持つ役割割り当てを作成する際に、受信者書き込みスコープを含めることもできます。

役割の割り当てと管理スコープの詳細については、次のトピックを参照してください。

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

次の構文を使用して、構成スコープを持つ役割グループに役割を割り当てます。指定しない場合、役割割り当ての名前は自動的に作成されます。

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>
```

この例では、"Seattle Server Admins/Seattle のサーバー管理者" という役割グループにデータベースの役割を割り当て、これを "Seattle Servers/Seattle のサーバー" というスコープに適用しています。

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"
```

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## シェルを使用して、OU スコープを持つ役割割り当てを作成する

OU に対して役割の書き込みスコープをスコープする場合、*RecipientOrganizationalUnitScope* パラメーターに OU を直接指定できます。

役割の割り当てと管理スコープの詳細については、次のトピックを参照してください。

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

次のコマンドを使用して役割を役割グループに割り当て、役割の書き込みスコープを特定の OU に限定できます。指定しない場合、役割割り当ての名前は自動的に作成されます。

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>
```

この例では、メール受信者の役割を "Seattle Recipient Admins/Seattle の受信者管理者" という役割グループに割り当て、割り当てのスコープを "Contoso.com" ドメインの "Sales\\Users" という OU に指定しています。

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users
```

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

役割グループに役割が正常に追加されたことを確認するには、次の手順を実行します。

1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  役割を追加した役割グループを選択します。役割グループの詳細ウィンドウで、追加した役割が一覧表示されていることを確認します。

## 役割グループから役割を削除する

管理者または専門家ユーザーのグループに付与されているアクセス許可を取り消すには、管理役割グループから役割を削除するのが最適で最も簡単です。ある機能を管理するアクセス許可を管理者または専門家ユーザーに与えたくない場合、そのアクセス許可を管理する管理役割グループから管理役割を削除します。役割を削除すると、この役割グループのメンバーがこの機能を管理するアクセス許可はなくなります。


> [!NOTE]
> 組織の管理 役割グループなど、一部の役割グループでは、役割グループから削除できる役割に関する制限があります。詳細については、「<A href="understanding-management-role-groups-exchange-2013-help.md">管理役割グループについて</A>」を参照してください。<BR>管理者が、ある機能のアクセス許可を管理者に付与する管理役割を含む別の役割グループのメンバーである場合は、その管理者をその役割グループから削除するか、その機能を管理するアクセス権を付与する役割を別の役割グループから削除する必要があります。



## EAC を使用して役割グループから管理役割を削除する


> [!IMPORTANT]
> シェルを使用して、役割グループに複数のスコープまたは排他的スコープを構成した場合は、役割グループから役割を削除する際に EAC を使用することはできません。役割グループに複数のスコープまたは排他的なスコープを構成している場合は、この後で説明するシェルを使用する手順に従って、役割グループから役割を削除する必要があります。管理役割スコープの詳細については、「<A href="understanding-management-role-scopes-exchange-2013-help.md">管理役割スコープについて</A>」を参照してください。



1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  役割を削除する役割グループを選択して、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>役割</strong> セクションで役割グループから削除する役割を選択します。

4.  役割グループから役割を削除し終えたら <strong>保存</strong> をクリックします。

## シェルを使用して役割グループから役割を削除する

**Get-ManagementRoleAssignment** コマンドレットを使用して関連する管理役割の割り当てを取得し、これによって返された役割の割り当てをパイプ処理をして **Remove-ManagementRoleAssignment** コマンドレットに渡すことで、役割グループから役割を削除できます。委任と正規の役割割り当てを両方同時に削除する場合以外は、*Delegating* パラメーターを指定し、正規の役割割り当てを削除するか、委任の役割割り当てを削除するかを指定します。

正規と委任の役割割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

この手順では、パイプライン処理を使用します。パイプライン処理の詳細については、「[パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))」を参照してください。

役割グループから役割を削除するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment
```

この例では、"Seattle Recipient Administrators/Seattle の受信者管理者" 役割グループから、管理者が配布グループを管理できる "Distribution Groups/配布グループ" 役割を削除します。配布グループを管理するためのアクセス許可を付与する役割割り当てを削除するので、正規の役割割り当てのみが返されるよう、*Delegating* パラメーターを `$False` に設定します。

```powershell 
Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment
```


構文およびパラメーターの詳細については、「[Remove-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351205\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

役割グループから役割が正常に削除されたことを確認するには、次の手順を実行します。

1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  役割を削除した役割グループを選択します。役割グループの詳細ウィンドウで、削除した役割が一覧表示されなくなったことを確認します。

## 役割グループのスコープを変更する

役割グループと役割間の管理役割割り当てには、管理範囲が含まれています。この管理範囲に基づいて、該当の役割グループのメンバーに利用可能にするオブジェクトが特定されます。役割グループの書き込みスコープを変更することで、作成、変更、または削除するのに役割グループのメンバーが使用できるオブジェクトを変更できます。役割グループの読み取りスコープを変更することはできません。

Exchange 2013 には、カスタムのスコープが作成されていない場合に、役割の割り当てに既定で適用されるスコープが含まれています。役割グループ上で役割が割り当てられているカスタムのスコープを使用する場合は、それを最初に作成する必要があります。高度なタスクである、カスタムのスコープの作成については、「[通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)」を参照してください。

Exchange 2013 での管理役割スコープおよび割り当ての詳細については、以下のトピックを参照してください。

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

## EAC を使用して、役割グループのスコープを変更する

EAC を使用して役割グループのスコープを変更する場合、実際には、役割グループと役割グループに割り当てられたそれぞれの管理役割の間のすべての役割割り当てのスコープを変更しています。特定の役割割り当てのスコープを変更する場合、このトピックで後述されているシェルの手順を使用する必要があります。


> [!IMPORTANT]
> シェルを使用して複数のスコープまたは排他的スコープをそれらの役割割り当てに構成した場合は、役割と役割グループの間の役割割り当てのスコープを管理する際に EAC を使用することはできません。それらの役割割り当てに複数のスコープまたは排他的スコープを構成した場合は、このトピックに記載されている、シェルの手順を使用してスコープを管理する必要があります。管理役割スコープの詳細については、「<A href="understanding-management-role-scopes-exchange-2013-help.md">管理役割スコープについて</A>」を参照してください。



1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。

2.  スコープを変更する役割グループを選択して、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  次の 2 つの <strong>書き込みスコープ</strong> オプションのいずれかを選択します。
    
      - ドロップダウン ボックスの書き込みスコープでは、既定の書き込みスコープまたはカスタムの書き込みスコープを選択できます。
    
      - **組織単位**   この役割グループのスコープを OU に制限する場合は、このオプションを選択し、組織単位 (OU) を入力します。

4.  <strong>保存</strong> をクリックして、役割グループに加えた変更を保存します。

## シェルを使用して、ある役割グループに属するすべての役割の割り当て範囲を一括して変更する

役割グループとそれに割り当てられた役割の間の役割の割り当ては、役割自身から取得した暗黙的なスコープ、同じカスタムのスコープ、または異なるカスタムのスコープを使用できます。役割割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

役割の割り当てのスコープは、**Set-ManagementRoleAssignment** コマンドレットを使用して管理されます。**Set-RoleGroup** コマンドレットは、範囲を管理する用途には対応していません。

ある役割グループと管理役割間のすべての役割の割り当て範囲を一括して変更するには、まずその役割グループの役割の割り当てを取得してから、各割り当てに新しい範囲を設定する必要があります。この操作を実行するには、**Get-ManagementRoleAssignment** コマンドレットを使用して取得した役割の割り当てを、**Set-ManagementRoleAssignment** コマンドレットにパイプ処理します。

この手順では、パイプライン処理の概念と *WhatIf* スイッチを使用します。詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [WhatIf、Confirm、および ValidateOnly スイッチ](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

シェルを使用して、ある役割グループに属するすべての役割の割り当て範囲を一括して変更するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
```

使用するスコープの構成に必要なパラメーターのみを使用します。たとえば、"Sales Recipient Management/営業受信者の管理" 役割グループに属するすべての役割の割り当ての受信者の範囲を "Direct Sales Employees/直販従業員" に変更する場合は、次のコマンドを使用します。

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"
```


> [!NOTE]
> 変更対象の役割の割り当てだけが変更されたかどうかを確認するには、<EM>WhatIf</EM> スイッチを使用します。<EM>WhatIf</EM> スイッチ付きで上記のコマンドを実行して結果を確認したら、<EM>WhatIf</EM> スイッチを削除して、変更内容を適用します。



管理役割の割り当ての変更の詳細については、「[役割の割り当てを変更する](change-a-role-assignment-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## シェルを使用して、ある役割グループに属する役割の割り当て範囲を個別に変更する

役割グループとそれに割り当てられた役割の間の役割の割り当ては、役割自身から取得した暗黙的なスコープ、同じカスタムのスコープ、または異なるカスタムのスコープを使用できます。役割割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

役割の割り当てのスコープは、**Set-ManagementRoleAssignment** コマンドレットを使用して管理されます。**Set-RoleGroup** コマンドレットは、範囲を管理する用途には対応していません。

この手順では、パイプライン処理の概念と **Format-List** コマンドレットを利用します。詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

ある役割グループと管理役割間の役割の割り当て範囲を変更するには、まずその役割グループの役割の割り当ての名前を取得してから、役割の割り当てに範囲を設定します。

1.  ある役割グループに属するすべての役割の割り当ての名前を検索するには、次のコマンドを使用します。管理役割の割り当てを **Format-List** コマンドレットにパイプ処理すると、その割り当てのフル ネームを表示することができます。
    
    ```powershell
    Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name
    ```

2.  変更する役割の割り当ての名前を検索します。役割割り当ての名前は、次の手順で使用します。

3.  割り当て範囲を個別に設定するには、次の構文を使用します。
    
    ```powershell
    Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
    ```

使用するスコープの構成に必要なパラメーターのみを使用します。たとえば、"Mail Recipients\_Sales Recipient Management/メール受信者\_営業受信者管理" 役割の割り当ての受信者の範囲を "All Sales Employees/すべての営業従業員" に変更する場合は、次のコマンドを使用します。

```powershell
Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"
```

管理役割の割り当ての変更の詳細については、「[役割の割り当てを変更する](change-a-role-assignment-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

役割グループの役割割り当てのスコープが正常に変更されたことを確認するには、次の手順を実行します。

  - EAC を使用して役割グループのスコープを構成した場合、次の手順を実行します。
    
    1.  EAC で <strong>アクセス許可</strong> \> <strong>管理者の役割</strong> に移動します。組織のすべての役割グループが一覧表示されます。
    
    2.  役割グループを選択し、役割グループに構成されているスコープを表示します。

  - シェルを使用して役割グループのスコープを構成した場合、次の手順を実行します。
    
    1.  シェルで、次のコマンドを実行します。
        
        ```powershell
        Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
        ```
    
    2.  役割割り当ての書き込みスコープが、指定のスコープに変更されたことを確認します。

## 役割グループの委任を追加または削除する

役割グループの代理人は、役割グループのメンバーの追加または削除、あるいは役割グループのプロパティの変更を許可された、ユーザーまたはユニバーサル セキュリティ グループ (USG) です。役割グループの代理人の追加または削除によって、役割グループの管理を誰に許可するかを制御できます。


> [!IMPORTANT]
> グループにいったん代理人を追加した後、役割グループの管理を許可されるのは、その役割グループの代理人のみ、または "Role Management/役割管理" 役割に直接的または間接的に割り当てられているユーザーのみです。<BR>直接的または間接的に "Role Management/役割管理" 役割が割り当てられていても、役割グループの代理人として追加されていないユーザーは、<STRONG>Add-RoleGroupMember</STRONG>、<STRONG>Remove-RoleGroupMember</STRONG>、<STRONG>Update-RoleGroupMember</STRONG>、および <STRONG>Set-RoleGroup</STRONG> の各コマンドレットに対して <EM>BypassSecurityGroupManagerCheck</EM> スイッチを使用しない限り、役割グループを管理できません。




> [!NOTE]
> EAC を使用して役割グループに代理人を追加することはできません。



## シェルを使用して役割グループに代理人を追加する

役割グループの委任の一覧を変更するには、**Set-RoleGroup** コマンドレットの *ManagedBy* パラメーターを使用します。*ManagedBy* パラメーターは、役割グループの委任一覧全体を上書きします。委任一覧全体を上書きするよりも、役割グループに代理人を追加する方が望ましい場合は、以下の手順を実行してください。

1.  以下のコマンドを使用して、変数に役割グループを格納します。
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  次のコマンドを使用して、変数に格納されている役割グループに代理人を追加します。

    ```powershell
    $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    ```
    

    > [!NOTE]
    > USG を追加する場合は、<STRONG>Get-Group</STRONG> コマンドレットを使用します。



3.  追加する各代理人に対して、手順 2 を繰り返します。

4.  以下のコマンドを使用して、実際の役割グループに対し委任の新しい一覧を適用します。
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

この例では、ユーザー David Strome を 組織の管理 役割グループの代理人として追加します。

```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
$RoleGroup.ManagedBy += (Get-User "David Strome").Identity
Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
```

構文およびパラメーターの詳細については、「[Set-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638182\(v=exchg.150\))」を参照してください。

## シェルを使用して役割グループから代理人を削除する

役割グループの委任の一覧を変更するには、**Set-RoleGroup** コマンドレットの *ManagedBy* パラメーターを使用します。*ManagedBy* パラメーターは、役割グループの委任一覧全体を上書きします。委任一覧全体を上書きするよりも、役割グループから代理人を削除する方が望ましい場合は、以下の手順を実行してください。

1.  以下のコマンドを使用して、変数に役割グループを格納します。
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  次のコマンドを使用して、変数に格納されている役割グループから代理人を削除します。
    
    ```powershell
    $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    ```


    > [!NOTE]
    > USG を削除する場合は、<STRONG>Get-Group</STRONG> コマンドレットを使用します。



3.  削除する各代理人に対して、手順 2 を繰り返します。

4.  以下のコマンドを使用して、実際の役割グループに対し委任の新しい一覧を適用します。
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

この例では、ユーザー David Strome を 組織の管理 役割グループの代理人として削除します。

```powershell
$RoleGroup = Get-RoleGroup "Organization Management"
$RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
```

構文およびパラメーターの詳細については、「[Set-RoleGroup](https://technet.microsoft.com/ja-jp/library/dd638182\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

役割グループの委任一覧が正常に変更されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
    ```powershell
    Get-RoleGroup <role group name> | Format-List ManagedBy
    ```

2.  *ManagedBy* プロパティに一覧表示された代理人には、役割グループの管理を行うべき代理人だけが含まれることを確認します。

