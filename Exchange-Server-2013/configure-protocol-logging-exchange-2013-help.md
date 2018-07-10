---
title: 'プロトコル ログ出力を構成する: Exchange 2013 Help'
TOCTitle: プロトコル ログ出力を構成する
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 49896468
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# プロトコル ログ出力を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-03-15_

プロトコル ログ出力では、送信コネクタおよび受信コネクタ上でメッセージ配信の一部として行われる SMTP 通信が記録されます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「Transport Service (トランスポート サービス)」、「Front End Transport service (フロント エンド トランスポート サービス)」、「Mailbox Transport service (メールボックス トランスポート サービス)」、「Receive connectors (受信コネクタ)」、および「Send connectors (送信コネクタ)」。

  - Exchange 管理センター (EAC) を使用して、メールボックス サーバー上のトランスポート サービスの送信コネクタ/受信コネクタ、およびクライアント アクセス サーバー上のフロント エンド トランスポート サービスの受信コネクタのプロトコル ログ出力を有効または無効にできます。EAC を使用して、トランスポート サービス専用のプロトコル ログのパスを構成することもできます。他のすべてのプロトコル ログ出力オプションの場合は、シェルを使用する必要があります。

  - プロトコル ログ出力の有効化または無効化は、コネクタごとに行います。Exchange サーバー上のすべての受信コネクタでは、同一のプロトコル ログ ファイルおよびプロトコル ログ オプションが共有されます。これらのプロトコル ログ設定は、同じサーバーの送信コネクタのプロトコル ログ ファイルやプロトコル ログ オプションとは別になっています。

  - 
    

    > [!NOTE]
    > EdgeSync を使用して Exchange 組織にサブスクライブしたエッジ トランスポート サーバーでは、この手順を実行しないでください。代わりに、メールボックス サーバーのトランスポート サービスで変更を行います。この変更は、次に EdgeSync 同期が行われるときにエッジ トランスポート サーバーにレプリケートされます。



  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してプロトコル ログを構成する

EAC を使用して、メールボックス サーバー上のトランスポート サービスの送信コネクタ/受信コネクタ、またはクライアント アクセス サーバー上のフロント エンド トランスポート サービスの受信コネクタのプロトコル ログ出力を有効または無効にするには、次の手順を実行します。

1.  EAC で、**\[メール フロー\]** \> **\[送信コネクタ\]** または **\[メール フロー\]** \> **\[受信コネクタ\]**に移動します。

2.  構成するコネクタを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[プロトコルのログ出力レベル\]** セクションの **\[全般\]** タブで、次のいずれかのオプションを選択します。
    
      - **\[なし\]**   コネクタ上でのプロトコル ログ出力は無効になります。
    
      - **\[詳細\]**   コネクタ上でのプロトコル ログ出力は有効になります。
    
    完了したら、**\[保存\]** をクリックします。

EAC を使用して、メールボックス サーバー上のトランスポート サービスにおける送信コネクタおよび受信コネクタのプロトコル ログのパスを構成するには、次の手順を実行します。

1.  EAC で **\[サーバー\]** \> **\[サーバー\]** に移動します。

2.  構成するメールボックス サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバーのプロパティ ページで、**\[トランスポート ログ\]** をクリックします。

4.  **\[プロトコル ログ\]** セクションで、次のいずれかの設定を変更します。
    
      - **\[送信プロトコル ログのパス\]**   指定する値は、ローカルの Exchange サーバー上にある必要があります。フォルダーが存在しない場合は、**\[保存\]** をクリックするとフォルダーが作成されます。
    
      - **\[受信プロトコル ログのパス\]**   指定する値は、ローカルの Exchange サーバー上にある必要があります。フォルダーが存在しない場合は、**\[保存\]** をクリックするとフォルダーが作成されます。
    
    完了したら、**\[保存\]** をクリックします。

## 正常な動作を確認する方法

EACを使用してプロトコル ログ設定が正常に構成されたことを確認するには、次の手順を実行します。

1.  送信コネクタまたは受信コネクタのプロトコル ログに対して指定した場所を参照します。

2.  プロトコル ログを有効にした場合は、ログ ファイルが作成されていることを確認します。プロトコル ログを無効にした場合は、最新のログ ファイルが更新されていないことを確認します。

## シェルを使用して送信コネクタまたは受信コネクタでのプロトコル ログ出力を有効または無効にする

送信コネクタまたは受信コネクタ上でのプロトコル ログ出力を有効または無効にするには、次のコマンドを実行します。

    <Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>

この例では、Connection from Contoso.com という名前の受信コネクタのプロトコル ログ出力を有効にします。

    Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose

## 正常な動作を確認する方法

プロトコル ログ出力が正常に有効化または無効化されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel

2.  表示された値が構成した値であることを確認します。

## シェルを使用して組織内の送信コネクタでのプロトコル ログ出力を有効または無効にする

メールボックス サーバー上のトランスポート サービスおよびクライアント アクセス サーバー上のフロント エンド トランスポート サービスに存在する、暗黙的な不可視の組織内送信コネクタ上でのプロトコル ログ出力を有効または無効にするには、次のコマンドを実行します。

    <Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>

この例では、Mailbox01 というメールボックス サーバー上のトランスポート サービスの組織内送信コネクタ上でのプロトコル ログ出力を有効にします。

    Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose

## 正常な動作を確認する方法

組織内送信コネクタ上でのプロトコル ログ出力が正常に有効化または無効化されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel

2.  表示された値が構成した値であることを確認します。

## シェルを使用してメールボックス配信の送信コネクタでのプロトコル ログ出力を有効または無効にする

メールボックス サーバー上のメールボックス トランスポート サービスに存在する、暗黙的な不可視のメールボックス配信の送信コネクタ上でのプロトコル ログ出力を有効または無効にするには、次のコマンドを実行します。

    Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>

この例では、Mailbox01 というメールボックス サーバー上のメールボックス トランスポート サービスの、メールボックス配信の送信コネクタ上でのプロトコル ログ出力を有効にします。

    Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose

## 正常な動作を確認する方法

メールボックス配信コネクタ上でのプロトコル ログ出力が正常に有効化または無効化されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel

2.  表示された値が構成した値であることを確認します。

## シェルを使用してプロトコル ログ出力設定を構成する

プロトコル ログ出力設定を構成にするには、次のコマンドを実行します。

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>

この例では、Mailbox01 というメールボックス サーバー上のトランスポート サービスにおいて、次のようなプロトコル ログ設定を行います。

  -  すべての受信コネクタのプロトコル ログの場所を D:\\Hub Receive SMTP Log に設定し、すべての送信コネクタのプロトコル ログを D:\\Hub Send SMTP Log に設定します。フォルダーが存在しない場合は、新たに作成されます。

  -  受信コネクタのプロトコル ログ ファイルおよび送信コネクタのプロトコル ログ ファイルの最大サイズを、20 MB に設定します。

  -  受信コネクタのプロトコル ログ フォルダーおよび送信コネクタのプロトコル ログ フォルダーの最大サイズを、400 MB に設定します。

  -  受信コネクタのプロトコル ログ ファイルおよび送信コネクタのプロトコル ログ ファイルの最大保存期間を、45 日に設定します。

<!-- end list -->

    Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>メールボックス サーバー上のメールボックス トランスポート サービスのプロトコル ログ設定を構成するには、<STRONG>Set-MailboxTransportService</STRONG> コマンドレットを使用します。クライアント アクセス サーバー上のフロント エンド トランスポート サービスのプロトコル ログ設定を構成するには、<STRONG>Set-FrontEndTransportService</STRONG> コマンドレットを使用します。</P>
> <LI>
> <P><EM>SendProtocolLogPath</EM> パラメーターまたは <EM>ReceiveProtocolLogPath</EM> パラメーターの値を <CODE>$null</CODE> に設定すると、そのサーバーのすべての送信コネクタまたはすべての受信コネクタでプロトコル ログ出力を効率的に無効にできます。ただし、組織内送信コネクタまたはメールボックス配信の送信コネクタを含むサーバー上の他のいずれかのコネクタにおいてプロトコル ログ出力が有効になっている場合に、これらのパラメータを<CODE>$null</CODE> に設定すると、イベント ログ エラーが発生します。</P>
> <LI>
> <P><EM>ReceiveProtocolLogMaxAge</EM> パラメーターまたは <EM>SendProtocolLogMaxAge</EM> パラメーターの値を <CODE>00:00:00</CODE> に設定すると、プロトコル ログ ファイルが保存期間によって自動的に削除されなくなります。</P></LI></UL>



## 正常な動作を確認する方法

プロトコル ログ設定が正常に構成されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*

2.  表示された値が構成した値であることを確認します。

