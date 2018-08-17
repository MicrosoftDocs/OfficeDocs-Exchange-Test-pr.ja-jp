---
title: 'インターネットへの電子メール送信に対応した送信コネクタの作成: Exchange 2013 Help'
TOCTitle: インターネットへの電子メール送信に対応した送信コネクタの作成
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 49896303
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インターネットへの電子メール送信に対応した送信コネクタの作成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-01-23_

既定では、Microsoft Exchange Server 2013 では、ドメインの外部にメールを送信することは許可されていません。ドメインの外部にメールを送信するには、送信コネクタを作成する必要があります。次の図は、インターネットにメールを送信する送信コネクタを作成する場合のメール フローを示しています。

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [メール フローおよびクライアント アクセスの構成](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「送信コネクタ」。

  - インストールを開始する際には、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。インストールすると、このトピックの手順を使用して送信コネクタを作成できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EAC を使用してインターネットに送信される電子メール用の送信コネクタを作成する

1.  EAC で、<strong>メール フロー</strong> \> <strong>送信コネクタ</strong> に移動して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **送信コネクタの新規作成**ウィザードで、送信コネクタの名前を指定し、<strong>種類</strong> として <strong>インターネット</strong> を選択します。<strong>次へ</strong> をクリックします。

3.  <strong>受信者のドメインに関連付けられた MX レコード</strong> が選択されていることを確認します。これは、コネクタがドメイン ネーム システム (DNS) を使用してメールをルーティングすることを示します。<strong>次へ</strong> をクリックします。

4.  <strong>アドレス スペース</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>ドメインの追加</strong> ウィンドウで、SMTP が <strong>種類</strong> として一覧されていることを確認します。<strong>完全修飾ドメイン名 (FQDN)</strong> に「\*」を入力します。「\*」は、この送信コネクタが任意のドメインにアドレス指定されたメッセージに適用されることを示します。<strong>保存</strong> をクリックします。

5.  <strong>スコープ送信コネクタ</strong> チェック ボックスがオフになっていることを確認し、<strong>次へ</strong> をクリックします。

6.  <strong>送信元サーバー</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>サーバーの選択</strong> ウィンドウで、クライアント アクセス サーバー経由でインターネットにメールを送信する際に使用するメールボックス サーバーを選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。サーバーを選択した後に、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>OK</strong> をクリックします。

7.  <strong>終了</strong> をクリックします。

送信コネクタの作成が完了すると、送信コネクタ一覧に表示されます。

## シェルを使用してクライアント アクセス サーバー経由でメールをルーティングする

Exchange 2013 では、**Set-SendConnector** コマンドレットの *FrontendProxyEnabled* パラメーターを使用して、クライアント アクセス サーバー経由で送信メッセージをルーティングできます。このパラメーターは、既定で `$true` に設定されていませんが、多くの場合、特に多数のメッセージング サーバーがある環境で作業している場合は、メール フローを統合して単純化することができます。

この例では、送信コネクタに対して *FrontendProxyEnabled* パラメーターを `$true` に設定します。

    Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true

## 正常な動作を確認する方法

インターネットに送信される電子メール用の送信コネクタが正しく作成されたことを確認するには、組織のユーザーの 1 人から外部の受信者にメールを送信し、メッセージが正常に着信したかどうかを確認します。

## 詳細情報

[送信コネクタ](send-connectors-exchange-2013-help.md)

[送信コネクタを作成し送信電子メールをスマート ホスト経由でルーティングする](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

