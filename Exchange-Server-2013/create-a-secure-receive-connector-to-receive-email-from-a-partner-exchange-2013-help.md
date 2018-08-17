---
title: 'パートナーから電子メールを受信するためのセキュリティで保護された受信コネクタを作成する: Exchange 2013 Help'
TOCTitle: パートナーから電子メールを受信するためのセキュリティで保護された受信コネクタの作成
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 49895222
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パートナーから電子メールを受信するためのセキュリティで保護された受信コネクタを作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

この手順は、受信コネクタを構成してパートナーからセキュリティで保護された電子メールを受信する方法を示します。この手順は、信頼できるパートナーとの間で通信を暗号化する必要がある場合に使用します。コネクタは、トランスポート層セキュリティ (TLS) で認証するサーバーからのみ接続を受け入れるように構成されます。

この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [メール フローおよびクライアント アクセスの構成](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「受信コネクタ」。

  - インストールを開始する際には、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。インストール後に、このトピックの手順を使用して受信コネクタを作成できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用してパートナーからセキュリティで保護されたメッセージを受信するための受信コネクタを作成する

1.  EAC で、<strong>メール フロー</strong> \> <strong>受信コネクタ</strong> に移動します。新しい受信コネクタを作成する場合は、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>受信コネクタの新規作成</strong> ページで、受信コネクタの名前を指定してから <strong>役割</strong> に <strong>フロントエンド トランスポート</strong> を選択します。この場合はパートナーからメールを受信するので、最初にメールをフロント エンド サーバーにルーティングしてメール フローを簡略化および統合することをお勧めします。

3.  種類には <strong>パートナー</strong> を選択します。受信コネクタは、信頼できるサード パーティからのメールを受信します。

4.  <strong>ネットワーク アダプター バインド</strong> の場合、<strong>利用可能なすべての IPv4 アドレス</strong> が <strong>IP アドレス</strong> リストに表示され、<strong>ポート</strong> が 25 (簡易メール転送プロトコルではポート 25 を使用) であることを確認します。これは、コネクタがローカル サーバーのネットワーク アダプターに割り当てられたすべての IP アドレスで接続をリッスンすることを示します。<strong>次へ</strong> をクリックします。

5.  \[リモート ネットワーク設定\] ページに「0.0.0.0-255.255.255.255」と表示される場合 (つまり、受信コネクタがすべての IP アドレスからの接続を受け入れる場合) は、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックしてこれを削除します。<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし、パートナーのサーバーの IP アドレスを追加し、<strong>保存</strong> をクリックします。
    

    > [!NOTE]
    > CIDR 表記で IP アドレス範囲を指定することもできます (例: 64.4.6.100/24)。



6.  <strong>完了</strong> をクリックしてコネクタを作成します。

受信コネクタの作成が完了すると、受信コネクタ一覧に表示されます。コマンドレットを使用して受信コネクタを作成する手順の例については、「[New-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125139\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

パートナーからメッセージを受信するための受信コネクタが正常に作成されたことを確認するには、パートナーがユーザーのいずれかにメールを送信できて、そのメールをユーザーが正常に受信できることをテストします。暗号化されたメールを受信できれば (メッセージ ヘッダーを調べれば TLS が使用されていることを確認できます)、その構成は正常に機能しています。

## 詳細情報

[受信コネクタ](receive-connectors-exchange-2013-help.md)

