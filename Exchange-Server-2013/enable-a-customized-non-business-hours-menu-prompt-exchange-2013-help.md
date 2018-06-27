---
title: 'カスタマイズされた勤務時間外メニュー プロンプトの有効化: Exchange Online Help'
TOCTitle: カスタマイズされた勤務時間外メニュー プロンプトの有効化
ms:assetid: 094c50b2-072b-4929-aaf8-f7db5b19e9b6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb266919(v=EXCHG.150)
ms:contentKeyID: 50555730
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# カスタマイズされた勤務時間外メニュー プロンプトの有効化

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

勤務時間外のユニファイド メッセージング (UM) 自動応答によって使用されるメニュー プロンプトをカスタマイズできます。UM 自動応答を作成した後、勤務時間外の案内応答の再生後に発信者に聞かせるメニュー プロンプトとして、既定のシステム プロンプト ("ユニファイド メッセージングへようこそ") が使用されます。システム プロンプトの置き換えまたは変更はできませんが、UM 自動応答で使用される案内応答およびメニューのプロンプトをカスタマイズできます。カスタマイズされた勤務時間外のメニュー プロンプト音声ファイルを作成した後、勤務時間外の UM 自動応答のメニュー ナビゲーション エントリを有効にする必要があります。

既定のシステム プロンプトの一部として組織または会社の名前を含めることのみを希望している場合は、UM 自動応答の **\[会社名\]** ボックスにその名前を入力できます。詳細については、「[会社名を入力する](enter-a-business-name-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> 自動応答の勤務時間を構成する必要があります。勤務時間を構成すると、勤務時間外が自動的に設定されます。詳細については、「<A href="configure-business-hours-exchange-2013-help.md">営業時間の構成</A>」を参照してください。



UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - メニュー プロンプトとして使用する .wav または .wma ファイルを作成します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、カスタマイズされた勤務時間外のメニュー プロンプトを有効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** の下で、カスタマイズされた勤務時間外メニュー プロンプトを有効にする UM 自動応答を選択して、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  **\[UM 自動応答\]** ページ \> **\[メニュー ナビゲーション\]** の **\[勤務時間外のメニュー ナビゲーション\]** で、**\[変更\]** をクリックしてから **\[参照\]** をクリックし、カスタマイズされた勤務時間外のメニュー プロンプト ファイルを探します。
    

    > [!IMPORTANT]
    > メニュー プロンプトに使用するファイルは .wav または .wma ファイルである必要があります。



4.  ファイルを見つけたら、**\[開く\]** をクリックし、**\[保存\]** をクリックします。

## シェルを使用して、カスタマイズされた勤務時間外のメニューのプロンプトを有効にする

この例では、`MyUMAutoAttendant` という名前の UM 自動応答を有効にします。勤務時間を 10:45 ～ 13:15 (日曜)、09:00 ～ 17:00 (月曜)、および 09:00 ～ 16:30 (土曜) に設定し、休業時間とそれに関連した案内応答を 2013 年 1 月 1 日は "`New Year`"、2013 年 4 月 24 ～ 28 日は "`Building Closed for Construction`" に設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

この例では、`MyAutoAttendant` という名前の UM 自動応答を構成します。発信者が 1 を押すと `SalesAutoAttendant` という名前の別の UM 自動応答に転送されるように、勤務時間外ナビゲーション メニューを有効にします。発信者が 2 を押すと `Support` 用の内線番号 12345 に転送され、3 を押すと音声ファイルを再生する別の UM 自動応答に転送されます。

    Set-UMAutoAttendant -Identity MyAutoAttendant - 
    AfterHoursKeyMappingEnabled $true -
    AfterHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

