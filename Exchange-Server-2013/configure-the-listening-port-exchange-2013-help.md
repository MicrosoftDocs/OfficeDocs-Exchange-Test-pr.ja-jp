---
title: 'リスニング ポートの構成: Exchange Online Help'
TOCTitle: リスニング ポートの構成
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50555744
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# リスニング ポートの構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) IP ゲートウェイでセッション開始プロトコル (SIP) 要求をリッスンするのに使用する TCP ポートを構成できます。既定では、UM IP ゲートウェイを作成する際に、TCP SIP リスニング ポート番号が 5060 に設定されます。EAC を使用して TCP SIP リスニング ポートを構成または変更することはできません。TCP SIP リスニング ポート番号は、**Set-UMIPGateway** コマンドレットを使用して構成する必要があります。

必要に応じて、TCP リスニング ポート番号を 5061 に構成することができます。

  - UM ダイヤル プランの VoIP セキュリティ設定を \[セキュリティで保護された SIP\] に設定する場合。

  - UM ダイヤル プランの VoIP セキュリティ設定を \[セキュリティで保護\] に設定する場合。

  - MicrosoftOffice Communications Server 2007 R2 または Microsoft Lync Server と統合します。

  - 相互トランスポート層セキュリティ (相互 TLS) を使用して、Exchange サーバーと VoIP ゲートウェイ、SIP が有効な構内交換機 (PBX)、IP PBX、またはセッション ボーダー コントローラー (SBC) との間でネットワーク データを暗号化します。

UM IP ゲートウェイとセキュリティ保護された SIP モードまたはセキュリティ保護されたモードで動作するダイヤル プラン間で相互 TLS を使用する場合は、UM IP ゲートウェイを作成する際に、完全修飾ドメイン名 (FQDN) を使用して構成した後にシェルを使用して UM IP ゲートウェイを TCP ポート 5061 で待機するように構成する必要があります。また、VoIP ゲートウェイ、SIP が有効な PBX、IP PBX、および SBC が相互 TLS 要求をポート 5061 で待機するように構成されていることを確認する必要もあります。


> [!IMPORTANT]
> FQDN を使用して UM IP ゲートウェイを作成している場合、DNS 正引きゾーンに適切な HOST (A) レコードを作成する必要があります。FQDN を使用して UM IP ゲートウェイを作成している場合、UM IP ゲートウェイの DNS 構成が変更されたら、UM IP ゲートウェイの構成情報が正しく更新されるようにするために、UM IP ゲートウェイを無効にしてから再度有効にする必要があります。



UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - また、この手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して TCP リスニング ポートを構成する

この例では、FQDN が mTLS.MyUMIPGateway.contoso.com の `MyUMIPGateway` という名前の UM IP ゲートウェイを構成し、TCP ポート 5061 で SIP 要求をリッスンします。

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

この例では、FQDN が SIPSecured.MyUMIPGateway.contoso.com の `MyUMIPGateway` という名前の UM IP ゲートウェイを構成し、TCP ポート 5061 で SIP 要求をリッスンします。

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

この例では、FQDN が MyOCSUMIPGateway.contoso.com の `MyUMIPGateway` という名前の UM IP ゲートウェイを構成し、TCP ポート 5061 で SIP 要求をリッスンします。

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

