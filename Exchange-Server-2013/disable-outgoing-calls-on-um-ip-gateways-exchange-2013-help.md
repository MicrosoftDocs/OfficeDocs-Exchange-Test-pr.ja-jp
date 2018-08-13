---
title: 'UM IP ゲートウェイで送信呼び出しを無効にする: Exchange Online Help'
TOCTitle: UM IP ゲートウェイで送信呼び出しを無効にする
ms:assetid: a3777cc6-37e4-4359-ada3-a962ac0ef0c3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232153(v=EXCHG.150)
ms:contentKeyID: 49896393
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM IP ゲートウェイで送信呼び出しを無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) IP ゲートウェイ経由の送信呼び出しを有効または無効にできます。UM IP ゲートウェイのプロパティで **\[この UM IP ゲートウェイ経由の送信呼び出しを許可する\]** チェック ボックスをオフにすると、送信呼び出しを受け入れず、Voice over IP (VoIP) ゲートウェイ、IP PBX、またはセッション ボーダー コントローラー (SBC) に送信しないように UM IP ゲートウェイが構成されます。**\[この UM IP ゲートウェイ経由の送信呼び出しを許可する\]** の設定は、UM IP ゲートウェイがユーザーの送信呼び出しを開始できるかどうかを制御しますが、VoIP ゲートウェイ、IP PBX、または SBC からの呼び出し転送または着信呼び出しには影響しません。

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM IP ゲートウェイ経由の送信呼び出しを無効にする

1.  EAC で **\[ユニファイド メッセージング\]** \> **\[UM IP ゲートウェイ\]** に移動し、変更する UM IP ゲートウェイを選択してから、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM IP ゲートウェイ\]** ページで、**\[この UM IP ゲートウェイ経由の送信呼び出しを許可する\]** の横にあるチェック ボックスをオフにします。

3.  **\[保存\]** をクリックします。

## シェルを使用して UM IP ゲートウェイ経由の送信呼び出しを無効にする

この例では、UM IP ゲートウェイ `MyUMIPGateway` での送信呼び出しを無効にします。

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $false

