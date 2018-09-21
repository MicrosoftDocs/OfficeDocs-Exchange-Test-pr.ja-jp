---
title: 'アドレス帳ポリシー ルーティング エージェントをインストールおよび構成する: Exchange 2013 Help'
TOCTitle: アドレス帳ポリシー ルーティング エージェントをインストールおよび構成する
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51407513
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アドレス帳ポリシー ルーティング エージェントをインストールおよび構成する

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2014-01-09_

メールボックス サーバーで動作するトランスポート エージェントであるアドレス帳ポリシー ルーティング エージェントは、組織において受信者を解決する方法を制御します。ABP ルーティング エージェントがインストールおよび構成されると、異なる GAL を割り当てられたユーザーは外部受信者として表示されるようになり、この場合、外部受信者の連絡先カードは表示できません。

ABP に関連する追加の管理タスクについては、「[アドレス帳ポリシーの手順](address-book-policy-procedures-exchange-2013-help.md)」を参照してください。

このトピックの Exchange Online バージョンについては、「[アドレス帳ポリシー ルーティング \[オンライン\] を有効にする](https://technet.microsoft.com/ja-jp/library/jj891095\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:15 分。

  - ABP ルーティング エージェントをインストールおよび構成した後、エージェントが組織の電子メールを評価するまでに最大 30 分かかることがあります。

  - EAC を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:ABP ルーティング エージェントをインストールする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート エージェント」。

次のコマンドを実行し、ABP ルーティング エージェントをインストールします。このコマンドと構文をこのまま使用する必要があります。

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

変更を有効にするためにトランスポート サービスの再起動が必要という警告が表示されますが、先に手順 2 を実行すると、トランスポート サービスの再起動は 1 回で済みます。

構文およびパラメーターの詳細については、「[Install-TransportAgent](https://technet.microsoft.com/ja-jp/library/aa997998\(v=exchg.150\))」を参照してください。

## 手順 2:トランスポート ルーティング エージェントを有効にする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート エージェント」。

ABP ルーティング エージェントをインストールしたら、次のコマンドを実行して有効にする必要があります。

```powershell
Enable-TransportAgent "ABP Routing Agent"
```

構文およびパラメーターの詳細については、「[Enable-TransportAgent](https://technet.microsoft.com/ja-jp/library/bb124921\(v=exchg.150\))」を参照してください。

## 手順 3:トランスポート サービスを再起動し、ABP ルーティング エージェントがインストールされて有効になっていることを確認する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート エージェント」。

1.  次のコマンドを実行して、トランスポート サービスを再起動します。
    
    ```powershell
Restart-Service MSExchangeTransport
```

2.  サービスの再起動後に次のコマンドレットを実行し、ABP ルーティング エージェントがインストールされて有効になっていることを確認します。
    
    ```powershell
Get-TransportAgent
```
    
    ABP ルーティング エージェントが一覧表示される場合、エージェントは正しくインストールされています。

構文およびパラメーターの詳細については、「[Get-TransportAgent](https://technet.microsoft.com/ja-jp/library/bb123536\(v=exchg.150\))」を参照してください。

## 手順 4:ABP ルーティング エージェントを有効にする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート構成」。

このプロセスの最終手順では、組織で ABP ルーティングを有効にします。次のコマンドを実行します。

```powershell
Set-TransportConfig -AddressBookPolicyRoutingEnabled $true
```

構文およびパラメーターの詳細については、「[Set-TransportConfig](https://technet.microsoft.com/ja-jp/library/bb124151\(v=exchg.150\))」を参照してください。

