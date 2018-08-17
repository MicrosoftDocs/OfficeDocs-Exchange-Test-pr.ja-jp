---
title: 'ピックアップ ディレクトリと再生ディレクトリの構成: Exchange 2013 Help'
TOCTitle: ピックアップ ディレクトリと再生ディレクトリの構成
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 49896477
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ピックアップ ディレクトリと再生ディレクトリの構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

ピックアップ ディレクトリおよび再生ディレクトリは、メッセージ ファイルを直接トランスポート パイプラインに挿入するためにメールボックス サーバーおよびエッジ トランスポート サーバーのトランスポート サービスによって使用されます。正しい形式の電子メール メッセージ ファイルをピックアップ ディレクトリまたは再生ディレクトリにコピーすると、そのメッセージ ファイルが配信のために送信されます。ピックアップ ディレクトリは、管理者がメール フローのテストに使用したり、独自のメッセージを作成して送信する必要があるアプリケーションが使用します。再生ディレクトリは、SMTP 以外の外部ゲートウェイ サーバーからメッセージを受信し、Microsoft Exchange サーバーのキューからエクスポートするメッセージを再送信します。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート サービス」。

  - この手順を実行するには、シェルを使用する必要があります。

  - **Set-TransportService** コマンドレットの *PickupDirectoryMaxMessagesPerMinute* パラメーターの値は、ピックアップ ディレクトリおよび再生ディレクトリによって使用されます。

  - ピックアップ ディレクトリまたは再生ディレクトリの場所を変更すると、既存のメッセージ ファイルは古い場所から新しい場所へコピーされません。新しいピックアップ ディレクトリまたは再生ディレクトリの場所は構成の変更後すぐにアクティブになりますが、既存のメッセージ ファイルはすべて古い場所に残ります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行内容

## シェルを使用してピックアップ ディレクトリを構成する

ピックアップ ディレクトリを構成するには、次の構文を使用します。

    Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>

この例では、Exchange01 というメールボックス サーバーのピックアップ ディレクトリに次の変更を行います。

  - ピックアップ ディレクトリの場所は、D:\\Pickup Directory に設定されます。

  - メッセージ ファイルのメッセージ ヘッダーの最大サイズは 96 KB に増やされます。

  - 1 つのメッセージ ファイルの最大受信者数は、250 に増やされます。

  - Pickup ディレクトリおよび Replay ディレクトリのメッセージ処理の最大速度は、1 分あたり 200 件のメッセージに上がります。

<!-- end list -->

    Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200


> [!NOTE]
> <UL>
> <LI>
> <P><EM>PickupDirectoryPath</EM> パラメーターの値を <CODE>$null</CODE> に設定すると、ピックアップ ディレクトリは無効になります。</P>
> <LI>
> <P><EM>PickupDirectoryPath</EM> パラメーターと <EM>ReplayDirectoryPath</EM> パラメーターで指定されるディレクトリは、同一にはできません。</P></LI></UL>



## シェルを使用してピックアップ ディレクトリを構成する

再生ディレクトリを構成するには、次の構文を使用します。

    Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>

この例では、Exchange01 というメールボックス サーバーの再生ディレクトリに次の変更を行います。

  - 再生ディレクトリの場所は、D:\\Replay Directory に設定されます。

  - Pickup ディレクトリおよび Replay ディレクトリのメッセージ処理の最大速度は、1 分あたり 200 件のメッセージに上がります。

<!-- end list -->

    Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200


> [!NOTE]
> <UL>
> <LI>
> <P><EM>ReplayDirectoryPath</EM> パラメーターの値を <CODE>$null</CODE> に設定すると、再生ディレクトリは無効になります。</P>
> <LI>
> <P><EM>PickupDirectoryPath</EM> パラメーターと <EM>ReplayDirectoryPath</EM> パラメーターで指定されるディレクトリは、同一にはできません。</P></LI></UL>



## 正常な動作を確認する方法

ピックアップ ディレクトリおよび再生ディレクトリが正常に構成されたことを確認するには、次の手順を実行します。

1.  次のコマンドを実行します。
    
        Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*

2.  表示された値が構成した値であることを確認します。

