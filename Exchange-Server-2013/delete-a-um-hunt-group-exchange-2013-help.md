---
title: 'UM ハント グループを削除する: Exchange Online Help'
TOCTitle: UM ハント グループを削除する
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50555732
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM ハント グループを削除する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ハント グループを削除すると、UM ハント グループに関連付けられていた UM IP ゲートウェイは着信呼び出しへサービスの提供や応答を停止します。UM ハント グループの削除によって、構成済みのハント グループが存在しない状態で UM IP ゲートウェイが残された場合、UM IP ゲートウェイは UM 呼び出しを処理できなくなります。

UM ハント グループに関連するその他のタスクについては、「[UM ハント グループ手順](um-hunt-group-procedures-exchange-2013-help.md)」を参照してください。


> [!WARNING]
> UM ハント グループの設定を変更する必要がある場合は、そのハント グループを削除して、適切な設定を持つ別のハント グループを作成する必要があります。



## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ハント グループ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM ハント グループが作成されていることを確認してください。詳細な手順については、「[UM ハント グループを作成する](create-a-um-hunt-group-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM ハント グループを削除する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランをクリックし、ツール バーで **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM ハント グループ\]** で、削除するハント グループを選択し、ツール バーの **\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

3.  **\[警告\]** ページで **\[はい\]** をクリックします。

## シェルを使用して UM ハント グループを削除する

この例では、`MyUMHuntGroup` という名前の UM ハント グループを削除します。

    Remove-UMHuntGroup -identity MyUMHuntGroup

