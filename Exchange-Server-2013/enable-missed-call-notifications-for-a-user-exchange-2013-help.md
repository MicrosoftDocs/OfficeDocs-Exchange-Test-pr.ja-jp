---
title: 'ユーザーの不在着信通知を有効にする: Exchange Online Help'
TOCTitle: ユーザーの不在着信通知を有効にする
ms:assetid: aa0cbb60-5422-474f-af16-621aade31c1f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232159(v=EXCHG.150)
ms:contentKeyID: 52057488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーの不在着信通知を有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

シェルまたは EAC を使用して、ユニファイド メッセージング (UM) メールボックス ポリシーで不在着信通知を有効または無効にすることができます。不在着信通知とは、ユーザーが着信呼び出しに応答せず、発信者が音声メッセージを残さなかった場合にユーザーに送信される電子メール メッセージです。この電子メール メッセージは、ユーザーに残される音声メッセージを含むメッセージとは異なります。

UM メールボックス ポリシーで不在着信通知を無効にすると、その UM メールボックス ポリシーに関連付けられたユーザーが着信呼び出しに応答せず、発信者が音声メッセージを残さなかった場合、こうしたユーザーはすべて、電子メール メッセージを受信できなくなります。既定では、作成する各 UM メールボックス ポリシーで不在着信通知が有効になります。同じく既定では、UM ダイヤル プランを作成するたびに UM メールボックス ポリシーが作成されます。


> [!NOTE]
> ユニファイド メッセージングと Microsoft Lync Server を統合した場合、Exchange 2007 または Exchange 2010 メールボックス サーバーに配置されたメールボックスを持つユーザーは、Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーに送信される前に通話を切断すると、不在着信通知を使用できません。



UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシーの管理](manage-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM メールボックス ポリシーでの不在着信通知を有効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページの **\[全般\]** で、**\[不在着信通知を許可する\]** の横にあるチェック ボックスをオンにします。

4.  **\[保存\]** をクリックします。

## シェルを使用して UM メールボックス ポリシーでの不在着信通知を有効にする

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーでの不在着信通知を有効にします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $true

