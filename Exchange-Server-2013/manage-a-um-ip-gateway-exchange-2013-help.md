---
title: 'UM IP ゲートウェイの管理: Exchange Online Help'
TOCTitle: UM IP ゲートウェイの管理
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 49896206
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: HT
---

# UM IP ゲートウェイの管理

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) IP ゲートウェイを作成した後は、各種設定の表示または構成ができます。たとえば、IP アドレスまたは完全修飾ドメイン名 (FQDN) の構成、送信呼び出し設定の構成、およびメッセージ待機インジケーターの有効化または無効化が実行できます。

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM IP ゲートウェイのプロパティを表示または構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM IP ゲートウェイ</strong> に移動します。リスト ビューで、管理する UM IP ゲートウェイを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.      
    <strong>UM IP ゲートウェイ</strong> ページで UM IP ゲートウェイの設定を表示および構成します。以下の設定を表示または構成することもできます。
    
      - <strong>状態</strong>   この表示専用フィールドには、UM IP ゲートウェイの状態が表示されます。
    
      - <strong>名前</strong>   このボックスを使用して、UM IP ゲートウェイの一意の名前を指定します。これは、EAC に表示される表示名です。UM IP ゲートウェイの作成後に表示名を変更する必要がある場合、最初に既存の UM IP ゲートウェイを削除し、次に適切な名前を持つ別の UM IP ゲートウェイを作成します。UM IP ゲートウェイ名は必須ですが、表示にのみ使用されます。組織では複数の UM IP ゲートウェイを使用することがあるため、UM IP ゲートウェイにはわかりやすい名前を使用することをお勧めします。UM IP ゲートウェイ名は最大 64 文字です。スペースも使用できます。
    
      - <strong>アドレス</strong>   IP アドレスまたは完全修飾ドメイン名 (FQDN) を使用して UM IP ゲートウェイを構成できます。このボックスでは、VoIP ゲートウェイ、SIP が有効な PBX、IP PBX、または SBC に構成した IP アドレスや FQDN を指定できます。
        
        このボックスにはアルファベットと数字を入力できます。IPv4 アドレス、IPv6 アドレス、および FQDN がサポートされています。FQDN を使用する場合、ホスト名が IP アドレスに正しく解決されるよう、VoIP ゲートウェイに DNS ホスト レコードを正しく構成しておく必要があります。また、IP アドレスの代わりに FQDN を使用していて、かつ UM IP ゲートウェイの DNS 構成が変更される場合、UM IP ゲートウェイをいったん無効化してから有効化し、UM IP ゲートウェイの構成情報が正しく更新されていることを確認する必要があります。
        
        UM IP ゲートウェイと、セキュリティで保護された SIP モードまたはセキュリティ保護されたモードで運用されているダイヤル プランの間で相互トランスポート層セキュリティ (相互 TLS) を使用するには、FQDN を使用して UM IP ゲートウェイを構成する必要があります。また、ポート 5061 で接続要求を待つように構成し、IP ゲートウェイまたは IP PBX もすべて、ポート 5061 で相互 TLS の接続要求を待つように構成されていることを確認する必要があります。UM IP ゲートウェイを構成するには、次のコマンドを実行します。`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
    
      - <strong>この UM IP ゲートウェイ経由の送信呼び出しを許可する</strong>   UM IP ゲートウェイが送信呼び出しを受け付けて処理するように設定するには、このチェック ボックスをオンにします。この設定は、VoIP ゲートウェイからの呼び出し転送や着信呼び出しには影響しません。
        
        既定では、この設定は UM IP ゲートウェイの作成時に有効に設定されます。この設定を無効にすると、ダイヤル プランに関連付けられているユーザーは、<strong>アドレス</strong> のフィールドに定義されている VoIP ゲートウェイ、IP PBX、または SBC 経由の送信呼び出しができなくなります。
    
      - <strong>メッセージ待機インジケーターを許可する</strong>   UM IP ゲートウェイが処理する呼び出しがあったときに、ボイス メール通知をユーザーに送信するには、このチェック ボックスをオンにします。この設定は、ユーザーに対する SIP NOTIFY メッセージの送受信を UM IP ゲートウェイに許可します。この設定は既定で有効であり、メッセージ待機通知がユーザーに送信されることを許可します。
        
        メッセージ待機インジケーターは、新規メッセージや未確認メッセージの有無を示すすべてのメカニズムを参照できます。新しい音声メッセージの到着の通知は、クライアントの受信トレイに Outlook および Outlook Web App のように表示されます。これは、登録済みの携帯電話に対して送信されるショート メッセージ サービス (SMS) またはテキスト メッセージや、Exchange サーバーから事前に構成された番号に対する送信呼び出しを行ったり、ユーザーのデスクトップの電話のランプを点灯したりといった形式を取ることができます。

## シェルを使用して、UM IP ゲートウェイのプロパティを構成する

この例では、`MyUMIPGateway` という名前の UM IP ゲートウェイの IP アドレスを変更します。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

この例では、`MyUMIPGateway` という名前の UM IP ゲートウェイが着信呼び出しを受け付けないようにし、また、発信呼び出しを行えないようにします。

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

この例では、UM IP ゲートウェイに VoIP ゲートウェイのシミュレーターとしての機能を持たせ、**Test-UMConnectivity** コマンドレットに対応させます。

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true


> [!IMPORTANT]
> UM IP ゲートウェイの構成に加えたすべての変更が、UM IP ゲートウェイと同じ UM ダイヤル プラン内のすべての Exchange サーバーにレプリケートされるまでには少し時間がかかります。



この例では、`MyUMIPGateway` という UM IP ゲートウェイが着信することを禁止し、発信することを禁止し、IPv6 アドレスを設定し、この UM IP ゲートウェイで IPv4 および IPV6 アドレスを使用することを許可します。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## シェルを使用して、UM IP ゲートウェイのプロパティを表示する

この例では、Active Directory フォレストのすべての UM IP ゲートウェイの書式化された一覧を表示します。

    Get-UMIPGateway |Format-List

この例では、`MyUMIPGateway` という名前の UM IP ゲートウェイのプロパティを表示します。

    Get-UMIPGateway -Identity MyUMIPGateway

この例では、Active Directory フォレストの VoIP ゲートウェイ シミュレーターなど、すべての UM IP ゲートウェイを表示します。

    Get-UMIPGateway -IncludeSimulator $true

