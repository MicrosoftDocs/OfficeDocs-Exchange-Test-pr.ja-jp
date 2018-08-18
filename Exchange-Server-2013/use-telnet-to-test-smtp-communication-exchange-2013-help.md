---
title: 'Telnet を使用した SMTP 通信のテスト: Exchange 2013 Help'
TOCTitle: Telnet を使用した SMTP 通信のテスト
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52057829
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Telnet を使用した SMTP 通信のテスト

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

ここでは、Telnet を使用してメッセージング サーバー間の SMTP (簡易メール転送プロトコル) 通信をテストする方法について説明します。既定では、SMTP はポート 25 で待機します。Telnet をポート 25 で使用すると、SMTP サーバーへの接続に使用する SMTP コマンドを入力し、Telnet セッションが SMTP メッセージング サーバーである場合とまったく同様にメッセージを送信することができます。接続プロセスおよびメッセージ送信プロセスの手順ごとに、成功または失敗を確認することができます。

以下に、Microsoft Exchange 組織に存在するトランスポート サーバーとの SMTP 通信を、Telnet を使用してテストするシナリオを示します。

  - 境界ネットワークの外部に配置されているホストから、組織のインターネットに直接接続している Exchange サーバーに接続し、テスト メッセージを送信する。

  - 組織のインターネットに直接接続している Exchange サーバーからリモート メッセージング サーバーに接続し、テスト メッセージを送信する。

このトピックの手順では、Microsoft Windows に含まれるコンポーネントである Telnet クライアントを使用する方法を示します。サードパーティの Telnet クライアントは、Windows Telnet コンポーネントの構文とは異なる構文を必要とする場合があります。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 30 分

  - Exchange のアクセス許可は、このトピックの手順には適用されません。これらの手順は、Exchange サーバーやクライアント コンピューターのオペレーティング システムで実行されます。

  - このトピックの手順は、インターネットに直接接続している、匿名接続が可能なサーバーとの間で接続を確立する場合に最適です。内部の Exchange サーバー間のメッセージ送信は、暗号化され、認証されます。Telnet を使用してメールボックス サーバーのハブ トランスポート サービスに接続するには、受信コネクタを作成し、匿名アクセスまたは基本認証によってメッセージを受信できるように構成する必要があります。コネクタで基本認証が可能な場合は、ユーザー名とパスワードに使用されるテキスト文字列を Base64 形式に変換するユーティリティが必要です。基本認証を使用するとユーザー名とパスワードが簡単に識別されてしまうため、暗号化を行わない基本認証を使用することはお勧めしません。

  - リモート メッセージング サーバーに接続する場合は、インターネットに直接接続している Exchange サーバーでこのトピックの手順を実行することを検討してください。この手順により、このサーバーにメッセージの送信を試みるすべてのインターネット ホストについて、送信元 IP アドレス、対応する DNS (ドメイン ネーム システム) のドメイン名、および逆引き参照 IP アドレスを検証するように構成されているリモート メッセージング サーバーでテキスト メッセージが拒否されないようにすることができます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1: Windows に Telnet クライアントをインストールする

既定では、Telnet クライアントは、Microsoft Windows オペレーティング システムのほとんどのクライアントまたはサーバー バージョンにインストールされていません。Telnet クライアントをインストールするには、「[Telnet クライアントのインストール](https://go.microsoft.com/fwlink/p/?linkid=179054)」を参照してください。

## 手順 2: Nslookup を使用してリモート SMTP サーバーの MX レコードの FQDN または IP アドレスを特定する

Telnet をポート 25 で使用して相手先の SMTP サーバーに接続するには、SMTP サーバーの完全修飾ドメイン名 (FQDN) または IP アドレスを使用する必要があります。FQDN または IP アドレスがわからない場合、この情報を得る最も簡単な方法は、Nslookup コマンドライン ツールを使用して相手先ドメインの MX レコードを特定することです。

1.  コマンド プロンプトで「**nslookup**」と入力し、Enter キーを押します。このコマンドによって、Nslookup セッションが開きます。

2.  「**set type=mx**」と入力し、Enter キーを押します。

3.  「**set timeout=20**」と入力し、Enter キーを押します。既定では、Windows DNS サーバーの再帰的な DNS クエリのタイムアウト制限は 15 秒です。

4.  MX レコードを特定するドメインの名前を入力します。たとえば、fabrikam.com ドメインの MX レコードを特定するには、「**fabrikam.com.**」と入力して Enter キーを押します。
    

    > [!NOTE]
    > 末尾のピリオド (&nbsp;<STRONG>.</STRONG>&nbsp;) は、FQDN であることを示しています。末尾にピリオドを使用することで、ネットワークで構成されている既定の DNS サフィックスが、意図に反してドメイン名に追加されることを防ぎます。

    
    このコマンドの出力は次のようになります。
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    相手先の SMTP サーバーとして、MX レコードに関連付けられている任意のホスト名または IP アドレスを使用することができます。優先順位の値が小さいほど優先度の高い SMTP サーバーであることを示します。負荷分散とフォールト トレランスについて、複数の MX レコードおよび異なる優先順位の値を使用することができます。

5.  Nslookup セッションを終了するには、「**exit**」と入力して Enter キーを押します。


> [!NOTE]
> 組織の内部ネットワークに設定されているファイアウォールまたはインターネット プロキシの制限によって、Nslookup ツールを使用してインターネット上のパブリック DNS サーバーに対するクエリを実行できない場合があります。



## 手順 3: Telnet をポート 25 で使用して SMTP 通信をテストする

この例では、次の値が使用されます。

  - **相手先 SMTP サーバー**   mail1.fabrikam.com

  - **送信元ドメイン**   contoso.com

  - **送信者の電子メール アドレス**   chris@contoso.com

  - **受信者の電子メール アドレス**   kate@fabrikam.com

  - **メッセージの件名**   Test from Contoso

  - **メッセージの本文**   This is a test message


> [!NOTE]
> <UL>
> <LI>
> <P>Telnet クライアントのコマンドでは、大文字と小文字が区別されません。SMTP コマンドの動詞は、判別しやすいように大文字にしています。</P>
> <LI>
> <P>Telnet セッションで相手先の SMTP サーバーに接続した後で、BackSpace キーを使用することはできません。SMTP コマンドを誤って入力した場合は、Enter キーを押して再度コマンドを入力する必要があります。認識できない SMTP コマンドや構文エラーがあると、次のようなエラー メッセージが表示されます。</P><PRE><CODE>500 5.3.3 Unrecognized command</CODE></PRE></LI></UL>



1.  コマンド プロンプトで「**telnet**」と入力し、Enter キーを押します。このコマンドによって、Telnet セッションが開きます。

2.  「**set localecho**」と入力し、Enter キーを押します。これは入力した文字を画面に表示するためのコマンドですが、省略することもできます。SMTP サーバーの種類によっては、この設定が必要になります。

3.  「**set logfile**<em>\<filename\></em>」と入力します。これは、指定したログ ファイルに Telnet セッションをログ出力するためのコマンドですが、省略することもできます。ファイル名のみを指定した場合、ログ ファイルの場所は現在の作業ディレクトリになります。パスとファイル名を指定する場合、パスはコンピューターのローカル パスである必要があります。指定するパスとファイル名はいずれも Microsoft DOS の 8.3 形式で入力する必要があります。指定するパスは、既に存在するパスでなければなりません。存在しないログ ファイルを指定した場合は、そのログ ファイルが新しく作成されます。

4.  「**open mail1.fabrikam.com 25**」と入力し、Enter キーを押します。

5.  「**EHLO contoso.com**」と入力し、Enter キーを押します。

6.  「<strong>MAIL FROM:chris@contoso.com</strong>」と入力し、Enter キーを押します。

7.  「**RCPT TO:kate@fabrikam.com NOTIFY=success,failure**」と入力し、Enter キーを押します。NOTIFY コマンドは、相手先の SMTP サーバーが送信者に提供しなければならない特定の配信状態通知 (DSN) メッセージを定義するコマンドですが、省略することもできます。DSN メッセージは RFC 1891 で定義されます。この場合は、メッセージ配信の成功または失敗を確認するために DSN メッセージを要求することになります。

8.  「**DATA**」と入力し、Enter キーを押します。以下のような応答を受信します。
    
        354 Start mail input; end with <CLRF>.<CLRF>

9.  「**Subject:Test from Contoso**」と入力し、Enter キーを押します。

10. Enter キーを押します。RFC 2822 に従って、`Subject:` ヘッダー フィールドとメッセージ本文の間に空白行を 1 行入れる必要があります。

11. 「**This is a test message**」と入力し、Enter キーを押します。

12. Enter キーを押し、ピリオド ( **.** ) を入力して、再度 Enter キーを押します。以下のような応答を受信します。
    
        250 2.6.0 <GUID> Queued mail for delivery

13. 相手先の SMTP サーバーとの接続を解除するには、「**QUIT**」と入力し、Enter キーを押します。以下のような応答を受信します。
    
        221 2.0.0 Service closing transmission channel

14. Telnet セッションを閉じるには、「**quit**」と入力し、Enter キーを押します。

## 手順 4: Telnet セッションの結果を評価する

ここでは、前の例で使用された次のコマンドに対する応答について説明します。

  - Open mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    

    > [!NOTE]
    > RFC 2821 で定義されている 3 桁の SMTP 応答コードは、すべての SMTP メッセージング サーバーで同じです。SMTP メッセージング サーバーの種類によっては、テキストの部分が少し異なる場合があります。



## Open mail1.fabrikam.com 25

**成功応答**   `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**失敗応答**   `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**考えられる失敗の原因**

  - 相手先の SMTP サービスが利用できない状態にある。

  - 相手先のファイアウォールの制限がある。

  - 送信元のファイアウォールの制限がある。

  - 相手先の SMTP サーバーとして指定された FQDN または IP アドレスが正しくない。

  - 指定されたポート番号が正しくない。

## EHLO contoso.com

**成功応答**   `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**失敗応答**   `501 5.5.4 Invalid domain name`

**考えられる失敗の原因**   ドメイン名に無効な文字が含まれている。あるいは、相手先の SMTP サーバーに接続制限がある。


> [!NOTE]
> EHLO は、RFC 2821 で定義されている ESMTP (Extended Simple Message Transfer Protocol) コマンドです。ESMTP サーバーは、最初の接続時に機能について通知することができます。これらの機能には、受け付け可能なメッセージの最大サイズや、サポートしている認証方法などがあります。HELO は、RFC 821 で定義されている以前の SMTP コマンドです。ほとんどの SMTP メッセージング サーバーは、ESMTP および EHLO をサポートしています。



## MAIL FROM:chris@contoso.com

**成功応答**   `250 2.1.0 Sender OK`

**失敗応答**   `550 5.1.7 Invalid address`

**考えられる失敗の原因**   送信者の電子メール アドレスに構文エラーがある。

**失敗応答**   `530 5.7.1 Client was not authenticated`

**考えられる失敗の原因**   相手先サーバーが匿名によるメッセージ送信を受け付けない。このエラーは、Telnet を使用して、直接ハブ トランスポート サーバーにメッセージを送信しようとした場合に返されます。

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**成功応答**   `250 2.1.5 Recipient OK`

**失敗応答**   `550 5.1.1 User unknown`

**考えられる失敗の原因**   指定された受信者が組織内に存在しない。

