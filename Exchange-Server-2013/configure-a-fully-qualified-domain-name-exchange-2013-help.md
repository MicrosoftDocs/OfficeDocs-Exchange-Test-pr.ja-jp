---
title: '完全修飾ドメイン名の構成: Exchange Online Help'
TOCTitle: 完全修飾ドメイン名の構成
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 49896418
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 完全修飾ドメイン名の構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

IP アドレスまたは全修飾ドメイン名 (FQDN) を使用してユニファイド メッセージング（UM）IP ゲートウェイを構成できます。UM IP ゲートウェイを作成する場合は、使用している VoIP ゲートウェイ、IP PBX 、またはセッション ボーダー コントローラー (SBC) で構成されている IP アドレスまたは FQDN を定義する必要があります。IP アドレスまたは FQDN は UM IP ゲートウェイの作成後に変更することができます。

FQDN を使用して UM IP ゲートウェイを作成している場合、DNS 正引きゾーンに適切な HOST (A) レコードを作成する必要があります。FQDN を使用して UM IP ゲートウェイを作成している場合、UM IP ゲートウェイの DNS 構成が変更されたら、そのゲートウェイの構成情報が正しく更新されるようにするために、UM IP ゲートウェイを無効にしてから再度有効にする必要があります。

UM IP ゲートウェイと、セキュリティで保護された SIP モードまたはセキュリティ保護されたモードで運用されているダイヤル プランの間で相互トランスポート層セキュリティ (相互 TLS) を使用するには、FQDN を使用して UM IP ゲートウェイを構成する必要があります。また、ポート 5061 で接続要求を待つように構成し、VoIP ゲートウェイ、 IP PBX、または SBC もすべてポート 5061 で相互 TLS の接続要求を待つように構成されていることを確認する必要があります。UM IP ゲートウェイを構成するには、次のコマンドを実行します。`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して FQDN を構成する

1.  EAC で <strong>ユニファイド メッセージング</strong> \> <strong>UM IP ゲートウェイ</strong> に移動し、変更する UM IP ゲートウェイを選択してから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM IP ゲートウェイ</strong> ページの<strong>アドレス</strong> で、VoIP ゲートウェイ、SIP 有効化された PBX、IP PBX 、または SBC のいずれかの FQDN を入力します。

3.  <strong>保存</strong> をクリックします。


> [!IMPORTANT]
> UM IP ゲートウェイで IP アドレスではなく FQDN を使用する場合は、DNS レコードが正しく作成されていることを確認してください。



## シェルを使用して FQDN を構成する

この例では、voipgateway.contoso.com という FQDN を使用して `MyUMIPGateway` という名前の UM IP ゲートウェイを構成します。

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

この例では、sbc.contoso.com の FQDN を使用して `MySBC` という名前の UM IP ゲートウェイを構成し、TCP ポート 5061 で SIP 要求を待ちます。

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

