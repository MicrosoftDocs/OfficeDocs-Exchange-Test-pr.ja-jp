---
title: '役割の割り当てを変更する: Exchange 2013 Help'
TOCTitle: 役割の割り当てを変更する
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 49895246
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割の割り当てを変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

管理役割割り当ては、管理役割を役割の被割り当て者に割り当てます。役割の割り当てを変更することで、役割が割り当てられた役割担当者が変更できるオブジェクトを制御できます。役割の割り当てに適用される管理役割スコープは、役割の暗黙的な書き込みスコープを上書きします。ただし、役割の暗黙的な読み取りスコープは引き続き適用されます。適用されるスコープは、役割の暗黙的な書き込みスコープ外にあるオブジェクトを返すことはできません。

Microsoft Exchange Server 2013 での管理役割スコープおよび割り当ての詳細については、以下のトピックを参照してください。

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

役割の割り当てに関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割の割り当て」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して役割の割り当てを有効または無効にする

役割の割り当ては、既定で有効になっています。つまり、その役割が割り当てられている役割担当者に、関連する役割が適用されます。役割の割り当てを無効にすると、役割担当者に関連する役割が適用されなくなります。

役割の割り当てを有効にするには、次の構文を使用します。

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $true
```

役割の割り当てを無効にするには、次の構文を使用します。

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $false
```

この例では、"Help Desk Assignment/ヘルプ デスク割り当て" の役割の割り当てを無効にします。

```powershell
Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false
```

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## シェルを使用して、役割の割り当ての管理役割または役割担当者を変更する

役割の割り当てに指定されている管理役割または役割担当者を変更することはできません。役割の割り当てを別の役割または役割担当者に関連付ける場合、新しい役割の割り当てを作成してから、古い役割の割り当てを削除する必要があります。役割の割り当てを追加および削除する方法の詳細については、次のトピックを参照してください。

  - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [ユーザーまたは USG から役割を削除する](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

ユーザーまたはユニバーサル セキュリティ グループ (USG) に対して直接割り当てを作成した場合は、管理役割グループと管理役割の割り当てポリシーの使用を考慮することをお勧めします。役割グループと割り当てポリシーを使用すると、アクセス許可モデルを単純化し、管理する必要がある役割割り当て数を減らすことができます。詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

## シェルを使用して、役割の割り当ての定義済み相対スコープを変更する

役割の割り当ての定義済み相対スコープを変更または追加できます。定義済みスコープを追加または変更すると、役割の割り当てから以前に指定した受信者スコープが削除されます。定義済みスコープとその説明の一覧については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

役割の割り当ての定義済みスコープを変更または追加するには、次の構文を使用します。

    Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

この例では、"John's Assignment/John の割り当て" の役割の割り当て上の定義済みスコープを MyDistributionGroups に変更します。

```powershell
Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups
```

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## シェルを使用して、役割の割り当ての受信者フィルター スコープを変更する

新しい受信者フィルター ベースのスコープを指定するか、既に役割の割り当てに適用されている受信者フィルター ベースのスコープを変更できます。受信者フィルター スコープを追加すると、役割の割り当てから以前に定義した受信者スコープが削除されます。

新しい受信者フィルター ベースのスコープを指定するか、既存のスコープを置き換えるには、次の構文を使用します。

    Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>

この例では、Redmond Recipients に対して受信者フィルター ベースのスコープを追加または変更します。

    Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"

役割の割り当てに適用されている受信者フィルター ベースのスコープと同じスコープを保持するが、受信者オブジェクトとの照合に使用される受信者フィルターを変更する場合、スコープ自身の受信者フィルターを変更する必要があります。スコープを変更する方法の詳細については、「[役割のスコープを変更する](change-a-role-scope-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## シェルを使用して、役割の割り当てのサーバー フィルターまたはリスト ベースの構成スコープを変更する

新しいサーバー フィルターまたはリスト ベースの構成スコープを指定するか、既に役割の割り当てに適用されているスコープを変更できます。構成スコープを追加または変更すると、役割の割り当てから以前に指定した構成スコープが削除されます。

新しい構成スコープを指定するか、既存のスコープを置き換えるには、次の構文を使用します。

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

この例では、Redmond Servers に対して構成スコープを追加または変更します。

    Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"

役割の割り当てに適用されている構成スコープと同じスコープを保持するが、スコープのサーバー フィルターまたはサーバー リストを変更する場合、構成スコープ自身を変更する必要があります。スコープを変更する方法の詳細については、「[役割のスコープを変更する](change-a-role-scope-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## シェルを使用して、役割の割り当てのデータベース フィルターまたはリスト ベースの構成スコープを変更する

新しいデータベース フィルターまたはリスト ベースの構成スコープを指定するか、既に役割の割り当てに適用されているスコープを変更できます。構成スコープを追加または変更すると、役割の割り当てから以前に指定した構成スコープが削除されます。

新しい構成スコープを指定するか、既存のスコープを置き換えるには、次の構文を使用します。

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

この例では、Redmond Databases に対して構成スコープを追加または変更します。

```powershell
Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"
```

役割の割り当てに適用されている構成スコープと同じスコープを保持するが、スコープのデータベース フィルターまたはデータベース リストを変更する場合、構成スコープ自身を変更する必要があります。スコープを変更する方法の詳細については、「[役割のスコープを変更する](change-a-role-scope-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## シェルを使用して、役割の割り当ての組織単位を変更する

新しい OU を追加するか、既に役割の割り当てに適用されている OU を変更することができます。新しい OU を指定すると、役割の割り当てから以前に指定した受信者スコープが削除されます。

役割の割り当ての新しい OU を変更または追加するには、次の構文を使用します。

```powershell
Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>
```

この例では、contoso.com ドメインの Engineering\\Users OU を "Engineering Help Desk/エンジニアリング ヘルプ デスク" 役割の割り当てに追加します。

    Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

## シェルを使用して、排他的受信者スコープまたは排他的構成スコープを変更する

排他的受信者スコープまたは排他的構成スコープを変更するには、前述の「シェルを使用して、役割の割り当ての受信者フィルター スコープを変更する」、「シェルを使用して、役割の割り当てのサーバー フィルターまたはリスト ベースの構成スコープを変更する」、および「シェルを使用して、役割の割り当てのデータベース フィルターまたはリスト ベースの構成スコープを変更する」の手順を使用できます。唯一異なるのは、排他的スコープを変更する場合、排他的受信者スコープまたは排他的構成スコープを変更しているかどうかに応じて、次の排他的パラメーターを指定する必要があることです。

  - **排他的な受信者の範囲** *CustomRecipientWriteScope* パラメーターではなく *ExclusiveRecipientWriteScope* パラメーターを使用します。

  - **排他的なサーバーまたはデータベースの構成スコープ** *CustomConfigWriteScope* パラメーターではなく *ExclusiveConfigWriteScope* パラメーターを使用します。

正規の受信者スコープと構成スコープと同様に、排他的スコープを追加または変更すると、以前に定義した受信者スコープまたは構成スコープが置き換えられます。

この例では、排他的受信者書き込みスコープを変更します。

    Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"

構文およびパラメーターの詳細については、「[Set-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335173\(v=exchg.150\))」を参照してください。

