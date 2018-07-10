---
title: 'MAPI over HTTP: Exchange 2013 Help'
TOCTitle: MAPI over HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61204836
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MAPI over HTTP

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-05-10_

Messaging Application Programming Interface (MAPI) over HTTP は、MicrosoftExchange Server 2013 Service Pack 1 (SP1) に実装されている新しいトランスポート プロトコルです。MAPI over HTTP では、Outlook と Exchange の接続の信頼性および安定性を改善するために、トランスポート層を業界標準の HTTP モデルに移行させています。これにより、トランスポート エラーの可視性レベルが向上するとともに、回復性が強化されます。追加機能には、明示的な一時停止後再開機能のサポートが含まれています。これにより、サポートされているクライアントは、同じサーバー コンテキストを維持しながら、ネットワークを変更したり、休止状態から再開したりできます。

MAPI over HTTP の実装は、Outlook でこのプロトコルを使用しなければ Exchange にアクセスできないことを意味するものではありません。MAPI over HTTP に対応していない Outlook クライアントは、引き続き Outlook を使用して、MAPI 対応のクライアント アクセス サーバーを介して Exchange にアクセスできます。

## MAPI over HTTP の利点

MAPI over HTTP には、それをサポートするクライアントで次の利点があります。

  - HTTP ベースのプロトコルを使用して、将来の認証技術の革新に対応できます。

  - 通信が切断された場合、再作成する必要があるのは (RPC 接続ではなく) TCP 接続だけなので、再接続時間が短縮されます。通信切断が発生する例には、以下があります。
    
      - デバイスの休止状態
    
      - 有線ネットワークからワイヤレスまたは携帯電話ネットワークへの変更

  - 接続に依存しないセッション コンテキストを提供します。サーバーは、ユーザーがネットワークを変更したとしても、一定の期間 (構成可能です)、セッション コンテキストを維持します。

## MAPI over HTTP を展開する

MAPI over HTTP を有効にするには、次の要件を検討してください。

  - **サポート**   必要な構成バージョンがサポートされていることを確認します。

  - **前提条件**   MAPI over HTTP に対応するように環境がアップグレードされて準備済みであることを確認します。

  - **構成**   仮想ディレクトリを構成し、組織の MAPI を有効にします。

## サポート

以下の表を使用して、クライアントとサーバーが MAPI over HTTP をサポートすることを確認します。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>製品</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI over HTTP</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010 SP2 と更新 KB2956191 および KB2965295 (2015 年 4 月 14 日)</p></td>
<td><ul>
<li><p>MAPI over HTTP<span></span></p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 SP2 以前のバージョン</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook Anywhere</p></td>
<td><p>Outlook Anywhere</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook Anywhere</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 前提条件

MAPI over HTTP をサポートするようにクライアントとサーバーを準備するには、以下の手順を実行します。

1.  Outlook クライアントを Outlook 2013 SP1 または Outlook 2010 SP2 と更新 KB2956191 および KB2965295 (2015 年 4 月 14 日) にアップグレードします。

2.  クライアント アクセス サーバーおよびメールボックス サーバーを Exchange 2013 SP1 にアップグレードします。アップグレード方法については、「[Exchange 2013 から最新の累積更新プログラムまたは Service Pack へのアップグレード](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > MAPI over HTTP を有効にする前に、すべてのクライアント アクセス サーバーが Exchange 2013 SP1 にアップグレードされていなければなりません。そうでない場合、Outlook がメールボックスに接続できない可能性があります。<BR>データベース可用性グループ (DAG) に属するメールボックス サーバーが 1 つでもアップグレードされていないと、電子メールの遅延が発生する可能性があります。さらに、データベース フェールオーバーの発生時に、クライアントは Outlook の再起動が必要になります。



3.  すべての Exchange 2013 サーバーで、Microsoft.NET Framework 4.5.2 をインストールする必要があります。詳細については、「[.NET Framework のインストール](https://go.microsoft.com/fwlink/p/?linkid=518380)」をご覧ください。

4.  すべての Exchange 2013 SP1 クライアント アクセス サーバーで、次の手順を実行して Windows 環境変数 **COMPLUS\_DisableRetStructPinning** を追加します。
    
    1.  コマンド プロンプト ウィンドウで、`systempropertiesadvanced` を実行してから **\[環境変数\]** をクリックします。
    
    2.  **\[システム変数\]** セクションで、**\[新規\]** をクリックしてから次の情報を入力します。
        
          - **変数の名前**   `COMPLUS_DisableRetStructPinning`
        
          - **変数の値** 1
    
    3.  完了したら、**\[OK\]** をクリックします。

## 構成

組織の MAPI over HTTP を構成するには、以下の手順を実行します。

1.  **仮想ディレクトリの構成**   既定では、Exchange 2013 SP1 は MAPI over HTTP 用の仮想ディレクトリを作成します。仮想ディレクトリを構成するには、**Set-MapiVirtualDirectory** コマンドレットを使用します。内部 URL、外部 URL、またはその両方を構成する必要があります。詳細については、「[Set-MapiVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dn595082\(v=exchg.150\))」を参照してください。
    
    たとえば、内部 URL 値を https://contoso.com/mapi に設定し、認証方式を `Negotiate` に設定して、ローカル Exchange サーバー上に既定の MAPI 仮想ディレクトリを構成するには、以下のコマンドを実行します。
    
        Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate

2.  **証明書の構成**   Exchange 環境で使用するデジタル証明書には、MAPI 仮想ディレクトリに定義した *InternalURL* および *ExternalURL* の値と同じ値が含まれている必要があります。Exchange 2013 証明書管理の詳細については、「[デジタル証明書と SSL](digital-certificates-and-ssl-exchange-2013-help.md)」を参照してください。Exchange 証明書が Outlook クライアント ワークステーションで信頼されること、および証明書エラーがないことを確認する必要があります。これは、MAPI 仮想ディレクトリに構成された URL にアクセスする場合には特に重要です。

3.  **サーバー ルールの更新**   ロード バランサー、リバース プロキシ、ファイアウォールが、MAPI over HTTP 仮想ディレクトリへのアクセスを許可するように構成されていることを確認します。

4.  **Exchange 組織内で MAPI over HTTP を有効にする**
    
    次のコマンドを実行します。
    
        Set-OrganizationConfig -MapiHttpEnabled $true

## MAPI over HTTP 接続をテストする

エンド ツー エンドの MAPI over HTTP 接続をテストするには、**Test-OutlookConnectivity** コマンドレットを使用します。**Test-OutlookConnectivity** コマンドレットを使用するには、Microsoft Exchange Health Manager (MSExchangeHM) サービスが開始されている必要があります。

以下の例では、ContosoMail という名前の Exchange サーバーからの MAPI over HTTP 接続をテストします。

    Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe

テストが成功すると、次のような出力が返されます。

    MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
    ---------------                                          ---------              -------                ------      -----     ---------
    OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded

詳細については、「[Test-OutlookConnectivity](https://technet.microsoft.com/ja-jp/library/dd638082\(v=exchg.150\))」を参照してください。

MAPI over HTTP の動作状況ログは、以下の場所にあります。

  - %ExchangeInstallPath%Logging\\MAPI Address Book Service\\

  - %ExchangeInstallPath%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## MAPI over HTTP を管理する

次のコマンドレットを使用して、MAPI over HTTP の構成を管理できます。

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dn595083\(v=exchg.150\))

