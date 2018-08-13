---
title: '自動音声認識を有効または無効にする: Exchange Online Help'
TOCTitle: 自動音声認識を有効または無効にする
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 52057462
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動音声認識を有効または無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答の自動音声認識 (ASR) を有効にすることができます。UM 自動応答の音声認識を有効にすると、発信者が自動応答用の音声ガイダンスに言葉で応答し、自動応答のメニュー システム内を移動できるようになります。既定では、自動応答を作成した時点では、自動応答は音声認識に対応していません。自動応答の音声認識を有効にすると、その後は発信者は音声コマンドのみを使用して自動応答メニュー システム内を移動でき、タッチトーン入力は使用できません。

必須ではありませんが、音声認識が有効な自動応答によって言葉が認識または理解されない場合に発信者がタッチトーン入力を使用できるように、音声認識が有効な自動応答ごとにデュアル トーン多重周波数 (DTMF) フォールバック自動応答を構成することをお勧めします。DTMF フォールバック自動応答が構成されている場合、発信者は DTMF 入力 (タッチトーン入力とも呼ばれます) を使用して、自動応答のメニュー システム内を移動したり、ユーザーの名前を綴ったり、独自のメニュー音声ガイダンスを使用したりすることができます。DTMF フォールバック自動応答については音声認識を有効にしないことをお勧めします。

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

## EAC を使用して UM 自動応答の音声認識を有効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で音声認識を有効にする UM 自動応答を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM 自動応答\]** ページの **\[全般\]** で、**\[自動応答を設定して音声コマンドに応答する\]** の横にあるチェック ボックスをオンにし、音声認識を有効にします。自動音声認識を無効にするには、このチェック ボックスをオフにします。

4.  **\[保存\]** をクリックします。

## シェルを使用して UM 自動応答の音声認識を有効にする

この例では、`MySpeechEnabled AA` という名前の UM 自動応答の ASR を有効にします。

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true

