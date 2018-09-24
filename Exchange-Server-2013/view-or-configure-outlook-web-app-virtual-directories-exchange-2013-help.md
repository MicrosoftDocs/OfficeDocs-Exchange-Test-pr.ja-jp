---
title: 'Outlook Web App 仮想ディレクトリの表示や構成: Exchange 2013 Help'
TOCTitle: Outlook Web App 仮想ディレクトリの表示や構成
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 49896367
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 仮想ディレクトリの表示や構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-08-12_

EAC またはシェルを使用して、Outlook Web App 仮想ディレクトリのプロパティを表示または構成できます。


> [!WARNING]
> Exchange Online では、管理者が Outlook Web App 仮想ディレクトリを表示または構成することはできません。



シェルを使用して Outlook Web App 仮想ディレクトリのプロパティを表示する場合、返される情報は参照可能な情報のサブセットです。たとえば、**Get-OWAVirtualDirectory** コマンドレットを使用してプロパティを表示する場合、Exchange により次の情報が返されます。

  - 仮想ディレクトリ名

  - サーバー名

  - Exchange サーバーのバージョン

また、使用可能なパラメーターを使用することにより、特定のサーバーの特定の仮想ディレクトリに関する情報を取得できます。**Get-OWAVirtualDirectory** コマンドレットのパラメーターの詳細については、「[Get-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/aa998588\(v=exchg.150\))」を参照してください。

EAC を使用して Outlook Web App 仮想ディレクトリのプロパティを表示する場合、表示している仮想ディレクトリのほとんどのプロパティを表示できます。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App 仮想ディレクトリ」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Outlook Web App 仮想ディレクトリ プロパティを表示または構成する

1.  EAC で、<strong>サーバー</strong> \> <strong>仮想ディレクトリ</strong> をクリックします。
    
    ドロップダウン リストを使用して、サーバーと仮想ディレクトリの種類を選択できます。既定では、すべてのサーバーおよび仮想ディレクトリが表示されます。

2.  結果ウィンドウで、表示または編集する仮想ディレクトリをクリックして選択し、<strong>編集</strong> をクリックします。

3.      
    <strong>全般</strong> タブで、Outlook Web App の既定 Web サイトのプロパティを表示することと、外部 URL および内部 URL を指定することが可能です。次のオプションから表示または選択します。
    
      - <strong>サーバー</strong>   (読み取り専用)<strong>サーバー</strong> には、Outlook Web App 仮想ディレクトリをホストするサーバーの名前が表示されます。
    
      - <strong>バージョン</strong>   (読み取り専用)<strong>バージョン</strong> には、仮想ディレクトリが使用している Exchange サーバーのバージョンが表示されます。
    
      - <strong>Web サイト</strong>   (読み取り専用)<strong>Web サイト</strong> には、Web サイトの名前が表示されます。
    
      - <strong>Outlook Web App バージョン</strong>    (読み取り専用)<strong>Outlook Web App バージョン</strong> には、Exchange サーバーのバージョンが表示されます。
    
      - <strong>最終変更日時</strong>   (読み取り専用)<strong>最終変更日時</strong> には、仮想ディレクトリが最後に変更された日付と時刻が表示されます。
    
      - <strong>内部 URL</strong>   このテキスト ボックスで、内部ネットワークから Web サイトにアクセスするために使用する URL を指定します。内部 URL は、Exchange 2013 セットアップ時に自動的に構成されます。インターネットに直接接続している、または直接接続していないサーバーの既定の内部 URL 設定は、https://\<コンピューター名\>/owa です。
    
      - <strong>外部 URL</strong>   このテキスト ボックスで、インターネットから Web サイトにアクセスするために使用する URL を指定します。既定では、<strong>外部 URL</strong> は空白になっています。インターネットに直接接続しているクライアント アクセス サーバーでは、<strong>外部 URL</strong> を Active Directory サイトの DNS で公開されている値に設定する必要があります。インターネット プレゼンスがない Exchange 2013 サーバーでは、<strong>外部 URL</strong> を空白のままにする必要があります。

4.      
    <strong>認証</strong> タブでは、認証方法、サインイン形式、およびサインイン ドメインを指定します。
    
      - <strong>1 つまたは複数の標準認証方法を使用する</strong>   次の標準的な認証方法の 1 つまたは複数を使用するには、このオプションを選択します。
        
        <strong>統合 Windows 認証</strong>   この方法の場合、ユーザーは、情報にアクセスするために、Windows Server 2008 または Windows Server 2012 の有効なユーザー アカウント名とパスワードを持っている必要があります。ユーザーは、自分のアカウント名およびパスワードの入力を求められません。代わりに、サーバーはクライアント コンピューターにインストールされた Windows セキュリティ パッケージと通信し、それらの情報を確認します。統合 Windows 認証では、ユーザーに情報の入力を求めるプロンプトを表示することなく、また暗号化されていない情報をネットワーク経由で転送することなく、サーバーがユーザーを認証することができます。この方法が機能するには、クライアント コンピューターが、Exchange を実行しているサーバーと同じドメインのメンバー、または Exchange サーバーが所属しているドメインによって信頼されているドメインのメンバーである必要があります。
        
        <strong>Windows ドメイン サーバーでダイジェスト認証を使用する</strong>   この方法では、セキュリティをさらに高めるため、パスワードをハッシュ値に変換してネットワーク経由で転送します。ダイジェスト認証は、Windows Server 2008 および Windows Server 2012 ドメインで、アカウントが Active Directory に格納されているユーザーに対してのみ使用できます。ダイジェスト認証の詳細については、Windows Server のドキュメントを参照してください。
        
        <strong>基本認証 (パスワードはクリア テキストで送信されます)</strong>   この方法は、HTTP 仕様で定義されている単純な認証機構で、ユーザーのサインイン名とパスワードをエンコードしてから、ユーザーの資格情報をサーバーに送信します。パスワードのセキュリティを可能な限り保護するため、クライアント コンピューターと、クライアント アクセス サーバーの役割がインストールされているサーバーとの間で、SSL (Secure Sockets Layer) 暗号化を使用する必要があります。
    
      - <strong>フォーム ベースの認証を使用する</strong>   フォーム ベースの認証では、Outlook Web App 仮想ディレクトリのセキュリティが強化されます。フォーム ベースの認証では、Outlook Web App のサインイン ページが作成されます。フォーム ベースの認証で使用されるサインイン プロンプトの種類は構成できます。たとえば、Outlook Web App のサインイン ページで、ユーザーがドメインとユーザー名情報を "ドメイン\\ユーザー名" の形式で入力するように構成できます。
        

        > [!IMPORTANT]
        > フォーム ベースの認証では、SSL を有効にしない限り、セキュリティは保護されません。

        
        次のいずれかを選択します。
        
        <strong>ドメイン\\ユーザー名</strong>   ユーザーに、"ドメイン\\ユーザー名" の形式でドメインとユーザー名を入力するよう求めます。たとえば、Contoso ドメイン内の Kweku という名前のユーザーの場合、サインインは "contoso\\kweku" の形式で行います。
        
        <strong>ユーザー プリンシパル名 (UPN)</strong> ユーザー プリンシパル名 (UPN) サインイン形式を指定した場合、Outlook Web App サインイン ページの <strong>ユーザー名</strong> ボックスでは、ユーザーは電子メール アドレス (kweku@contoso.com など) を入力するように求められます。ユーザーの UPN と電子メール アドレスが同じでない場合、そのユーザーは、**PrincipalName** サインイン プロンプトを使用して Outlook Web App にアクセスすることはできません。ユーザーの UPN と電子メール アドレスが一致する場合のみ、**PrincipalName** サインイン プロンプトを使用することをお勧めします。
        
        <strong>ユーザー名のみ</strong> ユーザーはユーザー名 (Kweku など) のみを入力し、ドメイン名は入力しません。フォーム ベース認証に**ユーザー名のみ** サインイン プロンプトを使用する場合は、**ログオン ドメイン** プロパティも指定する必要があります。**ログオン ドメイン** プロパティは、ユーザーが Outlook Web App へのサインインを試みたときに使用する既定のドメインを判別します。たとえば、既定のドメインが Contoso の場合、Kweku という名前のドメイン ユーザーが Outlook Web App にサインインするときは、ユーザー名として「Kweku」とだけ入力する必要があります。既定のドメイン Contoso はサーバーによって使用されます。ユーザーが Contoso ドメインのメンバーでない場合は、ドメインとユーザー名を入力する必要があります。

5.      
    <strong>機能</strong> タブでは、仮想ディレクトリ上で Outlook Web App ユーザーに対して有効にする機能と無効にする機能を指定できます。
    

    > [!NOTE]
    > 個々のユーザーの機能の設定は、仮想ディレクトリの設定より優先されます。個々のユーザーのセグメンテーション設定は、<STRONG>Set-CASMailbox</STRONG> コマンドレットを使用するか、Outlook Web App&nbsp;メールボックス ポリシーを使用します。詳細については、「<A href="https://docs.microsoft.com/ja-jp/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-web-app-mailbox-policies">Outlook Web App メールボックス ポリシー</A>」を参照してください。

    
    このチェック ボックスを使用して、機能を有効または無効にします。既定では、最も一般的な機能が表示されます。有効または無効にできるすべての機能を表示するには、<strong>その他のオプション</strong> をクリックします。
    

    > [!NOTE]
    > <STRONG>[プレミアム クライアント]</STRONG> チェックボックスを使用して標準バージョンの Outlook Web App を有効または無効にするオプションは廃止されたため、設定から削除されます。標準バージョンの Outlook Web App は常に有効です。



6.      
    <strong>ファイル アクセス</strong> タブで、チェック ボックスを使用して、ファイル アクセスとユーザーの表示オプションを構成します。ファイル アクセスによって、ユーザーは電子メール メッセージに添付されているファイルの内容を開いたり、表示したりすることができます。
    
    ファイル アクセスは、ユーザーが公共または個人のコンピューターにサインインしているかどうかに基づいて制御できます。ユーザーが公共または個人のコンピューターへのアクセスを選択するオプションは、フォーム ベース認証を使用している場合にのみ選択可能です。個人のコンピューターへのアクセスに対する他の形態の既定認証。
    
      - <strong>ファイルへの直接アクセス</strong>   ファイルへの直接アクセスを有効にするには、このチェック ボックスをオンにします。ファイルへの直接アクセスが可能になると、電子メール メッセージに添付されているファイルを開くことができます。
    
      - <strong>WebReady ドキュメント表示</strong>   サポートされているドキュメントを HTML に変換して Web ブラウザーで表示できるようにするには、このチェック ボックスをオンにします。
    
      - <strong>コンバーターを使用できる場合に WebReady ドキュメント表示を強制する</strong>   ユーザーが表示アプリケーションでドキュメントを開く前に、ドキュメントを強制的に HTML に変換して Web ブラウザーで表示できるようにするには、このチェック ボックスをオンにします。ドキュメントを表示アプリケーションで開くことができるのは、ファイルへの直接アクセスが有効になっている場合だけです。

7.  <strong>保存</strong> をクリックしてポリシーの更新を完了します。

## シェルを使用して Outlook Web App 仮想ディレクトリ プロパティを構成する

この例では、サーバー Contoso 上の既定の Outlook Web App 仮想ディレクトリで基本認証を有効にします。

```powershell
    set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true
```

構文およびパラメーターの詳細については、「[Set-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123515\(v=exchg.150\))」を参照してください。

## シェルを使用して Outlook Web App 仮想ディレクトリ プロパティを表示する

この例では、Exchange 組織内でインストールされているクライアント アクセス サーバーの役割を持つすべてのコンピューター上のすべてのインターネット インフォメーション サービス (IIS) Web サイトにあるすべての Outlook Web App 仮想ディレクトリのプロパティを表示します。

```powershell
Get-OWAVirtualDirectory
```

この例では、ローカル Exchange サーバー上の既定 IIS Web サイトにある Outlook Web App 仮想ディレクトリのプロパティを表示します。

```powershell
    Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"
```

この例では、特定の Exchange サーバー上の IIS Web サイトにあるすべての Outlook Web App 仮想ディレクトリのプロパティを表示します。

```powershell
Get-OWAVirtualDirectory -server <Exchange Server Name>
```

この例では、Exchange 組織内ですべてのクライアント アクセス サーバーにあるすべての IIS Web サイトの各 Outlook Web App 仮想ディレクトリに対するプロパティ値を表示します。

```powershell
Get-OWAVirtualDirectory | format-list
```

構文およびパラメーターの詳細については、「[Get-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/aa998588\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

Outlook Web App 仮想ディレクトリが正常に編集されたことを確認するには、次の手順を実行します。

1.  EAC で、<strong>サーバー</strong> \> <strong>仮想ディレクトリ</strong> をクリックし、特定の Outlook Web App 仮想ディレクトリを選択します。

2.  <strong>編集</strong> ボタンをクリックして、仮想ディレクトリのプロパティを表示します。

3.  <strong>保存</strong> または <strong>キャンセル</strong> をクリックしてプロパティ ページを閉じます。

