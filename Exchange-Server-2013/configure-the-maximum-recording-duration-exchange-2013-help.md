---
title: '最大録音時間の構成: Exchange Online Help'
TOCTitle: 最大録音時間の構成
ms:assetid: 18eeb567-1048-4c82-93cf-612cb12ec5e3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423539(v=EXCHG.150)
ms:contentKeyID: 49895272
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 最大録音時間の構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

発信者がボイス メール メッセージを残すとき、各音声録音に使用できる最大時間 (分単位) を指定できます。この値には 1 ～ 100 の値を設定できます。ほとんどの組織では、この値は既定の 20 分に設定してください。この値が小さすぎると、音声メッセージが終わる前に切断される可能性があります。この値が大きすぎると、ユーザーが受信トレイに長い音声メッセージを保存することになります。

ユーザーに対して厳密なディスク クォータを実装している場合、この設定は重要です。この値は、**\[最大通話時間 (分)\]** の設定値よりも低く設定する必要があります。

UM ダイヤル プランに関連するその他のタスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して最大録音時間を構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

4.  **\[最大録音時間 (分)\]** の下の**\[設定\]** で分単位で数字を入力します。

5.  **\[保存\]** をクリックします。

## シェルを使用して最大録音時間を構成する

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランの最大録音時間を 10 に設定します。

    Set-UMDialPlan -identity MyUMDialPlan -MaxRecordingDuration 10

