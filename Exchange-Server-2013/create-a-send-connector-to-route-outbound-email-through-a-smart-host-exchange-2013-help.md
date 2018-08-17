---
title: '送信コネクタを作成し送信電子メールをスマート ホスト経由でルーティングする: Exchange 2013 Help'
TOCTitle: 送信コネクタを作成し送信電子メールをスマート ホスト経由でルーティングする
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 49896237
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 送信コネクタを作成し送信電子メールをスマート ホスト経由でルーティングする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-07_

送信メッセージに対してポリシー チェックを実行する必要があるネットワーク アプライアンスがある場合など、電子メールをサード パーティのスマート ホスト経由でルーティングする必要がある場合があります。


> [!NOTE]
> サード パーティのスマート ホストはトランスポートに SMTP を使用する必要があります。 トランスポートに SMTP が使用されない場合、外部コネクタまたは配信エージェント コネクタを使用する必要があります。



この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [メール フローおよびクライアント アクセスの構成](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「送信コネクタ」。

  - インストールを開始する際には、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。インストールすると、このトピックの手順を使用して送信コネクタを作成できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して送信電子メールをスマート ホスト経由でルーティングする送信コネクタを作成する

1.  EAC で、<strong>メール フロー</strong> \> <strong>送信コネクタ</strong> に移動して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **送信コネクタの新規作成** ウィザードで、送信コネクタの名前を指定し、<strong>種類</strong> に <strong>カスタム</strong> を選択します。 Microsoft Exchange Server 2013 を実行していないコンピューターにメッセージをルーティングする場合は、通常このオプションを選択します。<strong>次へ</strong> をクリックします。

3.  <strong>スマート ホストを経由してメールをルーティングする</strong> を選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。 <strong>スマート ホストの追加</strong> ウィンドウで、192.168.100.1 などの IP アドレスを指定するか、contoso.com などの完全修飾ドメイン名 (FQDN) を指定します。次に <strong>保存</strong> をクリックします。
    
    <strong>スマート ホスト認証</strong> では、スマート ホストに必要な認証の種類を選択します。 <strong>基本認証</strong> を選択する場合は、ユーザー名とパスワードを入力する必要があります。
    

    > [!NOTE]
    > 基本認証を選択する場合は、ユーザー名とパスワードはクリア テキストで送信されるため暗号化された接続を使用することをお勧めします。



4.  <strong>アドレス スペース</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>ドメインの追加</strong> ウィンドウで、SMTP が <strong>種類</strong> として一覧されていることを確認します。 <strong>完全修飾ドメイン名 (FQDN)</strong> では、この送信コネクタが任意のドメインに送信されるメッセージに適用することを指定するために「\*」を入力します。<strong>保存</strong> をクリックします。

5.  <strong>送信元サーバー</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>サーバーの選択</strong> ウィンドウで、クライアント アクセス サーバー経由でインターネットにメールを送信する際に使用するメールボックス サーバーを選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。 サーバーを選択した後に、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>OK</strong> をクリックします。

6.  <strong>終了</strong> をクリックします。

送信コネクタの作成が完了すると、作成された送信コネクタが送信コネクタ一覧に表示されます。

## 正常な動作を確認する方法

送信電子メールをスマート ホスト経由でルーティングするための送信コネクタが正常に作成されたことを確認するには、<strong>アドレス スペース</strong> に指定したドメインに Outlook Web App を使用できる組織内のユーザーからメッセージを送信します。受信者がメッセージを受信する場合は、送信コネクタが正常に構成されています。

## 詳細情報

[インターネットへの電子メール送信に対応した送信コネクタの作成](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[送信コネクタ](send-connectors-exchange-2013-help.md)

