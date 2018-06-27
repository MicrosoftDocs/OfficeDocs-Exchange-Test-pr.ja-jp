---
title: 'Exchange と Exchange Online 組織の間の OAuth 認証の構成: Exchange 2013 Help'
TOCTitle: Exchange と Exchange Online 組織の間の OAuth 認証の構成
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170788
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange と Exchange Online 組織の間の OAuth 認証の構成

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Exchange 2013 のみのハイブリッド展開では、ハイブリッド構成ウィザードを使用すると OAuth 認証が構成されます。Exchange 2013/2010 と Exchange 2013/2007 の混在したハイブリッド展開の場合は、Office 365 と社内 Exchange 組織との間の新しいハイブリッド展開の OAuth ベースの認証接続を、ハイブリッド構成ウィザードは構成しません。既定では、これらの展開は引き続きフェデレーション信頼プロセスを使用します。ただし、特定の Exchange 2013 機能は、新しい Exchange OAuth 認証プロトコルを使用してはじめて、組織間で完全に使用できます。

現在のところ、新しい Exchange OAuth 認証プロセスにより Exchange の機能のうち以下のものが有効になります。

  - Message Rights Management (MRM)

  - Exchange のインプレース電子情報開示

  - Exchange インプレース アーカイブ

Exchange 2013 および Exchange Online とのハイブリッド展開を実装する、Exchange が混在するすべての組織では、ハイブリッド構成ウィザードでハイブリッド展開を構成した後に、Exchange OAuth 認証を構成することをお勧めします。


> [!IMPORTANT]
> オンプレミスの組織で、累積更新プログラム 5 以降のインストールされた Exchange 2013 サーバーだけが実行されている場合は、このトピックの手順を実行する代わりにハイブリッド展開ウィザードを実行します。<BR>Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」トピックの「フェデレーションと証明書のアクセス許可」。

  - ハイブリッド展開ウィザードを使用して完成させた、ハイブリッド展開の構成。詳細については、「[Exchange Server のハイブリッド展開](https://technet.microsoft.com/ja-jp/library/jj200581\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 社内の Exchange 組織と Exchange Online 組織の間で OAuth の認証を構成する方法

## ステップ 1:Exchange Online 組織のための認証サーバー オブジェクトを作成する

この手順では、Exchange Online 組織のために検証済みのドメインを指定する必要があります。このドメインは、クラウド ベースの電子メール アカウント用にプライマリ SMTP ドメインとして使用されるものと同じドメインであることが必要です。以下の手順で、このドメインは *\<検証済みドメイン\>* と呼ばれます。

社内 Exchange 組織の Exchange 管理シェル (Exchange PowerShell) で次のコマンドを実行します。

    New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1

## ステップ 2:Exchange Online 組織のパートナー アプリケーションを使用可能にする

社内 Exchange 組織の Exchange PowerShell で、次のコマンドを実行します。

    Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true

## ステップ 3:社内の認証証明書をエクスポートする

このステップでは、PowerShell スクリプトを実行して社内の認証証明書をエクスポートする必要があります。それは次のステップで、Exchange Online 組織にインポートされます。

1.  次のテキストを、たとえば **ExportAuthCert.ps1** という名前の PowerShell スクリプト ファイルに保存します。
    
        $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
         
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)

2.  社内 Exchange 組織の Exchange PowerShell で、直前の手順で作成した PowerShell スクリプトを実行します。たとえば、
    
        .\ExportAuthCert.ps1

## ステップ 4:オンプレミスの認証証明書を Azure Active Directory ACS にアップロードする

次に、Windows PowerShell を使用して、直前の手順でエクスポートしたオンプレミスの認証証明書を Azure Active Directory アクセス制御サービス (ACS) にアップロードする必要があります。これを行うには、Windows PowerShell の Azure Active Directory モジュール コマンドレットをインストールする必要があります。インストールされていない場合、<https://aka.ms/aadposh> に移動して、Windows PowerShell の Azure Active Directory モジュール をインストールしてください。Windows PowerShell の Azure Active Directory モジュール のインストール後、以下の手順を実行します。

1.  **\[Windows PowerShell 用 Azure Active Directory モジュール\]** ショートカットをクリックして、Azure AD コマンドレットがインストールされた Windows PowerShell ワークスペースを開きます。この手順のすべてのコマンドは、Azure Active Directory コンソール用の Windows PowerShell を使用して実行されます。

2.  次のテキストを、たとえば **UploadAuthCert.ps1** という名前の PowerShell スクリプト ファイルに保存します。
    
        Connect-MsolService;
        Import-Module msonlineextended;
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        $objFSO = New-Object -ComObject Scripting.FileSystemObject;
        $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
        $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
        $cer.Import($CertFile);
        $binCert = $cer.GetRawCertData();
        $credValue = [System.Convert]::ToBase64String($binCert);
        
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
        New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue

3.  直前の手順で作成した PowerShell スクリプトを実行します。たとえば、
    
        .\UploadAuthCert.ps1

4.  スクリプトを起動した後に、\[資格情報\] ダイアログ ボックスが表示されます。Microsoft Online Azure AD 組織のテナント管理者アカウントの資格情報を入力します。スクリプトの実行後、Azure AD 用 Windows PowerShell セッションを開いたままにします。これは、次のステップで PowerShell スクリプトを実行するために使用します。

## ステップ 5:外部のオンプレミス Exchange HTTP エンドポイントのホスト名管理機関をすべて、Azure Active Directory に登録する

公的にアクセス可能な社内 Exchange 組織のエンドポイントごとに、このステップのスクリプトを実行する必要があります。可能な場合は、ワイルドカードを使用することをお勧めします。たとえば、Exchange が **https://mail.contoso.com/ews/exchange.asmx** で外部的に使用可能であるとします。この場合は、単一のワイルドカードが使用される可能性があります。**\*.contoso.com**。これにより、autodiscover.contoso.com や mail.contoso.com のエンドポイントがカバーされます。ただし、最上位ドメインの **contoso.com** はカバーされません。Exchange 2013 クライアント アクセスのサーバーが最上位のホスト名管理機関によって外部的にアクセス可能な場合、そのホスト名管理機関も **contoso.com** として登録する必要があります。追加の外部ホスト名管理機関を登録する際の制限はありません。

社内の Exchange 組織にある外部 Exchange エンドポイントが不明な場合は、社内の Exchange 組織の Exchange PowerShell で以下のコマンドを実行することにより、外部の構成済み Web サービス エンドポイントのリストを取得できます。

    Get-WebServicesVirtualDirectory | FL ExternalUrl


> [!NOTE]
> 以下のスクリプトを正常に実行するためには、直前のセクションのステップ 4 で説明されているように、Azure Active Directory 用 Windows PowerShell が Microsoft Online Azure AD テナントに接続されている必要があります。



1.  次のテキストを、たとえば **RegisterEndpoints.ps1** という名前の PowerShell スクリプト ファイルに保存します。この例では、ワイルドカードを使用して contoso.com のすべてのエンドポイントを登録します。**contoso.com** を社内の Exchange 組織のホスト名管理機関に置き換えてください。
    
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;

2.  Azure Active Directory 用 Windows PowerShell で、直前のステップで作成した Windows PowerShell スクリプトを実行します。たとえば、次のようにです。
    
        .\RegisterEndpoints.ps1

## ステップ 6:社内の組織から Office 365 への IntraOrganizationConnector を作成する

Exchange Online でホストされるメールボックスのターゲット アドレスを定義する必要があります。このターゲット アドレスは、Office 365 テナントを作成すると自動的に作成されます。たとえば、Office 365 テナントでホストされる組織のドメインが "contoso.com" の場合、ターゲットのサービス アドレスは "contoso.mail.onmicrosoft.com" となります。

Exchange PowerShell を使用して、社内の組織で次のコマンドレットを実行します。

    New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>

## ステップ 7:Office 365 テナントから社内の Exchange 組織への IntraOrganizationConnector を作成する

社内の組織でホストされているメールボックスのターゲット アドレスを定義する必要があります。組織のプライマリ SMTP アドレスが "contoso.com" の場合、これは "contoso.com" になります。

また、社内の組織の外部自動検出エンドポイントも定義する必要があります。企業が "contoso.com" の場合、これは通常は次のいずれかとなります。

  - https://autodiscover.\<プライマリ SMTP ドメイン\>/autodiscover/autodiscover.svc

  - https://\<プライマリ SMTP ドメイン\>/autodiscover/autodiscover.svc


> [!NOTE]
> 社内と Office 365 テナントの両方で <A href="https://technet.microsoft.com/ja-jp/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</A> コマンドレットを使用して、<A href="https://technet.microsoft.com/ja-jp/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</A> コマンドレットに必要なエンドポイント値を判別できます。



Windows PowerShell を使用して、次のコマンドレットを実行します。

    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>

## ステップ 8:Exchange 2013 SP1 よりも前のサーバー用に AvailabilityAddressSpace を構成する

Exchange 2013 より前の組織でハイブリッド展開を構成する場合、クライアント アクセス サーバーおよびメールボックス サーバーの役割を持つ少なくとも 1 つの Exchange 2013 SP1 以上のサーバーを、既存の Exchange 組織にインストールする必要があります。Exchange 2013 クライアント アクセス サーバーおよびメールボックス サーバーは、フロントエンド サーバーの役割をし、既存の Exchange 社内組織と Exchange Online 組織間の通信を調整します。この通信には、社内組織と Exchange Online 組織間のメッセージ トランスポート機能およびメッセージング機能が使用されます。ハイブリッド展開機能の信頼性と可用性を向上するために、社内組織に 2 台以上の Exchange 2013 サーバーを展開することを強くお勧めします。

Exchange 2013/2010 または Exchange 2013/2007 が含まれる混在展開では、インターネットに直接接続されたすべての社内組織用サーバーを、Exchange 2013 SP1 以上が実行されているクライアント アクセス サーバーにすることをお勧めします。Office 365 および Exchange Online からのすべての Exchange Web サービス (EWS) 要求は、社内展開の Exchange 2013 クライアント アクセス サーバーに接続する必要があります。さらに、Exchange Online の社内 Exchange 組織からのすべての EWS 要求は、Exchange 2013 SP1 以上が実行されているクライアント アクセス サーバーを介してプロキシされる必要があります。これらの Exchange 2013 クライアント アクセス サーバーはこの追加の受信および送信 EWS 要求を処理する必要があるため、処理負荷を扱い、接続の冗長性を提供する十分な数の Exchange 2013 クライアント アクセス サーバーが備わっていることが重要です。必要なクライアント アクセス サーバーの数は、EWS 要求の平均量に依存しており、組織によって異なります。

次の手順を完了する前に、以下の点を確認してください。

  - フロントエンド ハイブリッド サーバーが Exchange 2013 SP1 以上である

  - Exchange 2013 サーバー用の一意の外部 EWS URL がある。ハイブリッド機能のクラウドベースの要求が正常に行われるようにするには、Office 365 テナントがこれらのサーバーに接続している必要があります。

  - サーバーにメールボックス サーバーとクライアント アクセス サーバーの両方の役割がある

  - 既存の Exchange 2010/2007 メールボックス サーバーおよびクライアント アクセス サーバーに、最新の累積更新プログラム (CU) またはサービス パック (SP) が適用されている。
    

    > [!NOTE]
    > 既存の Exchange 2010/2007 メールボックス サーバーは、非ハイブリッド機能接続用に Exchange 2010/2007 クライアント アクセス サーバーをフロントエンド サーバーとして引き続き使用できます。Exchange 2013 サーバーに接続する必要があるのは、Office 365 テナントからのハイブリッド展開機能の要求のみです。



Exchange 2013 より前のクライアント アクセス サーバーでは、*AvailabilityAddressSpace* は、社内 Exchange 2013 SP1 クライアント アクセス サーバーの Exchange Web サービス エンドポイントを指すよう構成する必要があります。このエンドポイントは、手順 5 で概説したエンドポイントと同じものですが、社内の Exchange 2013 SP1 クライアント アクセス サーバーから、次のコマンドレットを実行することで判別できます。

    Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl


> [!NOTE]
> 複数のサーバーから仮想ディレクトリ情報が返ってくる場合は、Exchange 2013 SP1 クライアント アクセス サーバーへ返されたエンドポイントを使用していることを確認してください。<EM>AdminDisplayVersion</EM> パラメータには、15.0 (Build 847.32) 以上が表示されます。



*AvailabilityAddressSpace* を構成するには、社内組織で Exchange PowerShell を使用して、次のコマンドレットを実行します。

    Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True

## 正常な動作を確認する方法

[Test-OAuthConnectivity](https://technet.microsoft.com/ja-jp/library/jj218623\(v=exchg.150\)) コマンドレットを使用して、OAuth 構成が正しいことを検証できます。このコマンドレットは、社内の Exchange と Exchange Online のエンドポイントが、相互からの要求を正常に認証できることを検証します。


> [!IMPORTANT]
> リモート PowerShell を使用して Exchange Online 組織に接続するとき、<EM>AllowClobber</EM> パラメーターを <STRONG>Import-PSSession</STRONG> コマンドレットと共に使用して、最新のコマンドをローカルの PowerShell セッションにインポートしなければならないことがあります。



社内の Exchange 組織が Exchange Online に正常に接続できることを検証するために、社内の組織の Exchange PowerShell で次のコマンドを実行します。

    Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl

Exchange Online 組織が社内の Exchange 組織に正常に接続できることを検証するために、[リモート PowerShell](https://technet.microsoft.com/ja-jp/library/jj984289\(v=exchg.150\)) を使用して Exchange Online 組織に接続し、次のコマンドを実行します。

    Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl

例: Test-OAuthConnectivity -Service EWS -TargetUri https://lync.contoso.com/metadata/json/1 -Mailbox ExchangeOnlineBox1 -Verbose | fl


> [!IMPORTANT]
> 「SMTP アドレスにメールボックスが関連付けられていません」のエラーは無視できます。<EM>ResultTask</EM> パラメーターが返す値が <STRONG>Success</STRONG> であることだけが重要です。たとえば、テスト出力の最後のセクションは次のようであることが必要です。<BR><CODE>ResultType: Success</CODE><BR><CODE>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</CODE><BR><CODE>IsValid: True</CODE><BR><CODE>ObjectState: New</CODE>




> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


