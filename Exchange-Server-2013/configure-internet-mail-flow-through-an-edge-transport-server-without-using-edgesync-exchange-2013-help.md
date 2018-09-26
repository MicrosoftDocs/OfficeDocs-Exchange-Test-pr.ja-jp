---
title: 'EdgeSync を使用せずにエッジ トランスポート サーバー経由のインターネット メール フローを構成する: Exchange 2013 Help'
TOCTitle: EdgeSync を使用せずにエッジ トランスポート サーバー経由のインターネット メール フローを構成する
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61180558
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# EdgeSync を使用せずにエッジ トランスポート サーバー経由のインターネット メール フローを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-01-23_

通常は、エッジ サブスクリプション プロセスを使用して Exchange 組織とエッジ トランスポート サーバーの間のメール フローを確立することをお勧めします。ただし、状況によっては、エッジ サブスクリプション プロセスを使用してエッジ トランスポート サーバーから Exchange 組織へのサブスクライブを実行できないことがあります。Exchange 組織とエッジ トランスポート サーバーとの間のメール フローを手動で確立するには、Exchange 組織内のエッジ トランスポート サーバーおよびメールボックス サーバー上に送信コネクタと受信コネクタを作成して構成する必要があります。

## 開始する前に

  - このタスクの予想所要時間:30 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」トピックの「送信コネクタ」、「送信コネクタ - エッジ トランスポート」、および「受信コネクタ - エッジ トランスポート」。

  - この手順では、トランスポート層セキュリティ (TLS) 経由で基本認証を使用して暗号化と認証を提供します。TLS 経由の基本認証を使用する場合、受信側のサーバーに X.509 SSL (Secure Sockets Layer) サーバー証明書がインストールされている必要があります。受信コネクタに構成される完全修飾ドメイン名 (FQDN) の値は、SSL サーバー証明書内の FQDN に一致する必要があります。既定では、受信コネクタの FQDN の値は、その受信コネクタを含むサーバーの FQDN です。

  - 外部的にセキュリティで保護された認証方法も使用できます。ただし、その場合は、エッジ トランスポート サーバーとメールボックス サーバーの間の通信は Exchange によって認証または暗号化されません。外部的にセキュリティで保護された認証方法を使用するのは、追加の暗号化方法を使用している場合に限ることをお勧めします。暗号化方法には、インターネット プロトコル セキュリティ (IPsec) アソシエーションまたは仮想プライベート ネットワーク (VPN) などを使用できます。

  - エッジ トランスポート サーバーは通常は*マルチホーム*です。つまり、エッジ トランスポート サーバーには、複数のネットワーク セグメントに接続されたネットワーク アダプターがあります。それらネットワーク アダプターのそれぞれが、固有の IP 構成を持ちます。外部、つまりパブリックのネットワーク セグメントに接続されるネットワーク アダプターは、パブリック DNS (ドメイン ネーム システム) サーバーを名前解決に使用するよう構成する必要があります。この構成を行うことで、サーバーは SMTP ドメイン名を MX リソース レコードに解決してインターネットにメールをルーティングすることが可能になります。内部つまりプライベートのネットワーク セグメントに接続されるネットワーク アダプターは、境界ネットワーク内の DNS サーバーを使用するよう構成するか、Hosts ファイルが利用可能になっている必要があります。

  - Active Directory にユーザー アカウントを作成して、そのアカウントを Exchange Server コンピューターのユニバーサル セキュリティ グループに追加する必要があります。このアカウントは、Exchange 組織内の送信先のメールボックス サーバーに対する認証のために、エッジ トランスポート サーバーの送信コネクタによって使用されます。
    

    > [!IMPORTANT]
    > このアカウントには、Exchange Server を実行するコンピューターに関連するアクセス許可が付与されます。アカウントが悪用されないように、アカウントの資格情報を保護してください。特定のコンピューターにのみログオンを許可するようにアカウントを構成することができます。



## エッジ トランスポート サーバーの手順

エッジ トランスポート サーバーには、次のコネクタが必要です。

  - インターネットにメッセージを送信するように構成されている送信コネクタ

  - Exchange 組織内のメールボックス サーバーにメッセージを送信するように構成された送信コネクタ

  - Exchange 組織内のメールボックス サーバーからのみメッセージを受信するように構成された受信コネクタ

  - インターネットからのメッセージのみを受け付けるように構成された受信コネクタ

既定では、エッジ トランスポート サーバーの役割のインストール中に 1 つの受信コネクタが作成されます。このコネクタは、インターネットからの受信メッセージとメールボックス サーバーからの受信メッセージの両方に使用できます。通常、エッジ サブスクリプション プロセスは、既定の受信コネクタの正しいアクセス許可と認証を自動的に構成します。エッジ サブスクリプション プロセスを使用しない場合は、エッジ トランスポート サーバーの既定の受信コネクタに変更を加えて、インターネットからのメッセージのみを受け付けるようにすることをお勧めします。この変更を行ったら、内部のメールボックス サーバーからのみメッセージを受け付けるように構成された受信コネクタをエッジ トランスポート サーバーに作成する必要があります。

次のセクションでは、エッジ トランスポート サーバーが Exchange 組織と通信するための準備に必要なすべての構成手順について説明します。


> [!NOTE]
> エッジ トランスポート サーバーでこれらの手順を実行するには、シェルのみが使用できます。



## 手順 1:インターネットにメッセージを送信するよう構成された送信コネクタを作成する

この送信コネクタには、次の構成が必要です。

  - **名前**   To Internet (または任意のわかりやすい名前)

  - **使用法の種類**   インターネット

  - **アドレス スペース**   "\*" (すべてのドメイン)

  - **ネットワーク設定**   DNS の MX レコードを使用してメールを自動的にルーティングする。ネットワーク構成によっては、スマート ホスト経由でメールをルーティングすることもできます。スマート ホストはメールをインターネットにルーティングします。

インターネットにメッセージを送信するように構成された送信コネクタを作成するには、次のコマンドを実行します。

  ```powershell
  New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true
  ```

構文およびパラメーターの詳細については、「[New-SendConnector](https://technet.microsoft.com/ja-jp/library/aa998936\(v=exchg.150\))」を参照してください。

## 手順 2:メッセージを Exchange 組織に送信するよう構成された送信コネクタを作成する

送信コネクタを作成するには、**New-SendConnector** コマンドレットを使用します。


> [!NOTE]
> 送信コネクタを作成する前に、最初に <STRONG>Get-Credential</STRONG> コマンドを実行して、一時変数で使用するユーザー名とパスワードを保存する必要があります。<STRONG>New-SendConnector</STRONG> コマンドレットはプレーン テキストのユーザー資格情報を受け付けないため、これを実行する必要があります。



この送信コネクタには、次の構成が必要です。

  - **名前**   To Internal Org (または任意のわかりやすい名前)

  - **使用法の種類**   インターネット

  - **アドレス スペース**   Exchange 組織のすべての承認済みドメイン。たとえば、"\*.contoso.com"。

  - DNS ルーティングが無効 (スマート ホストのルーティングが有効)

  - **スマート ホスト**   1 つ以上のメールボックス サーバーのスマート ホストとしての FQDN。たとえば、mbxserver01.contoso.com と mbxserver02.contoso.com。

  - **スマート ホストの認証方法**   TLS 経由の基本認証

  - **スマート ホストの認証資格情報**   内部ドメインのユーザー アカウントの資格情報。**New-SendConnector** コマンドレットはプレーン テキストのユーザー資格情報を受け付けないため、ユーザー名とパスワードを最初に一時変数に保存しておく必要があります。

Exchange 組織にメッセージを送信するように構成された送信コネクタを作成するには、次のコマンドを実行します。

  ```powershell
  $MailboxCredentials = Get-Credential
  New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials
  ```

構文およびパラメーターの詳細については、「[New-SendConnector](https://technet.microsoft.com/ja-jp/library/aa998936\(v=exchg.150\))」を参照してください。

## 手順 3:インターネットからのメッセージのみを受け付けるよう既定の受信コネクタを変更する

既定の受信コネクタには、次のような構成変更を加える必要があります。

  - インターネットからの電子メールの受信だけに使用されるコネクタであることを反映した名前に変更します既定の受信コネクタの名前は「Default internal Receive connector \<エッジ トランスポート サーバー名\>」です。

  - インターネットからアクセス可能なネットワーク アダプターからのみメッセージを受け付けるようにネットワーク バインドを変更しますたとえば、10.1.1.1 と、標準 SMTP TCP ポート値 25。

インターネットからのメッセージのみを受け付けるように既定の受信コネクタを変更するには、次のコマンドを実行します。

  ```powershell
  Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25
  ```

構文およびパラメーターの詳細については、「[Set-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125140\(v=exchg.150\))」を参照してください。

## 手順 4:Exchange 組織からのメッセージのみ受け付けるよう構成された受信コネクタを作成する

この受信コネクタには、次の構成が必要です。

  - **名前**   From Internal Org (または任意のわかりやすい名前)

  - **使用法の種類**   インターネット

  - **ローカル ネットワーク バインド**   内部ネットワークに直接接続しているネットワーク アダプター。たとえば、10.1.1.2 と、標準 SMTP TCP ポート値 25。

  - **リモート ネットワーク設定**   Exchange 組織の 1 つ以上のメールボックス サーバーの IP アドレス。たとえば、192.168.5.10 と 192.168.5.20。

  - **認証方法** TLS、基本認証、TLS 経由の基本認証、および Exchange Server 認証。

Exchange 組織からのみメッセージを受け付けるように構成した受信コネクタを作成するには、次のコマンドを実行します。

  ```powershell
  New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20
  ```

構文およびパラメーターの詳細については、「[New-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125139\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

必要な送信コネクタおよび受信コネクタを正常に構成できたことを検証するには、エッジ トランスポート サーバー上で次のコマンドを実行し、表示される値が構成した値と同じであることを確認します。

  ```powershell
  Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
  Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges
  ```

## メールボックス サーバーの手順

組織内のメールボックス サーバーには、インターネットへの中継のためにメッセージをエッジ トランスポート サーバーに送信するように構成された送信コネクタが必要です。

既定では、メールボックス サーバーの役割のインストール中に 2 つの受信コネクタが作成されます。クライアント *サーバー名* という名前のコネクタは、すべての POP3 メッセージング クライアントおよび IMAP メッセージング クライアントからのメッセージを受け付けるように構成されます。既定 *サーバー名* という名前のコネクタは、エッジ トランスポート サーバーからのメッセージを受け付けるように構成されます。これらのコネクタに変更は必要ありません。

## 手順 5:エッジ トランスポート サーバーに送信メッセージを送信するように構成された送信コネクタの作成

この送信コネクタには、次の構成が必要です。

  - **名前**   To Edge (または任意のわかりやすい名前)

  - **使用法の種類**   インターネット

  - **アドレス スペース**   "\*" (すべてのドメイン)

  - DNS ルーティングが無効 (スマート ホストのルーティングが有効)

  - **スマート ホスト**   エッジ トランスポート サーバーの IP アドレス または FQDN。たとえば、edge01.contoso.net。

  - **ソース メールボックス サーバー** 1 つ以上のメールボックス サーバーの FQDN。たとえば、mbxserver01.contoso.com と mbxserver02.contoso.com。

  - **スマート ホストの認証方法**   TLS 経由の基本認証。

  - **スマート ホストの認証資格情報**   エッジ トランスポート サーバー上のユーザー アカウントの資格情報。**New-SendConnector** コマンドレットはプレーン テキストのユーザー資格情報を受け付けないため、ユーザー名とパスワードを最初に一時変数に保存しておく必要があります。

送信メッセージをエッジ トランスポート サーバーに送信するように構成された送信コネクタを作成するには、次のコマンドを実行します。

  ```powershell
  $EdgeCredentials = Get-Credential
  New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials
  ```

構文およびパラメーターの詳細については、「[New-SendConnector](https://technet.microsoft.com/ja-jp/library/aa998936\(v=exchg.150\))」を参照してください。

## このステップの検証方法

送信メッセージをエッジ トランスポート サーバーに送信するように構成した送信コネクタを正常に作成できたことを検証するには、メールボックス サーバーで次のコマンドを実行しし、表示される値が構成した値と同じであることを確認します。

  ```powershell
  Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism
  ```

