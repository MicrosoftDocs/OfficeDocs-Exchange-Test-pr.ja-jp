---
title: '着信 FAX の設定: Exchange Online Help'
TOCTitle: 着信 FAX の設定
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52057426
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 着信 FAX の設定

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Microsoft Exchange ユニファイド メッセージング (UM) は、送信 FAX や FAX ルーティングなどの拡張 FAX 機能用として認定された FAX パートナー ソリューションに依存します。既定では、Exchange サーバーは、UM が有効なユーザーへの着信 FAX の配信を許可するよう構成されていません。代わりに、Exchange サーバーは着信 FAX 呼び出しを認定 FAX パートナー ソリューションにリダイレクトします。FAX パートナーのサーバーは FAX データを受信し、FAX が.tif 添付ファイルとして含まれている電子メール メッセージ内のユーザーのメールボックスにその FAX データを送信します。

FAX パートナーの詳細は、「[Microsoft Pinpoint の FAX パートナー](https://go.microsoft.com/fwlink/?linkid=190238)」を参照してください。

## FAX 送受信の展開と構成

UM は、受信 FAX 呼び出しを専門の FAX パートナー ソリューションに転送します。この FAX パートナー ソリューションは、FAX 送信者と FAX 通話を確立し、UM が有効なユーザーの代わりに FAX を受信します。ただし、UM が有効なユーザーが自分のメールボックスで FAX メッセージを受信できるようにするには、まず着信 FAX を有効にして、UM が有効なユーザーにリンクされた UM メールボックス ポリシーで FAX パートナーの URI を設定する必要があります。UM ダイヤル プラン、UM メールボックス ポリシー、および UM が有効なユーザーのメールボックスで着信 FAX を許可または禁止できます。詳細については、以下のトピックを参照してください。

  - [同じダイヤル プランのユーザーが FAX を受信できるようにする](allow-users-in-the-same-dial-plan-to-receive-faxes-exchange-2013-help.md)

  - [同じダイヤル プランのユーザーが FAX を受信できないようにする](prevent-users-in-the-same-dial-plan-from-receiving-faxes-exchange-2013-help.md)

  - [ユーザー グループの FAX 送受信を有効にする](enable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [ユーザー グループの FAX 送受信を無効にする](disable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [ユーザーが FAX を受信できるようにする](enable-a-user-to-receive-faxes-exchange-2013-help.md)

  - [ユーザーが FAX を受信できないようにする](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)

## 手順 1:ユニファイド メッセージングを展開する

社内組織またはハイブリッド組織の FAX 送受信を設定する前に、クライアント アクセス サーバーおよびメールボックス サーバーを展開して、サポートしている VoIP (Voice over IP) ゲートウェイを構成し、FAX 送受信を許可する必要があります。UM を展開する方法の詳細については、「[Exchange 2013 UM の展開](deploy-exchange-2013-um-exchange-2013-help.md)」を参照してください。VoIP ゲートウェイおよび IP 構内交換機 (PBX) を展開する方法の詳細については、「[UM を電話システムに接続する](connect-um-to-your-telephone-system-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> T.38 または G.711 を使用した FAX の送受信は、ユニファイド メッセージングと MicrosoftOffice Communications Server 2007 R2 または Microsoft Lync Server が統合された環境ではサポートされていません。



## 手順 2:FAX パートナー サーバーを構成する

次に、着信 FAX を有効にして、組織内で必要なそれぞれの UM メールボックス ポリシーで FAX パートナーの URI を構成する必要があります。着信 FAX を正常に展開するには、認定 FAX パートナー ソリューションと Exchange ユニファイド メッセージングを統合する必要があります。詳細については、「[Exchange UM の FAX アドバイザー](fax-advisor-for-exchange-um-exchange-2013-help.md)」を参照してください。認定 FAX パートナーの一覧については、「[Microsoft Pinpoint の FAX パートナー](https://go.microsoft.com/fwlink/?linkid=190238)」を参照してください。


> [!NOTE]
> FAX パートナー サーバーは組織の外にあるため、ファイアウォール ポートを構成して、IP ベースのネットワークを介した FAX の送受信を有効にする T.38 プロトコル ポートを許可する必要があります。既定では、T.38 プロトコルは TCP ポート 6004 を使用します。ユーザー データグラム プロトコル (UDP) のポート 6044 も使用しますが、これはハードウェアの製造元によって定義されます。ファイアウォール ポートを構成して、TCP、または製造元が定義する UDP ポートまたはポート範囲を使用する FAX データを許可する必要があります。



## 手順 3:ユニファイド メッセージングの FAX 送受信を有効にする

ユーザーがユニファイド メッセージングを使用して FAX を受信できるようにするには、次の 3 つのコンポーネントを正しく構成する必要があります。

  - UM ダイヤル プラン

  - UM メールボックス ポリシー

  - UM メールボックス

UM ダイヤル プラン、UM メールボックス ポリシー、または個別の UM が有効なユーザーのメールボックスで、FAX 送受信を有効または無効にできます。UM メールボックス ポリシーは、Exchange 管理センター (EAC) または Exchange 管理シェルのいずれかを使用して、FAX 送受信を有効または無効にできます。ダイヤル プランと個別の UM が有効なユーザーの有効化および無効化は、Exchange 管理シェルを使用して実行する必要があります。次の表に、使用可能なオプションと、FAX 送受信の有効化および無効化に使用するコマンドレットとパラメーターを示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM コンポーネント</th>
<th>EAC を使用した有効化/無効化</th>
<th>FAX 送受信を有効にするシェルの例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ダイヤル プラン</p></td>
<td><p>X</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>UM メールボックス ポリシー</p></td>
<td><p>○</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>UM が有効なユーザー</p></td>
<td><p>X</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


既定では、UM ダイヤル プランおよびユーザーのメールボックスで FAX 受信が許可されていますが、UM が有効なユーザーに割り当てられている UM メールボックス ポリシーで最初に FAX 受信を有効にし、FAX パートナー サーバーの URI を入力する必要があります。

UM が有効なユーザーが FAX を受信できるようにするには、次の操作を行う必要があります。

  - 各 UM ダイヤル プランでダイヤル プランと関連付けられているユーザーが FAX 受信を許可されていることを確認します。既定では、ダイヤル プランに関連づけられたすべてのユーザーが FAX を受信できます。UM が有効なユーザーが自分のメールボックスで FAX メッセージを受信する場合は、着信 FAX 呼び出しを受け入れるように VoIP ゲートウェイまたは IP PBX を構成する必要があります。また、ダイヤル プランにリンクされているユーザーが FAX メッセージを受信できるようにする必要があります。ダイヤル プランにリンクされたユーザーによる FAX の受信を許可または禁止する方法の詳細については、「[ユーザーが FAX を受信できるようにする](enable-a-user-to-receive-faxes-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > ダイヤル プランで FAX メッセージの受信を禁止した場合は、個々のユーザーのプロパティで FAX を受信できるように構成しても、そのダイヤル プランと関連付けられているユーザーは FAX を受信できなくなります。UM ダイヤル プランでの FAX 送受信の有効化または無効化は、個々の UM が有効なユーザーに対する設定より優先されます。



  - UM が有効になっているユーザーに関連付けられている UM メールボックス ポリシーを構成する。UM メールボックス ポリシーは、FAX パートナーの URI および FAX パートナーのサーバー名を含む、着信 FAX を許可するように構成する必要があります。*FaxServerURI* パラメーターは、次の形式を使用する必要があります。sip:\<*FAX サーバーの URI*\>:\<*ポート*\>;\<*トランスポート*\>。ここで、"FAX サーバーの URI" は、完全修飾ドメイン名 (FQDN) または FAX パートナー サーバーの IP アドレスです。"ポート" は、FAX サーバーが着信 FAX 呼び出しを待機するポート、"トランスポート" は、着信 FAX で使用されるトランスポート プロトコル (UDP、TCP、またはトランスポート層セキュリティ (TLS)) です。たとえば、UM メールボックス ポリシーの構成によって、次のように FAX を受信できるようになります。
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - 詳細については、「[パートナー FAX サーバーの URI を設定して FAX 送受信を許可する](set-the-partner-fax-server-uri-to-allow-faxing-exchange-2013-help.md)」を参照してください。
    

    > [!WARNING]
    > セミコロンで区切ると <EM>FaxServerURI</EM> の形式で複数のエントリを含めることができますが、使用されるエントリは 1 つのみです。このパラメーターでは、1 つのエントリのみが使用されるようになるため、複数のエントリを追加しても、FAX 要求を負荷分散することはできません。



  - UM が有効なメールボックスで FAX メッセージを受信できることを確認します。既定では、ダイヤル プランに関連づけられたすべてのユーザーが FAX を受信できます。ただし、FAX を受信する機能がメールボックスで無効になっているために、ユーザーが FAX を受信できない場合もあります。UM が有効なユーザーが FAX を受信できるようにする方法の詳細については、「[ユーザーが FAX を受信できるようにする](enable-a-user-to-receive-faxes-exchange-2013-help.md)」を参照してください。
    
    ダイヤル プランと関連付けられている個別のユーザーが FAX メッセージを受信できないようにすることが可能です。これを行うには、シェルで **Set-UMMailbox** コマンドレットを使用してユーザーのプロパティを構成します。また、**Set-UMMailboxPolicy** コマンドレットを使用して、複数のユーザーが FAX メッセージの受信できないようにすることも可能です。1 人または複数のユーザーが FAX メッセージを受信しないようにする方法の詳細については、「[ユーザーが FAX を受信できないようにする](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)」を参照してください。

## 手順 4:認証を構成する

UM ダイヤル プラン、UM メールボックス ポリシー、および UM が有効なユーザーの構成に加えて、Exchange サーバーと FAX パートナー サーバー間の認証を構成する必要があります。Exchange サーバーは、FAX パートナー サーバーから着信したメッセージの発信元を認証できるようにする必要があります。FAX パートナー サーバーから着信しても認証されていないメッセージは、Exchange サーバーでは処理されません。

FAX パートナー サーバーと Exchange サーバーの接続を認証するには、以下を使用できます。

  - 相互 TLS

  - 送信者 ID の検証

  - 専用の受信コネクタ

受信コネクタは、組織内に展開された FAX パートナー サーバーの認証に対応できるものを使用してください。受信コネクタは、Exchange サーバーが FAX パートナー サーバーからのすべてのトラフィックを認証済みとして処理できるようにします。

受信コネクタは、FAX パートナー サーバーが SMTP FAX メッセージの送信に使用する Exchange サーバーで構成し、次の値にする必要があります。

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

詳細については、「[コネクタ](connectors-exchange-2013-help.md)」を参照してください。

FAX パートナー サーバーから Exchange サーバーに、パブリック ネットワークを通してネットワーク トラフィックを送信する場合、たとえば、クラウドでホストされているサービス ベースの FAX パートナー サーバーでは、送信者の ID チェックを使用して FAX パートナー サーバーを認証するとよいでしょう。この種類の認証は、FAX メッセージの送信元である IP アドレスを認証して、メッセージの送信元を称する FAX パートナー ドメインの代理として電子メール メッセージを送信できるようにします。DNS は、送信者の ID レコード (または、SPF (Sender Policy Framework) レコード) を格納するために使用され、FAX パートナーは DNS 前方参照ゾーン内のそれぞれの SPF レコードを発行する必要があります。Exchange は、DNS を照会して IP アドレスを検証します。ただし、DNS 参照を実行できるように、メールボックス サーバーで送信者 ID エージェントを実行する必要があります。

また、TLS を使用してネットワーク トラフィックを暗号化したり、相互 TLS で FAX パートナー サーバーと Exchange サーバー間の暗号化や認証を実行したりできます。

