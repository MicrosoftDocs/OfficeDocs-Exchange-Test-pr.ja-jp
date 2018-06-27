---
title: '受信コネクタを作成して内部の Exchange サーバーからメッセージを受信する: Exchange 2013 Help'
TOCTitle: 受信コネクタを作成して内部の Exchange サーバーからメッセージを受信する
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 49896253
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信コネクタを作成して内部の Exchange サーバーからメッセージを受信する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-03_

Exchange サーバーからメールを受信する場合は、種類が **\[内部\]** の受信コネクタを作成します。この種類のコネクタを使用して、組織内のメール ルーティングを制御します。 たとえば、メールボックス サーバー上のトランスポート サービスから特定のエッジ トランスポート サーバーに、またはあるメールボックス サーバーから別のサーバーにメールをルーティングする場合です。

この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [メール フローおよびクライアント アクセスの構成](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「受信コネクタ」。

  - インストールを開始する際には、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。インストール後に、このトピックの手順を使用して受信コネクタを作成します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 受信コネクタを作成して内部の Exchange サーバーからメッセージを受信する

1.  EAC で、**\[メール フロー\]** \> **\[受信コネクタ\]** に移動します。新しい受信コネクタを作成するには、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **\[新しい受信コネクタ\]** ページで、受信コネクタの名前を指定し、**\[役割\]** で **\[ハブ トランスポート\]** を選択します。 この場合、ネットワーク内部でのメールのルーティングを仮定していて、組織の外部との送受信は仮定していません。

3.  種類に **\[内部\]** を選択します。コネクタは Exchange サーバー認証で構成されています。

4.  \[リモート ネットワーク設定\] ページに 0.0.0.0-255.255.255.255 が表示される場合 (つまり、受信コネクタがすべての IP アドレスからの接続を受信する場合) は、**\[削除\]**![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックしてこれを削除します。 **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、メールを受信するサーバーの IP アドレス (192.168.1.1 など) を追加し、**\[保存\]** をクリックします。

5.  **\[完了\]** をクリックしてコネクタを作成します。

受信コネクタの作成が完了すると、受信コネクタ一覧に表示されます。コマンドレットを使用して受信コネクタを作成する手順の例については、「[New-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125139\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

内部サーバーからメッセージを受信するための受信コネクタが正常に作成されたことを確認するには、送信サーバーから発信されたメッセージが受信者のサーバーに正常に届くことをテストします。 これを実行するための 1 つの方法としては、Exchange 管理シェルで [Set-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125140\(v=exchg.150\)) コマンドレットを使用して、作成した受信コネクタの *ProtocolLoggingLevel* を `Verbose` に設定し、ログを確認してメッセージが配信されていることを確認します。

## 詳細情報

[受信コネクタを作成してインターネットからの電子メールを受信する](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[パートナーから電子メールを受信するためのセキュリティで保護された受信コネクタを作成する](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

