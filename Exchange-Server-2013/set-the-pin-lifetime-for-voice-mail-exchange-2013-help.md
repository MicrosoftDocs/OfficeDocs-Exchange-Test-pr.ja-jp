---
title: 'ボイス メールの PIN の有効期限を設定する: Exchange Online Help'
TOCTitle: ボイス メールの PIN の有効期限を設定する
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50555877
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メールの PIN の有効期限を設定する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) が有効なユーザーに対して、PIN の有効期限を構成することができます。PIN の有効期限とは、UM が有効な受信者の Outlook Voice Access PIN が有効な期間の最大値です。PIN の有効期限の設定は、UM メールボックス ポリシーで構成され、UM メールボックス ポリシーに関連付けられているすべての UM が有効なユーザーに適用されます。

いくつかの PIN に関連した設定は、UM メールボックス ポリシーで構成できます。PIN の有効期限の設定は、Outlook Voice Access ユーザーが最後に PIN を変更した日付から次に PIN の変更を要求される日付までの日数を制御します。指定できる範囲は 0 ～ 999 で、既定値は 60 日です。「0」を入力した場合、PIN の有効期限は設定されません。この設定を 0 に構成すると、ネットワークのセキュリティ レベルが大幅に低下するため、これを 0 に構成しないことをお勧めします。


> [!IMPORTANT]
> ユニファイド メッセージングでは、ユーザーの PIN の有効期限が切れるとき、その通知は行われません。



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

## EAC を使用して PIN の有効期限を構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で、変更する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  **\[PIN ポリシー\]** をクリックし、**\[PIN の有効期間を設定する (日数)\]** の横に 0 ～ 999 の値を入力します。

5.  **\[保存\]** をクリックします。

## シェルを使用して PIN の有効期限を構成する

この例では、`MyUMMailboxPolicy` という UM メールボックス ポリシーに関連付けられた Outlook Voice Access ユーザーが PIN を使用できる日数を 30 に設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

この例では、`MyUMMailboxPolicy` という UM メールボックス ポリシーに関連付けられた Outlook Voice Acces ユーザーに対し、次の PIN 関連の設定を構成します。

  - ユーザーの PIN がリセットされるまでのログオン失敗回数を 3 に設定する。

  - ログオンの最大試行回数を 5 に設定する。

  - PIN の最小長を 9 桁に設定する。

  - PIN の有効期限を 40 日間に設定する。

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

