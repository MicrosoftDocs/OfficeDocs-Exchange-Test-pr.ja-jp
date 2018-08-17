---
title: '受信コネクタを作成してインターネットからの電子メールを受信する: Exchange 2013 Help'
TOCTitle: 受信コネクタを作成してインターネットからの電子メールを受信する
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 49896250
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信コネクタを作成してインターネットからの電子メールを受信する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-15_

この手順では、受信コネクタを構成してインターネットから電子メールを受信する方法を示します。


> [!NOTE]
> 通常は、インターネットから電子メールを受信するために受信コネクタを明示的にセットアップする必要はありません。なぜなら、インターネットからの電子メールを受け入れる受信コネクタは Exchange をインストールすると暗黙的に作成されるからです。詳細は「<A href="receive-connectors-exchange-2013-help.md">受信コネクタ</A>」を参照してください。



この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [メール フローおよびクライアント アクセスの構成](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「受信コネクタ」。

  - インストールを開始する際には、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。インストール後に、このトピックの手順を使用して受信コネクタを作成します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して受信コネクタを作成してインターネットからの電子メールを受信する

1.  EAC で、<strong>メール フロー</strong> \> <strong>受信コネクタ</strong> に移動します。<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして受信コネクタを作成します。

2.  <strong>新しい受信コネクタ</strong> ページで、受信コネクタの名前を指定してから <strong>役割</strong> の <strong>フロントエンド トランスポート</strong> を選択します。 この場合はインターネットから電子メールを受信するので、最初はメールがフロント エンド サーバーを経由するようにしてメール フローを簡略化し統合することをお勧めします。

3.  種類に <strong>インターネット</strong> を選択します。受信コネクタはインターネットの送信者からメールを受け取ります。

4.  <strong>ネットワーク アダプター バインド</strong> について、<strong>利用可能なすべての IPv4</strong> が <strong>IP アドレス</strong> の一覧に表示され <strong>ポート</strong> が 25 であることを確認します。これは、コネクタがローカル サーバーのネットワーク アダプターに割り当てられたすべての IP アドレスで接続を待機していることを示します。
    

    > [!NOTE]
    > ネットワーク アダプターが複数ある場合は、ローカル サーバー上の特定のネットワーク アダプターに割り当てられている IP アドレスをこのページで追加できますが、必須ではありません。



5.  <strong>終了</strong> ボタンをクリックしてユーザーのコネクタを作成します。

受信コネクタの作成が完了すると、受信コネクタ一覧に表示されます。コマンドレットを使用して受信コネクタを作成する手順の例については、「[New-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125139\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

インターネットからメッセージを受信するための受信コネクタが正常に作成されたことを確認するには、外部のソースからメールを送信して、ユーザーの 1 人がそれを受信できることをテストします。メールを受信することができれば、構成は正常に機能しています。

## 詳細情報

[パートナーから電子メールを受信するためのセキュリティで保護された受信コネクタを作成する](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[Exchange を実行していないシステムから電子メールを受信するための受信コネクタの作成](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)

