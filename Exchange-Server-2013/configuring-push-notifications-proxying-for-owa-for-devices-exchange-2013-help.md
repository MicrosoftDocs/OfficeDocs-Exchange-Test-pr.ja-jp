---
title: 'OWA for Devices のプッシュ通知のプロキシの設定: Exchange 2013 Help'
TOCTitle: OWA for Devices のプッシュ通知のプロキシの設定
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59955435
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# OWA for Devices のプッシュ通知のプロキシの設定

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange 2013 の社内展開のための OWA for Devices (OWA for iPhone および OWA for iPad) のプッシュ通知を有効にすると、ユーザーは、自分の OWA for iPhone および OWA for iPad において、Outlook Web App アイコンで更新プログラムを受け取ることになります。その通知では、ユーザーの受信ボックスで不可視になっているメッセージの数が示されます。プッシュ通知が設定されず有効にもされていない場合、OWA for Devices を持つユーザーにとって、アプリを起動する以外、受信ボックス内に不可視メッセージがあることを知る手段はありません。新しいメッセージが利用可能になると、OWA for Devices バッジがユーザーのデバイス上で更新され、以下のバッジのように表示されます。

![OWA for Devices バッジ](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "OWA for Devices バッジ")

## プッシュ通知を有効にする方法

プッシュ通知を有効にするには、Exchange 2013 社内サーバーが iPhone および iPad にプッシュ通知を送信するための Office 365 プッシュ通知サービスに接続されていなければなりません。Exchange 2013 社内サーバーは、その更新通知を Office 365 通知サービスを通じて送信します。それにより、サード パーティ プッシュ通知サービスの開発者アカウントを登録する必要はなくなります。iPhone ユーザーと iPad ユーザーが、不可視メッセージのバッジ更新プログラムを入手するプロセスを以下の図に示します。

![プッシュ通知の処理](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "プッシュ通知の処理")

プッシュ通知を有効にするため、管理者は次のことを行う必要があります。

1.  組織を Office 365 for business に登録します。

2.  社内サーバーのすべてを更新して、Exchange Server 2013 累積更新プログラム 3 (CU3) 以降にします。

3.  社内 Exchange 2013 を Office 365 認証に対して設定する

4.  社内 Exchange Server 2013 から Office 365 へのプッシュ通知を有効にし、プッシュ通知が動作していることを確認します。

## 組織を Office 365 for business に登録する

Office 365 は、堅牢なセキュリティ、信頼性、ユーザー生産性を求める組織のニーズを満たすためのクラウド ベースのサービスです。Office 365 は、Office アプリケーションに加え、Lync Web カンファレンスや Exchange Online でホストされたビジネス用の電子メールなど、インターネットを通じて有効になる他の生産性サービス (クラウド サービス) へのアクセスを含むサブスクリプション プランです。

多くの Office 365 プランには、最新の Office アプリケーションのデスクトップ バージョンが含まれており、ユーザーはそれらを複数のコンピューターやデバイスにインストールできます。すべての Office 365 プランは、サブスクリプション ベースの月単位または年単位での支払いになります。Office 365 の詳細情報、また自分の組織についての登録に関しては、「[Office 365 for business とは?](http://go.microsoft.com/fwlink/?linkid=335705)」を参照してください。Office 365 で提供されるサービスのそれぞれに関する詳細については、「[Office 365 サービスの説明](http://go.microsoft.com/fwlink/?linkid=335704)」を参照してください。

## CU3 以降への更新

Exchange Server 2013 用累積更新プログラム 3 (CU3) は、Exchange Server 2013 の RTM がリリースされて以来見つかった問題を解決します。それには、CU1 と CU2 に含まれていた問題とその修正のすべてが含まれており、さらに CU2 がリリースされて以来見つかったその他の修正と更新プログラムも含まれています。この更新プログラムは、Exchange Server 2013 のすべての社内カスタマーに対して推奨されているレベルのものですが、プッシュ通知に関しては必須となっています。CU3 を含む累積更新プログラムについては、「[Exchange 2013 の更新プログラム](updates-for-exchange-2013-exchange-2013-help.md)」を参照してください。

## 社内 Exchange 2013 を Office 365 認証に対してセット アップする

Exchange Server 2013 では、サーバー間認証のための単一の標準化された方法を使用するというアプローチが使用されています。「[Exchange Server 2013](http://go.microsoft.com/fwlink/?linkid=290946)」([Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=273796) および [SharePoint 2013](http://go.microsoft.com/fwlink/?linkid=335701)) および [Office 2013](http://go.microsoft.com/fwlink/?linkid=335696) では、サーバー間の認証と承認のために OAuth (Open Authorization) プロトコルがサポートされています。OAuth は、メジャーな Web サイトの多くで使用されている標準の承認プロトコルです。それを使用した場合、ユーザーの資格情報とパスワードが 1 つのコンピューターから別のコンピューターに渡されるということはありません。その代わり、認証と承認は OAuth セキュリティ トークンに基づくものとなります。それらのトークンによって、特定の期間に渡り、特定のリソースの集合に対するアクセス権が付与されます。

OAuth 認証には、多くの場合、1 つの認証サーバーと、互いに通信する必要のある 2 つの領域の合計 3 つのコンポーネントが関係します。セキュリティ トークンは、認証サーバー (セキュリティ トークン サーバー) によって、通信する必要のある 2 つの領域に対して発行されます。それらのトークンにより、1 つの領域からの通信をもう一方の領域が信頼すべきかどうかが検証されます。たとえば、特定の Lync Server 2013 領域のユーザーが指定された Exchange 2013 の領域にアクセスできるかどうか、およびその逆を検証するトークンを、認証サーバーが発行することが可能です。


> [!TIP]  
> 領域は、セキュリティのコンテナーとなるものです。



しかし、社内のサーバー間認証の場合、サード パーティのトークン サーバーを使用する必要はありません。Lync Server 2013 や Exchange 2013 などのサーバー製品にはそれぞれ、サーバー間認証をサポートする他の Microsoft サーバー (SharePoint Server など) との認証のために使用できる組み込みトークン サーバーがあります。たとえば、Lync Server 2013 はセキュリティトークンを自ら発行して署名し、そのトークンを使用して Exchange 2013 と通信できます。このような場合、サード パーティのトークン サーバーは不要です。

Exchange Server 2013 から Office 365 への社内実装のためのサーバー間認証を設定するには、2 つの手順を実行する必要があります。

  - **ステップ 1 – オンプレミスの Exchange Server の組み込みトークン発行者に証明書を割り当てます。** まず、まだ証明書が作成されていないなら、オンプレミスの Exchange 管理者は、以下の Exchange 管理シェル スクリプトを使用して証明書を作成し、オンプレミスの Exchange Server の組み込みトークン発行者に割り当てる必要があります。これは、1 度限りのプロセスであり、証明書作成後は、他の認証シナリオでもその証明書を再利用しなければならず、置き換えてはなりません。*$tenantDomain* の値を、実際のドメイン名に必ず更新してください。そのためには、以下のコードをコピーおよび貼り付けてください。
    

    > [!WARNING]  
    > コードをコピーしてメモ帳などのテキスト エディターに貼り付け、拡張子 .ps1 として保存しておくと、シェル スクリプトの実行が非常に楽になります。

    
        # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
        
        $tenantDomain = "Fabrikam.com"
        
        # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
        
        $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
        If ($c.Count -eq 0)
        {
            Write-Host "Creating certificate for oAuth..."
            $ski = [System.Guid]::NewGuid().ToString("N")
            $friendlyName = "Exchange S2S OAuth"
            New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
            $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
        }
        ElseIf ($c.Count -gt 1)
        {
            $c = $c[0]
        }
        
        $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
        If ($a.Count -eq 0)
        {
            Set-AuthConfig -CertificateThumbprint $c.Thumbprint
        }
        Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
        
        # Export the certificate
        
        Write-Host "Exporting certificate..."
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
        
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
        
        # Set AuthServer
        $authServer = Get-AuthServer MicrosoftSts;
        if ($authServer.Length -eq 0)
        {
            Write-Host "Creating AuthServer Config..."
            New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
        {
            Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
            Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        else
        {
            Write-Host "AuthServer Config already exists."
        }
        Write-Host "Complete."
    
    予期される結果は、以下の出力のようなものになるはずです。
    
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
    

    > [!WARNING]  
    > 続行する前に、Windows PowerShell の Azure Active Directory モジュール コマンドレットが必要です。Windows PowerShell の Azure Active Directory モジュール コマンドレット (旧称 Microsoft Online Services Module for Windows PowerShell) がまだインストールされていない場合、<A href="http://aka.ms/aadposh">Windows PowerShell を使用した Azure AD の管理</A>からインストールできます。



  - **ステップ 2 – Exchange 2013 オンプレミスとの通信が可能になるよう Office 365 を構成する。** Exchange Server 2013 の通信相手となる Office 365 サーバーを構成し、パートナー アプリケーションとなるように構成します。たとえば、Exchange Server 2013 社内で Office 365 と通信することが必要になった場合は、社内 Exchange をパートナー アプリケーションとなるよう設定する必要があります。パートナー アプリケーションは、サード パーティ セキュリティ トークン サーバーを使用せずに、Exchange 2013 が直接セキュリティ トークンを交換できるアプリケーションです。社内 Exchange 2013 管理者は、Exchange Management の以下のシェル スクリプトを使用して、Exchange 2013 の通信相手である Office 365 テナントをパートナー アプリケーションとなるよう設定する必要があります。実行中に、Office 365 テナント ドメインの管理者ユーザー名 (administrator@fabrikam.com など) とパスワードを入力するよう求めるプロンプトが表示されます。証明書が前のスクリプトから作成されたのではない場合、*$CertFile* の値を更新し証明書の場所を設定します。そのためには、以下のコードをコピーおよび貼り付けてください。
    
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        } 
    
    予期される結果は、以下のようなものになります。
    
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.

## プッシュ通知のプロキシを有効にする

前述の手順に従って OAuth 認証が正常に設定されたら、社内管理者は、以下のスクリプトを使用して、プッシュ通知のプロキシを有効にする必要があります。*$tenantDomain* の値を、実際のドメイン名に必ず更新してください。そのためには、以下のコードをコピーおよび貼り付けてください。

    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain

予期される結果は、以下の出力のようなものになるはずです。

    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged

## プッシュ通知の動作検証

前述の手順の実行が終了したら、プッシュ通知を以下のいずれかの方法でテストすることができます。

  - **テスト電子メール メッセージをユーザーのメールボックスに送信する。**
    
    1.  モバイル デバイス上の OWA for Devices で通知サブスクライブのためのアカウントを設定します。
    
    2.  デバイスのホーム画面に戻ります。OWA for Devices はバックグラウンドになります。
    
    3.  PC などの別のデバイスから、モバイル デバイスに設定されたアカウントの受信ボックス宛てに電子メール メッセージを送信します。
    
    4.  数分以内に、アプリのアイコン上に不可視カウントが表示されるはずです。

  - **モニターを有効にする。** プッシュ通知のテスト、あるいは通知が失敗する原因を調べる別の方法として、組織内のメールボックス サーバーに対するモニターを有効にするという方法があります。社内 Exchange 2013 サーバー管理者は、以下のスクリプトを使用して、プッシュ通知プロキシのモニターを起動する必要があります。そのためには、以下のコードをコピーおよび貼り付けてください。
    
        # Send a push notification to verify connectivity.
        
        $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
        If ($s.Count -gt 1)
        {
            $s = $s[0]
        }
        If ($s.Count -ne 0)
        {
            # Restart the monitoring service to clear the cache from when push was previously disabled.
            Restart-Service MSExchangeHM
        
            # Give the monitoring service enough time to load.
            Start-Sleep -Seconds:120
        
            Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
        }
        Else
        {
            Write-Error "Cannot find a Mailbox server in the current site."
        }
    
    予期される結果は、以下の出力のようなものになるはずです。
    
        ResultType : Succeeded
        Error      :
        Exception  :

