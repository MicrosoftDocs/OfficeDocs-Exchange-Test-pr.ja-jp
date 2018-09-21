---
title: 'Exchange 2013 クライアント アクセス サーバーの構成: Exchange 2013 Help'
TOCTitle: Exchange 2013 クライアント アクセス サーバーの構成
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 49895209
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 クライアント アクセス サーバーの構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-07-25_

Exchange 2013 クライアント アクセス サーバーをインストールした後、さまざまな構成タスクを実行できます。Exchange 2013 内のクライアント アクセス サーバーはクライアント プロトコルの処理を扱いませんが、仮想ディレクトリ設定および証明書設定など、いくつかの設定をクライアント アクセス サーバーに適用する必要があります。

## サーバー証明書の構成

Exchange 2013 で、証明書ウィザードを使用して証明機関からデジタル証明書を要求できます。デジタル証明書を要求した後、それをクライアント アクセス サーバーにインストールする必要があります。

組織のメールボックス サーバーには、デジタル証明書をインストールする必要はありません。自己署名証明書は、既定でメールボックス サーバーにインストールされるため、それを置き換える必要はありません。組織内のクライアント アクセス サーバーは、メールボックス サーバー上の自己署名証明書を暗黙的に信頼します。詳細については、「[Exchange 2013 証明書管理 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)」を参照してください。

## 仮想ディレクトリの構成

オフライン アドレス帳 (OAB)、Exchange Web サービス、Exchange ActiveSync、Outlook Web App、および Exchange 管理センターの仮想ディレクトリ上でいくつかの設定を構成できます。仮想ディレクトリの管理については、「[仮想ディレクトリの管理](virtual-directory-management-exchange-2013-help.md)」を参照してください。次のコマンドを使用して、仮想ディレクトリを構成できます。

  - Exchange 2013 では、Outlook Anywhere 構成用の HTTP 接続設定が 2 セット用意されているため、管理者は内部と外部の両方のエンドポイントを構成できます。
    
    接続用の単一の URL を使用して Outlook Anywhere を構成するには、Exchange 管理シェルで次のコマンドを使用して、ホスト名を入力し、SSL が必要かどうかを指定し、Authpackage を設定する必要があります。
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    Exchange 管理シェルで次のコマンドを使用して、外部から到達可能なエンドポイントを指定することもできます。
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    

    > [!TIP]
    > Exchange 2013 は Outlook Anywhere HTTP 認証のネゴシエートをサポートしていますが、環境内のすべてのサーバーで Exchange 2013 が動作している場合以外は使用しないでください。



  - Exchange ActiveSync を構成するには、次のコマンドを実行します。
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"

  - Exchange Web サービス仮想ディレクトリを構成するには、次のコマンドを実行します。
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx

  - オフライン アドレス帳を構成するには、次のコマンドを実行します。
    
        Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"

  - サービス接続ポイントを構成するには、次のコマンドを実行します。
    
        Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml

## Exchange 2007 および 2010 クライアント アクセスからのアップグレード

このセクションを通じて、Exchange 2013 クライアント アクセス サーバーでプロトコルへの外部アクセスを構成します。上記の仮想ディレクトリの構成セクションに記載されている Exchange 管理シェルのコマンド、および次のコマンドを実行します。

Exchange 2013 の仮想ディレクトリを構成するには、次のコマンドを実行する必要があります。

1.  Outlook Web App の外部 URL を構成するには、Exchange 管理シェルで次のコマンドを実行します。
    
        Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    
    Outlook Web App の仮想ディレクトリを設定したら、コマンド プロンプトで次のコマンドを実行します。
      ```
  ```powershell
Net stop IISAdmin /y
```
      ```
      ```
  ```powershell
Net start W3SVC
```
      ```
      
2.  外部 EAC アクセスを構成するには、Exchange 管理シェルで次のコマンドを実行します。
    
        Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 

3.  可用性サービスを構成するには、Exchange 管理シェルで次のコマンドを実行します。
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx

外部 URL が Exchange ActiveSync または Outlook Web App に対して正しく構成されていることを確認する場合は、マイクロソフトが提供する無料の Web ベース ツールであるリモート接続アナライザーを使用できます。リモート接続アナライザーは、[ここ](http://go.microsoft.com/fwlink/?linkid=154308) にあります。

認証が Exchange ActiveSync または Outlook Web App で正しく構成されていることを確認する場合にも、ExRCA を使用できます。

直接ファイル アクセスが Outlook Web App で正しく構成されていることを確認するには、共有のコンピューターのオプションを使用して、ユーザーとして Outlook Web App にログオンし、電子メール メッセージに添付されたファイルにアクセスして保存します。

## Exchange 2007 クライアント アクセス サーバー上のプロトコルを構成する

Exchange 2007 の仮想ディレクトリを構成するには、次のコマンドを実行する必要があります。

  - Exchange ActiveSync 仮想ディレクトリで外部 URL を構成するには、Exchange 管理シェルで次のコマンドを実行します。
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync

  - Outlook Web App 仮想ディレクトリで外部 URL を構成するには、Exchange 管理シェルで次のコマンドを実行します。
    
        Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa

