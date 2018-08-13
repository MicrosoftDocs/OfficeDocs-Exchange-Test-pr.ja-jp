---
title: 'UM IP ゲートウェイを削除する: Exchange Online Help'
TOCTitle: UM IP ゲートウェイを削除する
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 49896256
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM IP ゲートウェイを削除する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) IP ゲートウェイを削除すると、Exchange サーバーはそれ以降、VoIP (Voice over IP) ゲートウェイ、セッション開始プロトコル (SIP) が有効な構内交換機 (PBX)、IP PBX、または UM IP ゲートウェイに関連付けられたセッション ボーダー コントローラー (SBC) からの着信呼び出しを受け付けることができなくなります。


> [!IMPORTANT]
> VoIP ゲートウェイ、IP PBX、または SBC との通信を無効にすることによる影響を完全に理解した場合にのみ UM IP ゲートウェイを削除してください。



UM IP ゲートウェイに関連する追加のタスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM IP ゲートウェイを削除する

1.  EAC で **\[ユニファイド メッセージング\]** \> **\[UM IP ゲートウェイ\]** に移動し、削除する UM IP ゲートウェイを選択してから、**\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

2.  **\[警告\]** ページで **\[はい\]** をクリックします。

## シェルを使用して UM IP ゲートウェイを削除する

この例では、UM IP ゲートウェイ `MyUMIPGateway` を削除します。

    Remove-UMIPGateway -Identity MyUMIPGateway

