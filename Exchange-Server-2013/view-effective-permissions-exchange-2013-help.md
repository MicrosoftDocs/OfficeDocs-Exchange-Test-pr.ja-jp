---
title: '有効なアクセス許可を表示する: Exchange 2013 Help'
TOCTitle: 有効なアクセス許可を表示する
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 49896417
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 有効なアクセス許可を表示する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-09_

Microsoft Exchange Server 2013 内のアクセス許可は管理役割を使用して付与されるもので、管理役割グループ、管理役割の割り当てポリシー、ユニバーサル セキュリティ グループ (USG)、またはユーザーに直接割り当てられます。 ユーザーは役割グループまたは USG のメンバーであるか、役割の割り当てポリシーを割り当てられている場合は、アクセス許可を付与されます。

ほとんどのアクセス許可は、役割グループのメンバーシップ、または割り当てポリシーの割り当てによって、エンド ユーザーに付与されます。 役割グループと割り当てポリシーを使用することによって、多数のユーザーへのアクセス許可の付与が容易になりますが、誰が役割グループのメンバーであるのか、または誰が割り当てポリシーを割り当てられているのかを管理者が意識していない可能性があります。 この状況では、**Get-ManagementRoleAssignment** コマンドレットの *GetEffectiveUsers* スイッチが役立ちます。 このコマンドを実行すると、ユーザーに対して割り当てられた役割グループ、割り当てポリシー、および USG を経由して、管理役割によってどのユーザーにアクセス許可が付与されているかが表示されます。

*Role* パラメーターを使用する場合は、**Get-ManagementRoleAssignment** コマンドレットと共に *GetEffectiveUsers* スイッチを使用します。 このスイッチを特定の役割と共に指定すると、**Get-ManagementRoleAssignment** コマンドレットによって、役割グループ、割り当てポリシー、USG のような役割に割り当てられた役割担当者すべてが確認され、各役割のメンバーが一覧表示されます。


> [!NOTE]
> <EM>GetEffectiveUser</EM> スイッチを使用しても、リンクされた外部の役割グループのメンバーであるユーザーは一覧表示されません。 リンクされた役割グループが見つかった場合は、ユーザーの一覧の代わりに、<STRONG>[すべてのリンクされたグループ メンバー]</STRONG> が表示されます。 複数のフォレスト内でのアクセス許可の詳細については、「<A href="understanding-multiple-forest-permissions-exchange-2013-help.md">複数フォレストのアクセス許可について</A>」を参照してください。



管理役割、役割グループ、および割り当てポリシーの詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。 管理役割の割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

アクセス許可の管理に関連する他の管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「役割グループ」または「役割割り当てポリシー」。

  - このトピックの手順は、シェルでのみ実行できます。 Exchange 管理センター (EAC) を使用して有効なアクセス許可を表示することはできません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してすべての有効なユーザーを一覧表示する

管理役割によって与えられるアクセス許可を付与されているすべてのユーザーを一覧表示するには、次の構文を使用します。

```powershell
Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers
```

この例では、メール受信者の役割によって提供されるアクセス許可を付与されたすべてのユーザーを一覧表示します。

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers
```

一覧の中で返されるプロパティを変更したり、一覧をコンマ区切り値 (.csv) ファイルにエクスポートする場合は、後の「シェルを使用して出力をカスタマイズし表示する」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## シェルを使用して 1 つの役割の中で特定のユーザーを検索する

管理役割によってアクセス許可を付与された特定のユーザーを検索するには、**Get-ManagementRoleAssignment** コマンドレットを使用してすべての有効なユーザーの一覧を取得し、次にコマンドレットの出力を **Where** コマンドレットにパイプ処理します。 **Where** コマンドレットは、出力をフィルタ処理し、指定したユーザーのみを返します。 以下の構文を使用します。

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

この例では、ジャーナリングの役割の中でユーザー David Strome を検索します。

    Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }

一覧の中で返されるプロパティを変更したり、一覧を CSV ファイルにエクスポートする場合は、後の「シェルを使用して出力をカスタマイズし表示する」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## シェルを使用してすべての役割の中で特定のユーザーを検索する

ユーザーがアクセス許可を受け取るために経由しているすべての役割を調べるには、**Get-ManagementRoleAssignment** コマンドレットを使用してすべての管理役割ですべての有効なユーザーを取得し、次にコマンドレットの出力を **Where** コマンドレットにパイプ処理します。 **Where** コマンドレットは、出力をフィルタ処理し、ユーザーにアクセス許可を付与している役割の割り当てのみを返します。

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

この例では、ユーザー Kim Akers にアクセス許可を付与しているすべての役割の割り当てを検索します。

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where {     Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }.EffectiveUserName -Eq "Kim Akers" }
```

一覧に返されるプロパティを変更したり、CSV ファイルに一覧をエクスポートするには、後の「シェルを使用して出力をカスタマイズし表示する」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## シェルを使用して出力をカスタマイズし表示する

**Get-ManagementRoleAssignment** コマンドレットの既定の出力には、必要とする情報が含まれていない可能性があります。 コマンドレットの出力には、アクセス可能なさらに多くのプロパティが含まれています。 役立つ可能性のあるプロパティの一部を次に示します。

  - **EffectiveUserName**   ユーザーの名前

  - **Role**   アクセス許可を付与している役割

  - **RoleAssigneeName**   役割に対して割り当てられた役割グループ、割り当てポリシー、または USG で、`EffectiveUserName` プロパティの中にユーザーが含まれています。

  - **RoleAssigneeType**   役割の割り当てが、役割グループ、割り当てポリシー、USG、ユーザーのどれを対象にしているかを示します。

  - **AssignmentMethod**   役割と役割担当者の間の割り当てが直接的か間接的かを示します。

  - **CustomRecipientWriteScope**   カスタム受信者書き込みスコープが存在する場合は、作成時に役割の割り当てに適用されたカスタム受信者書き込みスコープを示します。 このプロパティの中で指定されたスコープは、`RecipientWriteScope` プロパティの中で指定された暗黙的な受信者書き込みスコープより優先されます。

  - **CustomConfigWriteScope**   カスタム構成書き込みスコープが存在する場合は、作成時に役割の割り当てに適用されたカスタム構成書き込みスコープを示します。 このプロパティの中で指定されたスコープは、`ConfigWriteScope` プロパティの中で指定された暗黙的な構成書き込みスコープより優先されます。

  - **RecipientReadScope**   役割に適用された暗黙的な受信者読み取りスコープを示します。

  - **RecipientReadScope**   役割に適用された暗黙的な受信者書き込みスコープを示します。

  - **ConfigReadScope**   役割に適用された暗黙的な構成読み取りスコープを示します。

  - **ConfigWriteScope**   役割に適用された暗黙的な構成書き込みスコープを示します。

一覧の中で表示するプロパティを選択するには、「シェルを使用してすべての有効なユーザーを一覧表示する」、「シェルを使用して 1 つの役割の中で特定のユーザーを検索する」、および「シェルを使用してすべての役割の中で特定のユーザーを検索する」で使用したものと類似のコマンドを使用します。 違いは、これらのコマンドの結果を、**Format-Table** または **Select-Object** コマンドレットにパイプ処理することです。 **Format-Table** コマンドレットは、結果の一覧を画面に出力するときに役立ちます。 **Select-Object** コマンドレットは、結果の一覧を CSV ファイルに出力するときに役立ちます。

両方のコマンドレットを使用すると、表示するプロパティと、その順序を指定できます。 **Format-Table** コマンドレットには、結果を画面で一覧表示するときにより多くのオプションがあるのに対し、**Select-Object** が出力を変更することはないため、一覧を CSV ファイルにパイプ処理するときに役立ちます。

**Format-Table** および **Select-Object** コマンドレットの詳細については、「[コマンド出力の操作](working-with-command-output-exchange-2013-help.md)」を参照してください。

## カスタマイズした一覧を画面に出力する

1.  調べる情報を選択して、以下の手順のいずれかから関連付けられたコマンドを見つけます。
    
      - シェルを使用してすべての有効なユーザーを一覧表示する
    
      - シェルを使用して 1 つの役割の中で特定のユーザーを検索する
    
      - シェルを使用してすべての役割の中で特定のユーザーを検索する

2.  一覧に表示するプロパティを選択します。

3.  次の構文を使用して一覧を表示します。
    
        <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>

この例では、すべての役割からユーザー David Strome を検索し、`EffectiveUserName`、`Role`、`CustomRecipientWriteScope`、および `CustomConfigWriteScope` プロパティを表示します。

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

## カスタマイズした一覧を CSV ファイルに出力する

一覧を CSV ファイルにエクスポートするには、前述で一覧表示した、適切な手順を使用して取得した **Get-ManagementRoleAssignment** コマンドの結果を、**Select-Object** コマンドレットにパイプ処理します。 その後、**Select-Object** コマンドレットの出力を **Export-CSV** コマンドレットにパイプ処理し、CSV 出力をユーザーが指定したファイル名で保存します。

1.  調べる情報を選択して、以下の手順のいずれかから関連付けられたコマンドを見つけます。
    
      - シェルを使用してすべての有効なユーザーを一覧表示する
    
      - シェルを使用して 1 つの役割の中で特定のユーザーを検索する
    
      - シェルを使用してすべての役割の中で特定のユーザーを検索する

2.  一覧に表示するプロパティを選択します。

3.  次の構文を使用して一覧を CSV ファイルにエクスポートします。
    
        <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>

この例では、すべての役割からユーザー David Strome を検索し、`EffectiveUserName`、`Role`、`CustomRecipientWriteScope`、および `CustomConfigWriteScope` プロパティを表示します。

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv

任意のビューアーで CSV ファイルを表示できます。

構文およびパラメーターの詳細については、「[Get-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351024\(v=exchg.150\))」を参照してください。

