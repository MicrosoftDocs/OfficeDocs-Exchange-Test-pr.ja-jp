---
title: '役割から役割エントリを削除する: Exchange 2013 Help'
TOCTitle: 役割から役割エントリを削除する
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 49896230
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割から役割エントリを削除する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

管理役割の中にある管理役割エントリによって、管理役割でどのコマンドレットとパラメーターが使用できるかが決まります。 役割エントリを削除、または役割エントリからパラメーターを削除すると、管理役割を割り当てられたユーザーが実行できる機能に制限を加えることができます。Microsoft Exchange Server 2013 での管理役割エントリの詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 単一の全体的な役割エントリを役割から削除する

役割から役割エントリを削除すると、その役割を割り当てられたユーザーが、エントリに関連付けられているコマンドレットまたはスクリプトにアクセスできる能力も削除されます。

役割から全体的な管理役割エントリを削除するには、次の構文を使用します。

```powershell
Remove-ManagementRoleEntry <management role>\<management role entry>
```

この例では、"Seattle Server Administrators/Seattle のサーバー管理者" という役割から **Enable-MailUser** コマンドレットを削除します。

```powershell
Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"
```

構文およびパラメーターの詳細については、「[Remove-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351187\(v=exchg.150\))」を参照してください。

## 役割から複数の全体的な役割エントリを削除する

役割から複数の役割エントリを削除すると、その役割を割り当てられたユーザーが、エントリに関連付けられているコマンドレットまたはスクリプトにアクセスできる能力も削除されます。

役割から複数の役割エントリを削除するには、**Get-ManagementRoleEntry** コマンドレットを使用して、削除する役割エントリのリストを取得する必要があります。 次に、その出力を **Remove-ManagementRoleEntry** コマンドレットにパイプ出力する必要があります。 **Get-ManagementRoleEntry** コマンドレットでワイルドカード文字を使用して、複数の役割エントリに一致させることができます。 *WhatIf* スイッチを使用して、削除しようとしている役割エントリが正しいかどうかを確認することをお勧めします。 以下の構文を使用します。

    Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf

この例では、"Seattle Server Administrators/Seattle のサーバー管理者" という役割から、"journal" という単語を含むすべての役割エントリを削除します。

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf

*WhatIf* スイッチを指定してコマンドを実行すると、削除しようとしているすべての役割エントリのリストがコマンドレットから返されます。 リストが正しいと思える場合は、*WhatIf* スイッチなしでコマンドをもう一度実行して、役割エントリを削除できます。

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」と「[Remove-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351187\(v=exchg.150\))」を参照してください。

## 役割内の役割エントリからパラメーターを削除する

役割内の役割エントリからパラメーターを削除すると、役割を割り当てられたユーザーは、それらのパラメーターを使用できなくなります。

役割エントリからパラメーターを削除するには、次の構文を使用します。

    Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter

この例では、*MaxSafeSenders*、*MaxSendSize*、*SecondaryAddress*、および*UseDatabaseQuotaDefaults* パラメーターを、"Seattle Server Administrators/Seattle のサーバー管理者" という役割にある **Set-Mailbox** 役割エントリから削除します。

    Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

