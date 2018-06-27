---
title: 'Exchange 2013 のリリース ノート: Exchange 2013 Help'
TOCTitle: Exchange 2013 のリリース ノート
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 48269213
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 のリリース ノート

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2018-04-16_

Microsoft Exchange Server 2013 へようこそ\! このトピックには、Exchange 2013 を正しく展開するために知っておくべき重要な情報が含まれています。展開を開始する前に、このトピックのすべてに目を通しておいてください。

このトピックは、以下のセクションで構成されています。

  - セットアップと展開

  - Exchange 管理シェル

  - メールボックス

  - パブリック フォルダー

  - メール フロー

  - クライアント接続

  - Exchange 2010 との共存

## セットアップと展開

  - **msExchProductId が、インストーﾙされている Exchange 2013 リリース バージョンを反映しない** Exchange によって Active Directory スキーマが拡張され、Exchange 用に Active Directory の準備を行った後、いくつかのプロパティが更新されて準備が整ったことが示されます。こうしたプロパティの 1 つは、`Configuration` 名前付けコンテキスト内の `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` コンテナーにある *msExchangeProductId* です。 インストールしている Exchange 2013 のリリースに Active Directory スキーマの変更が導入されていない場合、このプロパティは更新されないか、予期しない値を示すことがあります。この値が、インストールしている Exchange 2013 のバージョンと一致しないと、混乱の原因となる恐れがあります。
    
    *msExchProductId* の値が、インストールされている Exchange 2013 のバージョンを反映していないと、この動作が予想されます。このプロパティは、Active Directory スキーマに最後に変更を加えた Exchange 2013 のバージョンを反映します。混乱を避けるため、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」の「[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)」セクションに記されている手順に従って、Active Directory が更新されており、インストールしている Exchange 2013 リリースに対して準備が整っていることを確認するようお勧めします。

  - **セットアップが誤って .NET Framework 4.0** を要求する   .NET Framework がインストールされていないコンピューターに Exchange 2013 をインストールしようとすると、実際には .NET Framework 4.5 以降が必要である場合に、セットアップは誤って .NET Framework 4.0 のインストールを要求します。
    
    この問題を回避するには, .NET Framework 4.5 以降をインストールします。.NET Framework 4.0 をインストールする必要はありません。すべての前提条件の一覧については、「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」を参照してください。

  - **ExchangeXML アプリケーション構成ファイルが累積更新プログラムのインストール中に上書きされる**   クライアント アクセス サーバーの web.config ファイルやメールボックス サーバーの EdgeTransport.exe.config ファイルなどの Exchange XML アプリケーション構成ファイルで行う、カスタマイズ済みのサーバーごとの設定は、Exchange の累積更新プログラムまたはサービス パックのインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、この情報を保存しておいてください。これらの設定は、Exchange の累積更新プログラムまたはサービス パックのインストール後に構成し直す必要があります。

  - **代理管理者のアクセス許可を使用して Exchange をインストールするとセットアップに失敗する**委任セットアップ役割グループのみのメンバーであるユーザーが事前に準備されたサーバーに Exchange をインストールしようとすると、セットアップに失敗します。この失敗は、委任セットアップ役割グループに、Active Directory 内で特定のオブジェクトを作成および構成するために必要なアクセス許可がないために起こります。
    
    この問題を回避するには、次のいずれかの操作を行います。
    
      - Exchange をインストールするユーザーを、Active Directory セキュリティ グループの Domain Admins に追加します。
    
      - 組織の管理役割グループのメンバーであるユーザーを使用して、Exchange をインストールします。

Exchange 2013 のインストール方法の詳細については、「[計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)」を参照してください。

## Exchange 管理シェル

  - **シェルが予期せずに Exchange 2007 または Exchange 2010 コマンドレットを読み込む** 以前、Exchange 2013 サーバーでシェルを開くと、ローカル サーバーまたは Exchange 2013 を実行している別のサーバーとの接続がシェルによって開かれていました。接続が確立されると、Exchange 2013 コマンドレットが読み込まれます。Exchange 2013 CU11 以降、シェルは、ログオンするユーザーのメールボックスが置かれている Exchange サーバーに接続します。ログオンするユーザーがメールボックスを持っていない場合、シェルは、SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 調停メールボックスが置かれているサーバーに接続します。ターゲット サーバーとして、Exchange のサポートされているバージョンを指定できます。これは、ログオンするユーザーのメールボックス (ユーザーがメールボックスを持っていない場合は調停メールボックス) が Exchange 2010 サーバーに置かれている場合、シェルはそのサーバーに接続し、Exchange 2010 コマンドレットを読み込むことを意味します。これにより、特定のタスクを実行できなくなる場合があります。Exchange 2010 コマンドレットは、Exchange 2013 構成またはサーバーを管理できないからです。
    
    Exchange 2013 CU11 以降、この動作は仕様です。シェルが Exchange 2013 コマンドレットを読み込むようにするには、ログオンするユーザーのメールボックスを Exchange 2013 に移動します。ログオンするユーザーがメールボックスを持っていない場合は、SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 調停メールボックスを Exchange 2013 サーバーにします。
    
    調停メールボックスを移動する方法について詳しくは、Exchange チームのブログの「[Exchange 管理シェルおよびメールボックスのアンカー](https://go.microsoft.com/fwlink/?linkid=717722)」をご覧ください。

## メールボックス

  - **バージョンが異なる Exchange を実行しているメールボックス サーバーを、同一のデータベース可用性グループに追加できる** **Add-DatabaseAvailabilityGroupServer** コマンドレットと Exchange 管理センターにより、Exchange 2013 サーバーを Exchange 2016 ベースのデータベース可用性グループ (DAG) に追加する操作、またはその反対の操作が誤って許可されています。Exchange では、同じバージョン (Exchange 2013 や Exchange 2016 など) を実行しているメールボックス サーバーを DAG に追加する操作のみをサポートしています。一方、Exchange 管理センターでは、Exchange 2013 サーバーと Exchange 2016 サーバーの両方が、DAG に追加できるサーバーの一覧に表示されます。この結果、互換性のないバージョンの Exchange を実行するサーバーを、管理者が誤って DAG に追加する (Exchange 2013 サーバーを Exchange 2016 ベースの DAG に追加するなど) 可能性があります。
    
    この問題に対する回避策はありません。管理者は、メールボックス サーバーを DAG に追加するときに十分に注意して行う必要があります。Exchange 2013 のサーバーは Exchange 2013 ベースの DAG にのみ、Exchange 2016 のサーバーは Exchange 2016 ベースの DAG にのみ追加します。Exchange 管理センターで、サーバーの一覧の **\[バージョン\]** 列を確認することにより、Exchange の各バージョンを区別できます。Exchange 2013 および Exchange 2016 のサーバーのバージョンを次に示します。
    
      - **Exchange 2013** 15.0 (ビルド xxx.xx)
    
      - **Exchange 2016** 15.1 (ビルド xxx.xx)

  - **以前の Exchange バージョンから移行するときにメールボックス サイズが増加する**   以前の Exchange バージョンから Exchange 2013 にメールボックスを移行するとき、報告されるメールボックスのサイズは 30 パーセントから 40 パーセント増加する場合があります。メールボックス データベースが使用するディスク容量は増加していません。増加したのは各メールボックスが使用する領域の属性だけです。このメールボックス サイズの増加は、すべてのアイテムのプロパティをクォータの計算に含めて、メールボックス内のアイテムが消費する領域の消費量を正確に計算したためです。この増加によって、ユーザーによっては、Exchange 2013 にメールボックスを移行するとき、そのメールボックス サイズ クォータを超えてしまうことがあります。
    
    ユーザーのメールボックス サイズがクォータを超えないようにするため、新しいクォータ計算に対応できるよう、データベースやメールボックスのクォータ値を増やします。データベースやメールボックスのクォータ値を構成するには、*IssueWarningQuota* パラメーター、*ProhibitSendQuota* パラメーター、*ProhibitSendReceiveQuota* パラメーターをそれぞれ **Set-MailboxDatabase** コマンドレットと **Set-Mailbox** コマンドレットで使用します。

  - **Outlook 2007 クライアントと Outlook 2010 クライアントでオフライン アドレス帳をダウンロードできない**   オフライン アドレス帳 (OAB) の内部 URL にインターネットからアクセスできない場合、Outlook 2007 クライアントと Outlook 2010 クライアントでは OAB をダウンロードできない可能性があります。
    
    Outlook 2007 クライアントと Outlook 2010 クライアントでこの問題を回避するには、OAB の内部 URL にインターネットからアクセスできるようにしてください。この問題が Outlook 2013 に影響を与えることはありません。

  - **既存の Exchange 組織に Exchange 2013 をインストールすると、すべてのクライアントで OAB がダウンロードされる**   最初の Exchange 2013 サーバーを既存の Exchange 2007 組織か Exchange 2010 組織にインストールすると、組織のすべてのクライアントで OAB の新しいコピーがダウンロードされ、ネットワークが混雑してサーバー パフォーマンスの問題が発生することがあります。この問題が発生するのは、組織において、Exchange 2007 か Exchange 2010 の OAB よりも優先される新しい既定の OAB が Exchange 2013 によって作成されるためです。特定の OAB が割り当てられていないメールボックス、または特定の OAB が割り当てられていないメールボックス データベースに配置されているメールボックスは、新しい既定の OAB をダウンロードします。
    
    Exchange 2013 のインストール時にクライアントで OAB の新しいコピーがダウンロードされないようにするには、すべてのメールボックス、またはメールボックスが配置されているメールボックス データベースに OAB を割り当てます。これを行ってから、Exchange 2013 を組織にインストールする必要があります。

  - **要求された OAB と関係のない OAB 生成メールボックスにユーザーがルーティングされる可能性がある**   Exchange 2013 CU5 とそれ以降の CU では、OAB を OAB 生成メールボックスにリンクする方法が変更されました。この変更によって、ユーザーが要求している OAB と関係のない OAB 生成メールボックスにユーザーがルーティングされる可能性があります。この現象は、以下のすべての条件が満たされている場合に発生する可能性があります。
    
      - 組織内に複数の OAB 生成メールボックスが存在する。
    
      - クライアント アクセス サーバーをアップグレードする前に、OAB 生成メールボックスをホストするメールボックス サーバーをアップグレードする。
    
      - Exchange 2013 サーバーを CU5 より前のリリースからそれ以降のリリースにアップグレードしている (たとえば、Exchange 2013 CU3 から Exchange 2013 CU6 にアップグレードしている)。
    
      - クライアント アクセス サーバーが CU5 より前のリリースを実行している。
    
    この問題を回避するには、メールボックス サーバーをアップグレードする前に、クライアント アクセス サーバーを Exchange 2013 CU6 以降にアップグレードします。これにより、クライアント アクセス サーバーが、ユーザーの OAB の生成を実行する OAB 生成メールボックスに対する要求のプロキシ方法を認識します。
    
    Exchange 2013 CU5 における OAB 変更の詳細については、[「Exchange 2013 累積更新プログラム 5 での OAB の強化」](https://go.microsoft.com/fwlink/p/?linkid=400642)を参照してください。

## パブリック フォルダー

  - **許可されていない送信者がメールが有効なパブリック フォルダーにメッセージを送信できなくなった**  Exchange 2013 CU6 より前には、許可されていない送信者が電子メールが有効なパブリック フォルダーにメッセージを送信できました。これにより、パブリック フォルダーに設定された許可には関係なく、外部の送信者がメールが有効なパブリック フォルダーにメールを送信することが可能でした。
    
    Exchange 2013 CU6 以降、外部の送信者がメールが有効なパブリック フォルダーにメールを送信する場合、**\[匿名\]** ユーザーに **\[アイテムの作成\]** 以上のアクセス許可が付与されている必要があります。メールが有効なパブリック フォルダーをセットアップしていて、このアクセス許可の付与を行っていない場合、外部のユーザーは配信失敗の通知を受け取り、メッセージはメールが有効なパブリック フォルダーに配信されません。
    
    匿名ユーザーのアクセス許可を設定するには、シェルや Outlook を使用できます。匿名ユーザーにアクセス許可を設定する方法について詳しくは、「[パブリック フォルダーのメールの有効化またはメールの無効化](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)」を参照してください。

  - 従来の Exchange サーバーから Exchange 2013 に移行できるパブリック フォルダーの最大数は、500,000 です。パブリック フォルダーの移行については、「[バッチ移行を使用して以前のバージョンから Exchange 2013 にパブリック フォルダーを移行する](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)」をご覧ください。

## メール フロー

  - **クライアント アクセス サーバーの TransportAgent コマンドレットがローカルの Windows PowerShell を要求する**   **\*-TransportAgent** コマンドレットに問題があって、これらのコマンドレットでは、Exchange 管理シェルを使用してクライアント アクセス サーバー上でトランスポート エージェントをインストール、アンインストール、管理することができません。クライアント アクセス サーバーに対してトランスポート エージェントをインストール、アンインストール、管理するには、ExchangeWindows PowerShell スナップインを手動で読み込んでから **\*-TransportAgent** コマンドレットを実行する必要があります。Exchange 管理シェルでトランスポート エージェントをインストール、アンインストール、管理しようとすると、変更が接続先の Exchange 2013 メールボックス サーバーに適用されます。
    
    クライアント アクセス サーバーで、トランスポート エージェントをインストール、アンインストール、管理するには、管理するクライアント アクセス サーバーで以下の操作をしてください。
    

    > [!NOTE]
    > <CODE>Microsoft.Exchange.Management.PowerShell.SnapIn</CODE>Windows PowerShell スナップインを読み込んで、<STRONG>*-TransportAgent</STRONG> コマンドレット以外のコマンドレットを実行することはサポート対象外であり、回復不能な損傷が Exchange 展開に生じるおそれがあります。<BR>トランスポート エージェントのインストール、アンインストール、管理ができるのは、それらの操作の対象になるクライアント アクセス サーバーのローカル管理者だけです。Exchange のファイル、ディレクトリ、または Active Directory のオブジェクト上でアクセス制御リスト (ACL) を変更することはサポート対象外です。

    

    > [!IMPORTANT]
    > 以下の手順は、クライアント アクセス サーバー上だけで実行してください。メールボックス サーバーでトランスポート エージェントを管理する場合、ExchangeWindows PowerShell スナップインを読み込む必要はありません。

    
    1.  新しい Windows PowerShell ウィンドウを開きます。
    
    2.  次のコマンドを実行します。
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  通常どおりトランスポート エージェント管理タスクを実行します。
    
    4.  管理するクライアント アクセス サーバーごとにこの手順を繰り返します。

## クライアント接続

  - **ドメインに参加していないクライアントの NTLM 認証が失敗する**   以下の条件に当てはまる場合、Windows Live Mail などのクライアントと Exchange 2013 との間の認証が失敗することがあります。
    
      - クライアントの使用する認証方法が NTLM である。
    
      - コンピューターがドメインに参加していない。
    
    この問題を回避するには、次のいずれかを実行できます。
    
      - クライアントが実行されているコンピューターをドメインに参加させます。
    
      - クライアントが使用する認証の種類を、NTLM から TLS 上の基本認証に変更します。

  - **Send-MailMessage コマンドレットで使用すると GSSAPI 認証が失敗する**   Windows PowerShell の既定のインストールに付属の **Send-MailMessage** コマンドレットを使用して認証メールを Exchange 2013 に送信すると、Generic Security Service Application Program Interface (GSSAPI) 認証が失敗することがあります。これが発生すると、接続を受信した Exchange 2013 クライアント アクセス サーバーの **アプリケーション** イベント ログに次の情報を含むエントリが表示されます。
    
      - **送信元**   MSExchangeFrontEndTransport
    
      - **イベント ID**   1035
    
      - **説明**   受信コネクタ Client Frontend \<*サーバー名*\> に対するエラー `IllegalMessage` が発生したため、受信認証に失敗しました。認証機構は Gssapi です。Exchange に対して認証しようとしたクライアントの送信元 IP アドレスは \<*\[クライアントの IP アドレス\]*\> です。
    
    この問題を回避するには、Exchange 2013 クライアント アクセス サーバー上のクライアント受信コネクタから `Integrated` 認証方法を削除する必要があります。クライアント受信コネクタから `Integrated` 認証方法を削除するには、**Send-MailMessage** コマンドレットを実行しているコンピューターから接続を受信する可能性のある各 Exchange 2013 クライアント アクセス サーバーで次のコマンドを実行します。
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **Exchange 2013 SP1 にアップグレードすると MAPI over HTTP のパフォーマンスが低下する**   Exchange 2013 累積更新プログラムから Exchange 2013 SP1 にアップグレードして、MAPI over HTTP を有効にすると、このプロトコルを使用して Exchange 2013 SP1 サーバーに接続しているクライアントのパフォーマンスが低下する場合があります。これは、累積更新プログラムから Exchange 2013 SP1 へのアップグレード時に必要な設定が構成されないためです。この問題は、Exchange 2013 RTM から Exchange 2013 SP1 にアップグレードした場合、または新しい Exchange 2013 SP1 以降のサーバーをインストールした場合には発生しません。
    

    > [!NOTE]
    > これは、クライアント アクセス サーバー上で MAPI over HTTP プロトコルが有効になっている場合にのみ発生する問題です。このプロトコルは既定で無効になっています。MAPI over HTTP が無効になっている場合、クライアントでは代わりに RPC over HTTP プロトコルを使用します。

    
    この問題に対処するには、次の手順を実行します。
    
    1.  クライアント アクセス サーバーの役割を実行しているサーバー上で、Windows コマンド プロンプトから次のコマンドを実行します。
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  メールボックス サーバーの役割を実行しているサーバー上で、Windows コマンド プロンプトから次のコマンドを実行します。
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Exchange 2010 との共存

  - **Exchange 2013 クライアント アクセス サーバー経由でプロキシ処理されているときに Exchange 2010 メールボックスに対するアクセス要求が機能しないことがある**   状況によっては、Exchange 2013 クライアント アクセス サーバーと、更新プログラムのロールアップがインストールされていない Exchange 2010 Service Pack 3 (SP3) クライアント アクセス サーバーの間でプロキシ要求が正しく機能せず、エラーが発生する場合があります。この問題は、以下のすべての条件に該当する場合に発生します。
    
      - Exchange 2013 のメールボックスを持つユーザーが、次の方法のいずれかによって Exchange 2010 のメールボックスを開こうとする。
        
          - Outlook Web App にある **\[別のメールボックスを開く\]** オプション**、または**
        
          - Exchange 管理センターの **\[別のユーザー\]** オプション
    
      - ユーザーが接続したクライアント アクセス サーバーが Exchange 2013 を実行している。
    
      - Exchange 2010 クライアント アクセス サーバーが Release to Manufacturing (RTM) バージョンの Exchange 2010 または以前の Exchange 2010 サービス パックから Exchange 2010 SP3 にアップグレードされている。
    
    上記条件のすべてに該当する場合、ユーザーは他のユーザーの Exchange 2010Outlook Web App オプションにアクセスできないため、空白のページが表示される場合があります。
    
    この問題を解決するには、Exchange 2010 サーバーごとに Exchange 2010 SP3 更新プログラムのロールアップ 1 以降をインストールします。

