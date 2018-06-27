---
title: 'IP アドレスの構成: Exchange Online Help'
TOCTitle: IP アドレスの構成
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 49895251
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IP アドレスの構成

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) IP ゲートウェイを作成する前に、使用している VoIP ゲートウェイ、IP PBX、またはセッション ボーダー コントローラー (SBC) 上に IP アドレスまたは完全修飾ドメイン名 (FQDN) をまず設定する必要があります。続いて、UM IP ゲートウェイを作成するときに、IP アドレスまたは FQDN を設定します。IP アドレスまたは FQDN は後で変更できます。

EAC またはシェルのいずれかを使用して、IP アドレスまたは FQDN を構成できます。EAC で、**\[UM IP ゲートウェイ\]** ページの **\[アドレス\]** ボックスに IPv4 IP アドレス、IPv6 アドレス、または FQDN を入力できます。シェル内の **Set-UMIPGateway** コマンドレットで *Address* パラメーターを使用して、IPv4 IP アドレス、IPv6 アドレス、または FQDN を設定することもできます。FQDN を使用して UM IP ゲートウェイを作成する場合、DNS 前方参照ゾーンに適切な HOST A レコードを作成する必要があります。UM IP ゲートウェイの DNS 構成が変更される場合、UM IP ゲートウェイをいったん無効化してから有効化し、構成情報が正しく更新されていることを確認する必要があります。

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM IP ゲートウェイで IP アドレスを構成する

1.  EAC で **\[ユニファイド メッセージング\]** \> **\[UM IP ゲートウェイ\]** に移動し、変更する UM IP ゲートウェイを選択してから、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM IP ゲートウェイ\]** ページで、**\[アドレス\]** ボックスに VoIP ゲートウェイ、IP PBX、またはセッション ボーダー コントローラー (SBC) の IP アドレスを入力します。

3.  **\[保存\]** をクリックして変更を保存します。


> [!IMPORTANT]
> UM IP ゲートウェイで IP アドレスではなく FQDN を使用する場合は、DNS レコードが正しく作成されていることを確認してください。



## シェルを使用して UM IP ゲートウェイで IP アドレスを構成する

この例では、10.10.10.1 の IP アドレスを使用して `MyUMIPGateway` という名前の UM IP ゲートウェイを構成します。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

この例では、10.10.10.10 の IP アドレスを使用して `MyUMIPGateway` という名前の UM IP ゲートウェイを構成し、TCP ポート 5061 で SIP 要求をリッスンします。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

この例では、`MyUMIPGateway` という UM IP ゲートウェイが着信および発信することを禁止し、IPv6 アドレスを設定し、この UM IP ゲートウェイで IPv4 および IPV6 アドレスを使用することを許可します。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

