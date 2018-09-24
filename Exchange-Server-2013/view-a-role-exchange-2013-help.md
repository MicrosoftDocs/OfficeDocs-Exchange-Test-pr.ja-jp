---
title: '役割を表示する: Exchange 2013 Help'
TOCTitle: 役割を表示する
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 49895271
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割を表示する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

管理役割は、目的の情報に応じて、さまざまな方法で一覧表示できます。 たとえば、特定の役割の種類の役割のみ返すか、特定のコマンドレットとパラメーターのみ含む役割を返すか、特定の管理役割の詳細を表示するかを選択できます。Microsoft Exchange Server 2013 での管理役割の詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

役割のすべての管理役割エントリの一覧を表示する場合は、「[役割エントリを表示する](view-role-entries-exchange-2013-help.md)」を参照してください。

役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - ここでは、パイプライン処理と **Format-List** および **Format-Table** コマンドレットを利用します。 これらの概念の詳細については、以下のトピックを参照してください。
    
      - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))
    
      - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 特定の管理役割を表示する

**Get-ManagementRole** コマンドレットを使用して特定の役割を取得し、**Format-List** コマンドレットの出力をパイプ処理することで、特定の役割の詳細を表示できます。

特定の役割の詳細を表示するには、次の構文を使用します。

```powershell
Get-ManagementRole <role name> | Format-List
```

この例では、"Mail Recipient/メール受信者" 管理役割に関する詳細を取得します。

```powershell
Get-ManagementRole "Mail Recipients" | Format-List
```

構文およびパラメーターの詳細については、「[Get-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351125\(v=exchg.150\))」を参照してください。

## すべての管理役割を一覧表示する

**Get-ManagementRole** コマンドレットの実行時に何も役割を指定しなければ、組織内のすべての管理役割の一覧を表示できます。 既定では、各役割の役割名と役割の取得が結果に含まれます。

この例では、組織内のすべての役割の一覧を返します。

```powershell
Get-ManagementRole
```

組織内のすべての役割に関する特定のプロパティの一覧を返すには、**Format-Table** コマンドレットの結果をパイプ処理し、結果の一覧で目的のプロパティを指定します。 以下の構文を使用します。

```powershell
Get-ManagementRole | Format-Table <property 1>, <property 2...>
```

この例では、組織内のすべての役割の一覧を返し、**Name** プロパティ、およびプロパティ名の先頭に単語 **Implicit** を持つ任意のプロパティを含めます。

```powershell
    Get-ManagementRole | Format-Table Name, Implicit*
```

構文およびパラメーターの詳細については、「[Get-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351125\(v=exchg.150\))」を参照してください。

## 特定のコマンドレットを含む管理役割を一覧表示する

**Get-ManagementRole** コマンドレットで *Cmdlet* パラメーターを使用すると、指定したコマンドレットを含む役割の一覧を返すことができます。

指定したコマンドレットを含む役割の一覧を返すには、次の構文を使用します。

```powershell
Get-ManagementRole -Cmdlet <cmdlet>
```

この例では、**New-Mailbox** コマンドレットを含む役割の一覧を返します。

```powershell
Get-ManagementRole -Cmdlet New-Mailbox
```

構文およびパラメーターの詳細については、「[Get-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351125\(v=exchg.150\))」を参照してください。

## 特定のパラメーターを含む管理役割を一覧表示する

**Get-ManagementRole** コマンドレットで *CmdletParameters* パラメーターを使用すると、指定された 1 つ以上のパラメーターを含む役割の一覧を返すことができます。 指定したすべてのパラメーターを含む役割のみが返されます。

*CmdletParameters* パラメーターを使用する場合、*Cmdlet* パラメーターを含めることを選択できます。 *Cmdlet* パラメーターを含める場合、指定したコマンドレットで指定したパラメーターを含む役割のみ返されます。 *Cmdlet* パラメーターを含めない場合は、指定したパラメーターを含む役割が、そのパラメーターがあるコマンドレットに無関係に返されます。

指定したパラメーターを含む役割の一覧を返すには、次の構文を使用します。

```powershell
    Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>
```

この例では、パラメーターが存在しているコマンドレットに無関係に、*Database* パラメーターと *Server* パラメーターを含む役割の一覧を返します。

```powershell
Get-ManagementRole -CmdletParameters Database, Server
```

この例では、*EmailAddresses* パラメーターが **Set-Mailbox** コマンドレット上にのみ存在している役割の一覧を返します。

```powershell
Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses
```

*Cmdlet* パラメーターまたは *CmdletParameters* パラメーターと共にワイルドカード文字 (\*) を使用すると、コマンドレット名またはパラメーター名の一部を指定して一致するものを検索することもできます。

構文およびパラメーターの詳細については、「[Get-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351125\(v=exchg.150\))」を参照してください。

## 特定の役割の種類の管理役割を一覧表示する

**Get-ManagementRole** コマンドレットで *RoleType* パラメーターを使用すると、指定された役割の種類に基づいて役割の一覧を返すことができます。

指定した役割の種類に一致する役割の一覧を返すには、次の構文を使用します。

```powershell
Get-ManagementRole -RoleType <roletype>
```

この例では、`UmMailboxes` 役割の種類に基づいて役割の一覧を返します。

```powershell
Get-ManagementRole -RoleType UmMailboxes
```

構文およびパラメーターの詳細については、「[Get-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351125\(v=exchg.150\))」を参照してください。

## 親役割の直下の子役割を一覧表示する

**Get-ManagementRole** コマンドレットで *GetChildren* パラメーターを使用すると、指定した親役割の直下の子となっている役割の一覧を返すことができます。 親役割として指定した役割を含む役割のみ返されます。

親役割の直下の子役割の一覧を返すには、次の構文を使用します。

```powershell
Get-ManagementRole <parent role name> -GetChildren
```

この例では、"Disaster Recovery/障害回復" 役割の直下の子の一覧を返します。

```powershell
Get-ManagementRole "Disaster Recovery" -GetChildren
```

構文およびパラメーターの詳細については、「[Get-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351125\(v=exchg.150\))」を参照してください。

## 親役割の下にあるすべての子役割を一覧表示する

**Get-ManagementRole** コマンドレットで *Recurse* パラメーターを使用すると、指定された親役割から最後の子役割までの役割のチェーン全体の一覧を返すことができます。 *Recurse* パラメーターは、**Get-ManagementRole** コマンドレットに、最後の子役割に到達するまで、検出したすべての親と子の関係を再帰処理するように指示します。 親役割は、返される一覧に含まれています。

この例では、親役割のすべての子役割の一覧を返します。

```powershell
Get-ManagementRole <parent role name> -Recurse
```

この例では、"Mail Recipient/メール受信者" 役割のすべての子役割を返します。

```powershell
Get-ManagementRole "Mail Recipients" -Recurse
```

構文およびパラメーターの詳細については、「[Get-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd351125\(v=exchg.150\))」を参照してください。

