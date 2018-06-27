---
title: 'クライアント固有のメッセージのサイズ制限を構成する: Exchange 2013 Help'
TOCTitle: クライアント固有のメッセージのサイズ制限を構成する
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52057861
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント固有のメッセージのサイズ制限を構成する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2017-01-26_

Microsoft Exchange Server 2013 には、メッセージが Exchange 組織を経由する際にメッセージに適用されるいくつかの異なるメッセージ サイズ制限があります。詳細については、「[メッセージ サイズの制限](message-size-limits-exchange-2013-help.md)」を参照してください。

ただし、Outlook Web App および、ActiveSync または Exchange Web サービス (EWS) を使用している電子メール クライアントに構成できるクライアント固有のメッセージ サイズ制限があります。Exchange 組織全体のメッセージ サイズ制限を変更する場合は、Outlook Web App、ActiveSync、および Exchange Web サービスのメッセージ サイズ制限がそれに従って設定されていることを確認する必要があります。これらの値は、クライアント アクセス サーバーとメールボックス サーバー上の web.config ファイルで構成します。以下の表で、これらの制限を説明します。

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サーバーの役割</th>
<th>構成ファイル</th>
<th>キーと既定値</th>
<th>サイズ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>クライアント アクセス</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   既定では存在しません (コメントを参照)。</p></td>
<td><p>バイト</p></td>
</tr>
<tr class="even">
<td><p>クライアント アクセス</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>キロバイト</p></td>
</tr>
<tr class="odd">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   既定では存在しません (コメントを参照)。</p></td>
<td><p>バイト</p></td>
</tr>
<tr class="even">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>キロバイト</p></td>
</tr>
<tr class="odd">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>バイト</p></td>
</tr>
</tbody>
</table>


**ActiveSync 制限についてのコメント**

既定では、`web.config` ファイルに、ActiveSync のための *maxAllowedContentLength* キーはありません。ただし、ActiveSync の最大メッセージ サイズは、サーバー上のすべての Web サイトに適用される **maxAllowedContentLength** 値の影響を受けます。既定値は 30000000 バイト (30 MB) です。クライアント アクセス サーバーおよびメールボックス サーバーで、ActiveSync に対するこれらの値を IIS マネージャーに表示するには、以下の手順を実行します。

1.  次のいずれかの手順を実行します。
    
      - クライアント アクセス サーバーで、**\[IIS マネージャー\]** を開き、**\[サイト\]** \> **\[既定の Web サイト\]** に移動して、**\[Microsoft-Server-ActiveSync\]** を選択します。
    
      - メールボックス サーバーで、**\[IIS マネージャー\]** を開き、**\[サイト\]** \> **\[Exchange バックエンド\]** に移動して、**\[Microsoft-Server-ActiveSync\]** を選択します。

2.  **\[機能ビュー\]** が選択されていることを確認して、**\[管理\]** セクションの **\[構成エディター\]** をダブルクリックします。

3.  **\[セクション\]** フィールドのドロップダウン矢印をクリックし、**\[system.webServer\]** \> **\[セキュリティ\]** に移動して、**\[requestFiltering\]** を選択します。

4.  結果の中の **\[requestLimits\]** を展開すると、**\[maxAllowedContentLength\]** および既定値の 30000000 (バイト) が表示されます。

**maxAllowedContentLength** 値を変更するには、新しい値をバイト数で入力して、**\[適用\]** をクリックします。クライアント アクセス サーバーとメールボックス サーバーでの値を変更する必要があります。IIS マネージャーで値を変更した後、新しい *maxAllowedContentLength* キーが、対応する `web.config` ファイル (クライアント アクセス サーバーの `%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config` およびメールボックス サーバーの `%ExchangeInstallPath%ClientAccess\Sync\web.config`) に書き込まれます。

ActiveSync クライアントの最大メッセージ サイズを変更するには、クライアント アクセス サーバーとメールボックス サーバーの `web.config` ファイルで *maxRequestLength* の値、メールボックス サーバーの `web.config` ファイルで *MaxDocumentDataSize* の値、およびクライアント アクセス サーバーとメールボックス サーバーの IIS マネージャーで *maxAllowedContentLength* の値を変更する必要があります。

### Exchange Web サービス

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サーバーの役割</th>
<th>構成ファイル</th>
<th>キーと既定値</th>
<th>サイズ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>クライアント アクセス</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>バイト</p></td>
</tr>
<tr class="even">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>バイト</p></td>
</tr>
<tr class="odd">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxReceivedMessageSize=&quot;67108864&quot;</code> の 14 のインスタンス</p></td>
<td><p>バイト</p></td>
</tr>
</tbody>
</table>


**Exchange Web Services の制限に関するコメント**

  - 値 `maxReceivedMessageSize="67108864"` には、バインド (http および https) と認証方式の異なる組合せに対応した 14 の個別のインスタンスがあります。

  - Exchange Web サービス クライアントのメッセージの最大サイズを変更するには、両方の `web.config` ファイルで *maxAllowedContentLength* の値、およびメールボックス サーバー上の `web.config` ファイルで `maxReceivedMessageSize="67108864"` の 14 のすべてのインスタンスを変更する必要があります。

  - メールボックス サーバーの `web.config` ファイルには、**UMLegacyMessageEncoderSoap11Element** バインドに対する値 `maxReceivedMessageSize="1048576"` の 2 つのインスタンスもありますが、これらは変更する必要がありません。

  - *maxRequestLength* は、両方の web.config ファイルに存在する ASP.NET の設定ですが、Exchange Web サービスでは使用されないので変更する必要はありません。

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>サーバーの役割</th>
<th>構成ファイル</th>
<th>キーと既定値</th>
<th>サイズ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>クライアント アクセス</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>バイト</p></td>
</tr>
<tr class="even">
<td><p>クライアント アクセス</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>キロバイト</p></td>
</tr>
<tr class="odd">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>バイト</p></td>
</tr>
<tr class="even">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>キロバイト</p></td>
</tr>
<tr class="odd">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxReceivedMessageSize=&quot;35000000&quot;</code> の 2 つのインスタンス</p></td>
<td><p>バイト</p></td>
</tr>
<tr class="even">
<td><p>メールボックス</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxStringContentLength=&quot;35000000&quot;</code> の 2 つのインスタンス</p></td>
<td><p>バイト</p></td>
</tr>
</tbody>
</table>


**Outlook Web App 制限についてのコメント**

  - メールボックス サーバー上の `web.config` ファイルには、http と https バインドに対応する、値 `maxReceivedMessageSize="35000000"` と `maxStringContentLength="35000000"` の 2 つの別個のインスタンスがあります。

  - Outlook Web App クライアントの最大メッセージ サイズを変更するには、メールボックス サーバーの `web.config` ファイルにある *maxReceivedMessageSize* と *maxStringContentLength* の両方のインスタンスを含めて、両方のファイルでこれらの値すべてを変更する必要があります。

  - メールボックス サーバーの `web.config` ファイルには、**MsOnlineShellService** バインドに対する値 `maxStringContentLength="102400"` のインスタンスもありますが、それは変更する必要がありません。

すべてのメッセージ サイズ制限について、適用したい実際のサイズより大きい値を設定する必要があります。この値の増加が必要となるのは、メッセージの添付ファイルとその他のバイナリ データが Base64 エンコードされた後、メッセージ サイズが必ず増加するためです。Base64 エンコードによりメッセージのサイズは約 33% 増加するため、メッセージ サイズ制限に指定する値は、実際に使用可能なメッセージ サイズより約 33% 大きくなります。たとえば、最大メッセージ サイズの値を 64 MB に指定すると、実際の最大メッセージ サイズの値は約 48 MB になると予測できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - Exchange のアクセス許可は、このトピックの手順には適用されません。これらの手順は、Exchange Server のオペレーティング システムで実行されます。

  - Web.config 構成ファイルに保存した変更は、IIS の再起動後に適用されます。

  - Base64 エンコードによる 33% のサイズ増加を許容するには、必要な新しい最大サイズ値 (メガバイト単位) に 4/3 を乗算します。また、値をキロバイトに変換するには、1024 を乗算し、値をバイトに変換するには、1048756 (1024\*1024) を乗算します。Base64 エンコードに伴うサイズの増加は、たとえば、添付ファイルのサイズ、種類、圧縮、メッセージの作成と送信に使用されている電子メール クライアントなどのいくつかの要因に応じて、33% を上回ることがある点に注意してください。

  - Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## メモ帳を使用してクライアント固有のメッセージのサイズ制限を構成する

1.  適切な web.config ファイルをメモ帳で開きます。たとえば、Exchange Web サービス クライアントの web.config ファイルを開くには、次のコマンドを実行します。
    
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config

2.  このトピックの上記の表で説明したとおり、適切な web.config ファイルで関連するキーを見つけます。たとえば、Exchange Web サービス のクライアントでは、両方のファイルで *maxAllowedContentLength* キー、およびメールボックス サーバー上の `web.config` ファイルで値 `maxReceivedMessageSize="67108864"` の 14 のすべてのインスタンスを見つけます。
    
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    
    たとえば、約 64 MB の Base64 エンコードされた最大メッセージ サイズを許容するには、`67108864` のすべてのインスタンスを `89478486` (64\*4/3\*1048756) に変更します。
    
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...

3.  完了したら、web.config ファイルを保存して閉じます。

4.  次のコマンドを実行して IIS を再起動します。
    
        IISReset /noforce

## コマンド ラインからクライアント固有のメッセージのサイズ制限を構成する

メモ帳を使用する代わりに、コマンド ラインからクライアント固有のメッセージのサイズ制限を構成することもできます。Exchange サーバーで管理者特権でのコマンド プロンプト (**\[管理者として実行\]** を選択して開くコマンド プロンプト ウィンドウ) を開き、構成する制限に該当するコマンドを実行します。

**注**:

  - コマンドのサイズ値は既定値であり、変更する必要があります。

  - 値がバイト単位か、キロバイト単位かに注意してください。

**ActiveSync**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000

**Exchange Web サービス**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864

**Outlook Web App**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000

## 正常な動作を確認する方法

クライアントに固有のメッセージ サイズの制限が正常に構成されていることを確認するには、影響を受けるクライアントによってアクセスされているメールボックスとの間で、テスト メッセージを送受信する必要があります。テスト メッセージが構成した値を約 33% 下回るように、複数の小さい添付ファイルやサイズの大きい 1 つの添付ファイルを試すことができます。たとえば、構成した値が 85 MB の場合、実際の最大メッセージ サイズは約 64 MB になります。

