---
title: '送信コネクタを作成し、TLS (トランスポート層セキュリティ) を適用した状態でパートナーに電子メールを送信する: Exchange 2013 Help'
TOCTitle: 送信コネクタを作成し、TLS (トランスポート層セキュリティ) を適用した状態でパートナーに電子メールを送信する
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 49896574
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 送信コネクタを作成し、TLS (トランスポート層セキュリティ) を適用した状態でパートナーに電子メールを送信する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-15_

パートナーとの暗号化された安全な通信を確保する場合、パートナー ドメインに送信するメッセージにトランスポート層セキュリティ (TLS) を適用するように構成された送信コネクタを作成できます。TLS は、インターネット上の安全な通信を提供します。

この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [メール フローおよびクライアント アクセスの構成](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「送信コネクタ」。

  - インストールを開始する際には、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。インストールすると、このトピックの手順を使用して送信コネクタを作成できます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## EAC を使用して、送信コネクタを作成し TLS を適用した状態でパートナーに電子メールを送信する

このシナリオに対応する送信コネクタを作成するには、EAC にログインして次のステップを実行します。

1.  EAC で、<strong>メール フロー</strong> \> <strong>送信コネクタ</strong> に移動して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>送信コネクタの新規作成</strong> ウィザードで、送信コネクタの名前を指定し、<strong>種類</strong> として <strong>パートナー</strong> を選択します。<strong>パートナー</strong> を選択すると、TLS 証明書で認証されたサーバー向けに限定された接続を許可するようにコネクタが構成されます。<strong>次へ</strong> をクリックします。

3.  <strong>受信者のドメインに関連付けられた MX レコード</strong> が選択されていることを確認します。これは、コネクタがドメイン ネーム システム (DNS) を使用してメールをルーティングすることを示します。<strong>次へ</strong> をクリックします。

4.  <strong>アドレス スペース</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>ドメインの追加</strong> ウィンドウで、SMTP が <strong>種類</strong> として一覧されていることを確認します。<strong>完全修飾ドメイン名 (FQDN)</strong> で、パートナー ドメインの名前を入力します。<strong>保存</strong> をクリックします。

5.  <strong>送信元サーバー</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>サーバーの選択</strong> ウィンドウで、クライアント アクセス サーバー経由でインターネットにメールを送信する際に使用するメールボックス サーバーを選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。サーバーを選択した後に、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>OK</strong> をクリックします。

6.  <strong>終了</strong> をクリックします。

送信コネクタの作成が完了すると、送信コネクタ一覧に表示されます。

## 正常な動作を確認する方法

TLS が適用された状態で、パートナーに電子メールを送信する送信コネクタが正常に作成されたことを確認するには、組織内のユーザーからパートナー組織の受信者にメッセージを送信します。受信者がメッセージを受信すれば、コネクタは正しく作成されています。

## 詳細情報

[インターネットへの電子メール送信に対応した送信コネクタの作成](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[送信コネクタを作成し送信電子メールをスマート ホスト経由でルーティングする](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

