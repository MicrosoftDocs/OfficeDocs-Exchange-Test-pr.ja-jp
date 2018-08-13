---
title: 'UM メールボックス ポリシーを削除する: Exchange Online Help'
TOCTitle: UM メールボックス ポリシーを削除する
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 50555872
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM メールボックス ポリシーを削除する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーを削除すると、その UM メールボックス ポリシーを新しく UM を使用できるようになった受信者に関連付けることができなくなります。UM が有効なメールボックスによって UM メールボックスが参照されている場合は、その UM メールボックス ポリシーを削除できません。また、UM メールボックス ポリシーが UM ダイヤル プランに関連付けられている場合は、その UM ダイヤル プランを削除できません。

UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM メールボックス ポリシーを削除する

1.  
    
    EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で、ツールバーの **\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

## シェルを使用して UM メールボックス ポリシーを削除する

この例では、`MyUMMailboxPolicy` という UM メールボックス ポリシーを削除します。

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy

