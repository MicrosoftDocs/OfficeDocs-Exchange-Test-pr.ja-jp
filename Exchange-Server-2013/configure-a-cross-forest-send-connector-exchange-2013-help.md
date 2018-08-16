---
title: 'フォレスト間の送信コネクタを構成する: Exchange 2013 Help'
TOCTitle: フォレスト間の送信コネクタを構成する
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52057839
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フォレスト間の送信コネクタを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-21_

Active Directory において、*フォレスト*は、ディレクトリ サービスの外部境界を示します。フォレスト間の通信を有効にする送信コネクタを作成することができます。この例では、コネクタは基本認証を使用します。

コネクタの構成に関連するその他の管理タスクについては、「[コネクタ](connectors-exchange-2013-help.md)」を参照してください。

この手順を使用しているシナリオに興味はありますか?次のトピックを参照してください。

  - [フォレスト間のトポロジで Exchange 2013 を展開する](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 20 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「送信コネクタ」と「受信コネクタ」。

  - インストールを開始する際には、「[Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)」を参照してください。インストール後に、このトピックの手順を使用して、フォレスト間トポロジを構成するためのコネクタを作成します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## フォレストごとにユーザー アカウントを作成する

基本認証に使用する各フォレストのユーザー アカウントを作成する必要があります。各フォレストにアカウントを作成し、それぞれを通信に使用する Exchange サーバーのユニバーサル セキュリティ グループに追加します。このアカウントは、別のフォレスト内でメールを受信するサーバーを認証するために送信コネクタによって使用されます。たとえば、Contoso ドメイン内の Exchange サーバーにメールを送信する場合に、Fourth Coffee ドメイン内の Exchange サーバーが認証のために使用する必要のある資格情報として、FourthCoffee@Contoso.com というユーザー プリンシパル名 (UPN) を持つユーザー アカウントを提供します。

## EAC を使用して、電子メールを別の Exchange 2013 フォレストにルーティングする送信コネクタを作成する

基本認証を使用してフォレスト間の電子メール フローを確立します。

1.  EAC で、<strong>メール フロー</strong> \> <strong>送信コネクタ</strong> の順に移動します。<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>送信コネクタの新規作成</strong> ウィザードで、送信コネクタの名前を指定し、<strong>種類</strong> として <strong>内部</strong> を選択します。<strong>次へ</strong> をクリックします。

3.  <strong>スマート ホストを経由してメールをルーティングする</strong> を選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>スマート ホストの追加</strong> ウィンドウで、2 つ目のフォレストのターゲット サーバーの IP アドレス (64.4.6.100 など) を指定します。<strong>保存</strong>、<strong>次へ</strong> の順にクリックします。
    
    <strong>スマート ホスト認証</strong> で、<strong>基本認証</strong> を選択してユーザー名とパスワードを入力します。ここで <strong>TLS の起動後にのみ基本認証を提供する</strong> を選択することで、TLS により通信のセキュリティを保護できます。
    

    > [!NOTE]
    > TLS による基本認証を使用する場合、ターゲット サーバーが X.509 証明書を使用するように構成する必要があります。



4.  <strong>アドレス スペース</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>ドメインの追加</strong> ウィンドウで、SMTP が <strong>種類</strong> として一覧されていることを確認します。<strong>完全修飾ドメイン名 (FQDN) </strong> に fourthcoffee.com などの受信側ドメインを入力し、<strong>保存</strong>、<strong>次へ</strong> の順にクリックします。

5.  <strong>送信元サーバー</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>サーバーの選択</strong> ウィンドウで、使用するサーバーを選択し、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>OK</strong> をクリックします。

6.  <strong>終了</strong> をクリックします。コネクタが送信コネクタの一覧に表示されます。

送信コネクタを作成したら、元のフォレストに電子メールを送信する 2 つ目のフォレストに送信コネクタを作成します。この場合、指定する完全修飾ドメイン名 (FQDN) は、1 つ目のフォレストのドメイン名になります。たとえば、「contoso.com」と入力します。

## シェルを使用して送信コネクタにアクセス許可を設定する

この例では、シェルの Enable-CrossForestConnector.ps1 スクリプトを使用して、フォレスト間トポロジで使用する送信コネクタにアクセス許可を設定します。

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## 正常な動作を確認する方法

電子メールを 2 つ目のフォレストにルーティングするための送信コネクタが正常に作成されたことを確認するには、<strong>アドレス スペース</strong> に指定したドメインに Outlook Web App を使用できる組織内のユーザーからメッセージを送信します。受信者がメッセージを受信する場合は、送信コネクタが正常に構成されています。

## 詳細情報

[インターネットへの電子メール送信に対応した送信コネクタの作成](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[送信コネクタ](send-connectors-exchange-2013-help.md)

