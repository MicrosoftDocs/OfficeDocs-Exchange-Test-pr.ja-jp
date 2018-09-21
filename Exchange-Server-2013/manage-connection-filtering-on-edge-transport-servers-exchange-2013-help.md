---
title: 'エッジ トランスポート サーバーでの接続フィルターの管理: Exchange 2013 Help'
TOCTitle: エッジ トランスポート サーバーでの接続フィルターの管理
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60830037
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# エッジ トランスポート サーバーでの接続フィルターの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

接続フィルターは、接続フィルター エージェントが提供するスパム対策機能です。接続フィルター エージェントは、Microsoft Exchange 2013 のエッジ トランスポート サーバーでのみ使用できます。接続フィルターでは以下の機能を使用できます。

  - IP 禁止一覧

  - IP 禁止一覧プロバイダー

  - IP 許可一覧

  - IP 許可一覧プロバイダー

これらの機能はすべて別々に有効または無効にすることができます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[スパム対策とマルウェア対策のアクセス許可](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)」の「スパム対策機能」トピック。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して接続フィルターを有効または無効にする

接続フィルターを全面的に有効または無効にするには、接続フィルター エージェントを有効または無効にします。Microsoft Exchange トランスポート サービスの再起動後に変更が反映されます。エッジ トランスポート サーバー上で Microsoft Exchange トランスポート サービスを再起動すると、サーバー上のメール フローが一時的に中断されます。

接続フィルターを無効にするには、次のコマンドを実行します。

```powershell
Disable-TransportAgent "Connection Filtering Agent"
```

接続フィルターを有効にするには、次のコマンドを実行します。

```powershell
Enable-TransportAgent "Connection Filtering Agent"
```

変更を有効にするには、次のコマンドを実行して Microsoft Exchange トランスポート サービスを再起動します。

```powershell
Restart-Service MSExchangeTransport
```

## 正常な動作を確認する方法

接続フィルターが正常に有効または無効にされたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled
```

## IP 禁止一覧の手順

これらの手順は、手動で構成する IP 禁止一覧に適用されます。IP 禁止一覧プロバイダーには適用されません。

**IPBlockListConfig** コマンドレットを使用して、接続フィルターの IP 禁止一覧の使用方法を表示し、構成します。**IPBlockListEntry** コマンドレットを使用して、IP 禁止一覧の IP アドレスを表示し、構成します。

## シェルを使用して IP 禁止一覧の構成を表示する

IP 禁止一覧の構成を表示するには、次のコマンドを実行します。

    Get-IPBlockListConfig | Format-List *Enabled,*Response

## シェルを使用してIP 禁止一覧を有効または無効にする

IP 禁止一覧を無効にするには、次のコマンドを実行します。

```powershell
Set-IPBlockListConfig -Enabled $false
```

IP 禁止一覧を有効にするには、次のコマンドを実行します。

```powershell
Set-IPBlockListConfig -Enabled $true
```

## 正常な動作を確認する方法

IP 禁止一覧が正常に有効または無効にされたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPBlockListConfig | Format-List Enabled
```

## シェルを使用して IP 禁止一覧を構成する

IP 禁止一覧を構成するには、次の構文を使用します。

    Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]

この例では、IP 禁止一覧を次の設定を使って構成します。

  - IP 禁止一覧は、内部および外部メール サーバーからの受信接続をフィルター処理します。既定では、外部メール サーバーからの接続のみがフィルター処理されます (*ExternalMailEnabled* は `$true`、*InternalMailEnabled* は `$false` に設定されます)。外部パートナーからの接続は、認証済みかどうかにかかわらず、すべて外部と見なされます。

  - プロトコル分析エージェントの送信者評価機能によって IP 禁止一覧に自動的に追加された IP アドレスによってフィルター処理された接続のカスタム応答テキストは、「IP アドレス {0} からの接続は送信者評価によって拒否されました」という値に設定されます。

  - IP 禁止一覧に手動で追加した IP アドレスによってフィルター処理された接続のカスタム応答テキストは、「IP アドレス {0} は接続フィルターによって拒否されました」という値に設定されます。

<!-- end list -->

    Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."

## 正常な動作を確認する方法

IP 禁止一覧が正常に構成されたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

    Get-IPBlockListConfig | Format-List *MailEnabled,*Response

## シェルを使用して IP 禁止一覧のエントリを表示する

IP 禁止一覧のすべてのエントリを表示するには、次のコマンドを実行します。

```powershell
Get-IPBlockListEntry
```

IP 禁止一覧の各エントリは、整数値によって識別されます。IP 禁止一覧および IP 許可一覧にエントリを追加すると、それらを識別する整数値が昇順に割り当てられます。

IP 禁止一覧から特定のエントリを表示するには、次の構文を使用します。

```powershell
Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

たとえば、IP 禁止一覧で IP アドレス 192.168.1.13 を含むエントリを表示するには、次のコマンドを実行します。

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> <EM>IPAddress</EM> パラメーターを使用した場合に表示される IP 禁止一覧エントリは、個別の IP アドレス、IP アドレス範囲、またはクラスレス ドメイン間ルーティング (CIDR) IP の場合があります。<EM>Identity</EM> パラメーターを使用するには、IP 禁止一覧エントリに割り当てられた整数値を指定します。



## シェルを使用して IP 禁止一覧のエントリを追加する

IP 禁止一覧のエントリを追加するには、次の構文を使用します。

    Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]

次の例では、IP 禁止一覧に IP アドレス範囲が 192.168.1.10 - 192.168.1.15 のエントリを追加し、この IP 禁止一覧エントリが 2014 年 7 月 4 日 15:00 に有効期限切れになるように構成します。

```powershell
Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## 正常な動作を確認する方法

IP 禁止一覧にエントリが正常に追加されたことを確認するには、次のコマンドを実行し、新しい IP 禁止一覧エントリが表示されることを確認します。

```powershell
Get-IPBlockListEntry
```

## シェルを使用して IP 禁止一覧のエントリを削除する

IP 禁止一覧のエントリを削除するには、次の構文を使用します。

```powershell
Remove-IPBlockListEntry <IdentityInteger>
```

次の例では、*Identity* の値が 3 であるエントリを IP 禁止一覧から削除します。

```powershell
Remove-IPBlockListEntry 3
```

次の例では、*Identity* 整数値を使用せずに、IP アドレス 192.168.1.12 を含む IP 禁止一覧エントリを削除します。IP 禁止一覧のエントリには、個別の IP アドレスの場合と IP アドレス範囲の場合があります。

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry
```

## 正常な動作を確認する方法

IP 禁止一覧エントリが正常に削除されたことを確認するには、次のコマンドを実行し、削除した IP 禁止一覧エントリが表示されないことを確認します。

```powershell
Get-IPBlockListEntry
```

## IP 禁止一覧プロバイダーの手順

これらの手順は、IP 禁止一覧プロバイダーに適用されます。IP 禁止一覧には適用されません。

**IPBlockListProvidersConfig** コマンドレットを使用して、接続フィルターでのすべての IP 禁止一覧プロバイダーの使用方法を表示し、構成します。**IPBlockListProvider** コマンドレットを使用して、IP 禁止一覧プロバイダーを表示、構成、およびテストします。

## シェルを使用してすべての IP 禁止一覧プロバイダーの構成を表示する

接続フィルターで使用するすべての IP 禁止一覧プロバイダーの使用方法を表示するには、次のコマンドを実行します。

    Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*

## シェルを使用してすべての IP 禁止一覧プロバイダーを有効または無効にする

すべての IP 禁止一覧プロバイダーを無効にするには、次のコマンドを実行します。

```powershell
Set-IPBlockListProvidersConfig -Enabled $false
```

すべての IP 禁止一覧プロバイダーを有効にするには、次のコマンドを実行します。

```powershell
Set-IPBlockListProvidersConfig -Enabled $true
```

## 正常な動作を確認する方法

すべての IP 禁止一覧プロバイダーが有効または無効にされたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPBlockListProvidersConfig | Format-List Enabled
```

## シェルを使用してすべての IP 禁止一覧プロバイダーを構成する

接続フィルターで使用するすべての IP 禁止一覧プロバイダーの使用方法を構成するには、次のコマンドを実行します。

    Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

次の例では、すべての IP 禁止一覧プロバイダーを次の設定を使って構成します。

  - IP 禁止一覧プロバイダーは、内部および外部メール サーバーからの受信接続をフィルター処理します。既定では、外部メール サーバーからの接続のみがフィルター処理されます (*ExternalMailEnabled* は `$true`、*InternalMailEnabled* は `$false` に設定されます)。外部パートナーからの接続は、認証済みかどうかにかかわらず、すべて外部と見なされます。

  - 内部受信者 chris@fabrikam.com および michelle@fabrikam.com に送信されたメッセージは、IP 禁止一覧プロバイダーによるフィルター処理から除外されます。既存の受信者に影響を与えずに受信者を追加するには、`@{Add="<recipient1>","<recipient2>"...}` の構文を使用します。

<!-- end list -->

    Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true

詳細については、「[Set-IPBlockListProvidersConfig](https://technet.microsoft.com/ja-jp/library/aa998543\(v=exchg.150\))」をご覧ください。

## 正常な動作を確認する方法

すべての IP 禁止一覧プロバイダーが正常に構成されたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

    Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*

## シェルを使用して IP 禁止一覧プロバイダーを表示する

すべての IP 禁止一覧プロバイダーの要約リストを表示するには、次のコマンドを実行します。

```powershell
Get-IPBlockListProvider
```

特定のプロバイダーの詳細を表示するには、次の構文を使用します。

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity>
```

次の例では、Contoso IP Block List Provider というプロバイダーの詳細を表示します。

    Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response

## シェルを使用して IP 禁止一覧プロバイダーを追加する

IP 禁止一覧プロバイダーを追加するには、次の構文を使用します。

    Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

この例では、次のオプションを使用して Contoso IP Block List Provider という IP 禁止一覧プロバイダーを作成します。

  - **プロバイダーを使用するための FQDN**   rbl.contoso.com

  - **プロバイダーから使用するためのビットマスク コード**   127.0.0.1

<!-- end list -->

    Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1


> [!NOTE]
> 新しい IP 禁止一覧プロバイダーを追加すると、新しいプロバイダーは既定で有効 (<EM>Enabled</EM> の値は <CODE>$true</CODE>) になります。追加するプロバイダーごとに優先順位の値が 1 ずつ増加します (最初のエントリの <EM>Priority</EM> 値は 1)。



詳細については、「[Add-IPBlockListProvider](https://technet.microsoft.com/ja-jp/library/bb124358\(v=exchg.150\))」をご覧ください。

## 正常な動作を確認する方法

IP 禁止一覧プロバイダーが正常に追加されたことを確認するには、次のコマンドを実行し、新しい IP 禁止一覧プロバイダーが表示されることを確認します。

```powershell
Get-IPBlockListProvider
```

## シェルを使用して IP 禁止一覧プロバイダーを有効または無効にする

特定の IP 禁止一覧プロバイダーを有効または無効にするには、次の構文を使用します。

```powershell
Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>
```

次の例では、Contoso IP Block List Provider というプロバイダーを無効にします。

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false
```

次の例では、Contoso IP Block List Provider というプロバイダーを有効にします。

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true
```

## 正常な動作を確認する方法

IP 禁止一覧プロバイダーが正常に有効または無効にされたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled
```

## シェルを使用して IP 禁止一覧プロバイダーを構成する

**Set-IPBlockListProvider** コマンドレットに使用できる構成オプションは、**New-IPBlockListProvider** コマンドレットのオプションと同じです。

既存の IP 禁止一覧プロバイダーを構成するには、次の構文を使用します。

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

たとえば、Contoso IP Block List Provider というプロバイダーの既存の状態コードの一覧に IP アドレス状態コード 127.0.0.1 を追加するには、次のコマンドを実行します。

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

詳細については、「[Set-IPBlockListProvider](https://technet.microsoft.com/ja-jp/library/bb124979\(v=exchg.150\))」をご覧ください。

## 正常な動作を確認する方法

IP 禁止一覧プロバイダーが正常に構成されたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List
```

## シェルを使用して IP 禁止一覧プロバイダーをテストする

IP 禁止一覧プロバイダーをテストするには、次の構文を使用します。

```powershell
Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>
```

次の例では、IP アドレス 192.168.1.1 を参照して Contoso IP Block List Provider というプロバイダーをテストします。

```powershell
Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1
```

## シェルを使用して IP 禁止一覧プロバイダーを削除する

IP 禁止一覧プロバイダーを削除するには、次の構文を使用します。

```powershell
Remove-IPBlockListProvider <IPBlockListProviderIdentity>
```

次の例では、Contoso IP Block List Provider という IP 禁止一覧プロバイダーを削除します。

```powershell
Remove-IPBlockListProvider "Contoso IP Block list Provider"
```

## 正常な動作を確認する方法

IP 禁止一覧プロバイダーが正常に削除されたことを確認するには、次のコマンドを実行し、削除した IP 禁止一覧プロバイダーが表示されないことを確認します。

```powershell
Get-IPBlockListProvider
```

## IP 許可一覧の手順

これらの手順は、手動で構成する IP 許可一覧に適用されます。IP 許可一覧プロバイダーには適用されません。

**IPAllowListConfig** コマンドレットを使用して、接続フィルターの IP 許可一覧の使用方法を表示し、構成します。**IPAllowListEntry** コマンドレットを使用して、IP 許可一覧の IP アドレスを表示し、構成します。

## シェルを使用して IP 許可一覧の構成を表示する

IP 許可一覧の構成を表示するには、次のコマンドを実行します。

    Get-IPAllowListConfig | Format-List *Enabled

## シェルを使用してIP 許可一覧を有効または無効にする

IP 許可一覧を無効にするには、次のコマンドを実行します。

```powershell
Set-IPAllowListConfig -Enabled $false
```

IP 許可一覧を有効にするには、次のコマンドを実行します。

```powershell
Set-IPAllowListConfig -Enabled $true
```

## 正常な動作を確認する方法

IP 許可一覧が正常に有効または無効にされたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPAllowListConfig | Format-List *Enabled
```

## シェルを使用して IP 許可一覧を構成する

IP 許可一覧を構成するには、次の構文を使用します。

    Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>

この例では、内部および外部メール サーバーからの受信接続をフィルター処理する IP 許可一覧を構成します。既定では、外部メール サーバーからの接続のみがフィルター処理されます (*ExternalMailEnabled* は `$true`、*InternalMailEnabled* は `$false` に設定されます)。外部パートナーからの接続は、認証済みかどうかにかかわらず、すべて外部と見なされます。

```powershell
Set-IPAllowListConfig -InternalMailEnabled $true
```

## 正常な動作を確認する方法

IP 許可一覧が正常に構成されたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

    Get-IPAllowListConfig | Format-List *MailEnabled

## シェルを使用して IP 許可一覧のエントリを表示する

IP 許可一覧のすべてのエントリを表示するには、次のコマンドを実行します。

```powershell
Get-IPAllowListEntry
```

IP 許可一覧の各エントリは、整数値によって識別されます。IP 禁止一覧および IP 許可一覧にエントリを追加すると、それらを識別する整数値が昇順に割り当てられます。

IP 許可一覧から特定のエントリを表示するには、次の構文を使用します。

```powershell
Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

たとえば、IP 許可一覧で IP アドレス 192.168.1.13 を含むエントリを表示するには、次のコマンドを実行します。

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> <EM>IPAddress</EM> パラメーターを使用した場合に表示される IP 許可一覧エントリは、個別の IP アドレス、IP アドレス範囲、またはクラスレス ドメイン間ルーティング (CIDR) IP の場合があります。<EM>Identity</EM> パラメーターを使用するには、IP 許可一覧エントリに割り当てられた整数値を指定します。



## シェルを使用して IP 許可一覧のエントリを追加する

IP 許可一覧のエントリを追加するには、次の構文を使用します。

    Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]

この例では、IP 許可一覧に IP アドレス範囲が 192.168.1.10 - 192.168.1.15 のエントリを追加し、この IP 許可一覧エントリが 2014 年 7 月 4 日 15:00 に有効期限切れになるように構成します。

```powershell
Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## 正常な動作を確認する方法

IP 許可一覧にエントリが正常に追加されたことを確認するには、次のコマンドを実行し、新しい IP 許可一覧エントリが表示されることを確認します。

```powershell
Get-IPAllowListEntry
```

## シェルを使用して IP 許可一覧のエントリを削除する

IP 許可一覧のエントリを削除するには、次の構文を使用します。

```powershell
Remove-IPAllowListEntry <IdentityInteger>
```

次の例では、*Identity* の値が 3 であるエントリを IP 許可一覧から削除します。

```powershell
Remove-IPAllowListEntry 3
```

この例では、*Identity* 整数値を使用せずに、IP アドレス 192.168.1.12 を含む IP 許可一覧エントリを削除します。IP 許可一覧のエントリには、個別の IP アドレスの場合と IP アドレス範囲の場合があります。

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry
```

## 正常な動作を確認する方法

IP 許可一覧エントリが正常に削除されたことを確認するには、次のコマンドを実行し、削除した IP 許可一覧エントリが表示されないことを確認します。

```powershell
Get-IPAllowListEntry
```

## IP 許可一覧プロバイダーの手順

これらの手順は、IP 許可一覧プロバイダーに適用されます。IP 許可一覧には適用されません。

**IPAllowListProvidersConfig** コマンドレットを使用して、接続フィルターでのすべての IP 許可一覧プロバイダーの使用方法を表示し、構成します。**IPAllowListProvider** コマンドレットを使用して、IP 許可一覧プロバイダーを表示、構成、およびテストします。

## シェルを使用してすべての IP 許可一覧プロバイダーの構成を表示する

接続フィルターで使用するすべての IP 許可一覧プロバイダーの使用方法を表示するには、次のコマンドを実行します。

    Get-IPAllowListProvidersConfig | Format-List *Enabled

## シェルを使用してすべての IP 許可一覧プロバイダーを有効または無効にする

すべての IP 許可一覧プロバイダーを無効にするには、次のコマンドを実行します。

```powershell
Set-IPAllowListProvidersConfig -Enabled $false
```

すべての IP 許可一覧プロバイダーを有効にするには、次のコマンドを実行します。

```powershell
Set-IPAllowListProvidersConfig -Enabled $true
```

## 正常な動作を確認する方法

すべての IP 許可一覧プロバイダーが有効または無効にされたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPAllowListProvidersConfig | Format-List Enabled
```

## シェルを使用してすべての IP 許可一覧プロバイダーを構成する

接続フィルターで使用するすべての IP 許可一覧プロバイダーの使用方法を構成するには、次のコマンドを実行します。

    Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

この例では、すべての IP 許可一覧プロバイダーが内部および外部メール サーバーからの受信接続をフィルター処理するように構成します。既定では、外部メール サーバーからの接続のみがフィルター処理されます (*ExternalMailEnabled* は `$true`、*InternalMailEnabled* は `$false` に設定されます)。外部パートナーからの接続は、認証済みかどうかにかかわらず、すべて外部と見なされます。

```powershell
Set-IPAllowListProvidersConfig -InternalMailEnabled $true
```

詳細については、「[Set-IPBlockListProvidersConfig](https://technet.microsoft.com/ja-jp/library/aa998543\(v=exchg.150\))」をご覧ください。

## 正常な動作を確認する方法

すべての IP 許可一覧プロバイダーが正常に構成されたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

    Get-IPAllowListProvidersConfig | Format-List *MailEnabled

## シェルを使用して IP 許可一覧プロバイダーを表示する

すべての IP 許可一覧プロバイダーの要約リストを表示するには、次のコマンドを実行します。

```powershell
Get-IPAllowListProvider
```

特定のプロバイダーの詳細を表示するには、次の構文を使用します。

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity>
```

この例では、Contoso IP Allow List Provider というプロバイダーの詳細を表示します。

    Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match

## シェルを使用して IP 許可一覧プロバイダーを追加する

IP 許可一覧プロバイダーを追加するには、次の構文を使用します。

    Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

この例では、次のオプションを使用して Contoso IP Allow List Provider という IP 許可一覧プロバイダーを作成します。

  - **プロバイダーを使用するための FQDN**   allow.contoso.com

  - **プロバイダーから使用するためのビットマスク コード**   127.0.0.1

<!-- end list -->

    Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1


> [!NOTE]
> 新しい IP 許可一覧プロバイダーを追加すると、新しいプロバイダーは既定で有効 (<EM>Enabled</EM> の値は <CODE>$true</CODE> になります)。追加するプロバイダーごとに優先順位の値が 1 ずつ増加します (最初のエントリの <EM>Priority</EM> 値は 1)。



詳細については、「[Add-IPBlockListProvider](https://technet.microsoft.com/ja-jp/library/bb124358\(v=exchg.150\))」をご覧ください。

## 正常な動作を確認する方法

IP 許可一覧プロバイダーが正常に追加されたことを確認するには、次のコマンドを実行し、新しい IP 許可一覧プロバイダーが表示されることを確認します。

```powershell
Get-IPAllowListProvider
```

## シェルを使用して IP 許可一覧プロバイダーを有効または無効にする

特定の IP 許可一覧プロバイダーを有効または無効にするには、次の構文を使用します。

```powershell
Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>
```

この例では、Contoso IP Allow List Provider というプロバイダーを無効にします。

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false
```

この例では、Contoso IP Allow List Provider というプロバイダーを有効にします。

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true
```

## 正常な動作を確認する方法

IP 許可一覧プロバイダーが正常に有効または無効にされたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled
```

## シェルを使用して IP 許可一覧プロバイダーを構成する

**Set-IPAllowListProvider** コマンドレットに使用できる構成オプションは、**New-IPAllowListProvider** コマンドレットのオプションと同じです。

既存の IP 許可一覧プロバイダーを構成するには、次の構文を使用します。

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

たとえば、Contoso IP Allow List Provider というプロバイダーの既存の状態コードの一覧に IP アドレス状態コード 127.0.0.1 を追加するには、次のコマンドを実行します。

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

詳細については、「[Set-IPBlockListProvider](https://technet.microsoft.com/ja-jp/library/bb124979\(v=exchg.150\))」をご覧ください。

## 正常な動作を確認する方法

IP 許可一覧プロバイダーが正常に構成されたことを確認するには、次のコマンドを実行し、構成した値が表示されることを確認します。

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List
```

## シェルを使用して IP 許可一覧プロバイダーをテストする

IP 許可一覧プロバイダーをテストするには、次の構文を使用します。

```powershell
Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>
```

次の例では、IP アドレス 192.168.1.1 を参照して Contoso IP Allow List Provider というプロバイダーをテストします。

```powershell
Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1
```

## シェルを使用して IP 許可一覧プロバイダーを削除する

IP 許可一覧プロバイダーを削除するには、次の構文を使用します。

```powershell
Remove-IPAllowListProvider <IPAllowListProviderIdentity>
```

この例では、Contoso IP Allow List Provider という IP 許可一覧プロバイダーを削除します。

```powershell
Remove-IPAllowListProvider "Contoso IP Allow List Provider"
```

## 正常な動作を確認する方法

IP 許可一覧プロバイダーが正常に削除されたことを確認するには、次のコマンドを実行し、削除した IP 許可一覧プロバイダーが表示されないことを確認します。

```powershell
Get-IPAllowListProvider
```

