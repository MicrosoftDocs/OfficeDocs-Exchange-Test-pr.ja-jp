---
title: 'メール フローおよびクライアント アクセスの構成: Exchange 2013 Help'
TOCTitle: メール フローおよびクライアント アクセスの構成
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 49129424
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール フローおよびクライアント アクセスの構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

SSL 証明書を構成する方法など、Exchange Server 2013 メール フローおよびクライアント アクセスのインストール後の作業。

組織に Microsoft Exchange Server 2013 をインストールした後は、Exchange Server 2013 をメール フローとクライアント アクセス用に構成する必要があります。これらの手順を実行しないと、Microsoft Office Outlook などのインターネットおよび外部クライアントへのメールの送信や、Exchange 組織への Exchange ActiveSync デバイスの接続が行えなくなります。

このトピックの手順では、基本的な Exchange 展開に、Active Directory サイト 1 つと SMTP (簡易メール転送プロトコル) 名前空間 1 つが存在することを前提とします。


> [!IMPORTANT]
> このトピックの例では、Ex2013CAS や contoso.com、mail.contoso.com、172.16.10.11 などの値を使用します。これらの例の値は、組織のサーバー名、FQDN、および IP アドレスに置き換えてください。



メール フロー、およびクライアントとデバイスに関連するその他の管理タスクについては、「[メール フロー](mail-flow-exchange-2013-help.md)」および「[クライアントとモバイル](clients-and-mobile-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:50 分

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - クライアント アクセス サーバーで Secure Sockets Layer (SSL) 証明書を構成するまでは、Exchange 管理センター (EAC) Web サイトに接続する際に証明書の警告を受信することがあります。この証明書を構成する方法については、後述します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!IMPORTANT]
> 各組織では、Active Directory フォレスト内に最低でも 1 つのクライアント アクセス サーバーと 1 つのメールボックス サーバーが必要です。また、メールボックス サーバーを含む各 Active Directory サイトには、クライアント アクセス サーバーが少なくとも 1 つ含まれている必要があります。サーバーの役割を分離している場合は、最初にメールボックス サーバーの役割をインストールすることをお勧めします。




> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:送信コネクタを作成します。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「送信コネクタ」。

インターネットにメールを送信できるようにするには、事前に送信コネクタをメールボックス サーバー上に作成しておく必要があります。次の手順を実行します。

1.  クライアント アクセス サーバーの URL を参照して、EAC を開きます。(例: https://Ex2013CAS/ECP)。

2.  <strong>ドメイン\\ユーザー名</strong> と <strong>パスワード</strong> にユーザー名とパスワードを入力して、<strong>サイン イン</strong> をクリックします。

3.  <strong>メール フロー</strong> \> <strong>送信コネクタ</strong> に移動します。<strong>送信コネクタ</strong> ページで、<strong>新規作成</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  **送信コネクタの新規作成**ウィザードで、送信コネクタの名前を指定し、<strong>インターネット</strong> を選択します。<strong>次へ</strong> をクリックします。

5.  <strong>受信者のドメインに関連付けられた MX レコード</strong> が選択されていることを確認します。<strong>次へ</strong> をクリックします。

6.  <strong>アドレス スペース</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。<strong>ドメインの追加</strong> ウィンドウの <strong>種類</strong> フィールドで <strong>SMTP</strong> が選択されていることを確認します。<strong>完全修飾ドメイン名 (FQDN)</strong> フィールドに、「**\***」と入力します。<strong>保存</strong> をクリックします。

7.  <strong>スコープ送信コネクタ</strong> チェック ボックスがオフになっていることを確認し、<strong>次へ</strong> をクリックします。

8.  <strong>送信元サーバー</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>サーバーの選択</strong> ウィンドウで、メールボックス サーバーを選択します。サーバーを選択したら、<strong>追加</strong>、<strong>OK</strong> の順にクリックします。

9.  <strong>終了</strong> をクリックします。


> [!NOTE]
> 既定の受信側の受信コネクタは、Exchange 2013 をインストールしたときに作成されます。この受信コネクタは、外部サーバーからの匿名 SMTP 接続を受け入れます。既定の受信コネクタをそのまま使用するのであれば、追加の設定を行う必要はありません。外部サーバーからの受信接続を制限する必要がある場合は、クライアント アクセス サーバーで <STRONG>[既定のフロントエンド &lt;クライアント アクセス サーバー&gt;]</STRONG> 受信コネクタを変更してください。



## このステップの検証方法

送信側の送信コネクタが正常に作成されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>メール フロー</strong> \> <strong>送信コネクタ</strong> に新しい送信コネクタが表示されているのを確認します。

2.  Outlook Web App を開き、電子メール メッセージを外部の受信者に送信します。受信者がメッセージを受信する場合は、送信コネクタが正常に構成されています。

## 手順 2:承認済みドメインを追加する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「承認済みドメイン」。

既定では、Active Directory フォレスト内に新しい Exchange 2013 組織を展開すると、Exchange は Setup/PrepareAD を実行していた Active Directory ドメインのドメイン名を使用します。受信者が別のドメインとメッセージを送受信できるようにするには、ドメインを承認済みドメインとして追加する必要があります。また、このドメインは、次の手順で説明する既定の電子メール アドレス ポリシーにプライマリ SMTP アドレスとして追加されます。


> [!IMPORTANT]
> インターネットから電子メールを受け付ける SMTP ドメインごとに、パブリック ドメイン ネーム システム (DNS) の MX リソース レコードが必要です。各 MX レコードは、組織の電子メールを受信するための、インターネットに接続されているサーバーに解決される必要があります。



1.  クライアント アクセス サーバーの URL を参照して、EAC を開きます。(例: https://Ex2013CAS/ECP)。

2.  <strong>ドメイン\\ユーザー名</strong> と <strong>パスワード</strong> にユーザー名とパスワードを入力して、<strong>サイン イン</strong> をクリックします。

3.  <strong>メール フロー</strong> \> <strong>承認済みドメイン</strong> に移動します。<strong>承認済みドメイン</strong> ページで、<strong>新規作成</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  <strong>承認済みドメインの新規作成</strong> ウィザードで、承認済みドメインの名前を指定します。

5.  <strong>承認済みドメイン</strong> フィールドに、追加する SMTP 受信者ドメインを指定します。たとえば、contoso.com と指定します。

6.  <strong>権限のあるドメイン</strong> を選択し、<strong>保存</strong> をクリックします。

## このステップの検証方法

承認済みドメインが正常に作成されたことを確認するには、次の手順を実行します。

  - EAC で、<strong>メール フロー</strong> \> <strong>承認済みドメイン</strong> に新しい承認済みドメインが表示されているのを確認します。

## 手順 3:既定の電子メール アドレス ポリシーを構成する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「電子メール アドレス ポリシー」。

前の手順で承認済みドメインを追加し、そのドメインを組織内のすべての受信者に追加する場合は、既定の電子メール アドレス ポリシーを更新する必要があります。

1.  クライアント アクセス サーバーの URL を参照して、EAC を開きます。(例: https://Ex2013CAS/ECP)。

2.  <strong>ドメイン\\ユーザー名</strong> と <strong>パスワード</strong> にユーザー名とパスワードを入力して、<strong>サイン イン</strong> をクリックします。

3.  <strong>メール フロー</strong> \> <strong>電子メール アドレス ポリシー</strong> に移動します。<strong>電子メール アドレス ポリシー</strong> ページで、<strong>既定のポリシー</strong> を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>既定の電子メール アドレス ポリシー</strong> ページで、<strong>電子メール アドレスの形式</strong> をクリックします。

5.  <strong>電子メール アドレスの形式</strong> の下で、変更する SMTP アドレスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

6.  <strong>電子メール アドレスの形式</strong> ページの <strong>電子メール アドレスのパラメーター</strong> フィールドに、Exchange 組織内のすべての受信者に適用する SMTP 受信者ドメインを指定します。このドメインは、前の手順で追加した承認済みドメインに一致する必要があります。たとえば、「@contoso.com」と入力して <strong>保存</strong> をクリックします。

7.  <strong>保存</strong> をクリックします

8.  <strong>既定のポリシー</strong> 詳細ウィンドウで、<strong>適用</strong> をクリックします。


> [!NOTE]
> 各ユーザーのプライマリ電子メール アドレスに一致するユーザー プリンシパル名 (UPN) を設定することをお勧めします。ユーザーの電子メール アドレスに一致する UPN を入力しないと、ユーザーは電子メール アドレスのほかに、ドメイン/ユーザー名または UPN を手動で入力しなければならなくなります。ユーザーの UPN がユーザーの電子メール アドレスと一致しないと、Outlook Web App、ActiveSync、および Outlook はユーザーの電子メール アドレスを自動的に UPN に一致させます。



## このステップの検証方法

既定の電子メール アドレス ポリシーが正常に構成されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。

2.  メールボックスを選択して、受信者詳細ウィンドウで、<strong>ユーザー メールボックス</strong> フィールドに、*\<エイリアス\>*@*\<新しい承認済みドメイン\>* が設定されていることを確認します。(例: david@contoso.com)。

3.  必要に応じて、メールボックスを新規に作成し、次の手順を実行して作成したメールボックスに、新しい承認済みのドメインが設定されている電子メール アドレスが指定されていることを確認します。
    
    1.  <strong>受信者</strong> \> <strong>メールボックス</strong> の順に移動して、<strong>新規作成</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックし <strong>ユーザー メールボックス</strong> を選択します。
    
    2.  新しいユーザー メールボックス ページで、新しいメールボックスを作成するために必要な情報を入力します。<strong>保存</strong> をクリックします。
    
    3.  新しいメールボックスを選択して、受信者詳細ウィンドウで、<strong>ユーザー メールボックス</strong> フィールドに、*\<エイリアス\>*@*\<新しい承認済みドメイン\>* が設定されていることを確認します。(例: david@contoso.com)。

## 手順 4:外部 URL を構成する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「*\<サービス\>* 仮想ディレクトリの設定」。

クライアントがインターネットから新しいサーバーに接続する前に、外部ドメインまたは URL をクライアント アクセス サーバーの仮想ディレクトリで構成してから、パブリック ドメイン名サービス (DNS) レコードを構成する必要があります。以降の手順では、各仮想ディレクトリの外部 URL に同じ外部ドメインを構成します。1 つまたは複数の仮想ディレクトリの外部 URL に異なる外部ドメインを構成する場合は、外部 URL を手動で構成する必要があります。詳細については、「[仮想ディレクトリの管理](virtual-directory-management-exchange-2013-help.md)」を参照してください。

1.  クライアント アクセス サーバーの URL を参照して、EAC を開きます。(例: https://Ex2013CAS/ECP)。

2.  <strong>ドメイン\\ユーザー名</strong> と <strong>パスワード</strong> にユーザー名とパスワードを入力して、<strong>サイン イン</strong> をクリックします。

3.  <strong>サーバー</strong>\><strong>サーバー</strong> に移動して、インターネットに直接接続しているクライアント アクセス サーバーの名前を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>Outlook Anywhere</strong> をクリックします。

5.  <strong>外部ホスト名の指定</strong> フィールドに、クライアント アクセス サーバーの外部アクセス可能な FQDN を指定します。たとえば、「mail.contoso.com」と入力します。

6.  ここで、クライアント アクセス サーバーの内部アクセス可能な FQDN も併せて設定します。<strong>内部ホスト名の指定</strong> フィードに、前の手順で使用した FQDN を追加します。たとえば、「mail.contoso.com」と入力します。

7.  <strong>保存</strong> をクリックします。

8.  <strong>サーバー</strong> \> <strong>仮想ディレクトリ</strong> に移動し、<strong>外部のアクセス ドメインの構成</strong> ![\[構成\] アイコン](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "[構成] アイコン") をクリックします。

9.  <strong>外部 URL を使用するクライアント アクセス サーバーを選択します</strong> の下の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

10. 構成するクライアント アクセス サーバーを選択し、<strong>追加</strong> をクリックします。構成するクライアント アクセス サーバーをすべて追加したら、<strong>OK</strong> をクリックします。

11. <strong>外部のクライアント アクセス サーバーで使用するドメイン名を入力してください</strong> で、適用する外部ドメインを入力します。たとえば、「mail.contoso.com」と入力し、<strong>保存</strong> をクリックします。
    

    > [!NOTE]
    > 一部の組織では、Outlook Web App の FQDN を一意にすることで、基になるサーバーの FQDN の変更からユーザーを保護します。多くの組織では、Outlook Web App の FQDN に mail.contoso.com ではなく owa.contoso.com を使用します。Outlook Web App の一意の FQDN を構成する場合は、前の手順を実行した後に、以下を実行します。このチェックリストは、Outlook Web App の FQDN が一意に構成されていることを前提としています。 
    > <OL>
    > <LI>
    > <P><STRONG>[owa (既定の Web サイト)]</STRONG> を選択して、<STRONG>[編集]</STRONG>&nbsp;<IMG title=編集アイコン alt=編集アイコン src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> をクリックします。</P>
    > <LI>
    > <P><STRONG>[外部 URL]</STRONG> に、<STRONG>https://</STRONG>、使用する一意の Outlook Web App の FQDN、<STRONG>/owa</STRONG> の順に入力します。たとえば、https://owa.contoso.com/owa と入力します。</P>
    > <LI>
    > <P><STRONG>[保存]</STRONG> をクリックします。</P>
    > <LI>
    > <P><STRONG>[ecp (既定の Web サイト)]</STRONG> を選択して、<STRONG>[編集]</STRONG>&nbsp;<IMG title=編集アイコン alt=編集アイコン src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> をクリックします。</P>
    > <LI>
    > <P><STRONG>[外部 URL]</STRONG> に、<STRONG>https://</STRONG>、前の手順で指定した Outlook Web App の FQDN、<STRONG>/ecp</STRONG> の順に入力します。たとえば、https://owa.contoso.com/ecp と入力します。</P>
    > <LI>
    > <P><STRONG>[保存]</STRONG> をクリックします。</P></LI></OL>



クライアント アクセス サーバーの仮想ディレクトリに外部 URL を構成したら、自動検出、Outlook Web App、メール フローのパブリック DNS レコードを構成する必要があります。パブリック DNS レコードはインターネットに直接接続しているクライアント アクセス サーバーの外部 IP アドレスまたは FQDN をポイントし、クライアント アクセス サーバー上に構成した外部アクセス可能な FQDN を使用します。メール フローおよび外部クライアント接続を有効にするために作成する必要がある、推奨 DNS レコードの例を以下に示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS レコードの種類</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## このステップの検証方法

クライアント アクセス サーバーの仮想ディレクトリに外部 URL が正常に構成されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>サーバー</strong> \> <strong>仮想ディレクトリ</strong> に移動します。

2.  <strong>サーバーの選択</strong> フィールドで、インターネットに直接接続しているクライアント アクセス サーバーを選択します。

3.  仮想ディレクトリを選択し、\[仮想ディレクトリ\] 詳細ウィンドウで、以下に示すように <strong>外部 URL</strong> フィールドに適切な FQDN およびサービスが設定されていることを確認します。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>仮想ディレクトリ</th>
    <th>外部 URL 値</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自動検出</strong></p></td>
    <td><p>外部 URL は表示されない</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


パブリック DNS レコードが正しく構成されたかどうかを確認するには、以下の手順を実行します。

1.  コマンド プロンプトを開き、`nslookup.exe` を実行します。

2.  パブリック DNS ゾーンのクエリが可能な DNS サーバーに変更します。

3.  `nslookup` で、作成した各 FQDN のレコードを参照します。各 FQDN に返される値が正しいことを確認します。

4.  `nslookup` で、「`set type=mx`」を入力して、手順 1 で追加した承認済みのドメインを参照し、返された値がクライアント アクセス サーバーの FQDN に一致していることを確認します。

## 手順 5:内部 URL を構成します。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「*\<サービス\>* 仮想ディレクトリの設定」。

クライアントがイントラネットから新しいサーバーに接続する前に、内部ドメインまたは URL をクライアント アクセス サーバーの仮想ディレクトリで構成してから、プライベート ドメイン名サービス (DNS) レコードを構成する必要があります。

以下の手順では、ユーザーがイントラネット上とインターネット上で同じ URL を使用して Exchange サーバーにアクセスできるようにするか、または異なる URL を使用するかを選択します。どちらを選択するかは、使用中または導入予定のアドレス指定方式によって異なります。新しいアドレス指定方式を実装しようとしている場合、内部と外部の URL に同じ URL を使用することをお勧めします。同じ URL を使用すると、1 つのアドレスのみ記憶しておけばよいため、ユーザーは簡単に Exchange サーバーにアクセスできるようになります。どちらを選択する場合でも、構成するアドレス空間に対するプライベート DNS ゾーンを構成する必要があります。DNS ゾーンの管理の詳細については、「[DNS サーバーを管理する](http://go.microsoft.com/fwlink/p/?linkid=190631)」を参照してください。

仮想ディレクトリ上の内部 URL および外部 URL の詳細については、「[仮想ディレクトリの管理](virtual-directory-management-exchange-2013-help.md)」を参照してください。

## 内部 URL と外部 URL に同じ URL を構成する

1.  クライアント アクセス サーバー上で Exchange 管理シェルを開きます。

2.  クライアント アクセス サーバーのホスト名を、次の手順で使用する変数に保存します。たとえば、Ex2013CAS です。
    
    ```powershell
$HostName = "Ex2013CAS"
```

3.  シェルで次の各コマンドを実行して、仮想ディレクトリの外部 URL と一致するように各内部 URL を構成します。
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  引き続き、シェル上でオフライン アドレス帳 (OAB) を構成し、自動検出を使って、OAB を配布する上で正しい仮想ディレクトリを選択できるようにします。この手順を行うには、次のコマンドを実行します。
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

クライアント アクセス サーバーの仮想ディレクトリに内部 URL を構成したら、Outlook Web App とその他の接続用に個人用の DNS レコードを構成する必要があります。構成に応じて、クライアント アクセス サーバーの内部または外部 IP アドレスまたは完全修飾ドメイン名 (FQDN) をポイントするように、プライベート DNS レコードを構成する必要があります。内部クライアント接続を有効にする場合に作成する推奨 DNS レコードの例を以下に示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS レコードの種類</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## このステップの検証方法

クライアント アクセス サーバーの仮想ディレクトリに内部 URL が正常に構成されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>サーバー</strong> \> <strong>仮想ディレクトリ</strong> に移動します。

2.  <strong>サーバーの選択</strong> フィールドで、インターネットに直接接続しているクライアント アクセス サーバーを選択します。

3.  仮想ディレクトリを選択し、<strong>編集</strong> ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  次のように、<strong>内部 URL</strong> フィールドに正しい FQDN とサービスが読み込まれることを確認します。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>仮想ディレクトリ</th>
    <th>内部 URL の値</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自動検出</strong></p></td>
    <td><p>内部 URL は表示されない</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


プライベート DNS レコードが正しく構成されたかどうかを確認するには、以下の手順を実行します。

1.  コマンド プロンプトを開き、`nslookup.exe` を実行します。

2.  プライベート DNS ゾーンのクエリが可能な DNS サーバーに変更します。

3.  `nslookup` で、作成した各 FQDN のレコードを参照します。各 FQDN に返される値が正しいことを確認します。

## 内部 URL と外部 URL に異なる URL を構成する

1.  クライアント アクセス サーバーの URL を参照して、EAC を開きます。(例: https://Ex2013CAS/ECP)。

2.  <strong>サーバー</strong> \> <strong>仮想ディレクトリ</strong> に移動します。

3.  <strong>サーバーの選択</strong> フィールドで、インターネットに直接接続しているクライアント アクセス サーバーを選択します。

4.  変更する仮想ディレクトリを選択し、<strong>編集</strong> ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

5.  <strong>内部 URL</strong> で、**https://** と最初のスラッシュ (**/**) との間のホスト名を新しく使用する FQDN に置き換えます。たとえば、EWS 仮想ディレクトリの FQDN を Ex2013CAS.corp.contoso.com から internal.contoso.com に変更する場合、内部 URL を https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx から https://internal.contoso.com/ews/exchange.asmx に変更します。

6.  <strong>保存</strong> をクリックします。

7.  変更する仮想ディレクトリごとに手順 5 および 6 を繰り返します。
    

    > [!NOTE]
    > ECP 仮想ディレクトリと OWA 仮想ディレクトリの内部 URL は同じでなければなりません。<BR>自動検出仮想ディレクトリに内部 URL を設定することはできません。



8.  最後に、シェルを開いてオフライン アドレス帳 (OAB) を構成し、自動検出を使って、OAB を配布する上で正しい仮想ディレクトリを選択できるようにします。この手順を行うには、次のコマンドを実行します。
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

クライアント アクセス サーバーの仮想ディレクトリに内部 URL を構成したら、Outlook Web App とその他の接続用に個人用の DNS レコードを構成する必要があります。構成に応じて、クライアント アクセス サーバーの内部または外部 IP アドレスまたは FQDN をポイントするように、プライベート DNS レコードを構成する必要があります。仮想ディレクトリの内部 URL で internal.contoso.com を使用するよう構成した場合に、内部クライアントの接続を有効にするために作成する必要がある推奨の DNS レコードの例を以下に示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS レコードの種類</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## このステップの検証方法

クライアント アクセス サーバーの仮想ディレクトリに内部 URL が正常に構成されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>サーバー</strong> \> <strong>仮想ディレクトリ</strong> に移動します。

2.  <strong>サーバーの選択</strong> フィールドで、インターネットに直接接続しているクライアント アクセス サーバーを選択します。

3.  仮想ディレクトリを選択し、<strong>編集</strong> ![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>内部 URL</strong> フィールドに正しい FQDN が読み込まれることを確認します。たとえば、internal.contoso.com を使用するように内部 URL を設定したと仮定します。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>仮想ディレクトリ</th>
    <th>内部 URL の値</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自動検出</strong></p></td>
    <td><p>内部 URL は表示されない</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


プライベート DNS レコードが正しく構成されたかどうかを確認するには、以下の手順を実行します。

1.  コマンド プロンプトを開き、`nslookup.exe` を実行します。

2.  プライベート DNS ゾーンのクエリが可能な DNS サーバーに変更します。

3.  `nslookup` で、作成した各 FQDN のレコードを参照します。各 FQDN に返される値が正しいことを確認します。

## 手順 6:SSL 証明書を構成する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「証明書管理」。

Outlook Anywhere や Exchange ActiveSync などの一部のサービスでは、Exchange 2013 サーバー上で証明書を構成する必要があります。次の手順では、サードパーティの証明機関 (CA) 発行の SSL 証明書の構成方法を説明します。

1.  クライアント アクセス サーバーの URL を参照して、EAC を開きます。(例: https://Ex2013CAS/ECP)。

2.  <strong>ドメイン\\ユーザー名</strong> と <strong>パスワード</strong> にユーザー名とパスワードを入力して、<strong>サイン イン</strong> をクリックします。

3.  <strong>サーバー</strong> \> <strong>証明書</strong> に移動します。<strong>証明書</strong> ページの <strong>サーバーの選択</strong> フィールドで、お使いのクライアント アクセス サーバーが選択されていることを確認し、<strong>新規作成</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  <strong>Exchange 証明書の新規作成</strong> ウィザードで、<strong>証明機関発行の証明書の要求を作成する</strong> を選択し、<strong>次へ</strong> をクリックします。

5.  この証明書の名前を指定し、<strong>次へ</strong> をクリックします。

6.  ワイルドカード証明書を要求する場合は、<strong>ワイルドカード証明書の要求</strong> を選択し、<strong>ルート ドメイン</strong> フィールドにすべてのサブドメインのルート ドメインを指定します。ワイルドカード証明書を要求せずに、証明書に追加する各ドメインを指定する場合は、このページは空欄にしたままにします。<strong>次へ</strong> をクリックします。

7.  <strong>参照</strong> をクリックし、証明書を保存する Exchange サーバーを指定します。選択するサーバーは、インターネットに直接接続しているクライアント アクセス サーバーである必要があります。<strong>次へ</strong> をクリックします。

8.  リストに一覧表示される各サービスについて、ユーザーが Exchange サーバーに接続する際に使用する外部または内部サーバー名が正しいことを確認します。たとえば、
    
      - 内部 URL と外部 URL が同じになるように構成した場合、<strong>Outlook Web App (インターネットからアクセスした場合)</strong> と <strong>Outlook Web App (イントラネットからアクセスした場合)</strong> には "owa.contoso.com" が、<strong>OAB (インターネットからアクセスした場合)</strong> と <strong>OAB (イントラネットからアクセスした場合)</strong> には、"mail.contoso.com" が表示されている必要があります。
    
      - 内部 URL に internal.contoso.com を構成している場合は、<strong>Outlook Web App (インターネットからアクセスした場合)</strong> に owa.contoso.com と表示され、<strong>Outlook Web App (イントラネットからアクセスした場合)</strong> に internal.contoso.com と表示されます。
    
    これらのドメインは、SSL 証明書の要求を作成するために使用されます。<strong>次へ</strong> をクリックします。

9.  SSL 証明書に含める追加のドメインがあれば、それを追加します。

10. 証明書の共通名にするドメインを選択し、<strong>共通名として設定する</strong> をクリックします。たとえば、"contoso.com" を選択し、<strong>次へ</strong> をクリックします。

11. 組織に関する情報を入力します。この情報は、SSL 証明書に含まれます。<strong>次へ</strong> をクリックします。

12. この証明書の要求を保存するネットワーク上の場所を指定します。<strong>終了</strong> をクリックします。

証明書の要求を保存したら、この要求を証明機関 (CA) に送信します。組織によっては、この証明機関は内部 CA またはサードパーティ CA になります。クライアント アクセス サーバーに接続するクライアントは、使用する CA を信頼する必要があります。CA が発行する証明書を受信したら、次の手順を実行します。

1.  EAC の <strong>サーバー</strong> \> <strong>証明書</strong> ページで、前の手順で作成した証明書の要求を選択します。

2.  \[証明書の要求\] 詳細ウィンドウで、<strong>状態</strong> の下の <strong>完了</strong> をクリックします。

3.  \[保留中の要求の完了\] ページで、SSL 証明書ファイルのパスを指定し、<strong>OK</strong> をクリックします。

4.  追加した新しい証明書を指定し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

5.  \[証明書\] ページで、<strong>サービス</strong> をクリックします。

6.  この証明書に割り当てるサービスを選択します。少なくとも、<strong>SMTP</strong> と <strong>IIS</strong> は選択する必要があります。<strong>保存</strong> をクリックします。

7.  <strong>既存の既定の SMTP 証明書を上書きしますか?</strong> という警告メッセージが表示された場合は、<strong>はい</strong> をクリックします。

## このステップの検証方法

新しい証明書が正常に追加されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>サーバー</strong> \> <strong>証明書</strong> に移動します。

2.  新しい証明書を選択し、証明書の詳細ウィンドウで、以下のように設定されていることを確認します。
    
      - <strong>状態</strong> に <strong>有効</strong> が表示されていること。
    
      - <strong>サービスに割り当て済み</strong> に少なくとも <strong>IIS</strong> と <strong>SMTP</strong> が表示されていること。

## このタスクの検証方法

メール フローと外部クライアント アクセスが構成されたことを確認するには、次の手順を実行します。

1.  Outlook 内または Exchange ActiveSync デバイスで、あるいはその両方で、新しいプロファイルを作成します。Outlook またはモバイル デバイスによって新しいプロファイルが正しく作成されていることを確認します。

2.  Outlook 内またはモバイル デバイスで、新しいメッセージを外部の受信者に送信します。外部の受信者がメッセージを受信することを確認します。

3.  外部の受信者のメールボックスで、Exchange メールボックスから送信したメッセージに返信します。Exchange メールボックスがメッセージを受信することを確認します。

4.  https://owa.contoso.com/owa に移動し、証明書の警告がないことを確認します。

