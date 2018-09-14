---
title: 'UM ハント グループの表示: Exchange Online Help'
TOCTitle: UM ハント グループの表示
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50555892
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM ハント グループの表示

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ハント グループのプロパティを表示する場合は、単一の UM ハント グループに関連付けられているプロパティ、または単一の UM IP ゲートウェイに関連付けられているすべての UM ハント グループに関連付けられているプロパティを表示できます。いずれのパラメーターも指定されていない場合は、すべての UM ハント グループが返されます。EAC を使用して、UM ハント グループのプロパティを表示することはできません。シェルを使用する必要があります。

UM ハント グループを作成した後に、構成された設定を変更することはできません。UM ハント グループのパイロット ID などの構成設定を変更する場合は、既存の UM ハント グループを削除し、正しく設定された新しい UM ハント グループを作成する必要があります。

UM ハント グループに関連する追加のタスクについては、「[UM ハント グループ手順](um-hunt-group-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ハント グループ」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - また、この手順を実行する前に、UM ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)」を参照してください。

  - また、この手順を実行する前に、UM ハント グループが作成されていることを確認してください。詳細な手順については、「[UM ハント グループを作成する](create-a-um-hunt-group-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して UM ハント グループのプロパティを表示する

この例では、Active Directory フォレスト内のすべての UM ハント グループを表示しています。

    Get-UMHuntGroup

この例では、`MyUMHuntGroup` という名前の UM ハント グループの詳細を書式化された一覧で表示しています。

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List


> [!NOTE]
> <STRONG>Get-UMHuntGroup</STRONG> コマンドレットを使用している場合、UM ハント グループの名前だけを入力することはできません。UM ハント グループに関連付けられた UM IP ゲートウェイの名前も含める必要があります。


