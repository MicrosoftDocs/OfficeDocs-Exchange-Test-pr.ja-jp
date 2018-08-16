---
title: 'UM ダイヤル プランを削除する: Exchange Online Help'
TOCTitle: UM ダイヤル プランを削除する
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 49896474
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM ダイヤル プランを削除する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

既存のユニファイド メッセージング (UM) ダイヤル プランを削除できます。UM ダイヤル プランを削除すると、UM IP ゲートウェイ、UM メールボックス ポリシー、および UM ハント グループに使用できなくなります。UM メールボックス ポリシー、UM 自動応答、UM IP ゲートウェイ、または UM ハント グループに参照されている、もしくは関連付けられた UM ダイヤル プランは削除できません。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して既存のダイヤル プランを削除する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、削除する UM ダイヤル プランを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  警告ページで <strong>はい</strong> をクリックします。

## シェルを使用して既存のダイヤル プランを削除する

この例では、`MyUMDialPlan` という UM ダイヤル プランを削除します。

    RemoveUMDialplan -identity MyUMDialPlan

