---
title: 'UM IP ゲートウェイを無効にする: Exchange Online Help'
TOCTitle: UM IP ゲートウェイを無効にする
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 49896570
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM IP ゲートウェイを無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

既定では、ユニファイド メッセージング (UM) IP ゲートウェイを作成すると、UM IP ゲートウェイの状態は有効に設定されます。UM IP ゲートウェイを作成した後で、状態を無効に設定することにより、ゲートウェイの操作を無効にできます。UM IP ゲートウェイを無効にした後、ゲートウェイが使用するように構成された VoIP (Voice over IP) ゲートウェイ、IP 構内交換機 (PBX)、またはセッション ボーダー コントローラー (SBC) は、ユニファイド メッセージング着信呼び出しを処理しなくなります。

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成され、有効になっていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」および「[UM IP ゲートウェイを有効にする](enable-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM IP ゲートウェイを無効にする

1.  EAC で **\[ユニファイド メッセージング\]** \> **\[UM IP ゲートウェイ\]** の順にクリックし、無効にする UM IP ゲートウェイを選択してから、**下方向キー**![下矢印アイコン](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "下矢印アイコン")をクリックします。

2.  **\[警告\]** ページで **\[はい\]** をクリックします。

## シェルを使用して UM IP ゲートウェイを無効にする

この例では、`MyUMIPGateway` という名前の UM IP ゲートウェイを無効にして、VoIP ゲートウェイ、IP PBX、または SBC からの着信呼び出しの受付を停止しています。

    Disable-UMIPGateway -Identity MyUMIPGateway

この例では、`MyUMIPGateway` という名前の UM IP ゲートウェイを無効にして、現在の呼び出しすべてを直ちに切断しています。

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true

