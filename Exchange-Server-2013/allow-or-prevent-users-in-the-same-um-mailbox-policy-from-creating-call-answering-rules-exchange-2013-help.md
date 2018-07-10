---
title: '同じ UM メールボックス ポリシーのユーザーによる通話応答ルールの作成を許可または禁止する: Exchange Online Help'
TOCTitle: 同じ UM メールボックス ポリシーのユーザーによる通話応答ルールの作成を許可または禁止する
ms:assetid: e44acaa6-d5a8-41e8-94aa-100be0bd6391
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351209(v=EXCHG.150)
ms:contentKeyID: 50555889
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 同じ UM メールボックス ポリシーのユーザーによる通話応答ルールの作成を許可または禁止する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーに関連付けられているユーザーによる通話応答ルールの構成を許可または禁止することができます。UM ダイヤル プランで通話応答ルールの構成オプションが無効になっている場合、UM メールボックス ポリシーに関連付けられた UM が有効であるユーザーは、通話応答ルール機能を使用できません。既定の設定は有効です。

ユーザーによる通話の転送の許可に関連するその他の管理タスクについては、「[通話転送手順](forwarding-calls-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM メールボックス ポリシーでの通話応答ルールを有効または無効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM メールボックス ポリシー\]**で、管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページで、**\[通話応答ルールの構成をユーザーに許可する\]** の隣のチェック ボックスをオンまたはオフにします。

4.  **\[保存\]** をクリックします。

## シェルを使用して UM メールボックス ポリシーでの通話応答ルールを有効または無効にする

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` に関連付けられたユーザーによる通話応答ルールの作成を許可しています。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $true

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` に関連付けられたユーザーが通話応答ルールを作成できないようにします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $false

