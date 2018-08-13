---
title: 'UM IP ゲートウェイを有効にする: Exchange Online Help'
TOCTitle: UM IP ゲートウェイを有効にする
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 49895304
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM IP ゲートウェイを有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

既定では、ユニファイド メッセージング (UM) IP ゲートウェイを作成すると、状態の設定は有効になります。ただし、UM IP ゲートウェイをオフラインにして着信呼び出しと送信呼び出しの受け付けを禁止するために UM IP ゲートウェイを無効にしなければならない場合もあります。UM IP ゲートウェイを作成すると、状態変数を有効または無効に設定して、その動作や機能を制御できます。

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成され、無効になっていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM IP ゲートウェイを有効にする

1.  EAC で\> **\[ユニファイド メッセージング\]** \> **\[UM IP ゲートウェイ\]** に移動し、有効にする UM IP ゲートウェイを選択し、ツール バーで**上矢印**![上矢印アイコン](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "上矢印アイコン") をクリックします。

2.  **\[警告\]** ページで **\[はい\]** をクリックします。

## シェルを使用して UM IP ゲートウェイを有効にする

この例では、`MyUMIPGateway` という名前の UM IP ゲートウェイを有効にします。

    Enable-UMIPGateway -Identity MyUMIPGateway

