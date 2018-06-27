---
title: '情報アナウンスの有効化: Exchange Online Help'
TOCTitle: 情報アナウンスの有効化
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50555724
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 情報アナウンスの有効化

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答の情報アナウンスを有効にできます。情報アナウンスが有効になっている場合は、勤務時間内または勤務時間外の案内応答の直後に再生されます。既定では、情報アナウンスは構成されていません。情報アナウンスを有効にするには、情報アナウンスとして使用する .wav または .wma ファイルを作成し、このサウンド ファイルを使用するように自動応答を構成します。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - 情報アナウンスとして使用する .wav または .wma ファイルを作成します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して情報アナウンスを有効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** の下で、情報アナウンスを有効にする UM 自動応答を選択して、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  **\[UM 自動応答\]** ページ \> **\[案内応答\]** の **\[情報アナウンス\]** の下で、**\[変更\]** をクリックしてから **\[参照\]** をクリックし、この手順を開始する前に作成した情報アナウンス ファイルを探します。
    

    > [!IMPORTANT]
    > 案内応答に使用するファイルは .wav または .wma ファイルである必要があります。



4.  ファイルを見つけたら、**\[開く\]** をクリックし、**\[保存\]** をクリックします。

## シェルを使用して情報アナウンスを有効にする

この例では、`MyUMAutoAttendant` という名前の UM 自動応答の `MyInfoAnnouncement.wav` ファイルを使用している情報アナウンスを有効にします。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

