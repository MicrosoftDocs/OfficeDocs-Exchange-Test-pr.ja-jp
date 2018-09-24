---
title: 'エッジ トランスポート サーバー上でアドレス書き換えを管理する: Exchange 2013 Help'
TOCTitle: エッジ トランスポート サーバー上でアドレス書き換えを管理する
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61060532
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# エッジ トランスポート サーバー上でアドレス書き換えを管理する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

エッジ トランスポート サーバー上では、アドレス書き換えに関連したすべての管理タスクとアドレス書き換えエージェントに対して Exchange 管理シェルを使用します。アドレス書き換えの詳細については、「[エッジ トランスポート サーバー上でのアドレス書き換え](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)」を参照してください。

単一の受信者、特定のドメインまたはサブドメイン内のすべての受信者、あるいは複数のサブドメイン内のすべての受信者に適用されるアドレス書き換えエントリを作成できます。アドレス書き換えは、送信のみで行うことも、受信と送信 (双方向) で行うこともできます。アドレス書き換えエントリを作成する場合は、次の点に注意してください。

  - 生成される電子メール アドレスが組織内で一意であることを確認します。

  - 電子メール アドレス値でサポートされるのはリテラル文字列のみです。

  - ワイルドカード文字 (\*) は内部アドレス (変更するアドレス) でのみサポートされます。ワイルドカード文字を使用するための有効な構文は **\*.contoso.com** です。**\*contoso.com** や **sales.\*.com** という値は許可されません。

  - ワイルドカード文字を使用する場合は、アドレス書き換えを送信のみとして構成する必要があります (*OutboundOnly* パラメーターの値を `$true` に設定する必要があります)。

  - 送信のみのアドレス書き換えを構成する (*OutboundOnly* パラメーターの値を `$true` に設定する) 場合は、影響を受ける受信者でプロキシ アドレスを構成する必要があります。これにより、書き換えられたアドレスに送信されたメールが正しく配信されます。

  - 既定では、アドレス書き換えは単一の受信者または特定のドメインまたはサブドメイン内のすべての受信者に対して双方向です (*OutboundOnly* パラメーターの既定値は `$false` です)。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「エッジ トランスポート サーバー」。

  - この手順を実行するには、シェルを使用する必要があります。

  - アドレス書き換えを構成するタイミングに注意してください。すべての変更はコマンドの実行時に直ちに適用されます。*WhatIf* パラメーターを使用したコマンドの実行を検討します。*WhatIf* パラメーターの詳細については、「[WhatIf、Confirm、および ValidateOnly スイッチ](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してアドレス書き換えを有効または無効にする

アドレス書き換えを全面的に有効または無効にするには、アドレス書き換えエージェントを有効または無効にします。既定では、エッジ トランスポート サーバー上でアドレス書き換えエージェントが有効になっています。

アドレス書き換えを無効にするには、次のコマンドを実行します。

```powershell
Disable-TransportAgent "Address Rewriting Inbound Agent"
Disable-TransportAgent "Address Rewriting Outbound Agent"
```

アドレス書き換えを有効にするには、次のコマンドを実行します。

```powershell
Enable-TransportAgent "Address Rewriting Inbound Agent"
Enable-TransportAgent "Address Rewriting Outbound Agent"
```

## 正常な動作を確認する方法

アドレス書き換えが正常に有効または無効にされたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
    ```powershell
    Get-TransportAgent
    ```

2.  受信用アドレス書き換えエージェントと送信用アドレス書き換えエージェントの **Enabled** プロパティの値が構成した値になっていることを確認します。

## シェルを使用してアドレス書き換えエントリを表示する

すべてのアドレス書き換えエントリの要約リストを表示するには、次のコマンドを実行します。

```powershell
Get-AddressRewriteEntry
```

アドレス書き換えエントリの詳細を表示するには、次の構文を使用します。

```powershell
Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List
```

次の例では、Rewrite Contoso.com to Northwindtraders.com という名前のアドレス書き換えエントリの詳細を表示します。

```powershell
Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List
```

## シェルを使用してアドレス書き換えエントリを作成する

## 1 人の受信者の電子メール アドレスを書き換える

1 人の受信者の電子メール アドレスを書き換えるには、次の構文を使用します。

```powershell
New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]
```

次の例では、受信者 joe@contoso.com の Exchange 組織に出入りするすべてのメッセージの電子メール アドレスを書き換えます。送信メッセージは、support@nortwindtraders.com から到着したように書き換えられます。support@northwindtraders.com に送信された受信メッセージは joe@contoso.com に書き換えられて受信者に配信されます (既定で、*OutboundOnly* パラメーターは `$false` です)。

```powershell
New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com
```

## 単一のドメインまたはサブドメイン内の受信者の電子メール アドレスを書き換える

単一のドメインまたはサブドメイン内の受信者の電子メール アドレスを書き換えるには、次の構文を使用します。

```powershell
New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]
```

次の例では、contoso.com ドメイン内の受信者の Exchange 組織に出入りするすべてのメッセージの電子メール アドレスを書き換えます。送信メッセージは、fabrikam.com ドメインから到着したように書き換えられます。fabrikam.com 電子メール アドレスに送信された受信メッセージは contoso.com に書き換えられて受信者に配信されます (既定で、*OutboundOnly* パラメーターは `$false` です)。

```powershell
New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com
```

次の例では、sales.contoso.com サブドメイン内の受信者から送信された、Exchange 組織を離れるすべてのメッセージの電子メール アドレスを書き換えます。送信メッセージは、contoso.com ドメインから到着したように書き換えられます。contoso.com 電子メール アドレスに送信された受信メッセージは書き換えられません。

```powershell
New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true
```

## 複数のサブドメイン内の受信者の電子メール アドレスを書き換える

1 つのドメインのすべてのサブドメイン内の受信者の電子メール アドレスを書き換えるには、次の構文を使用します。

```powershell
New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]
```

次の例では、contoso.com ドメインとすべてのサブドメイン内の受信者から送信された、Exchange 組織を離れるすべてのメッセージの電子メール アドレスを書き換えます。送信メッセージは、contoso.com ドメインから到着したように書き換えられます。*InternalAddress* パラメーターにワイルドカードが使用されているため、contoso.com 受信者に送信された受信メッセージを書き換えることはできません。

```powershell
New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true
```

次の例は、legal.contoso.com サブドメインと corp.contoso.com サブドメイン内の受信者から送信されたメッセージが書き換えられないことを除いて、1 つ前の例と同様です。

```powershell
New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com
```

## 正常な動作を確認する方法

アドレス書き換えエントリが正常に作成されたことを確認するには、次の手順を実行します。

1.  `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` コマンドを実行して、表示された設定が構成した設定であることを確認します。

2.  アドレス書き換えエントリの影響を受けるメールボックスから、外部のメールボックスにテスト メッセージを送信します。テスト メッセージが、書き換えられた電子メール アドレスから送信されたように見えることを確認します。

3.  外部のメールボックスからテスト メッセージに返信します。元のメールボックスに返信が届くことを確認します。

## シェルを使用してアドレス書き換えエントリを変更する

既存のアドレス書き換えエントリの変更時に使用可能な構成オプションは、新しいアドレス書き換えエントリの作成時の構成オプションと全く同じです。

## 1 人の受信者のアドレス書き換えエントリを変更する

1 人の受信者の電子メール アドレスを書き換えるアドレス書き換えエントリを変更するには、次の構文を使用します。

```powershell
Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>
```

次の例では、"joe@contoso.com to support@nortwindtraders.com" という名前の単一受信者アドレス書き換えエントリの次のプロパティを変更します。

  - 外部アドレスを support@northwindtraders.net に変更します。

  - アドレス書き換えエントリの名前を "Joe@contoso.com to support@northwindtraders.net" に変更します。

  - *OutboundOnly* の値を `$true` に変更します。この変更では support@northwindtraders.net を Joe のメールボックスでプロキシ アドレスとして構成する必要があることに注意してください。

<!-- end list -->

```powershell
Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true
```

## 単一のドメインまたはサブドメイン内の受信者のアドレス書き換えエントリを変更する

単一のドメインまたはサブドメインからの受信者の電子メール アドレスを書き換えるアドレス書き換えエントリを変更するには、次の構文を使用します。

```powershell
Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>
```

次の例では、"Northwind Traders to Contoso" いう名前の単一ドメイン アドレス書き換えエントリの内部アドレス値を変更します。

```powershell
Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net
```

## 複数のサブドメイン内の受信者のアドレス書き換えエントリを変更する

1 つのドメインとすべてのサブドメイン内の受信者の電子メール アドレスを書き換えるアドレス書き換えエントリを変更するには、次の構文を使用します。

```powershell
Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>
```

複数サブドメイン アドレス書き換えエントリの既存の例外リストの値を置き換えるには、次の構文を使用します。

```powershell
Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>
```

次の例では、marketing.contoso.com と legal.contoso.com という値を持つ、"Contoso to Northwind Traders" という名前の複数サブドメイン アドレス書き換えエントリの既存の例外リストを置き換えます。

```powershell
Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com
```

既存の例外リストの値を変更せずに、複数サブドメイン アドレス書き換えエントリに対して選択的に例外リストの値を追加または削除するには、次の構文を使用します。

```powershell
Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}
```

次の例では、"Contoso to Northwind Traders" という名前の複数サブドメイン アドレス書き換えエントリの例外リストに対して、finanace.contoso.com を追加し、marketing.contoso.com を削除します。

```powershell
Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}
```

## 正常な動作を確認する方法

アドレス書き換えエントリが正常に変更されたことを確認するには、次の手順を実行します。

1.  `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` コマンドを実行して、表示された設定が構成した設定と同じであることを確認します。

2.  アドレス書き換えエントリの影響を受けるメールボックスから、外部のメールボックスにテスト メッセージを送信します。テスト メッセージが、書き換えられた電子メール アドレスから送信されたように見えることを確認します。

3.  外部のメールボックスから、テスト メッセージに返信します。元のメールボックスに返信が届くことを確認します。

## シェルを使用してアドレス書き換えエントリを削除する

単一のアドレス書き換えエントリを削除するには、次の構文を使用します。

```powershell
Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>
```

次の例では、"Contoso.com to Northwindtraders.com"という名前のアドレス書き換えエントリを削除します。

```powershell
Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"
```

複数のアドレス書き換えエントリを削除するには、次の構文を使用します。

```powershell
Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]
```

次の例では、すべてのアドレス書き換えエントリを削除します。

```powershell
Get-AddressRewriteEntry | Remove-AddressRewriteEntry
```

次の例は、名前に "to contoso.com" というテキストが含まれるアドレス書き換えエントリの削除をシミュレートします。*WhatIf* スイッチを使用すれば、変更をコミットせずに、結果をプレビューすることができます。

```powershell
Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf
```

結果に問題がなければ、*WhatIf* スイッチを使用せずにもう一度コマンドを実行して、アドレス書き換えエントリを削除します。

```powershell
Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry
```

## 正常な動作を確認する方法

アドレス書き換えエントリが正常に削除されたことを確認するには、次の手順を実行します。

1.  `Get-AddressRewriteEntry` コマンドを実行して、削除したアドレス書き換えエントリがリストに掲載されていないことを確認します。

2.  アドレス書き換えエントリの影響を受けるメールボックスから、外部のメールボックスにテスト メッセージを送信します。テスト メッセージが削除したアドレス書き換えエントリの影響を受けていないことを確認します。

3.  外部のメールボックスから、テスト メッセージに返信します。元のメールボックスに返信が届いたことと、メッセージが削除したアドレス書き換えエントリの影響を受けていないことを確認します。

