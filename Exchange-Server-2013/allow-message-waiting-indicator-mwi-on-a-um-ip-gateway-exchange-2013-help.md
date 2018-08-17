---
title: 'UM IP ゲートウェイ上でメッセージ待機インジケーター (MWI) を許可する: Exchange Online Help'
TOCTitle: UM IP ゲートウェイ上でメッセージ待機インジケーター (MWI) を許可する
ms:assetid: 5667e37c-48c6-4659-9dc9-94b1dd8ba232
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd297995(v=EXCHG.150)
ms:contentKeyID: 49896259
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM IP ゲートウェイ上でメッセージ待機インジケーター (MWI) を許可する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) IP ゲートウェイで受信する通話に対し、ユーザーへのボイス メール通知を許可または禁止できます。この設定を有効にすると、UM IP ゲートウェイでユーザーへの SIP NOTIFY メッセージを送受信できます。メッセージ待機インジケーター (MWI) は既定で有効になっており、メッセージ待機通知をユーザーに送信できます。ただし、必要に応じてオフにすることもできます。

メッセージ待機インジケーターは、新規または未確認の音声メッセージについてユーザーに通知します。Outlook や Outlook Web App といったクライアントの受信トレイに表示されます。メッセージ待機インジケーターでは、登録済み携帯電話へのテキスト (SMS) メッセージの送信、新規メッセージを再生するように構成された番号への Exchange サーバーからの発信通話、またはユーザー卓上電話機のランプの点灯を利用することもできます。


> [!TIP]
> MWI 通知は、ユーザーのグループに対して UM メールボックス ポリシーで有効および無効にすることもできます。



UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、メッセージ待機インジケーターを許可する

1.  EAC で <strong>ユニファイド メッセージング</strong> \> <strong>UM IP ゲートウェイ</strong> に移動し、変更する UM IP ゲートウェイを選択してから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM IP ゲートウェイ</strong> ページで、<strong>メッセージ待機インジケーターを許可する</strong> の隣のチェック ボックスをオンにします。

3.  <strong>保存</strong> をクリックします。

## シェルを使用して、メッセージ待機インジケーターを許可する

この例では、IP アドレスが 10.10.10.1 の `MyUMIPGateway` という名前の UM IP ゲートウェイに関連付けられたユーザーに対してメッセージ待機インジケーターの表示を許可します。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $true

