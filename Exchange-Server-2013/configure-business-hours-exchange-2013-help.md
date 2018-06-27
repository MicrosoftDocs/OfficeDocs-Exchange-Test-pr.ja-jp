---
title: '営業時間の構成: Exchange Online Help'
TOCTitle: 営業時間の構成
ms:assetid: 96b4be99-af94-4fa4-959a-48413387a044
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232133(v=EXCHG.150)
ms:contentKeyID: 49896380
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 営業時間の構成

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答の勤務時間を構成する場合は、組織の勤務時間である 1 日の時間帯、勤務時間内用案内応答、および自動応答で構成されている内線番号を呼び出したときに発信者に再生されるメニューの音声ガイダンスを定義します。発信者が、定義済みの勤務時間以外の時間帯に自動応答に接続された場合は、勤務時間外の音声ガイダンスと案内応答が再生されます。

いくつかの既定のスケジュール オプションが EAC で利用できます。たとえば、ほとんどの企業は、月曜日から金曜日の午前 8:00 ～午後 5.00 が勤務時間になっています。場合によっては、既定のオプションがニーズに合わず、スケジュールをカスタマイズする必要がある場合があります。勤務時間がシステムで定義されているスケジュールと異なる場合は、自動応答のカスタマイズされたスケジュールを定義できます。

UM 自動応答では、発信者が自動応答にダイヤルインする時刻にかかわらず、既定で勤務時間内の音声ガイダンスと案内応答が再生されます。


> [!NOTE]
> UM 自動応答に勤務時間内と勤務時間外のスケジュールを設定する場合は、タイム ゾーンが正しく構成されていることを確認してください。



UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM 自動応答の勤務時間を指定する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で、勤務時間を設定する UM 自動応答を選択して、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  **\[UM 自動応答\]** ページ \> **\[勤務時間\]** で、**\[勤務時間\]** の下の **\[勤務時間の構成\]** をクリックします。

4.  **\[勤務時間の構成\]** ページで、各曜日の勤務時間として使用する時間帯を選択します。

5.  **\[OK\]**、**\[保存\]** の順にクリックします。

## シェルを使用して UM 自動応答の業務時間を指定する

この例では、`MyUMAutoAttendant` という名前の UM 自動応答の勤務時間を設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30

