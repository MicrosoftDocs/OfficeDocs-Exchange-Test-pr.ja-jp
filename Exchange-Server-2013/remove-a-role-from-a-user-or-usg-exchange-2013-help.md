---
title: 'ユーザーまたは USG から役割を削除する: Exchange 2013 Help'
TOCTitle: ユーザーまたは USG から役割を削除する
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 49896519
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーまたは USG から役割を削除する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-02_

管理役割の割り当てによって、管理役割がユーザーまたはユニバーサル セキュリティ グループ (USG) に割り当てられます。 役割の割り当てを削除すると、役割に割り当てられていたユーザーは、その役割で使用可能なコマンドレットにアクセスできなくなります。Microsoft Exchange Server 2013 での管理役割の割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - この手順の予想所要時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割の割り当て」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 管理役割の割り当てを削除する

削除する役割の割り当ての名前がわかっている場合は、次の構文を使用します。

```powershell
Remove-ManagementRoleAssignment <assignment name>
```

たとえば、"Tier 2 Help Desk Assignment/Tier 2 ヘルプデスク割り当て" という役割の割り当てを削除するには、次のコマンドを使用します。

```powershell
Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"
```

削除する役割の割り当ての名前がわからない場合は、次の構文を使用します。

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 
```

たとえば、ユーザー "davids" から正規の役割の割り当て "Mail Recipients/メール受信者" を削除する場合、次のコマンドを使用します。

```powershell
    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment
```
