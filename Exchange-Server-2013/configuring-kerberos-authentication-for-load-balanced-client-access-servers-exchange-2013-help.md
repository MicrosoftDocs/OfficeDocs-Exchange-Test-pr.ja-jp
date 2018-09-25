---
title: '負荷分散されたクライアント アクセス サーバーの Kerberos 認証の構成: Exchange 2013 Help'
TOCTitle: 負荷分散されたクライアント アクセス サーバーの Kerberos 認証の構成
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835899
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 負荷分散されたクライアント アクセス サーバーの Kerberos 認証の構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

**概要:** Exchange 2013 の負荷分散クライアント アクセス サーバーで Kerberos 認証を使用する方法を説明します。

負荷分散クライアント アクセス サーバーで Kerberos 認証を使用するには、この記事で説明する構成手順を実行する必要があります。

## Active Directory ドメイン サービスで代替サービス アカウント資格情報を作成する

同じ名前空間と URL を共有するすべてのクライアント アクセス サーバーは、同じ代替サービス アカウント資格情報を使用する必要があります。通常、Exchange の各バージョンのフォレストには 1 つのアカウントがあれば十分です。*代替サービス アカウント資格情報*または *ASA 資格情報*。


> [!IMPORTANT]
> Exchange 2010 と Exchange 2013 とでは、同じ ASA 資格情報を共有できません。Exchange 2013 の新しい ASA 資格情報を作成する必要があります。




> [!IMPORTANT]
> CNAME レコードは共有名前空間でサポートされていますが、Microsoft は A レコードを使用することをお勧めします。これにより、クライアントは、サーバー FQDN ではなく、共有名に基づいて Kerberos チケット要求を常に正しく発行できるようになります。



ASA 資格情報を設定するときに、以下のガイドラインに留意してください。

  - <strong>アカウントの種類。</strong>ユーザー アカウントではなくコンピューター アカウントを作成することをお勧めします。コンピューター アカウントは対話型ログオンを許可しないため、ユーザー アカウントよりもセキュリティ ポリシーが単純になる可能性があります。コンピューター アカウントを作成する場合、パスワードが期限切れになることはありませんが、パスワードを定期的に更新することをお勧めします。ローカル グループ ポリシーを使用して、コンピューター アカウントの最大存続期間を指定したり、現在のポリシーに適合しないコンピューター アカウントを定期的に削除するスクリプトを指定したりできます。ローカル セキュリティ ポリシーでは、パスワードを変更する必要があるタイミングも決定します。コンピューター アカウントを使用することをお勧めしますが、ユーザー アカウントを作成することもできます。

  - <strong>アカウント名。</strong>アカウント名には要件はありません。名前付けスキームに準拠している任意の名前を使用できます。

  - <strong>アカウント グループ。</strong>ASA 資格情報に使用するアカウントには、特別なセキュリティ特権は必要ありません。コンピューター アカウントを使用する場合、そのアカウントのみが Domain Computers セキュリティ グループのメンバーである必要があります。ユーザー アカウントを使用する場合、そのアカウントのみが Domain Users セキュリティ グループのメンバーである必要があります。

  - <strong>アカウント パスワード。</strong>アカウントを作成するときに指定するパスワードが使用されます。したがって、アカウントを作成するときには、複雑なパスワードを使用し、組織のパスワード要件に準拠していることを確認する必要があります。

コンピューター アカウントとして ASA 資格情報を作成するには

1.  ドメインに参加しているコンピューターで、Windows PowerShell または Exchange 管理シェルを実行します。
    
    **Import-Module** コマンドレットを使用して、Active Directory モジュールをインポートします。
    
    ```powershell
    Import-Module ActiveDirectory
    ```

2.  **New-ADComputer** コマンドレットを次のコマンドレット構文で使用して、新しい Active Directory コンピューター アカウントを作成します。
    
    ```powershell
    New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    ```
    
    例: 
    
    ```powershell
    New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    ```
    
    ここで、*EXCH2013ASA* はアカウント名を指定します。説明 *Alternate Service Account credentials for Exchange* には任意の内容を指定できます。また、*SamAccountName* パラメーターの値 (この場合は *EXCH2013ASA*) は、ディレクトリで一意である必要があります。

3.  このコマンドレットの構文を使用して Kerberos で使用される AES 256 暗号化の暗号を有効にするには、**Set-ADComputer** コマンドレットを使用します。
    
    ```powershell
    Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    ```
    
    例:   
    
    ```powershell
    Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
    ```
    
    ここで、*EXCH2013ASA* はアカウントの名前であり、変更する属性は 28 の 10 進値を持つ *msDS-SupportedEncryptionTypes* です。これにより、次の暗号が有効になります。RC4-HMAC、AES128-CTS-HMAC-SHA1-96、AES256-CTS-HMAC-SHA1-96。

これらのコマンドレットの詳細については、「[Import-Module](https://technet.microsoft.com/library/hh849725.aspx)」および「[New-ADComputer](https://technet.microsoft.com/library/ee617245.aspx)」を参照してください。

## クロス フォレスト シナリオ

クロス フォレスト展開またはリソース フォレスト展開を使用しており、Exchange を含む Active Directory フォレストの外側に位置するユーザーが存在する場合は、フォレスト間の信頼関係を構成する必要があります。また、展開内の各フォレストについては、フォレスト内およびフォレスト間のすべての名前サフィックス間の信頼を有効にするルーティング ルールをセットアップする必要があります。クロス フォレストの信頼を管理する方法の詳細については、「[フォレストの信頼を管理する](https://technet.microsoft.com/library/cc772440.aspx)」を参照してください。

## サービス プリンシパル名を識別して ASA 資格情報に関連付ける

ASA 資格情報を作成したら、Exchange サービス プリンシパル名 (SPN) を ASA 資格情報に関連付ける必要があります。Exchange SPN の一覧は構成によって異なりますが、少なくとも以下が含まれている必要があります。

  - **http/**   Outlook Anywhere、MAPI over HTTP、Exchange Web サービス、Autodiscover、およびオフライン アドレス帳にこの SPN を使用します。

SPN 値は、個々のサーバーではなく、ネットワーク ロード バランサーのサービス名に一致している必要があります。使用する SPN 値を決定する際には、次のシナリオを考慮してください。

  - Single Active Directory site

  - Multiple Active Directory sites

これらの各シナリオでは、クライアント アクセス サーバーのメンバーによって使用される内部 URL、外部 URL、自動検出内部 URI に、負荷分散される完全修飾ドメイン名 (FQDN) が展開されていることを前提としています。詳細については、「プロキシとリダイレクトについて」を参照してください。

## 単一の Active Directory サイト

単一の Active Directory サイトが存在する場合、環境は以下の図のようになります。

![単一の AD サイトおよび Kerberos 認証のある CAS 配列](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "単一の AD サイトおよび Kerberos 認証のある CAS 配列")

前の図にある内部 Outlook クライアントで使用される FQDN に基づいて、ASA 資格情報に次の SPN を関連付ける必要があります。

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## 複数の Active Directory サイト

複数の Active Directory サイトが存在する場合、環境は以下の図のようになります。

![複数の AD サイトおよび Kerberos 認証のある CAS 配列](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "複数の AD サイトおよび Kerberos 認証のある CAS 配列")

前の図にある Outlook クライアントで使用される FQDN に基づいて、ADSite 1 のクライアント アクセス サーバーで使用される ASA 資格情報に次の SPN を関連付ける必要があります。

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

ADSite 2 のクライアント アクセス サーバーによって使用される ASA 資格情報に次の SPN を関連付ける必要もあります。

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## 各クライアント アクセス サーバーの ASA 資格情報を構成して確認する

アカウントを作成した後、そのアカウントがすべての AD DS ドメイン コントローラーにレプリケートされていることを確認する必要があります。特に、アカウントは、ASA 資格情報を使用する各クライアント アクセス サーバーに存在している必要があります。次に、展開されている各クライアント アクセス サーバーの ASA 資格情報としてアカウントを構成します。

以下の手順のいずれかに従って、Exchange 管理シェルで ASA 資格情報を構成します。

  - ASA 資格情報を最初の Exchange 2013 クライアント アクセス サーバーに展開する

  - ASA 資格情報を以降の Exchange 2013 クライアント アクセス サーバーに展開する

ASA 資格情報を展開するためのサポートされている唯一の方法は、RollAlternateServiceAcountPassword.ps1 スクリプトを使用することです。詳細については、「[シェルでの RollAlternateserviceAccountCredential.ps1 スクリプトの使用](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)」を参照してください。スクリプトの実行が完了したら、対象のサーバーのすべてが適切に更新されていることを確認することを推奨します。

## ASA 資格情報を最初の Exchange 2013 クライアント アクセス サーバーに展開する

1.  Exchange 2013 サーバー上で Exchange 管理シェルを開きます。

2.  ディレクトリを *\<Exchange 2013 installation directory\>*\\V15\\Scripts に変更します。

3.  ASA 資格情報を最初の Exchange 2013 クライアント アクセス サーバーに展開するには、次のコマンドを実行します。
    
    ```powershell
    .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$
    ```

4.  代替サービス アカウントのパスワードを変更するかどうかを確認するメッセージが表示されたら、<strong>はい</strong> で応答します。

RollAlternateServiceAccountPassword.ps1 スクリプトを実行すると表示される出力の例を次に示します。

```powershell
    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED
```

## ASA 資格情報を別の Exchange 2013 クライアント アクセス サーバーに展開する

1.  Exchange 2013 サーバー上で Exchange 管理シェルを開きます。

2.  ディレクトリを *\<Exchange 2013 installation directory\>*\\V15\\Scripts に変更します。

3.  ASA 資格情報を別の Exchange 2013 クライアント アクセス サーバーに展開するには、次のコマンドを実行します。
    
    ```powershell
    .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com
    ```

4.  ASA 資格情報を展開する各クライアント アクセス サーバーについて、手順 3 を繰り返します。

RollAlternateServiceAccountPassword.ps1 スクリプトを実行すると表示される出力の例を次に示します。

```powershell
    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED
```

## ASA 資格情報の展開の確認

  - Exchange 2013 サーバー上で Exchange 管理シェルを開きます。

  - クライアント アクセス サーバー上の設定を確認するには、次のコマンドを実行します。
    
    ```powershell
    Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration
    ```

  - ASA 資格情報の展開を確認する各クライアント アクセス サーバーについて、手順 2 を繰り返します。

上記の Get-ClientAccessServer コマンドを実行し、以前の ASA 資格情報が設定されていない場合に表示される出力の例を次に示します。

```powershell
    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...
```

上記の Get-ClientAccessServer コマンドを実行し、ASA 資格情報が以前に設定されていた場合に表示される出力の例を次に示します。以前の ASA 資格情報と、設定された日時が返されます。

```powershell
    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...
```

## サービス プリンシパル名 (SPN) を ASA 資格情報に関連付ける


> [!IMPORTANT]
> 「ASA 資格情報を最初の Exchange 2013 クライアント アクセス サーバーに展開する」で前述したように、少なくとも 1 つの Exchange Server に ASA 資格情報を展開するまで、SPN をその資格情報と関連付けしないでください。それ以外の場合、Kerberos 認証エラーが発生します。



SPN を ASA 資格情報に関連付ける前に、ターゲット SPN がフォレスト内の別のアカウントに関連付けられていないことを確認する必要があります。ASA 資格情報は、これらの SPN が関連付けられているフォレスト内の唯一のアカウントである必要があります。コマンド ラインから **setspn** コマンドを実行することによって、フォレスト内にその SPN が関連付けられた他のアカウントがないことを確認できます。

setspn コマンドを実行して SPN がフォレスト内でアカウントに既に関連付けられていないことを確認する

1.  <strong>開始</strong> を押します。<strong>検索</strong> ボックスに「**Command Prompt**」と入力し、その結果表示されるリストで <strong>コマンド プロンプト</strong> を選択します。

2.  コマンド プロンプトで、以下のコマンドを入力します。
    
    ```powershell
    setspn -F -Q <SPN>
    ```
    
    この \<SPN\> には、ASA 資格情報に関連付ける SPN を入力します。たとえば、次のように入力します。
    
    ```powershell
    setspn -F -Q http/mail.corp.tailspintoys.com
    ```
    
    コマンドは何も返さないはずです。何かを返した場合は、別のアカウントが既に SPN に関連付けられています。ASA 資格情報に関連付ける SPN ごとにこの手順を繰り返します。

setspn コマンドを使用して SPN を ASA 資格情報に関連付ける

1.  <strong>開始</strong> を押します。<strong>検索</strong> ボックスに「**Command Prompt**」と入力し、その結果表示されるリストで <strong>コマンド プロンプト</strong> を選択します。

2.  コマンド プロンプトで、以下のコマンドを入力します。
    
    ```powershell
    setspn -S <SPN> <Account>$
    ```
    
    この \<SPN\> には、ASA 資格情報に関連付ける SPN を入力します。そして、\<Account\> には、ASA 資格情報に関連付けるアカウントを入力します。たとえば、次のように入力します。
    
    ```powershell
    setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
    ```
    
    ASA 資格情報に関連付ける SPN ごとにこのコマンドを 1 回実行します。

setspn コマンドを使用して SPN を ASA 資格情報に関連付けたことを確認する

1.  <strong>開始</strong> を押します。<strong>検索</strong> ボックスに「**Command Prompt**」と入力し、その結果表示されるリストで <strong>コマンド プロンプト</strong> を選択します。

2.  コマンド プロンプトで、以下のコマンドを入力します。
    
    ```powershell
    setspn -L <Account>$
    ```
    
    この \<Account\> には、ASA 資格情報に関連付けるアカウントを入力します。たとえば、次のように入力します。
    
    ```powershell
    setspn -L tailspin\EXCH2013ASA$
    ```
    
    このコマンドは 1 度実行するだけで十分です。

## Outlook クライアントの Kerberos 認証を有効にする

1.  Exchange 2013 サーバー上で Exchange 管理シェルを開きます。

2.  Outlook Anywhere クライアントの Kerberos 認証を有効にするには、クライアント アクセス サーバー上で次のコマンドを実行します。
    
    ```powershell
    Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate
    ```

3.  MAPI over HTTP クライアントの Kerberos 認証を有効にするには、Exchange 2013 クライアント アクセス サーバー上で次のコマンドを実行します。
    
    ```powershell
    Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate
    ```

4.  Kerberos 認証を有効にする各 Exchange 2013 クライアント アクセス サーバーについて、手順 2 と 3 を繰り返します。

## Exchange クライアントの Kerberos 認証を検証する

Kerberos と ASA 資格情報を正常に構成したら、以下説明されているタスクに従って、クライアントが正常に認証することを確認します。

## Microsoft Exchange Service Host サービスが実行していることを確認する

クライアント アクセス サーバーの Microsoft Exchange Service Host サービス (MSExchangeServiceHost) は、ASA 資格情報を管理します。このサービスが実行されていないと、Kerberos 認証を実行できません。既定では、このサービスは、コンピューターの起動時に自動的に開始するように構成されています。

Microsoft Exchange Service Host サービスが開始していることを確認するには

1.  <strong>スタート</strong> をクリックし、「**services.msc**」と入力して、リストから <strong>services.msc</strong> を選択します。

2.  <strong>サービス</strong> ウィンドウに表示されるサービスのリストで、**Microsoft Exchange Service Host** サービスを探します。

3.  サービスの状態が <strong>実行中</strong> である必要があります。状態が <strong>実行中</strong> ではない場合は、そのサービスを右クリックし、<strong>開始</strong> をクリックします。

## クライアント アクセス サーバーから Kerberos を検証する

それぞれのクライアント アクセス サーバーで ASA 資格情報を構成する際、**set-ClientAccessServer** コマンドレットを実行しました。このコマンドレットを一度実行してあると、ログを使用して Kerberos が正常に接続されていることを確認することができます。

HttpProxy ログ ファイルを使用して Kerberos が正常に機能していることを検証するには

1.  テキスト エディターで HttpProxy ログが格納されているフォルダーを参照します。既定では、このログは次のフォルダーに格納されています。
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  最新のログ ファイルを開き、「**Negotiate**」という語句を検索します。ログ ファイルの行は、次の例のような形式になっています。
    
    ```powershell
    2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    ```
    
    **AuthenticationType** の値が「**Negotiate**」になっていれば、サーバーは Kerberos 認証接続を正常に作成しています。

## ASA 資格情報を管理する

ASA 資格情報のパスワードを定期的に更新する必要がある場合、この記事の ASA 資格情報を構成するための手順を使用します。定期的なパスワードの保守を実行するスケジュールされたタスクのセットアップを検討してください。指定されたときにパスワード ロールオーバーが行われていることを確認し、可能性のある認証の停止を防止するために、スケジュールされたタスクを監視してください。

## Kerberos 認証をオフにする

Kerberos を使用しないようにクライアント アクセス サーバーを構成するには、ASA 資格情報から SPN の関連付けを解除するか、削除します。SPN が削除されると、クライアントによる Kerberos 認証が試行されなくなり、ネゴシエート認証を使用するよう構成されたクライアントは代わりに NTLM を使用します。Kerberos だけを使用するよう構成されたクライアントは接続できません。SPN を削除したら、アカウントも削除する必要があります。

ASA 資格情報を削除するには

1.  Exchange 2013 サーバー上で Exchange 管理シェルを開き、次のコマンドを実行します。
    
    ```powershell
    Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials
    ```

2.  この手順はすぐに実行する必要はありませんが、最後的には、すべてのクライアント コンピューターを再起動して Kerberos チケット キャッシュをコンピューターから消去する必要があります。

