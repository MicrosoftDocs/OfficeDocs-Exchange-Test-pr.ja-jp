---
title: 'カスタマイズされた勤務時間案内応答を有効にする: Exchange Online Help'
TOCTitle: カスタマイズされた勤務時間案内応答を有効にする
ms:assetid: a2272b7d-de88-4d3f-81e6-ad81f0ee6c5e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232152(v=EXCHG.150)
ms:contentKeyID: 50555839
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# カスタマイズされた勤務時間案内応答を有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答でのカスタマイズした勤務時間の案内応答を有効にできます。勤務時間の案内応答は、UM 自動応答が勤務時間内の呼び出しに応答するときに、発信者が最初に耳にするものです。この案内応答には、カスタマイズが必要になるでしょう。

ユニファイド メッセージングには、勤務時間内に使用するための既定のシステム プロンプトが含まれています。既定のシステム プロンプトを置換または変更することはできませんが、カスタマイズした案内応答を用意することができます。.wav ファイル形式または .wma ファイル形式のカスタマイズした案内応答を作成し、発信者が勤務時間内に UM 自動応答に電話を掛けてきたときに使用できます。たとえば、"こちらは Woodgrove Bank です" などです。

既定の案内応答の一部として組織または会社の名前を含める場合は、UM 自動応答の <strong>会社名</strong> ボックスにその名前を入力できます。詳細については、「[会社名を入力する](enter-a-business-name-exchange-2013-help.md)」を参照してください。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - 案内応答に使用する .wav ファイルまたは .wma ファイルを作成します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、カスタマイズした勤務時間の案内応答を有効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> で、カスタマイズした勤務時間の案内応答を有効にする UM 自動応答を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  <strong>UM 自動応答</strong> ページ \> <strong>案内応答</strong> の <strong>勤務時間の案内応答</strong> で <strong>変更</strong> をクリックし、<strong>参照</strong> をクリックして、この手順を開始する前に作成した、カスタマイズした勤務時間の案内応答ファイルを特定します。
    

    > [!IMPORTANT]
    > 案内応答として使用するファイルは, .wav ファイルまたは .wma ファイルである必要があります。



4.  ファイルを特定した後に <strong>開く</strong> をクリックし、<strong>保存</strong> をクリックします。

## シェルを使用して、カスタマイズした勤務時間の案内応答を有効にする

この例では、UM 自動応答 `GreetingFile.wav` に対して `MyUMAutoAttendant` というカスタマイズした案内応答を使用する勤務時間の案内応答を有効にします。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursWelcomeGreetingEnabled $true -BusinessHoursWelcomeGreetingFilename GreetingFile.wav

この例では、`MyUMAutoAttendant` という名前の UM 自動応答を構成します。勤務時間を 10:45 ～ 13:15 (日曜)、09:00 ～ 17:00 (月曜)、および 09:00 ～ 16:30 (土曜) に設定し、休業時間とそれに関連した案内応答を 2013 年 1 月 2 日は "`New Year`"、2013 年 4 月 24 ～ 28 日は "`Building Closed for Construction`" に設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

この例では、`MyAutoAttendant` という名前の UM 自動応答を構成します。発信者が 1 を押すと `SalesAutoAttendant` という名前の別の UM 自動応答に転送されるように、勤務時間キー マッピングを有効にします。発信者が 2 を押すと `Support`用内線番号 12345 に転送され、3 を押すと音声ファイルを再生する別の自動応答に転送されます。

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

