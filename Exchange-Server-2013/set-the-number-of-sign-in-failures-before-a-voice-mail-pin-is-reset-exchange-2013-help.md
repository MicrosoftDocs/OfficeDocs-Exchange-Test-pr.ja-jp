---
title: 'ボイス メール PIN がリセットされるまでのサインイン失敗回数を設定する: Exchange Online Help'
TOCTitle: ボイス メール PIN がリセットされるまでのサインイン失敗回数を設定する
ms:assetid: 4de38499-0a6f-4f00-8697-eeff805d7266
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997939(v=EXCHG.150)
ms:contentKeyID: 50555775
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メール PIN がリセットされるまでのサインイン失敗回数を設定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access ユーザーの PIN をリセットするまでに許容されるサインイン失敗回数は、1 ～ 998 の値の範囲で構成できます。既定は 5 です。PIN をリセットするまでに許容されるサインイン失敗回数は、ユニファイド メッセージング (UM) メールボックス ポリシーで構成され、その UM メールボックス ポリシーに関連付けられているすべての Outlook Voice Access ユーザーに適用されます。


> [!NOTE]
> <STRONG>[PIN がリセットされるサインインの失敗回数]</STRONG> 設定を 5 未満に構成することによって、セキュリティを強化できます。5 よりも大きい数に構成するとセキュリティが低下します。



Outlook Voice Access の PIN セキュリティに関連するその他のタスクについては、「[PIN セキュリティ手順](pin-security-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して PIN をリセットするまでのサインイン失敗回数を構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** 下で変更したい UM メールボックス ポリシーを選択してから、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  **\[PIN ポリシー\]** をクリックし、**\[PIN がリセットされるサインインの失敗回数\]** に 0 ～ 999 の値を入力します。

5.  **\[保存\]** をクリックします。

## シェルを使用して PIN をリセットするまでのサインイン失敗回数を構成する

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられている UM が有効なユーザーの PIN がリセットされるサインイン失敗回数を 3 に設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられた UM が有効なユーザーの場合、ユーザーの PIN をリセットするまでに許容されるサインイン失敗回数を 3、サインインの最大試行回数を 5、PIN の最小の長さを 9 に設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MaxLogonAttempts 5 -MinPINLength 9

