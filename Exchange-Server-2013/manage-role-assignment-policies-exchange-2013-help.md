---
title: '役割の割り当てポリシーの管理: Exchange 2013 Help'
TOCTitle: 役割の割り当てポリシーの管理
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 49896561
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割の割り当てポリシーの管理

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-09_

エンド ユーザーから成るグループに割り当てるアクセス許可をカスタマイズする場合は、新しいカスタム管理役割の割り当てポリシーを作成します。作成する割り当てポリシーは、エンド ユーザー固有の要件に合わせてカスタマイズできます。Microsoft Exchange Server 2013 での割り当てポリシーの詳細については、「[管理役割の割り当てポリシーについて](understanding-management-role-assignment-policies-exchange-2013-help.md)」を参照してください。

アクセス許可の管理に関連する他の管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「割り当てポリシー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 割り当てポリシーを追加する

新しい割り当てポリシーを作成した後、このポリシーにユーザーを割り当てます。詳細については、「[メールボックスの割り当てポリシーを変更する](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)」を参照してください。

## EAC を使用して新しい割り当てポリシーを作成する


> [!NOTE]
> Exchange 管理センター (EAC) を使用してできるのは、明示的な割り当てポリシーの作成のみです。新しい既定の割り当てポリシーを作成するには、Exchange 管理シェルを使用する必要があります。詳細については、後の「シェルを使用して既定の割り当てポリシーを作成する」を参照してください。



1.  EAC で、<strong>受信者</strong> \> <strong>ユーザーの役割</strong> の順に選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  \[役割の割り当てポリシー\] ウィンドウで、新しい割り当てポリシーの名前を指定します。

3.  割り当てポリシーに追加する役割 (複数可) の横にあるチェック ボックスをオンにします。追加したエンド ユーザーの役割を含む複数の役割を選択できます。子役割を持つ役割を選択すると、子役割は自動的に選択されます。

4.  <strong>保存</strong> をクリックして割り当てポリシーの変更を保存します。

## シェルを使用して、明示的な割り当てポリシーを作成する

メールボックスに手動で割り当てることができる明示的な割り当てポリシーを作成するには、次の構文を使用します。

```powershell
New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>
```

この例では、明示的な割り当てポリシー Limited Mailbox Configuration を作成し、これに `MyBaseOptions`、`MyAddressInformation`、および `MyDisplayName` の役割を割り当てます。

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName

構文およびパラメーターの詳細については、「[New-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638101\(v=exchg.150\))」を参照してください。

## シェルを使用して既定の割り当てポリシーを作成する

新しいメールボックスに対して割り当てる既定の割り当てポリシーを作成するには、次の構文を使用します。

```powershell
New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault
```

この例では、既定の割り当てポリシー Limited Mailbox Configuration を作成し、これに `MyBaseOptions`、`MyAddressInformation`、および `MyDisplayName` の役割を割り当てます。

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault

構文およびパラメーターの詳細については、「[New-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638101\(v=exchg.150\))」を参照してください。

## 割り当てポリシーを削除する

役割管理の割り当てポリシーが不要になった場合は、削除することができます。

## 始める前に把握しておくべき情報

  - 割り当てポリシーが割り当てられているすべてのユーザーが、別の割り当てポリシーに変更される必要があります。メールボックスの割り当てポリシーを変更する方法の詳細については、「[メールボックスの割り当てポリシーを変更する](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)」を参照してください。

  - 割り当てポリシーと割り当てられた管理役割との間のすべての管理役割の割り当てを削除する必要があります。 割り当てポリシーから役割の割り当てを削除する方法の詳細については、後述する「シェルを使用して、割り当てポリシーから役割を削除する」を参照してください。

  - 既定の役割ポリシーを削除する場合は、その役割ポリシーが Exchange 2013 組織の最後の割り当てポリシーである必要があります。

## EAC を使用して割り当てポリシーを削除する

1.  EAC で、<strong>アクセス許可</strong> \> <strong>ユーザーの役割</strong> に移動します。

2.  削除する割り当てポリシーを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

## シェルを使用して割り当てポリシーを削除する

割り当てポリシーを削除するには、次の構文を使用します。

```powershell
Remove-RoleAssignmentPolicy <role assignment policy>
```

この例では、New York Temporary Users 割り当てポリシーを削除します。

```powershell
Remove-RoleAssignmentPolicy "New York Temporary Users"
```

構文およびパラメーターの詳細については、「[Remove-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638190\(v=exchg.150\))」を参照してください。

## 割り当てポリシーの一覧または割り当てポリシーの詳細を表示する

管理役割割り当てポリシーは、入手したい情報、および EAC を使用するか、またはシェルを使用するかによってさまざまな方法で表示できます。

EAC では、割り当てポリシーと、その割り当てポリシーに割り当てられている役割の一覧を表示できます。シェルでは、組織内のすべての割り当てポリシーの表示、特定のポリシーが割り当てられたメールボックスの一覧などが可能です。

## EAC を使用して割り当てポリシーの一覧を表示する

1.  EAC で、<strong>アクセス許可</strong> \> <strong>ユーザーの役割</strong> に移動します。ここには、組織内のすべての割り当てポリシーが表示されます。

2.  特定の割り当てポリシーの詳細を表示するには、表示する割り当てポリシーを選択します。割り当てポリシーの説明と、割り当てポリシーに割り当てられている役割が、詳細ウィンドウに表示されます。

## シェルを使用して割り当てポリシーの一覧を表示する

**Get-RoleAssignmentPolicy**コマンドレットの実行時に割り当てポリシーを指定しないことで、組織内のすべての割り当てポリシーの一覧を表示できます。

この手順では、パイプライン処理および **Format-Table** コマンドレットを利用します。これらの概念の詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

組織内のすべての割り当てポリシーの一覧を返すには、以下のコマンドレットを使用します。

```powershell
Get-RoleAssignmentPolicy
```

組織内のすべての割り当てポリシーの特定のプロパティの一覧を返すには、結果を **Format-Table** コマンドレットにパイプ処理して、結果の一覧に含めるプロパティを指定します。以下の構文を使用します。

```powershell
Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>
```

この例では、組織内のすべての割り当てポリシーの一覧を返し、**Name** と **IsDefault** プロパティを含めます。

```powershell
Get-RoleAssignmentPolicy | Format-Table Name, IsDefault
```

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」または「[Get-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638195\(v=exchg.150\))」を参照してください。

## シェルを使用して 1 つの割り当てポリシーの詳細を表示する

**Get-RoleAssignmentPolicy** コマンドレットを使用して、その出力を **Format-List** コマンドレットにパイプ処理することで、特定の割り当てポリシーの詳細を表示できます。

この手順では、パイプライン処理および **Format-List** コマンドレットを利用します。これらの概念の詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

特定の割り当てポリシーの詳細を表示するには、以下の構文を使用します。

```powershell
Get-RoleAssignmentPolicy <assignment policy name> | Format-List
```

この例では、"Redmond Users/Redmond ユーザー" に関する詳細を表示します (テキスト メッセージング割り当てポリシーは表示しません)。

```powershell
Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List
```

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」または「[Get-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638195\(v=exchg.150\))」を参照してください。

## シェルを使用して既定の割り当てポリシーを検索する

**Get-RoleAssignmentPolicy** コマンドレットの出力を **Where** コマンドレットにパイプ処理することで、既定の割り当てポリシーを検索できます。**Where** コマンドレットを使用すると、割り当てポリシーの *IsDefault* プロパティが `$True` に設定された割り当てポリシーのみを表示するために返されたデータをフィルター処理します。

この手順では、パイプライン処理および **Where** コマンドレットを利用します。これらの概念の詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

この例では、既定の割り当てポリシーが返されます。

```powershell
Get-RoleAssignmentPolicy | Where {     Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }.IsDefault -eq $True }
```

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」または「[Get-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638195\(v=exchg.150\))」を参照してください。

## シェルを使用して特定のポリシーが割り当てられているメールボックスを表示する

**Get-Mailbox** コマンドレットの出力を **Where** コマンドレットにパイプ処理することで、特定の割り当てポリシーが割り当てられているすべてのメールボックスを検索できます。**Where** コマンドレットを使用すると、メールボックスの *RoleAssignmentPolicy* プロパティが、指定した割り当てポリシー名に設定されたメールボックスのみを表示するために返されたデータをフィルター処理します。

この手順では、パイプライン処理および **Where** コマンドレットを利用します。これらの概念の詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

以下の構文を使用します。

```powershell
Get-Mailbox | Where {     Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }.RoleAssignmentPolicy -Eq "<role assignment policy>" }
```

この例では、ポリシー Vancouver エンドユーザーが割り当てられているすべてのメールボックスを検索します。

```powershell
Get-Mailbox | Where {     Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }.RoleAssignmentPolicy -Eq "Vancouver End Users" }
```

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」または「[Get-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638195\(v=exchg.150\))」を参照してください。

## 既定の割り当てポリシーを変更する

作成される新しいメールボックスに割り当てる管理役割の割り当てポリシーを変更できます。 既定の役割割り当てポリシーを変更しても、既存のメールボックスに割り当てられている割り当てポリシーは変更されません。既存のメールボックスに割り当てられている割り当てポリシーを変更するには、「[メールボックスの割り当てポリシーを変更する](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> EAC を使用して既定の割り当てポリシーを変更することはできません。 シェルを使用する必要があります。



## シェルを使用して既定の割り当てポリシーを変更する

既定の割り当てポリシーを変更するには、次の構文を使用します。

```powershell
Set-RoleAssignmentPolicy <assignment policy name> -IsDefault
```

この例では、Vancouver End Users という割り当てポリシーを既定の割り当てポリシーとして設定します。

```powershell
Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault
```


> [!IMPORTANT]
> ポリシーに対して管理役割が割り当てられていない場合でも、新しいメールボックスに対して既定の割り当てポリシーが割り当てられます。 割り当てられた管理の役割が存在しない割り当てポリシーが割り当てられているメールボックスは、Microsoft Outlook Web App でメールボックス構成機能にアクセスできません。



構文およびパラメーターの詳細については、「[Set-RoleAssignmentPolicy](https://technet.microsoft.com/ja-jp/library/dd638090\(v=exchg.150\))」を参照してください。

## 割り当てポリシーに役割を追加する

## EAC を使用して割り当てポリシーに役割を追加する

1.  EAC で、<strong>アクセス許可</strong> \> <strong>ユーザーの役割</strong> に移動します。

2.  1 つまたは複数の役割を追加する割り当てポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  割り当てポリシーに追加する役割 (複数可) の横にあるチェック ボックスをオンにします。追加したエンド ユーザーの役割を含む複数の役割を選択できます。子役割を持つ役割を選択すると、子役割は自動的に選択されます。

4.  <strong>保存</strong> をクリックして割り当てポリシーの変更を保存します。

## シェルを使用して割り当てポリシーに役割を追加する

役割と割り当てポリシーの間に管理役割の割り当てを作成するには、次の構文を使用します。

    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>

この例では、"MyVoicemail/自分のボイス メール" 役割と "Seattle Users/Seattle ユーザー" 割り当てポリシーの間に "Seattle Users - Voicemail/Seattle ユーザー - ボイス メール" 役割の割り当てを作成します。

    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"

構文およびパラメーターの詳細については、「[New-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd335193\(v=exchg.150\))」を参照してください。

## 割り当てポリシーから役割を削除する

メールボックスまたは配布グループの特定の管理機能をエンド ユーザーに許可したくない場合、ユーザーに割り当てられた管理役割の割り当てポリシーから、アクセス許可を与える管理役割を削除することができます。他のユーザーに対して同じ割り当てポリシーが割り当てられている場合、そのユーザーもその機能を管理できなくなります。

## EAC を使用して、割り当てポリシーから役割を削除する

1.  EAC で、<strong>アクセス許可</strong> \> <strong>ユーザーの役割</strong> に移動します。

2.  役割を削除する割り当てポリシー (複数可) を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  割り当てポリシーから削除する役割 (複数可) の横のチェック ボックスをオフにします。子役割を持つ役割のチェック ボックスをオフにすると、子役割のチェック ボックスもオフになります。

4.  <strong>保存</strong> をクリックして割り当てポリシーの変更を保存します。

## シェルを使用して、割り当てポリシーから役割を削除する

**Get-ManagementRoleAssignment** コマンドレットを使用して関連する管理役割の割り当てを取得し、返された役割の割り当てを **Remove-ManagementRoleAssignment** コマンドレットにパイプ処理することで、割り当てポリシーから役割を削除できます。

正規と委任の役割割り当ての詳細については、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」を参照してください。

この手順では、パイプライン処理を使用します。パイプライン処理の詳細については、「[パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))」を参照してください。

割り当てポリシーから役割を削除するには、次の構文を使用します。

    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment

この例では、ボイス メール オプションを管理できるようにする "MyVoicemail" 管理役割を、"Seattle Users/Seattle ユーザー" という割り当てポリシーから削除しています。

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment

構文およびパラメーターの詳細については、「[Remove-ManagementRoleAssignment](https://technet.microsoft.com/ja-jp/library/dd351205\(v=exchg.150\))」を参照してください。

