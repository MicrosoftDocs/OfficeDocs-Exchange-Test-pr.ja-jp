---
title: '役割エントリを変更する: Exchange 2013 Help'
TOCTitle: 役割エントリを変更する
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 49896269
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割エントリを変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

管理役割の各管理役割エントリは、1 つのコマンドレットを表します。 役割エントリに追加したパラメーター、または役割エントリから削除したパラメーターは、管理役割に追加されます。そのパラメーターを該当のコマンドレットで使用可能にするかどうかは、ユーザー自身で制御します。Microsoft Exchange Server 2013 での管理役割エントリの詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

組み込みの管理役割にある役割エントリは、変更することができません。


> [!NOTE]
> このトピックでは、スコープ外の管理役割にあるスコープ外の管理役割エントリを変更する方法については扱いません。 スコープ外の役割エントリを変更する方法の詳細については、「<A href="create-a-role-exchange-2013-help.md">役割を作成する</A>」を参照してください。




> [!NOTE]
> パラメーターを役割エントリに追加、または役割エントリから削除する場合、使用する必要のあるパラメーターは、<EM>AddParameter</EM> または <EM>RemoveParameter</EM> です。 <STRONG>Set-ManagementRoleEntry</STRONG> コマンドレットの実行時に <EM>AddParameter</EM> または <EM>RemoveParameter</EM> のどちらかのパラメーターを省略した場合、<EM>Parameters</EM> パラメーターで指定されたパラメーターのみが、役割エントリ内に含まれることになります。 役割エントリ上の他のパラメーターはいずれも削除されます。



役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - 役割エントリにパラメーターを追加する場合、その追加対象パラメーターは親役割内の役割エントリにあらかじめ存在している必要があります。 そのパラメーターは、指定したコマンドレット上にもあらかじめ存在している必要があります。

  - 役割エントリからパラメーターを削除する場合、その削除対象パラメーターはどの子役割の役割エントリにも存在していてはなりません。 そのパラメーターを子役割の役割エントリから削除する必要があります。 すべての子役割の役割エントリからパラメーターを削除する際は、このトピックで後述する「シェルを使用して役割エントリから 1 つ以上のパラメーターを削除する」の手順に従ってください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して 1 つ以上のパラメーターを役割エントリに追加する

役割エントリにパラメーターを追加するには、追加対象のパラメーターを *Parameters* パラメーターで指定する必要があります。 その際は、実行すべき操作が追加操作であることを示す *AddParameter* パラメーターも必ず指定するようにします。

パラメーターを役割エントリに追加するには、次の構文を使用します。

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter
```

この例では、"Recipient Administrators/受信者管理者" 役割の **Set-Mailbox** コマンドレットに *EmailAddresses* パラメーターと *Type* パラメーターを追加します。

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter
```

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

## シェルを使用して役割エントリから 1 つ以上のパラメーターを削除する

役割エントリからパラメーターを削除するには、削除対象のパラメーターを *Parameters* パラメーターで指定する必要があります。 その際は、実行すべき操作が削除操作であることを示す *RemoveParameter* パラメーターも必ず指定するようにします。

役割エントリからパラメーターを削除するには、次の構文を使用します。

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter
```

この例では、"Tier 1 Server Administrators/第 1 層サーバー管理者" 役割の **Set-SendConnector** コマンドレットから *Port*、*ProtocolLoggingLevel*、および *SmartHostAuthMechanism* の各パラメーターを削除します。

```powershell
Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter
```

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

## シェルを使用して役割エントリからすべてのパラメーターを削除する

役割エントリからパラメーターをすべて削除する場合は、*Parameters* パラメーターに値 `$Null` を指定する必要があります。 *RemoveParameters* パラメーターを指定する必要はありません。

役割エントリからパラメーターを一括削除する操作は、コマンドレットで使用可能にするパラメーターを 2 ～ 3 に限定してそれ以外のパラメーターをすべて除外する場合に、特に便利です。 役割をコマンドレットにアクセスさせないようにする場合、パラメーターの削除だけでは不十分です。関連付けられている役割エントリを役割から完全に削除してください。 役割から役割エントリを削除する方法の詳細については、「[役割から役割エントリを削除する](remove-a-role-entry-from-a-role-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 削除操作を元に戻すことはできません。 役割エントリからすべてのパラメーターを誤って削除した場合は、それらのパラメーターを再度手動で追加する必要があります。



役割エントリからすべてのパラメーターを削除するには、次の構文を使用します。

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 
```

この例では、"Recipient Administrators/受信者管理者" 役割の **Set-CASMailbox** コマンドレットからパラメーターをすべて削除します。

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 
```

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

## シェルを使用して特定のパラメーター セットを適用する

役割エントリに含めるパラメーターを特定のものだけに限定する場合、指定する *Parameters* パラメーターのみです。 *AddParameter* または *RemoveParameter* パラメーターを含めないでください。 *Parameters* パラメーターのみを指定した場合は、コマンドで指定したパラメーターだけが役割エントリに含まれます。 その他のパラメーターはすべて削除されます。

特定のパラメーター セットを指定するには、次の構文を使用します。

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>
```

この例では、"Seattle Mail Recipients/Seattle のメール受信者" 役割の **Set-UMMailbox** コマンドレットに、*Identity*、*DisplayName*、*MissedCallNotificationEnabled*、および *PersonalAuthAttendantEnabled* の各パラメーターのみを含めます。

```powershell
Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled
```

構文およびパラメーターの詳細については、「[Set-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351162\(v=exchg.150\))」を参照してください。

