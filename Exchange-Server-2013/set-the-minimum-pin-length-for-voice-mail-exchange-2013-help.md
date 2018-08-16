---
title: 'ボイス メールの PIN の最小の長さを設定する: Exchange Online Help'
TOCTitle: ボイス メールの PIN の最小の長さを設定する
ms:assetid: b2ecab54-42e6-45af-8322-615cc1f68dd9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124271(v=EXCHG.150)
ms:contentKeyID: 50555855
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メールの PIN の最小の長さを設定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) が有効になっている Outlook Voice Acces ユーザーの PIN の最小の長さを構成できます。UM メールボックス ポリシーで構成した PIN 設定は、UM メールボックス ポリシーに関連付けられている、すべての UM が有効なユーザーに適用されます。

Outlook Voice Access を使用すると、UM が有効なユーザーは、メールボックス内のボイス メール、電子メール、予定表、個人用連絡先情報にアクセスできます。ただし、メールボックスにアクセスする前に、PIN を入力してボイス メール システムに認証される必要があります。


> [!NOTE]
> PIN の最小の長さを変更した場合、既存の Outlook Voice Access ユーザーは、作業を続行する前に新しい最小の桁数を満たす PIN の入力を求められます。既定値は 6 です。



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

## EAC を使用して Outlook Voice Access の PIN の最小の長さを構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更するダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> で、変更する UM メールボックス ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>PIN ポリシー</strong> をクリックし、<strong>PIN の最小の長さ</strong> の横に 4 ～ 24 の値を入力します。

5.  <strong>保存</strong> をクリックします。

## シェルを使用して Outlook Voice Access の PIN の最小の長さを構成する

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられた Outlook Voice Access ユーザーに対し、PIN の最小長を 8 桁に設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MinPINLength 8

この例では、PIN の最小長を 8 桁に設定し、ユーザーの PIN が 3 にリセットされるまでに許容されるサインインの失敗回数を設定します。この設定は、`MyUMMailboxPolicy` という UM メールボックス ポリシーに関連付けられた UM が有効なユーザーに適用されます。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MinPINLength 8

