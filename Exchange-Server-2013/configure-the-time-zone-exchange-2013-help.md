---
title: 'タイム ゾーンの構成: Exchange Online Help'
TOCTitle: タイム ゾーンの構成
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50555750
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# タイム ゾーンの構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

既定では、ユニファイド メッセージング (UM) 自動応答は作成されたメールボックス サーバーのタイム ゾーンを使用します。ただし、UM 自動応答のタイム ゾーンを別のタイム ゾーンに変更する必要がある場合があります。たとえば、2 つの UM ダイヤル プランがあり、各ダイヤル プランが異なるタイム ゾーンを表している場合、片方の UM 自動応答はメールボックス サーバーとタイム ゾーンが同じになるよう構成し、もう片方の UM 自動応答はメールボックス サーバーとはタイム ゾーンが異なるように構成する必要があります。

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

## EAC を使用してタイム ゾーンを構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> で、タイム ゾーンを設定する UM 自動応答を選択して、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

3.  <strong>UM 自動応答</strong> ページで <strong>勤務時間</strong> をクリックした後に、<strong>タイム ゾーン</strong> でドロップダウン リストからタイム ゾーンを選択します。

4.  変更内容を保存するには、<strong>OK</strong> をクリックしてから <strong>保存</strong> をクリックします。

## シェルを使用してタイム ゾーンを構成する

この例では、タイム ゾーンを `MyUMAutoAttendant` という名前の UM 自動応答の太平洋タイム ゾーンに設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific

