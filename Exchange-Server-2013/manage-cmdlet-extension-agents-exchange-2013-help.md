---
title: 'コマンドレット拡張エージェントの管理: Exchange 2013 Help'
TOCTitle: コマンドレット拡張エージェントの管理
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50555816
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# コマンドレット拡張エージェントの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-19_

このトピックでは、Microsoft Exchange Server 2013 のコマンドレット拡張エージェントの優先度の有効化、無効化、表示、および変更を行う方法を示します。Exchange 2013 のコマンドレット拡張エージェントの詳細については、「[コマンドレット拡張エージェント](cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分未満

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「コマンドレット拡張エージェント」。

  - `Scripting Agent` を有効にする前に、それが正しく構成されていることを確認する必要がある。`Scripting Agent` の詳細については、「[コマンドレット拡張エージェント](cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## コマンドレット拡張エージェントを有効にする

Exchange 2013 のコマンドレット拡張エージェントを有効にすると、Exchange 2013 が実行されている組織内のすべてのサーバーでエージェントが実行されます。有効にしたエージェントはコマンドレットから使用可能になり、コマンドレットはそのエージェントを使用して追加の操作を実行できます。


> [!NOTE]
> エージェントを有効にする場合は、その前に、エージェントの動作とエージェントが組織に与える影響を把握してください。



この例では、**Enable-CmdletExtensionAgent** コマンドレットを使用してコマンドレット拡張エージェントを有効にします。コマンドレットを実行するときには有効にするエージェント名を指定する必要があります。`Scripting Agent` を有効にする前に、まず `ScriptingAgentConfig.xml` 構成ファイルが組織内のすべてのサーバーに展開されていることを確認する必要があります。構成ファイルを展開せずに `Scripting Agent` を有効にした場合は、**Get** コマンドレット以外のコマンドレットは実行しても失敗します。この例では、`Scripting Agent` を有効にします。

    Enable-CmdletExtensionAgent "Scripting Agent"

構文およびパラメーターの詳細については、「[Enable-CmdletExtensionAgent](https://technet.microsoft.com/ja-jp/library/dd335192\(v=exchg.150\))」を参照してください。

## コマンドレット拡張エージェントを無効にする

Exchange 2013 でコマンドレット拡張エージェントを無効にすると、Exchange 2013 を実行している組織内のすべてのサーバーでエージェントが無効になります。エージェントが無効の場合、コマンドレットがエージェントを使用できなくなります。コマンドレットは、追加の操作を行うために、エージェントを使用できなくなります。


> [!NOTE]
> エージェントを無効にする場合は、その前に、エージェントの動作とエージェントを無効にすることが組織に与える影響を把握してください。



コマンドレット拡張エージェントを無効にするには、**Disable-CmdletExtensionAgent** コマンドレットを使用します。コマンドレットを実行する場合は、無効にするエージェントの名前を指定します。この例では、`Scripting Agent` を無効にします。

    Disable-CmdletExtensionAgent "Scripting Agent"

構文およびパラメーターの詳細については、「[Disable-CmdletExtensionAgent](https://technet.microsoft.com/ja-jp/library/dd298132\(v=exchg.150\))」を参照してください。

## 既存のコマンドレット拡張エージェントを表示する

コマンドレット拡張エージェントの表示により、Exchange 2013 組織において最初に実行されるエージェントおよび有効なエージェントを確認できます。パイプラインと **Format-Table** コマンドレットの詳細については、以下のトピックを参照してください。

  - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))

  - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

この例では、**Get-CmdletExtensionAgent** コマンドレットを使用して特定のコマンドレット拡張エージェントの詳細を取得します。この例では、`Mailbox Permissions Agent` の詳細が返されます。

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

この例では、**Get-CmdletExtensionAgent** コマンドレットを使用して複数のコマンドレット拡張エージェントを取得してから、出力結果を **Format-Table** コマンドレットにパイプ処理します。この例では、組織内のすべてのコマンドレット拡張エージェントの一覧を表示します。**Format-Table** コマンドレットを使用することで、各エージェントの **Name**、**Enabled**、および **Priority** プロパティが表形式で表示されます。

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

構文およびパラメーターの詳細については、「[Get-CmdletExtensionAgent](https://technet.microsoft.com/ja-jp/library/dd297946\(v=exchg.150\))」を参照してください。

## コマンドレット拡張エージェントの優先度を変更する

Exchange 2013 でコマンドレット拡張エージェントの優先度を変更する機能は、コマンドレットによって特定のエージェントを呼び出してから別のエージェントを呼び出す場合に便利です。これは、`Scripting Agent` で実行されるカスタム スクリプトを作成して、そのスクリプトをビルトイン エージェントよりも優先させる場合に、特に役立ちます。`Scripting Agent` の詳細については、「[コマンドレット拡張エージェント](cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 優先度の変更またはビルトイン エージェントの機能の置き換えは、高度な操作です。変更について完全に理解するようにしてください。



エージェントは、ゼロからエージェントの最大数まで並べられます。ゼロに近いエージェントは、エージェント優先度が高くなります。優先度の高いエージェントが最初に呼び出されます。エージェント優先度の詳細については、「[コマンドレット拡張エージェント](cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

この例では、**Set-CmdletExtensionAgent** コマンドレットの使用により、コマンドレット拡張エージェントの優先度を変更します。この例では、`Scripting Agent` の優先度を 3 に変更します。

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

構文とパラメーターの詳細については、「[Set-CmdletExtensionAgent](https://technet.microsoft.com/ja-jp/library/dd335175\(v=exchg.150\))」を参照してください。

