---
title: 'スコープ外の最上位の役割における役割エントリを変更する: Exchange 2013 Help'
TOCTitle: スコープ外の最上位の役割における役割エントリを変更する
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 49896286
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# スコープ外の最上位の役割における役割エントリを変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

スコープ外の最上位の管理役割における管理役割エントリは、その役割を割り当てられているユーザーに利用可能にするスクリプト、非 Exchange のコマンドレットおよびパラメーターを参照します。 役割エントリで利用可能なパラメーターを変更することにより、役割を割り当てられたユーザーがスクリプトまたは非 Exchange のコマンドレットを使用して、どの操作を実行できるようにするかを制御できます。 スコープ外の役割のエントリの詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Exchange コマンドレットを含む管理の役割の役割エントリを変更する場合、「<A href="change-a-role-entry-exchange-2013-help.md">役割エントリを変更する</A>」を参照してください。



役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - 既定では、スコープ外の最上位の役割の役割エントリを変更する権限は、管理役割グループに付与されません。 ユーザーがスコープ外の最上位の役割エントリを追加または変更できるようにするには、その前にまず "Unscoped Role Management/スコープ外役割管理" 役割をユーザーに割り当てるか、ユニバーサル セキュリティ グループ (USG) あるいはユーザーがメンバーとして属している役割グループに割り当てる必要があります。 役割をユーザー、USG、または役割グループに追加する方法の詳細については、以下のトピックを参照してください。
    
      - [役割グループの管理](manage-role-groups-exchange-2013-help.md)
    
      - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して 1 つ以上のパラメーターを役割エントリに追加する

スコープ外の最上位の役割エントリにパラメーターを追加するには、次の手順を実行する必要があります。

  - *Parameters* パラメーターを使用して、追加するパラメーターを指定します。

  - 実行すべき操作が追加操作であることを示す *AddParameter* パラメーターを指定します。

  - スコープ外の最上位の役割のエントリを変更することを示すため、*UnscopedTopLevel* パラメーターを指定します。 スコープ外の役割の役割エントリを変更するときにこのパラメーターを指定しないと、エラーが発生します。

パラメーターを役割エントリに追加するには、次の構文を使用します。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

この例では、"Recipient Administrators/受信者管理者" スコープ外役割に関する **CreateUsers.ps1** スクリプトに、*EmailAddress* パラメーターと *City* パラメーターを追加します。

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

## シェルを使用して役割エントリから 1 つ以上のパラメーターを削除する

役割エントリからパラメーターを削除するには、次の手順を実行する必要があります。

  - *Parameters* パラメーターを使用して、削除するパラメーターを指定します。

  - 実行すべき操作が削除操作であることを示す *RemoveParameter* パラメーターを指定します。

  - スコープ外の最上位の役割のエントリを変更することを示すため、*UnscopedTopLevel* パラメーターを指定します。スコープ外の役割の役割エントリを変更するときにこのパラメーターを指定しないと、エラーが発生します。


> [!NOTE]
> 削除操作を元に戻すことはできません。 誤ってパラメーターを役割エントリから削除したら、手動で追加し直す必要があります。



役割エントリからパラメーターを削除するには、次の構文を使用します。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

この例では、"Tier 1 Server Administrators/第 1 層サーバー管理者" 役割の **Start-Widget** 非 Exchange コマンドレットから *Delay*、*Force*、および *Credential* の各パラメーターを削除します。

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

## シェルを使用して役割エントリからすべてのパラメーターを削除する

役割エントリからすべてのパラメーターを削除するには、次の手順を実行する必要があります。

  - *Parameters* パラメーターに値 `$Null` を指定します。 *RemoveParameter* パラメーターを指定する必要はありません。

  - スコープ外の最上位の役割のエントリを変更することを示すため、*UnscopedTopLevel* パラメーターを指定します。スコープ外の役割の役割エントリを変更するときにこのパラメーターを指定しないと、エラーが発生します。

役割エントリからパラメーターを一括削除する操作は、スクリプトまたは非 Exchange コマンドレットで使用可能にするパラメーターを 2 ～ 3 に限定してそれ以外のパラメーターをすべて除外する場合に、特に便利です。

役割をスクリプトまたは非 Exchange コマンドレットにアクセスさせないようにする場合は、パラメーターを単に削除する代わりに、関連付けられている役割エントリを役割から完全に削除してください。 役割から役割エントリを削除する方法の詳細については、「[役割から役割エントリを削除する](remove-a-role-entry-from-a-role-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 削除操作を元に戻すことはできません。 役割エントリからすべてのパラメーターを誤って削除した場合は、それらのパラメーターを再度手動で追加する必要があります。



役割エントリからすべてのパラメーターを削除するには、次の構文を使用します。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

この例では、"Recipient Administrators/受信者管理者" 役割に関する FindMailboxesOverQuota.ps1 スクリプトからすべてのパラメーターを削除します。

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

## シェルを使用して特定のパラメーター セットを適用する

役割エントリに特定のパラメーター セットのみを指定する場合、次の手順を実行する必要があります。

  - *Parameters* パラメーターのみを指定します。 *AddParameter* または *RemoveParameter* パラメーターを含めないでください。

  - スコープ外の役割の役割エントリが変更対象であることを示す、*UnscopedTopLevel* パラメーターを指定します。 このパラメーターを指定しておかないと、スコープ外の最上位の役割の役割エントリを変更する際に、エラーが発生します。


> [!NOTE]
> <EM>Parameters</EM> パラメーターのみを指定した場合は、コマンドで指定したパラメーターだけが役割エントリに含まれます。 その他のパラメーターはすべて削除されます。



特定のパラメーター セットを指定するには、次の構文を使用します。

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

この例では、"Seattle Mail Recipient Admins/Seattle のメール受信者管理者" 役割の **Set-Widget** コマンドレットに、*Alias*、*DisplayName*、*WidgetConfig*、および *Enabled* の各パラメーターのみを含めます。

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

## その他のタスク

スコープ外の最上位の役割の役割エントリを変更した後、必要に応じて次の操作も実行してください。

[役割エントリを役割に追加する](add-a-role-entry-to-a-role-exchange-2013-help.md)

[役割グループの管理](manage-role-groups-exchange-2013-help.md)

[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)

[ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[ユーザーまたは USG から役割を削除する](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

