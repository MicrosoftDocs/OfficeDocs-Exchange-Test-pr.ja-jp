---
title: 'Exchange 2013 での SSL オフロードの構成: Exchange 2013 Help'
TOCTitle: Exchange 2013 での SSL オフロードの構成
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61204838
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 での SSL オフロードの構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-08-22_

次の情報は、Service Pack 1 (SP1) をインストールした Exchange 2013 クライアント アクセス サーバーでプロトコルや関連サービスに対して SSL オフロードを構成する場合に役立ちます。複数のクライアント アクセス サーバーがある場合、社内組織の SP1 をインストールしたそれぞれのクライアント アクセス サーバーで、各プロトコルやサービスに必要な手順を実行する必要があります。組織内の各クライアント アクセス サーバーを同じ構成にする必要があることは言うまでもありません。新しい累積的な更新プログラム (CU) やサービス パックへのアップグレード中で、SSL オフロードを使い続ける場合、それらの更新プログラムを Exchange 2013 クライアント アクセス サーバーにアップグレードまたは適用した後に、もう一度次の手順を実行する必要があります。

SSL オフロードの最も大きな利点の 1 つは、使用されている証明書をより簡単に管理できることです。SP1 をインストールした各クライアント アクセス サーバーに別々の SSL 証明書を持つ代わりに、1 つの SSL 証明書を使用してすべてのクライアント アクセス サーバーにインポートします。SSL 証明書は既存のものでも、新たに作成した証明書ものでも使用することができます。


> [!NOTE]
> SSL オフロードを構成するためにインターネット インフォメーション サービス (IIS) マネージャ、Exchange 管理シェル、またはコマンドライン インターフェイスを使用する場合、<STRONG>既定の Web サイト</STRONG>と <STRONG>Exchange バックエンド</STRONG> サイトがあることに気を付けてください。SSL オフロードについては <STRONG>既定の Web サイト</STRONG>のみを構成し、<STRONG>Exchange バックエンド</STRONG> サイトは何も変更しないでください。



**目次**

Outlook Web App 用 SSL オフロードの構成

Exchange 管理センター (EAC) 用に SSL オフロードを構成します。

Outlook Anywhere 用の SSL オフロードの構成

オフライン アドレス帳 (OAB) 用 SSL オフロードの構成

Exchange ActiveSync (EAS) 用 SSL オフロードの構成

Exchange Web サービス (EWS) 用の SSL オフロードの構成

自動検出サービス用の SSL オフロードの構成

Mailbox Replication プロキシ (MRSProxy) サービス用の SSL オフロードの構成

Outlook クライアント (MAPI 仮想ディレクトリ) 用の SSL オフロードの構成

スクリプトを使用してすべてのプロトコルとサービスの SSL オフロードを有効にする

Exchange 2007 および Exchange 2010 との共存の構成

## 始める前に把握しておくべき情報

  - 組織内で必要なすべてのクライアント アクセス サーバーおよびメールボックス サーバーをインストールします。

  - 組織内の各クライアント アクセス サーバーおよびメールボックス サーバーに Service Pack 1 (SP1) をインストールします。SP1 をダウンロードするには、「[Exchange 2013 の更新プログラム](updates-for-exchange-2013-exchange-2013-help.md)」を参照してください。

  - [機能のアクセス許可](feature-permissions-exchange-2013-help.md)を確認して、Exchange 2013 に必要なアクセス許可を決定します。

  - クライアント アクセス サーバーに必要なアクセス許可については、「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「クライアント アクセス サーバーのアクセス許可」を参照してください。

  - クライアント アクセス サーバーに必要なアクセス許可については、「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「Outlook Web App のアクセス許可」を参照してください。

  - シェルだけを使用していくつかの手順を実行できる場合があります。社内 Exchange 組織でシェルを開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。

  - クライアント アクセス サーバーおよび SSL 接続を切断しているデバイス上で既存の証明書を使用するには、クライアント アクセス サーバーの証明書を秘密キーと共にエクスポートし、それをそのデバイスにインポートまたはインストールします。詳細については、「[Export-ExchangeCertificate](https://technet.microsoft.com/ja-jp/library/aa996305\(v=exchg.150\))」を参照してください。

  - 新しい証明書を使用するためには、EAC またはシェルを使用して新しい証明書を作成、インポートし、有効にする必要があります。詳細については、「[Exchange 2013 証明書管理 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Outlook Web App 用 SSL オフロードの構成

Outlook Web App 用に SSL オフロードを有効にするには、**既定の Web サイト**の **owa** 仮想ディレクトリの SSL 要件を削除する必要があります。

  - **ステップ 1**   インターネット インフォメーション サービス (IIS) マネージャーまたはコマンドラインを使用して、**owa** 仮想ディレクトリの SSL を無効にできます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**owa** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスをオフにしてから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。
    
      - コマンドラインを使用して次の入力を行い、Enter キーを押します。
        
            appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST

  - **ステップ 2**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeOWAAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。

ページのトップへ

## Exchange 管理センター (EAC) 用に SSL オフロードを構成します。

EAC 用に SSL オフロードを有効にするには、**既定の Web サイト** の **ecp** 仮想ディレクトリの SSL 要件を削除する必要があります。

  - **ステップ 1**   インターネット インフォメーション サービス (IIS) マネージャーまたはコマンドラインを使用して、**ecp** 仮想ディレクトリの SSL を無効にできます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**ecp** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスをオフにしてから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。
    
      - コマンドラインを使用して次の入力を行い、Enter キーを押します。
        
            appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
        


  - **ステップ 2**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeECPAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeECPAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。

ページのトップへ

## Outlook Anywhere 用の SSL オフロードの構成

Outlook Anywhere 用の SSL オフロードは既定で有効です。Outlook Anywhere クライアントは、プライベート ネットワークまたはパブリック ネットワークから電子メールを受け取れます。既定では、内部 Outlook クライアントの接続を有効にするために内部のホスト名またはサーバーの FQDN が使用されます。しかし、Outlook Anywhere が内部的に使用されない場合は、内部ホスト名を削除する必要があります。Outlook クライアントの内部および外部アクセスをどちらも許可するためには、内部および外部ホスト名を構成し、それぞれの認証方式を設定し、内部クライアント外部クライアントとも SSL を必要とするように設定します。以下に示すように、外部クライアントの認証方式を構成するには EAC や Exchange 管理シェルを使用できますが、内部クライアントにはシェルを使用しなければなりません。

  - **ステップ 1**   Outlook Anywhere の外部ホスト名を追加していない場合は、EAC またはシェルを使用できます。
    
      - EAC を使用して **\[サーバー\]** に移動し、リストでクライアント アクセス サーバーの名前を選択してから **\[編集\]** をクリックします。**\[Exchange Server\]** ウィンドウで **\[Outlook Anywhere\]** をクリックしてから **\[ユーザーが組織に接続する際に使用する外部ホスト名 (例: contoso.com) を指定します。\]** ボックスに外部ホスト名を入力します。**\[SSL オフロードを許可する\]** オプションがオンになっていることを確認し、**\[保存\]** をクリックします。
    
      - Exchange 管理シェルを使用して **\[開始\]** をクリックし、**\[開始\]** メニューで **\[Exchange 管理シェル\]** をクリックします。このウィンドウで次を入力してから、Enter キーを押します。
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic

  - **ステップ 2** 既定では SSL オフロードが有効になっています。しかし、SSL オフロードが無効にされており、これを有効にする場合は、EAC または Exchange 管理シェルを使用できます。
    
      - EAC を使用して **\[サーバー\]** に移動し、リストでクライアント アクセス サーバーの名前を選択してから **\[編集\]** をクリックします。**\[Exchange サーバー\]** ウィンドウで **\[Outlook Anywhere\]** をクリックし、**\[SSL オフロードを許可する\]** オプションをクリックしてから **\[保存\]** をクリックします。
    
      - シェルを使用して次を入力し、Enter キーを押します。
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true

  - **ステップ 3**   既定で **\[SSL が必要\]** は **Rpc** 仮想ディレクトリで選択されていませんが、SSL が無効になっていることを確認したい場合はインターネット インフォメーション サービス (IIS) マネージャーを使用できます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**Rpc** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスがオフであることを確認してから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。

  - **ステップ 4**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。


> [!IMPORTANT]
> クライアント アクセス サーバーで IIS を再起動した場合でも、サービス ホスト プロセスが 15 分ごとに Active Directory からの変更をインターネット インフォメーション サービス (IIS) に適用するのを待つ必要があります。



ページのトップへ

## オフライン アドレス帳 (OAB) 用 SSL オフロードの構成

オフライン アドレス帳 (OAB) 用に SSL オフロードを有効にするには、**既定の Web サイト**の **OAB** 仮想ディレクトリの SSL 要件を削除する必要があります。

  - **ステップ 1**   インターネット インフォメーション サービス (IIS) マネージャーまたはコマンドラインを使用して、**OAB** 仮想ディレクトリの SSL を無効にできます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**OAB** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスをオフにしてから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。
    
      - コマンドラインを使用して次の入力を行い、Enter キーを押します。
        
            appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST

  - **ステップ 2**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeOABAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeOABAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。

ページのトップへ

## Exchange ActiveSync (EAS) 用 SSL オフロードの構成

Exchange ActiveSync (EAS) 用に SSL オフロードを有効にするには、**既定の Web サイト** の **Microsoft-Server-ActiveSync** 仮想ディレクトリの SSL 要件を削除する必要があります。

  - **ステップ 1**   インターネット インフォメーション サービス (IIS) マネージャーまたはコマンドラインを使用して、**Microsoft-Server-ActiveSync** 仮想ディレクトリの SSL を無効にできます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**Microsoft-Server-ActiveSync** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスをオフにしてから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。
    
      - コマンドラインを使用して次の入力を行い、Enter キーを押します。
        
            appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST

  - **ステップ 2**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeSyncAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。

ページのトップへ

## Exchange Web サービス (EWS) 用の SSL オフロードの構成

Exchange Web サービス (EWS) 用に SSL オフロードを有効にするには、**既定の Web サイト**の **EWS** 仮想ディレクトリの SSL 要件を削除する必要があります。

  - **ステップ 1**   インターネット インフォメーション サービス (IIS) マネージャーまたはコマンドラインを使用して、**EWS** 仮想ディレクトリの SSL を無効にできます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**EWS** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスをオフにしてから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。
    
      - コマンドラインを使用して次の入力を行い、Enter キーを押します。
        
            appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST

  - **ステップ 2**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeServicesAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。

ページのトップへ

## 自動検出サービス用の SSL オフロードの構成

自動検出サービス用に SSL オフロードを有効にするには、**既定の Web サイト**の **Autodiscover** 仮想ディレクトリの SSL 要件を削除する必要があります。

  - **ステップ 1**   インターネット インフォメーション サービス (IIS) マネージャーまたはコマンドラインを使用して、**Autodiscover** 仮想ディレクトリの SSL を無効にできます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**Autodiscover** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスをオフにしてから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。
    
      - コマンドラインを使用して次の入力を行い、Enter キーを押します。
        
            appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST

  - **ステップ 2**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。

ページのトップへ

## Mailbox Replication プロキシ (MRSProxy) サービス用の SSL オフロードの構成

メールボックス レプリケーション プロキシ (MRSProxy) サービスは、すべての Exchange 2013 クライアント アクセス サーバーにインストールされます。MRSProxy は社内のフォレスト間移動要求を行ったり、社内メールボックスを Office 365 に移動したりするのに役立ちます。ただし、既定で MRSProxy は無効になっています。これを有効にする場合は、リモート Exchange フォレスト (社内フォレスト間メールボックス移動用) や社内 Exchange フォレスト (Office 365 へのメールボックス移動用) で MRSProxy を有効にする必要があります。MRSProxy サービスは Exchange Web サービス (EWS) 下で実行されますが、SSL オフロードの構成はサポートしていません。

この理由は、MRSProxy サービスはトラフィックが署名および暗号化されることを想定しているからです。すべてのハードウェア ロード バランサーまたはファイアウォールは、MRSProxy のトラフィックをクライアント アクセス サーバーに送信する前に、再度暗号化する必要があります。その場合、オフロードが機能するように SSL ブリッジを構成することをお勧めします。

**リバース SSL または SSL ブリッジ**   ハードウェア ロード バランサーでリバース SSL または SSL ブリッジを有効にすると、各 CAS サーバーについてこれまでの手順を実行する必要がなくなります。ただし、ハードウェア ロード バランサーでリバース SSL を有効にするということは、SSL 暗号化およ復号化がクライアント アクセス サーバーで行われることを意味します。この場合、SSL 暗号化および復号化はハードウェア ロード バランサーとクライアント アクセス サーバーの両方で発生します。Exchange 2013 SSL オフロードの使用を選択するか、またはリバース SSL (SSL ブリッジ) を選択するかは、組織の目標と実装する必要があるセキュリティ事項により左右されます。次の図は SSL ブリッジ (リバース SSL) が有効にされたクライアント接続を示しています。

![SSL ブリッジ](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "SSL ブリッジ")

## Outlook クライアント (MAPI 仮想ディレクトリ) 用の SSL オフロードの構成

Outlook クライアント用に SSL オフロードを有効にするには、**既定の Web サイト** の **MAPI** 仮想ディレクトリの SSL 要件を削除する必要があります。

  - **ステップ 1**   インターネット インフォメーション サービス (IIS) マネージャーまたはコマンドラインを使用して、**MAPI** 仮想ディレクトリの SSL を無効にできます。
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用して、**\[サイト\]** \> **\[既定の Web サイト\]** を展開し、**MAPI** 仮想ディレクトリを選択します。結果ウィンドウの **\[IIS\]** の下で **\[SSL 設定\]** をダブルクリックします。**\[SSL 設定\]** の結果ウィンドウで、**\[SSL が必要\]** チェック ボックスをオフにしてから**\[アクション\]** ウィンドウの **\[適用\]** をクリックします。
    
      - コマンドラインを使用して次の入力を行い、Enter キーを押します。
        
            appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST

  - **ステップ 2**   次のいずれかの方法で正しいアプリケーション プールをリサイクルするか、またはインターネット インフォメーション サービスを再起動する必要があります。
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
    
      - Windows PowerShell コマンドレットを使用して次を入力し、Enter キーを押します。
        
            IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
    
      - コマンドラインを使用: **\[スタート\]** \> **\[実行\]** を選択し、**「cmd」**と入力してから Enter キーを押します。コマンド プロンプト ウィンドウで次を入力し、Enter キーを押します。
        
            iisreset /noforce
    
      - インターネット インフォメーション サービス (IIS) マネージャーを使用: インターネット インフォメーション サービス (IIS) マネージャーの **\[アクション\]** ウィンドウで、**\[再起動\]** をクリックします。

ページのトップへ

## スクリプトを使用してすべてのプロトコルとサービスの SSL オフロードを有効にする

複数の Exchange 2013 クライアント アクセス サーバーがある大規模な組織で作業をしているなら、これまで見てきた手順をもっと迅速に実行することが必要な場合があります。次のいずれかのスクリプトのコマンドをメモ帳にコピー、貼り付けし、必要な変更を行い, .ps1 拡張子を付けてそのファイルを保存してから、それを Exchange 管理シェルから実行できます。単一または複数のクライアント アクセス サーバーのすべてのプロトコルおよびサービスに対して SSL オフロードを構成するためには、必要に応じて、これらのいずれのスクリプトも使用できます。


> [!NOTE]
> <STRONG>Set-OutlookAnywhere</STRONG> コマンドレット入力の場合は、"MyServer" をクライアント アクセス サーバーの名前に置き換えてください。



**Set-WebConfigurationProperty の使用**

    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
    iisreset /noforce

**Appcmd の使用**


> [!NOTE]
> <STRONG>Set-OutlookAnywhere</STRONG> コマンドレット入力の場合は、"MyServer" をクライアント アクセス サーバーの名前に置き換えてください。



    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
    iisreset /noforce

ページのトップへ

## Exchange 2007 および Exchange 2010 との共存の構成

組織に Exchange 2003 サーバーと Exchange 2010 サーバーが混在している場合の共存シナリオで、Exchange 2010 クライアント アクセス サーバーのデプロイ後に実行しなければならない最初のステップは、Exchange 2003 ユーザーが Exchange 2010 クライアント アクセス サーバーのグループから自分のメールボックスにアクセスできるように、DNSを変更することです。このようなシナリオでは、クライアントのトラフィックをクライアント アクセス サーバー間に分配するために使用されるロード バランサーの SSL オフロードを有効にすることが完全にサポートされます。

**Outlook Web App の他のバージョンとの共存**

Exchange 2013 のクライアント アクセス サーバーで構成されている SSL オフロードでは、Exchange 2007 と Exchange 2010 との共存が可能です。

  - Exchange 2007 との共存には以前の名前空間が必要で、Outlook Web App と Exchange Web サービスの場合にのみその名前空間へのリダイレクトが発生します。自動検出、Outlook Anywhere および Exchange ActiveSync は、以前のバージョンにプロキシされます。

  - 外部 URL を設定している場合、Exchange 2010 との共存にはリダイレクトが使用されます。それ以外の場合は、プロキシが使用されます。

ページのトップへ

