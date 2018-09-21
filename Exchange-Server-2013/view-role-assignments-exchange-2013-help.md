---
title: '役割の割り当ての表示: Exchange 2013 Help'
TOCTitle: 役割の割り当ての表示
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 49895234
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割の割り当ての表示

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

管理役割割り当ては、管理役割を役割担当者に割り当てます。Microsoft Exchange Server 2013 での管理役割の割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

役割に関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割の割り当て」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックでは、パイプライン処理および **Format-List** コマンドレットを利用します。これらの概念の詳細については、以下のトピックを参照してください。
    
      - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))
    
      - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## すべての役割の割り当ての一覧を表示する

**Get-ManagementRoleAssignment** コマンドレットを実行すると、組織内に構成されているすべての役割の割り当ての一覧を表示できます。指定した文字列と部分的に一致する役割割り当ての一覧を取得するには、ワイルドカード文字 (\*) を使用してください。この例では、「Tier 1」という文字列で始まるすべての役割割り当ての一覧が取得されます。

    Get-ManagementRoleAssignment "Tier 1*"

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 特定の役割の割り当ての詳細を表示する

**Get-ManagementRoleAssignment** コマンドレットの結果を **Format-List** コマンドレットにパイプ処理することで、役割割り当ての詳細を表示できます。以下の構文を使用します。

```powershell
Get-ManagementRoleAssignment <assignment name> | Format-List
```

この例では、"Help Desk Assignment/ヘルプ デスク割り当て" という役割の割り当ての詳細を取得します。

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List
```

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 特定の役割担当者に割り当てられている役割の割り当ての一覧を表示する

管理役割グループ、役割、役割の割り当てポリシーに関連付けられているか、ユーザーやユニバーサル セキュリティ グループ (USG) に関連付けられている役割の割り当ての一覧を表示するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -RoleAssignee <role assignee name>
```

この例では、"Server Management/サーバーの管理" 役割グループに関連付けられている役割の割り当てをすべて取得します。

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Server Management"
```

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 特定の役割に関連付けられている役割の割り当てを表示する

各役割には、複数の役割割り当てを設定できます。**Get-ManagementRoleAssigment** コマンドレットを使用すると、指定された役割に関連付けられている役割割り当ての一覧を表示できます。

指定された役割に関連付けられている役割の割り当ての一覧を表示するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -Role <role name>
```

この例では、"Mail Recipient/メール受信者" 役割に関連付けられている役割の割り当てをすべて取得します。

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients"
```

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 特定の定義済みスコープを使用している役割の割り当ての一覧を表示する

特定の定義済みスコープを使用している役割の割り当ての一覧を表示するには、次の構文を使用します。

    Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >

この例では、組織という定義済みスコープを使用している役割の割り当てをすべて取得します。

```powershell
Get-ManagementRoleAssignment -RecipientWriteScope Organization
```

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## スコープが特定の OU に設定されている役割の割り当ての一覧を表示する

スコープが特定の組織単位 (OU) に設定されている役割の割り当ての一覧を表示するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>
```

この例では、スコープが contoso.com ドメイン内の North America\\Engineering\\Users OU に設定されている役割の割り当てをすべて取得します。

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 特定のカスタム スコープを使用している割り当ての一覧を表示する

特定のカスタム スコープを使用している役割割り当ての一覧を表示するには、まず、そのスコープが受信者スコープ、構成スコープ、排他的受信者スコープ、排他的構成スコープのいずれであるかを特定する必要があります。スコープの種類ごとに、**Get-ManagementRoleAssignment** コマンドレットで異なるパラメーターが使用されます。各スコープおよびその関連パラメーターを次に示します。

  - **受信者スコープ** *CustomRecipientWriteScope*

  - **構成スコープ** *CustomConfigWriteScope*

  - **排他的受信者スコープ** *ExclusiveRecipientWriteScope*

  - **排他的構成スコープ** *ExclusiveConfigWriteScope*

各パラメーターの構文は同じです。スコープの種類と一致するパラメーターを使用してスコープ名を指定します。

この例では、Vancouver Recipients という受信者スコープを使用している役割の割り当てをすべて取得します。

```powershell
Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"
```

この例では、Seattle AD Site という排他的構成スコープを使用している役割の割り当てをすべて取得します。

```powershell
Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"
```

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 排他的スコープまたは正規のスコープの一覧を表示する

排他的または正規の役割の割り当ての一覧を表示するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -Exclusive < $True | $False >
```

たとえば、排他的スコープの一覧を表示するには、次のコマンドを実行します。

```powershell
Get-ManagementRoleAssignment -Exclusive $True
```

この例では、排他的スコープなしで、正規のスコープの一覧を取得します。

```powershell
Get-ManagementRoleAssignment -Exclusive $False
```

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 特定の受信者またはサーバーを変更できるユーザーを表示する

特定の受信者またはサーバーを変更できる役割割り当ての一覧を表示するには、*WritableRecipient* パラメーターおよび *WritableServer* パラメーターを使用します。受信者の名前は *WritableRecipient* パラメーター、サーバーの名前は *WritableServer* パラメーターを使用して指定します。

この例では、Brian という受信者を変更できる役割の割り当ての一覧を取得します。

```powershell
Get-ManagementRoleAssignment -WritableRecipient "Brian"
```

*WritableRecipient* パラメーターと *WritableServer* パラメーターを、*RoleAssignee* パラメーターや *GetEffectiveUsers* スイッチなどの他のパラメーターと組み合わせると、クエリの精度を高め、役割グループや USG を展開できます。この例では、サーバー EX02 を変更できるユーザーと "Server Management/サーバーの管理" 役割グループが割り当てられているユーザーをすべて取得します。

    Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 役割グループまたは USG 経由で割り当てからアクセス許可を受け取るユーザーを表示する

役割の割り当てからアクセス許可を受け取るユーザーの一覧を表示するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers
```

この例では、"Help Desk Assignment/ヘルプ デスク割り当て" という役割の割り当てのユーザーの一覧を取得します。

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers
```

また、*GetEffectiveUsers* スイッチを **Get-ManagementRoleAssignment** コマンドレットの他のいくつかのパラメーターと組み合わせると、役割割り当てが割り当てられている役割グループと USG を展開することもできます。*GetEffectiveUsers* スイッチを他のパラメーターと共に使用する方法の例については、このトピックの「特定の受信者またはサーバーを変更できるユーザーを表示する」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## 有効または無効になっている役割の割り当ての一覧を表示する

有効または無効になっている役割の割り当ての一覧を表示するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -Enabled < $True | $False >
```

この例では、無効になっている役割の割り当ての一覧を取得します。

```powershell
Get-ManagementRoleAssignment -Enabled $False
```

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

