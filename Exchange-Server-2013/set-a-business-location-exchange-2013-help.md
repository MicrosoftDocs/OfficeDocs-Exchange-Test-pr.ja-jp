---
title: 'ビジネスの場所を設定する: Exchange Online Help'
TOCTitle: ビジネスの場所を設定する
ms:assetid: 19bbc20d-d11e-4e75-9bb4-c5d85cf17fc5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423540(v=EXCHG.150)
ms:contentKeyID: 52057390
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ビジネスの場所を設定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答で勤務地を指定し、発信者のために勤務地が再生されるようにすることができます。既定では、勤務地は入力されていません。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して勤務地を構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> で、勤務地を設定する UM 自動応答を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM 自動応答</strong> ページの <strong>全般</strong> にある <strong>会社名</strong> に、会社の名前を入力します。

4.  <strong>保存</strong> をクリックします。

## シェルを使用して勤務地を構成する

この例では、`MyUMAutoAttendant` という UM 自動応答の勤務地を設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessLocation 'Redmond'

