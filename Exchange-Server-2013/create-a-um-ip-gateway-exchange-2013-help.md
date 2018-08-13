---
title: 'UM IP ゲートウェイを作成する: Exchange Online Help'
TOCTitle: UM IP ゲートウェイを作成する
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 49896252
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: HT
---

# UM IP ゲートウェイを作成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) IP ゲートウェイを作成すると、新しい VoIP (Voice over IP) ゲートウェイ、セッション開始プロトコル (SIP) が有効な構内交換機 (PBX) メールボックス サーバー、IP PBX、またはセッション ボーダー コントローラー (SBC) に接続するための Exchange サーバーが有効になります。UM IP ゲートウェイを作成したら直ちに新しい UM ハント グループを作成し、UM IP ゲートウェイにその UM ハント グループを関連付ける必要があります。1 つ以上の UM ハント グループを作成すると、UM IP ゲートウェイを 1 つ以上の UM ダイヤル プランに関連付けることができます。

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用した UM IP ゲートウェイの作成

1.  
    
    EAC で、**\[ユニファイド メッセージング\]** \> **\[UM IP ゲートウェイ\]** に移動してから、**\[新規作成\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **\[UM IP ゲートウェイの新規作成\]** ページで、以下の情報を入力します。
    
      - **\[名前\]**   このボックスを使用して、UM IP ゲートウェイの一意の名前を指定します。これは、EAC に表示される表示名です。UM IP ゲートウェイの作成後に表示名を変更する必要がある場合、最初に既存の UM IP ゲートウェイを削除し、次に希望する名前で別の UM IP ゲートウェイを作成します。UM IP ゲートウェイ名は必須ですが、表示にのみ使用されます。組織では複数の UM IP ゲートウェイを使用することがあるため、UM IP ゲートウェイにはわかりやすい名前を使用することをお勧めします。UM IP ゲートウェイ名は最大 64 文字です。スペースも使用できます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **\[アドレス\]**   IP アドレスまたは完全修飾ドメイン名 (FQDN) を使用して UM IP ゲートウェイを構成できます。このボックスを使用すると、VoIP ゲートウェイ、SIP 有効 PBX、IP PBX、SBC、または FQDN に対して構成された IP アドレスを指定できます。このボックスには、有効で正しい形式の FQDN のみ指定できます。
        
        このボックスにはアルファベットと数字を入力できます。IPv4 アドレス、IPv6 アドレス、および FQDN がサポートされています。UM IP ゲートウェイと、セキュリティで保護された SIP モードまたはセキュリティ保護されたモードで運用されているダイヤル プランの間で相互トランスポート層セキュリティ (相互 TLS) を使用するには、FQDN を使用して UM IP ゲートウェイを構成する必要があります。また、ポート 5061 で接続要求を待つように構成し、VoIP ゲートウェイまたは IP PBX もすべてポート 5061 で相互 TLS の接続要求を待つように構成されていることを確認する必要があります。UM IP ゲートウェイを構成するには、次のコマンドを実行します。`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        FQDN を使用する場合、IP アドレスについてホスト名を正しく解決できるように、VoIP ゲートウェイに対して DNS ホスト レコードを正しく構成したことも確認する必要があります。また、IP アドレスの代わりに FQDN を使用していて、かつ UM IP ゲートウェイの DNS 構成が変更される場合、UM IP ゲートウェイをいったん無効化してから有効化し、UM IP ゲートウェイの構成情報が正しく更新されていることを確認する必要があります。
    
      - **\[UM ダイヤル プラン\]**   **\[参照\]** をクリックして、UM IP ゲートウェイに関連付ける UM ダイヤル プランを選択します。UM IP ゲートウェイに関連付ける UM ダイヤル プランを選択すると、既定の UM ハント グループも作成され、選択した UM ダイヤル プランに関連付けられます。UM ダイヤル プランを選択しない場合、UM ハント グループを手動で作成し、作成した UM IP ゲートウェイとその UM ハント グループを関連付ける必要があります。

3.  
    
    **\[保存\]** をクリックします。

## シェルを使用した UM IP ゲートウェイの作成

この例では、Exchange サーバーを有効にする `MyUMIPGateway` という名前の UM IP ゲートウェイを作成して、VoIP ゲートウェイ、SIP に対して有効になった PBX、IP PBX、または IP アドレスが 10.10.10.1 の SBC からの着信の受け付けを開始します。

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

この例では、Exchange サーバーを有効にする `MyUMIPGateway` という名前の UM IP ゲートウェイを作成して、VoIP ゲートウェイ、SIP に対して有効になった PBX、IP PBX、または FQDN が MyUMIPGateway.contoso.com のポート 5061 で接続要求を待機する SBC からの着信の受け付けを開始します。

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

この例では、`MyUMIPGateway` という名前の UM IP ゲートウェイを作成し、その UM IP ゲートウェイが着信呼び出しを受け入れたり、発信呼び出しを送信したりしないようにし、IPv6 アドレスを設定して、UM IP ゲートウェイに IPv4 アドレスと IPV6 アドレスの使用を許可します。

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

