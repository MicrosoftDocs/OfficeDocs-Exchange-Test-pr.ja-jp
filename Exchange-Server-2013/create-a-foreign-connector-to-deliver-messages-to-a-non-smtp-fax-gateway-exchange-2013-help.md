---
title: '外部コネクタを作成して SMTP Fax ゲートウェイ以外にメッセージを配信する: Exchange 2013 Help'
TOCTitle: 外部コネクタを作成して SMTP Fax ゲートウェイ以外にメッセージを配信する
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 49896258
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 外部コネクタを作成して SMTP Fax ゲートウェイ以外にメッセージを配信する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-17_

SMTP をプライマリ トランスポート メカニズムとして使用しない FAX ゲートウェイ サーバーとメッセージの送受信を行うシナリオがある場合があります。 ここで示す手順に従って、外部システムに対してメッセージの配信および受信を行う外部コネクタを作成します。


> [!TIP]
> 送信メッセージを SMTP 以外のシステムに配信する必要があるほとんどの場合で、配信エージェント コネクタの使用をお勧めします。配信エージェント コネクタではメッセージのキューを管理することができ、メッセージをファイル システムに書き込む必要がないなど、他にも利点があるためです。詳細は、「<A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">配信エージェントと配信エージェント コネクタ</A>」を参照してください。



この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:30 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「外部コネクタ」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1: シェルを使用して、SMTP 以外のゲートウェイ サーバーにメッセージを送信する外部コネクタを作成します

1.  外部コネクタを作成するには、次のコマンドを実行します。
    
        New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    
    この例では、Hub01 および Hub02 はメッセージを外部システムに配信するように指定した組織内の送信元サーバーです。複数の送信元サーバーを使用することでフォールト トレランスを実現できます。

いったん外部コネクタを作成すると、組織の要件に応じてドロップ ディレクトリ、ピックアップ ディレクトリ、再生ディレクトリを構成できます。

## このステップの検証方法

外部コネクタが正常に作成されたことを確認するために、次のコマンドを実行します。

    Get-ForeignConnector | Format-List Name

作成した外部コネクタの名前が表示されることを確認します。

## 手順 2: シェルを使用して、トランスポート サービスを実行しているメールボックス サーバー用のドロップ ディレクトリを構成する

トランスポート サービスを実行しているメールボックス サーバー用のドロップ ディレクトリは、外部コネクタから送信メッセージを配信するのに使用します。

ドロップ ディレクトリとして使用するディレクトリを、ローカルのファイル システム上に作成します。ネットワーク ファイル共有上のディレクトリを使用することもできます。

1.  次のスクリプトを実行して、外部コネクタにドロップ ディレクトリを指定します (*DropDirectory* パラメーターの値をお使いの環境に合わせて変更します)。
    
        Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"

## このステップの検証方法

ドロップ ディレクトリが正常に設定されたことを確認するには、次のコマンドレット スクリプトを実行して、*DropDirectory* パラメーターの値を確認します。

    Get-ForeignConnector "Contoso Foreign Connector" | Format-List

外部コネクタを作成してドロップ ディレクトリを指定したら、外部コネクタを作成したメールボックス サーバーを使用してメッセージを配信し、ファイルがドロップ ディレクトリに配信されていることを確認します。

## 手順 3: シェルを使用して、メールボックス サーバー上にピックアップ ディレクトリを構成する

メールボックス サーバー上のトランスポート サービス用のピックアップ ディレクトリは、SMTP 以外のシステムによって生成されたメッセージの収集に使用されます。 SMTP 以外のシステム (FAX ゲートウェイ サーバーなど、ファイル転送を使用したシステム) で生成された新しいメッセージを収集する場合は、この手順を使用します。

ピックアップ ディレクトリを構成する手順の詳細については、「[ピックアップ ディレクトリと再生ディレクトリの構成](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)」を参照してください。

## このステップの検証方法

ピックアップ ディレクトリが正常に設定されたことを確認するには、次のコマンド スクリプトを実行して、*PickupDirectoryPath* パラメーターの値を確認します。

    Get-TransportService | Format-List PickupDirectoryPath

## 手順 4: シェルを使用して、メールボックス サーバー上に再生ディレクトリを構成する

メールボックス サーバー上のトランスポート サービス用の再生ディレクトリは、SMTP 以外のシステムによって生成されたメッセージの収集に使用します。 Exchange 環境で生成されて Exchange トランスポートからエクスポートされた電子メールのメッセージを再送信 (通常は SMTP 以外の外部ゲートウェイ サーバーから) する場合は、この手順を使用して再生ディレクトリを構成します。

ピックアップ ディレクトリを構成する手順の詳細については、「[ピックアップ ディレクトリと再生ディレクトリの構成](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)」を参照してください。

## このステップの検証方法

再生ディレクトリが正常に設定されたことを確認するには、次のコマンド スクリプトを実行して、*ReplayDirectoryPath* パラメーターの値を確認します。

    Get-TransportService | Format-List ReplayDirectoryPath

## 詳細情報

[外部コネクタ](foreign-connectors-exchange-2013-help.md)

[配信エージェントと配信エージェント コネクタ](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

