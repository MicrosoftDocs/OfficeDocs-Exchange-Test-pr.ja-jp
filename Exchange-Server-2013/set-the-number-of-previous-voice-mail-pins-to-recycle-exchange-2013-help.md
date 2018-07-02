---
title: 'リサイクルするまでに使う必要があるボイス メール PIN の数を設定する: Exchange Online Help'
TOCTitle: リサイクルするまでに使う必要があるボイス メール PIN の数を設定する
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50555848
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# リサイクルするまでに使う必要があるボイス メール PIN の数を設定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access ユーザーが Outlook Voice Access 番号にダイヤルすると、ボイス メール システムによるユーザー認証のための PIN の入力を求められます。認証されると、ユーザーはどの電話からでもメールボックス内のボイス メール、電子メール、予定表、および個人用連絡先情報にアクセスできます。

いくつかの PIN に関連した設定は、ユニファイド メッセージング (UM) メールボックス ポリシーで構成できます。**\[PIN リサイクル カウント\]** 設定では、ユーザーが古い PIN を再使用する前に使用する必要がある一意の PIN の数を設定します。この設定には 1 ～ 20 の値を指定できます。大部分の組織では、この値は既定の 5 PIN に設定してください。この値が大きすぎると、多くの PIN を作成し記憶することが難しいため、ユーザーに不満が生じる可能性があります。この値が小さすぎると、ネットワーク セキュリティの脅威を招く可能性があります。


> [!IMPORTANT]
> PIN リサイクル カウントは無効にできません。



Outlook Voice Access の PIN セキュリティに関連するその他のタスクについては、「[PIN セキュリティ手順](pin-security-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して PIN リサイクル カウントを変更する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、変更するダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で、変更する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  **\[PIN ポリシー\]** をクリックし、**\[PIN リサイクル カウント\]** の横に 1 ～ 20 の値を入力します。

5.  **\[保存\]** をクリックします。

## シェルを使用して PIN リサイクル カウントを変更する

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` の PIN リサイクル カウントを 10 に設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

