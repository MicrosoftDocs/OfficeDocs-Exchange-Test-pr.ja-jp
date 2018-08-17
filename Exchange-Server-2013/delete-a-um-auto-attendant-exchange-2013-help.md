---
title: 'UM 自動応答を削除する: Exchange Online Help'
TOCTitle: UM 自動応答を削除する
ms:assetid: 92846bbc-e6b9-45fc-8702-ef5c92eeb08f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123780(v=EXCHG.150)
ms:contentKeyID: 49896372
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 自動応答を削除する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答を削除した後は、UM 自動応答によって応答していた着信呼び出しにオペレーターが応答する必要があります。 UM 自動応答は、既定の UM 自動応答として UM ダイヤル プランと関連付けられている場合は削除できません。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答の管理](manage-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。 詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## EAC を使用して UM 自動応答を削除する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。 リスト ビューで、編集する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> で、削除する UM 自動応答を選択します。ツール バーの <strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。<strong>警告</strong> ページで <strong>はい</strong> をクリックします。

## シェルを使用して UM 自動応答を削除する

この例を実行すると、`MyUMAutoAttendant` という名前の UM 自動応答が削除されます。

    Remove-UMAutoAttendant -Identity MyUMAutoAttendant

