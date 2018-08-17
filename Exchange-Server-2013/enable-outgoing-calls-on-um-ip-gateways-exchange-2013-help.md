---
title: '送信呼び出しを有効にする: Exchange Online Help'
TOCTitle: 送信呼び出しを有効にする
ms:assetid: c3ad8e53-d37e-499e-b1f1-defb0ba1bd12
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673562(v=EXCHG.150)
ms:contentKeyID: 49896459
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 送信呼び出しを有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

送信呼び出しが無効になっている場合、ユニファイド メッセージング (UM) IP ゲートウェイ経由の送信呼び出しを有効にできます。UM IP ゲートウェイのプロパティで <strong>この UM IP ゲートウェイ経由の送信呼び出しを許可する</strong> オプションを選択すると、UM IP ゲートウェイが送信呼び出しを受け入れて、VoIP (Voice over IP) ゲートウェイ、セッション開始プロトコル (SIP) 対応の構内交換機 (PBX)、IP PBX、またはセッション ボーダー コントローラー (SBC) に送信するように構成されます。<strong>この UM IP ゲートウェイ経由の送信呼び出しを許可する</strong> の設定は、UM IP ゲートウェイがユーザーの送信呼び出しを開始できるかどうかを制御し、VoIP ゲートウェイ、SIP 対応 PBX、IP PBX、または SBC からの呼び出し転送または着信呼び出しには影響しません。

*アウトダイヤル*は、ある UM ダイヤル プランに属するユーザーが、別のダイヤル プランに属し、UM が有効になっているユーザー、または外部の電話番号への呼び出しを開始する状況を表すときに使用する用語です。

UM が有効になっているユーザーによるアウトダイヤルを可能にするには、次の操作を行う必要があります。

  - UM IP ゲートウェイが送信呼び出しを許可することを確認します。

  - ダイヤル情報グループを作成します。そのためには、UM IP ゲートウェイに関連付けられた UM ダイヤル プランにダイヤル情報のエントリを作成します。

  - UM ダイヤル プラン、自動応答または UM メールボックス ポリシーの <strong>ダイヤルの承認</strong> で、ダイヤルの制限についての一覧に、正しいダイヤル情報グループを追加します。

UM IP ゲートウェイに関連する追加の管理タスクについては、「[UM IP ゲートウェイ手順](um-ip-gateway-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM IP ゲートウェイ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - また、これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM IP ゲートウェイ経由の送信呼び出しを有効にする

1.  EAC で <strong>ユニファイド メッセージング</strong> \> <strong>UM IP ゲートウェイ</strong> に移動し、変更する UM IP ゲートウェイを選択してから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM IP ゲートウェイ</strong> ページで、<strong>この UM IP ゲートウェイ経由の送信呼び出しを許可する</strong> の横にあるチェック ボックスをオンにします。

3.  <strong>保存</strong> をクリックします。

## シェルを使用して UM IP ゲートウェイ経由の送信呼び出しを有効にする

この例では、`MyUMIPGateway` という UM IP ゲートウェイでの送信呼び出しを有効にします。

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $true

