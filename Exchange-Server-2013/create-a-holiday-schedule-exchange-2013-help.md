---
title: '祝日のスケジュールの作成: Exchange Online Help'
TOCTitle: 祝日のスケジュールの作成
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 49895236
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 祝日のスケジュールの作成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

祝日やその他の行事のために組織が休業する日付と時刻を定義できます。指定した開始日から終了日までの期間、ユニファイド メッセージング (UM) 自動応答に接続された発信者には、祝日のスケジュールを構成したときに指定した祝日の案内応答が再生されます。指定した祝日の案内応答が再生された後、勤務時間外の案内応答とメニュー プロンプトが発信者のために再生されます。

また、既存の祝日のスケジュール内に別の祝日のスケジュールを作成することもできます。祝日のスケジュールを複数作成する場合、ユニファイド メッセージングではスケジュールされた休業時間を重ねることができます。たとえば、工事のために組織が休業する期間の 12 月 15 ～ 31 日に祝日のスケジュールを定義し、それとは別に 12 月 24 ～ 26 日に祝日のスケジュールを定義できます。発信者が 12 月 15 ～ 23 日および 12 月 27 ～ 31 日の期間に自動応答に接続された場合は、この特定のスケジュールに対して指定した祝日の案内応答が再生されます。たとえば、"工事のために現在休業中です" と再生されます。発信者が 12 月 24 ～ 26 日の期間に自動応答に接続された場合は、別の祝日の案内応答、たとえば "従業員が祝日を家族と共に過ごせるように現在休業中です" と再生されます。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM 自動応答の祝日のスケジュールを指定する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択してから、ツール バーで <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページで、<strong>UM 自動応答</strong> の下から祝日スケジュールを設定する UM 自動応答を選択します。ツール バーの <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM 自動応答</strong> ページ \> <strong>勤務時間</strong> で、<strong>祝日のスケジュール</strong> の下から <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  <strong>祝日の新規作成</strong> ページで、次の項目を構成します。
    
      - <strong>名前</strong>   祝日のスケジュールに名前を入力します。
    
      - <strong>祝日の案内応答</strong>   案内応答として使用する .wav ファイルを指定します。これは必須フィールドです。
    
      - <strong>開始日</strong>   この一覧を使用して、祝日を開始する日付を選択します。祝日のスケジュールは、この一覧で指定した日付の午前 0 時から開始されます。
    
      - <strong>終了日</strong>   この一覧を使用して、祝日を終了する日付を選択します。祝日のスケジュールは、この一覧で指定した日付の午後 11 時 59 分に終了します。

5.  祝日のスケジュールを構成したら、<strong>OK</strong> をクリックしてから <strong>保存</strong> をクリックします。

## シェルを使用して UM 自動応答の祝日のスケジュールを指定する

この例では、`MyUMAutoAttendant` という名前の UM 自動応答を構成します。勤務時間を 10:45 ～ 13:15 (日曜)、09:00 ～ 17:00 (月曜)、および 09:00 ～ 16:30 (土曜) に設定し、休業時間とそれに関連した案内応答を 2013 年 1 月 2 日は「新年明けましておめでとうございます」、2013 年 4 月 24 ～ 28 日は「工事のため閉鎖中です」に設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

