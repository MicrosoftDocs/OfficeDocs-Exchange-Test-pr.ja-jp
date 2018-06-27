---
title: 'パイプライン トレースを構成する: Exchange 2013 Help'
TOCTitle: パイプライン トレースを構成する
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52057796
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パイプライン トレースを構成する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

パイプライン トレースでは、メールボックス サーバーとエッジ トランスポート サーバーのトランスポート サービスまたはメールボックス トランスポート サービスでトランスポート パイプラインを通過した電子メール メッセージがコピーされます。

## 始める前に把握しておくべき情報

  - この手順の予想所要時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート サービス」および「メールボックス トランスポート サービス」。

  - この手順を実行するには、シェルを使用する必要があります。

  - パイプライン トレースでは、送信者の電子メール アドレスから送信された電子メール メッセージの内容が完全にコピーされます。機密情報の不要な公開を防ぐには、パイプライン トレース フォルダーの場所に対して、適切なセキュリティのアクセス許可を設定する必要があります。

  - パイプライン トレースを長時間にわたって有効にしないでください。パイプライン トレースでは、短時間で蓄積する複数のメッセージ スナップショット ファイルが作成されます。パイプライン トレースを有効にしている場合は、使用可能なディスクの空き領域を常に監視してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## パイプライン トレースを有効化および構成する

## 手順 1:シェルを使用して、パイプライン トレース送信者アドレスを構成する

次の構文を使用して、パイプライン トレース送信者のアドレスを構成します。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">

この例では、Mailbox01 というメールボックス サーバーのトランスポート サービスで送信者 chris@contoso.com が送信したすべてのメッセージのスナップショットをキャプチャするようにパイプライン トレースを構成します。

    Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com

この例では、Mailbox02 というメールボックス サーバーのトランスポート サービスが受信したすべてのシステム生成メッセージのスナップショットをキャプチャするようにパイプライン トレースを構成します。

    Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"


> [!NOTE]
> トランスポート サービスですべてのサーバー生成メッセージをキャプチャするようにパイプライン トレースを構成すると、サーバーに大きな負荷がかかり、使用可能ディスク領域がすぐに消費されることがあります。パイプライン トレースを有効にしている場合は、使用可能なディスクの空き領域を常に監視してください。



## 手順 2:(省略可能) シェルを使用して、カスタム パイプライン トレース フォルダーを指定する

パイプライン トレースを有効にするまで、既定のパイプライン トレース フォルダーは存在せず、*PipelineTracingSenderAddress* パラメーターを使用して指定した基準を満たすメッセージはサーバーのトランスポート サービスを通過します。メールボックス サーバーのトランスポート サービスの場合、既定の場所は `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing` です。メールボックス サーバーのメールボックス トランスポート サービスの場合、既定の場所は `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing` です。カスタム パスを指定する場合は、そのパスがローカルの Exchange サーバー上に存在する必要があります。

次の構文を使用して、パイプライン トレース フォルダーを構成します。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>

この例では、Mailbox01 というメールボックス サーバーのトランスポート サービスのパイプライン トレース フォルダーを D:\\Hub\\Pipeline Tracing に設定します。

    Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"

## 手順 3:シェルを使用してパイプライン トレースを有効にする

既定では、すべての Exchange サーバーでパイプライン トレースが無効になっています。パイプライン トレースを有効にするときは、指定した Exchange サーバーの指定トランスポート サービスのみでパイプライン トレースを有効にします。パイプライン トレースを有効にする前に、手順 1 で説明したとおりに送信者アドレスを指定してください。

次の構文を使用してパイプライン トレースを有効にします。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true

この例では、Mailbox01 というメールボックス サーバーのトランスポート サービスでパイプライン トレースを有効にします。

    Set-TransportService Mailbox01 -PipelineTracingEnabled $true

## 正常な動作を確認する方法

パイプライン トレースが正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*

2.  表示された値が構成した値であることを確認します。

3.  トランスポート サービスまたはメールボックス トランスポート サービスのパイプライン トレース フォルダーを確認し、メッセージのスナップショット ファイルがそのフォルダーで作成されていることを確認します。

## パイプライン トレースを無効にする

ディスク領域とセキュリティの問題が懸念されるため、パイプライン トレースは診断やトラブルシューティングを目的とした一時的な操作となっています。パイプライン トレースを有効にした場合は、作業が終了した時点で必ず無効にしてください。

次の構文を使用してパイプライン トレースを無効にします。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false

この例では、Mailbox01 というメールボックス サーバーのトランスポート サービスでパイプライン トレースを無効にします。

    Set-TransportService Mailbox01 -PipelineTracingEnabled $false

## 正常な動作を確認する方法

パイプライン トレースが正常に無効になったことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled

2.  *PipelineTracingEnabled* パラメーターの値が $false になっていることを確認します。

3.  パイプライン トレース フォルダーを確認し、メッセージのスナップショット ファイルがフォルダーで作成されなくなったことを確認します。

