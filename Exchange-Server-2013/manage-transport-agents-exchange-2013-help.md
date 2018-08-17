---
title: 'トランスポート エージェントの管理: Exchange 2013 Help'
TOCTitle: トランスポート エージェントの管理
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 49896548
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート エージェントの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

トランスポート エージェントは、メッセージがトランスポート パイプラインを移動する際に、SMTP イベントを使用してメッセージを操作します。Microsoft Exchange Server 2013 に含まれるほとんどのビルトイン トランスポート エージェントは、表示も管理もできません。ただし、組織内の Exchange サーバーにサードパーティ製のトランスポート エージェントをインストールして構成できます。トランスポート エージェントの詳細については、「[トランスポート エージェント](transport-agents-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート エージェント」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 従来のトランスポート エージェントのサポートは既定では有効ではありませんが、有効にすることはできます。手順については、「[従来のトランスポート エージェントのサポートを有効にする](enable-support-for-legacy-transport-agents-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## クライアント アクセス サーバー上のフロント エンド トランスポート サービスでのトランスポート エージェント手順について

Exchange 管理シェルを使用して、クライアント アクセス サーバー上のフロント エンド トランスポート サービスのトランスポート エージェントを管理することはできません。その代わりに、クライアント アクセス サーバーで、Windows PowerShell を開いて、Exchange コマンドレットを Windows PowerShell セッションにインポートする必要があります。


> [!NOTE]
> フロント エンド トランスポート サービスのトランスポート エージェントの管理以外のタスクでは、Windows PowerShell で Exchange コマンドレットを実行することはできません。Windows PowerShell で Exchange コマンドレットを実行することで、Exchange 管理シェルと役割ベースのアクセス制御 (RBAC) をバイパスすると、深刻な結果につながることがあります。Exchange コマンドレットは必ず Exchange 管理シェルで実行してください。詳細については、「<A href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 のリリース ノート</A>」を参照してください。



フロント エンド トランスポート サービスでこのトピックで説明するトランスポート エージェントの手順のいずれかを実行する場合は、次の追加ステップを実行する必要があります。

1.  クライアント アクセス サーバーで、Windows PowerShell を開いて次のコマンドを実行します。
    
        Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

2.  コマンドは記述どおりに実行してください。ただし、次の値を追加してください。`-TransportService FrontEnd`.
    
    たとえば、クライアント アクセス サーバー上のフロントエンド トランスポート サービスのトランスポート エージェントを表示するには、次のコマンドを実行します。
    
        Get-TransportAgent -TransportService FrontEnd

## シェルを使用してトランスポート エージェントをインストールする

トランスポート エージェントをインストールする際、Exchange が行うのは、トランスポート エージェントに関連付けられる DLL の登録だけです。トランスポート エージェントが使用するすべてのファイル、レジストリ キー、およびその他のオブジェクトが正しくインストールされ、構成されていることを確認する必要があります。Exchange で DLL が読み込まれると、コマンドが完了した後も DLL を引き続き参照します。

トランスポート エージェントは、受信したすべての電子メール メッセージにフル アクセスできます。Exchange には、トランスポート エージェントの動作に対する制限はありません。トランスポート エージェントが不安定であったり、セキュリティ上の欠陥が含まれていたりすると、Exchange の安定性やセキュリティに影響を与えることがあります。したがって、トランスポート エージェントをインストールするときは、信頼性があり、テスト環境で十分にテストされたエージェントだけをインストールすることをお勧めします。

トランスポート エージェントは、無効な状態でインストールされます。これは、未構成のトランスポート エージェントによってメール フローに影響が出ないようにするためです。したがってトランスポート エージェントが正しく構成された後に、これを有効にする必要があります。

次の構文を使用してトランスポート エージェントをインストールします。

    Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">

この例では、メールボックス サーバーのトランスポート サービスで Contoso Transport Agent という架空のトランスポート エージェントがインストールされます。

    Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"

## 正常な動作を確認する方法

トランスポート エージェントが正常にインストールされたことを確認するには、`Get-TransportAgent` コマンドを実行して、トランスポート エージェントが一覧に表示されることを確認します。

## シェルを使用してトランスポート エージェントを有効にする

次の構文を使用してトランスポート エージェントを有効にします。

    Enable-TransportAgent <TransportAgentIdentity>

この例では、メールボックス サーバーのトランスポート サービスで Contoso Transport Agent という名前のトランスポート エージェントが有効になります。

    Enable-TransportAgent "Contoso Transport Agent"

## 正常な動作を確認する方法

トランスポート エージェントが正常に有効になったことを確認するには、コマンド `Get-TransportAgent | Format-List Name,Enabled` を実行して、トランスポート エージェントが有効になっていることを確認します。

## シェルを使用してトランスポート エージェントを無効にする

次の構文を使用してトランスポート エージェントを無効にします。

    Disable-TransportAgent <TransportAgentIdentity>

この例では、メールボックス サーバーのトランスポート サービスで Fabirkam Transport Agent という名前のトランスポート エージェントが無効になります。

    Disable-TransportAgent "Fabrikam Transport Agent"

## 正常な動作を確認する方法

トランスポート エージェントが正常に無効になったことを確認するには、コマンド `Get-TransportAgent | Format-List Name,Enabled` を実行して、トランスポート エージェントが無効になっていることを確認します。

## シェルを使用してトランスポート エージェントを表示する

トランスポート エージェントの要約リストを表示するには、次のコマンドを実行します。

    Get-TransportAgent

特定のトランスポート エージェントの詳細な構成を表示するには、次のコマンドを実行します。

    Get-TransportAgent <TransportAgentIdentity> | Format-List

この例では、Transport Rule Agent という名前のトランスポート エージェントの詳細な構成が提供されます。

    Get-TransportAgent "Transport Rule Agent" | Format-List

## シェルを使用してトランスポート エージェントの優先度を構成する

最も 0 に近い優先度を持つトランスポート エージェントが、最初に電子メール メッセージを処理します。ただし、トランスポート エージェントが登録されているトランスポート パイプラインで発生する SMTP イベントが原因で、優先度の低いエージェントが高いエージェントより先にメッセージを処理することがあります。

既存のトランスポート エージェントの優先度を変更するには、次のコマンドを実行します。

    Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>

この例では、メールボックス サーバーのトランスポート サービスの Contoso Transport Agent という名前の既存のトランスポート エージェントに優先エージェントの値 3 が設定されます。

    Set-TransportAgent "Contoso Transport Agent" -Priority 3

## 正常な動作を確認する方法

トランスポート エージェントの優先度を正常に構成したことを確認するには、コマンド `Get-TransportAgent | Format-List Name,Priority` を実行して、トランスポート エージェントの優先度の値を確認します。

## シェルを使用してトランスポート エージェントをアンインストールする

トランスポート エージェントがアンインストールされると、Exchange はそのエージェントで使用されていた DLL ファイルの登録を解除します。トランスポート エージェントのインストールによって追加されたファイル、レジストリ キー、またはその他のオブジェクトは削除されません。

トランスポート エージェントをアンインストールするには、次のコマンドを実行します。

    Uninstall-TransportAgent <TransportAgentIdentity>

この例では、メールボックス サーバーのトランスポート サービスから Fabirkam Transport Agent という名前のトランスポート エージェントがアンインストールされます。

    Uninstall-TransportAgent "Fabrikam Transport Agent"

## 正常な動作を確認する方法

トランスポート エージェントが正常にアンインストールされたことを確認するには、コマンド `Get-TransportAgent` を実行して、トランスポート エージェントが一覧に表示されていないことを確認します。

