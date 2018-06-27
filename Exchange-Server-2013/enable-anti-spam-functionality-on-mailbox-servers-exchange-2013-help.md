---
title: 'メールボックス サーバーのスパム対策機能を有効にする: Exchange 2013 Help'
TOCTitle: メールボックス サーバーのスパム対策機能を有効にする
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 49129462
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス サーバーのスパム対策機能を有効にする

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2014-01-23_

Microsoft Exchange Server 2013 では、メールボックス サーバー上のトランスポート サービスで次のスパム対策エージェントが使用できますが、それらは既定ではインストールされません。

  - コンテンツ フィルター エージェント

  - Sender ID エージェント

  - 送信者フィルター エージェント

  - 受信者フィルター エージェント

  - 送信者評価用のプロトコル分析エージェント

ただし、Exchange 管理シェルのスクリプトを使用して、これらのスパム対策エージェントをメールボックス サーバーにインストールできます。 一般的に、スパム対策エージェントをメールボックス サーバー上にインストールするのは、前段階に何のスパム対策フィルターもなしに組織がすべての受信メールを受け入れる場合のみです。

使用できるスパム対策エージェントを、メールボックス サーバー上のトランスポート サービスにインストールする場合に起こることですが、メッセージがメールボックス サーバーに到着する前に、他の Exchange スパム対策エージェントも動作するようにしていませんか? たとえば、Microsoft Exchange 2007 または Exchange 2010 エッジ トランスポート サーバーが境界ネットワークにあって、受信メールをメールボックス サーバー上のトランスポート サービスに直接に配信している場合は? メールボックス サーバー上のスパム対策エージェントは、他の Exchange スパム対策エージェントによって付加されるスパム対策の X ヘッダーの値を認識して、それらの X ヘッダーを含むメッセージは再度スキャンすることなく通過させます。 ただし、受信者フィルター エージェントによって実行される受信者の参照は、メールボックス サーバー上でもう一度起こります。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート構成」。

  - メールボックス サーバーでは、接続フィルター エージェントおよび添付ファイル フィルター エージェントを使用できません。それらは、エッジ トランスポート サーバー上でのみ使用できます。 ただし、マルウェア エージェントはメールボックス サーバー上に既定でインストールされて有効にされます。詳細については、「[マルウェア対策保護](anti-malware-protection-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:シェルを使用して、Install-AntispamAgents.ps1 スクリプトを実行するには

次のコマンドを実行します。

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## このステップの検証方法

スクリプトがエラーなしに実行されれば、このステップは成功していて Exchange トランスポート サービスを再起動するよう求められます。

## 手順 2:シェルを使用して Microsoft Exchange トランスポート サービスを再起動する

次のコマンドを実行します。

    Restart-Service MSExchangeTransport

## このステップの検証方法

Microsoft Exchange トランスポート サービスがエラーなしに再起動すれば、このステップは成功しています。

## 手順 3:シェルを使用して組織の内部 SMTP サーバーを指定する

Sender ID エージェントが無視する必要があるすべての内部 SMTP サーバーの IP アドレスを指定する必要があります。 実際には、少なくとも 1 つの内部 SMTP サーバーの IP アドレスを指定する必要があります。 スパム対策エージェントが実行されているメールボックス サーバーが組織内で唯一の SMTP サーバーである場合は、そのコンピューターの IP アドレスを指定します。

既存の値に影響を与えることなく内部 SMTP サーバーの IP アドレスを追加するには、次のコマンドを実行します。

    Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}

この例では、内部 SMTP サーバー アドレス 10.0.1.10 および 10.0.1.11 を組織のトランスポート構成に追加します。

    Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}

## このステップの検証方法

少なくとも 1 つの内部 SMTP サーバーの IP アドレスが正常に指定されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-TransportConfig | Format-List InternalSMTPServers

2.  少なくとも 1 つの有効な内部 SMTP サーバーの IP アドレスが表示されていることを確認します。

