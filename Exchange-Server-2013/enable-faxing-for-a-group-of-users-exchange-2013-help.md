---
title: 'ユーザー グループの FAX 送受信を有効にする: Exchange Online Help'
TOCTitle: ユーザー グループの FAX 送受信を有効にする
ms:assetid: b8d9f54d-ff06-4942-83e1-fc6c4ad02178
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423556(v=EXCHG.150)
ms:contentKeyID: 52057512
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザー グループの FAX 送受信を有効にする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーに関連付けられているユーザーに対して、着信 FAX を有効にすることができます。既定では、ユニファイド メッセージングを有効にしただけではユーザーは FAX を受信できません。受信できるようにするには、FAX パートナー サーバーの URI を指定して組織の FAX パートナー サーバーを展開し、UM メールボックス ポリシーで FAX を有効にする必要があります。着信 FAX を許可するオプションが UM ダイヤル プランで無効になっている場合、UM メールボックス ポリシーに関連付けられたユーザーは FAX を受信できません。同様に、着信 FAX を許可するオプションが個々のユーザーで無効になっている場合もユーザーは FAX を受信できません。

FAX パートナーの詳細は、「[Microsoft PinPoint の FAX パートナー](https://go.microsoft.com/fwlink/?linkid=190238)」を参照してください。

FAX に関するその他の管理タスクについては、「[FAX 送受信の手順](faxing-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して着信 FAX を有効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで変更したい UM ダイアル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン").

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で、変更する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページの **\[全般\]** で、**\[着信 FAX を許可する\]** の横にあるチェック ボックスをオンにします。

4.  **\[保存\]** をクリックして変更を保存します。

## シェルを使用して着信 FAX を有効にする

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` に関連付けられているユーザーに着信 FAX を許可します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $true

