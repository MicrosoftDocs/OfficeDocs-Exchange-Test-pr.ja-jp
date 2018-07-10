---
title: '個人用案内応答の制限を構成する: Exchange Online Help'
TOCTitle: 個人用案内応答の制限を構成する
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50555881
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 個人用案内応答の制限を構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

**\[個人用の案内応答の制限 (分)\]** の設定を使用して、ユニファイド メッセージング (UM) メールボックス ポリシーに関連付けられたユーザーがボイス メールの案内応答を記録するときに使用できる最大分数を入力することができます。この設定は、標準のボイス メールおよび不在時のボイス メールの両方の案内応答に適用されます。既定では、案内応答の最大時間は 5 分に設定されています。ただし、案内応答の最大時間は 1 ～ 10 分の任意の設定で構成することができます。

UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して案内応答の最大時間を変更する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、修正する UM ダイヤル プランを選択し、ツール バーで、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で、管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページ \> **\[全般\]** の **\[個人用の案内応答の制限 (分)\]** で、ボイス メール ユーザーが使用できる個人用の案内応答の時間の長さを分単位で入力します。

4.  **\[保存\]** をクリックします。

## シェルを使用して案内応答の最大時間を変更する

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` で、案内応答の最大時間を 3 分間に構成します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

