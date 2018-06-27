---
title: 'DTMF フォールバック自動応答の構成: Exchange Online Help'
TOCTitle: DTMF フォールバック自動応答の構成
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 49896405
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DTMF フォールバック自動応答の構成

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

デュアルトーン多重周波数 (DTMF) フォールバック自動応答に対応した、音声認識が有効なユニファイド メッセージング (UM) 自動応答を構成できます。 DTMF フォールバック自動応答は、UM 音声認識自動応答が発信者から提供された音声入力を理解または認識できないときに使用されます。 DTMF フォールバック自動応答が構成されている場合、発信者はタッチトーン入力とも呼ばれる DTMF 入力を使用して自動応答メニュー システム内を移動したり、ユーザーの名前を綴ったり、独自のメニュー音声ガイダンスを使用したりする必要があります。 DTMF フォールバック自動応答が構成されておらず、システムが発信者の発言内容を理解できないため最大音声入力数を超える場合は、システムは次のプロンプトを返します。「Sorry, I couldn't help.Please call back later.」

既定では、自動応答を作成した時点では、自動応答は音声認識に対応していません。 自動応答の音声認識を有効にすると、その後は発信者は音声コマンドのみを使用して自動応答メニュー システム内を移動でき、タッチトーン入力は使用できません。 必須ではありませんが、音声認識が有効な自動応答ごとに DTMF フォールバック自動応答を構成することをお勧めします。そうすることで、音声認識が有効な自動応答で発音した語句が認識されない場合、発信者はタッチトーン入力を使用できます。 また、DTMF フォールバック自動応答については音声認識を有効にしないことをお勧めします。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答の管理](manage-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。 詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## EMC を使用して、DTMF フォールバック自動応答を備えた音声認識が有効な自動応答を構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で、DTMF フォールバック自動応答を作成する UM 自動応答を選択します。ツール バーの **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM 自動応答\]** ページ \> **\[全般\]**で、**\[音声コマンドが正しく動作しない場合はこの自動応答を使用する\]** の横のチェック ボックスを選択し、**\[参照\]** をクリックします。

4.  **\[UM 自動応答の選択\]** ページで、DTMF フォールバック自動応答として使用する自動応答を選択し、**\[保存\]** をクリックします。


> [!IMPORTANT]
> 設定した DTMF フォールバック自動応答を参照できるようにするには、最初にその自動応答の音声認識を有効にする必要があります。



## シェルを使用して、DTMF フォールバック自動応答を備えた音声認識が有効な自動応答を設定する

この例では、`MyDTMFAA` という名前の DTMF フォールバック自動応答を使用するように、`MySpeechEnabledAA` という名前の UM 自動応答を構成します。

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

