---
title: 'クライアント プロトコルの管理: Exchange 2013 Help'
TOCTitle: クライアント プロトコルの管理
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 49896351
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント プロトコルの管理

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Exchange ActiveSync、Outlook Web App、POP3、IMAP4、自動検出サービス、Exchange Web サービス、および空き時間情報サービスのクライアント プロトコルの管理は、次の 3 つの異なる領域で行われます。Exchange 管理センター (EAC)、Exchange 管理シェル、およびインターネット インフォメーション サービス (IIS) マネージャー。各場所で管理される設定は、クライアント プロトコルごとに異なります。

## Outlook Web App の設定の管理

ユーザーが使用できる Outlook Web App の機能に影響を与えるほとんどの設定は、Outlook Web App 仮想ディレクトリ上で設定するか、Outlook Web App メールボックス ポリシーで構成できます。Outlook Web App メールボックス ポリシーを使用すると、個々のユーザーが使用できる機能を定義できます。メールボックス ポリシーの設定は、仮想ディレクトリの設定を上書きします。Outlook Web App の管理の詳細については、「[Outlook Web App](outlook-web-app-exchange-2013-help.md)」を参照してください。

## Exchange ActiveSync の設定の管理

Exchange 2010 では、すべてのクライアント アクセス プロトコルが、クライアント アクセス サーバーの役割という単一のサーバーの役割に実装され、管理されていました。プロトコルの管理は IIS の単一インスタンスで実行され、Active Directory 内にはクライアント プロトコルごとに 1 つの仮想ディレクトリ オブジェクトがあり、仮想ディレクトリの構成に一式のコマンドレットが使用されていました。

Exchange 2013 では、Exchange ActiveSync のクライアント プロトコル管理は、クライアント アクセス サーバーとメールボックス サーバー間で分割されています。こうしたアーキテクチャの変更により、クライアント アクセス サーバーとメールボックス サーバーの両方で異なる仮想ディレクトリ管理タスクを実行できます。これら 2 つのサーバーが同じ物理コンピューター上にインストールされていない場合、仮想ディレクトリのコマンドレットで使用するパラメーターは、コマンドレットを実行しているサーバーの役割に基づいて変わります。

Exchange 2013 のアーキテクチャの変更の詳細については、「[Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md)」を参照してください。

Exchange ActiveSync 仮想ディレクトリに適用できる設定には、次の 2 つの種類があります。

  - メールボックスのセッションに適用できる設定

  - サーバーと仮想ディレクトリに適用できる設定

メールボックス セッションに適用できる設定は、ユーザー セッション設定です。ユーザーがクライアント アクセス サーバーに接続すると、その接続はユーザーのメールボックスを含むメールボックス サーバーに転送されます。仮想ディレクトリの一意の識別子は、転送される要求に組み込まれます。その後、メールボックス サーバーは Active Directory から仮想ディレクトリの設定を取得し、セッションに適用します。仮想ディレクトリの設定は、パフォーマンスを向上するために、メールボックス サーバーでキャッシュされます。

接続が別の Active Directory サイトに転送される場合、仮想ディレクトリの設定は、接続が開始されたクライアント アクセス サーバーからでなく、メールボックス サーバーと同じサイトのクライアント アクセス サーバーから読み込まれます。

次の表に、サーバーで管理できる仮想ディレクトリの設定を示します。サーバー上で適用できない特定の設定を管理しようとすると、設定しようとするプロパティは操作しているサーバーでは読み取り専用であることを示すエラー メッセージを受信します。

**クライアント アクセス サーバー上の Exchange ActiveSync 仮想ディレクトリの設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BadItemReportingEnabled</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
</tbody>
</table>


**クライアント アクセス サーバーとメールボックス サーバー上の Exchange ActiveSync 仮想ディレクトリの設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
</tbody>
</table>


## POP3 および IMAP4 の設定の管理

Exchange 2013 では、POP3 プロトコルと IMAP4 プロトコルの実装も、クライアント アクセス サーバーの役割とメールボックス サーバーの役割間で分割されます。新しい実装であるため、POP3 接続と IMAP4 接続は、クライアント アクセス サーバー上のサービスと同様に、メールボックス サーバー上のサービスでもそれぞれ管理されます。クライアント アクセス サーバー上で実行されるサービスの名前は、次のように Exchange 2010 で存在していた名前と同じです。Microsoft Exchange IMAP4 サービスおよび Microsoft Exchange POP3 サービス。メールボックス サーバー上で実行される新しい 2 つのサービスの名前は、Microsoft Exchange IMAP4 バックエンド サービスと Microsoft Exchange POP3 バックエンド サービスです。

組織内の POP3 接続と IMAP4 接続を管理する場合、以下のことを考慮してください。

  - クライアント アクセス サーバーの役割とメールボックス サーバーの役割を同じコンピューター上で実行している場合、POP3 設定または IMAP4 設定に対して行った変更は、正しい POP3 サービスと IMAP4 サービスに自動的に適用されます。

  - クライアント アクセス サーバーの役割とメールボックス サーバーの役割を別のコンピューター上で実行している場合、変更する設定を管理しているコンピューター上で設定を管理する必要があります。

次の表は、各サーバーの役割に対応する POP/IMAP 設定を示します。

**クライアント アクセス サーバー上の POP3 および IMAP4 の設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>Banner</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>クライアント アクセス</p></td>
</tr>
</tbody>
</table>


**メールボックス サーバー上の POP3 および IMAP4 の設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>メールボックス</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>メールボックス</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>メールボックス</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>メールボックス</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>メールボックス</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>メールボックス</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>メールボックス</p></td>
</tr>
</tbody>
</table>


**クライアント アクセス サーバーとメールボックス サーバー上の POP3 と IMAP4 の設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="even">
<td><p>Server</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>クライアント アクセスおよびメールボックス</p></td>
</tr>
</tbody>
</table>

