---
title: 'ボイス メール ユーザーがロックアウトされるまでのサインインの失敗回数を設定する: Exchange Online Help'
TOCTitle: ボイス メール ユーザーがロックアウトされるまでのサインインの失敗回数を設定する
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50555810
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メール ユーザーがロックアウトされるまでのサインインの失敗回数を設定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access ユーザーがメールボックスからロックアウトされるまでに許容されるサインインの失敗回数を構成することができます。ボイス メール ユーザーがロックアウトされるまでに許容されるサインインの失敗回数は、ユニファイド メッセージング (UM) メールボックス ポリシーで構成され、UM メールボックス ポリシーに関連付けられている UM が有効なすべてのユーザーに適用されます。既定では、15 に設定されています。

セキュリティを強化するには、最大ログオン試行回数の値を小さくします。ただし、既定値よりはるかに小さい値にすると、ユーザーが不要にロックアウトされる可能性があるため注意してください。ユニファイド メッセージングでは、UM が有効なユーザーの PIN 認証が失敗した場合、またはユーザーがシステムへのサインインに失敗した場合、警告イベントが生成されます。警告イベントは、イベントビューアーで表示できます。この設定は、PIN がリセットされるまでのサインインの失敗回数の設定よりも大きい値にする必要があります。

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

## EAC を使用して、ボイス メール ユーザーがロックアウトされるまでに許容されるサインインの失敗回数を構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> で、変更する UM メールボックス ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>PIN ポリシー</strong> をクリックし、<strong>ロックアウトされるサインインの失敗回数</strong> の横に 1 ～ 999 の値を入力します。

5.  <strong>保存</strong> をクリックします。

## シェルを使用して、ボイス メール ユーザーがロックアウトされるまでに許容されるサインインの失敗回数を構成する

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられている UM が有効なユーザーのサインインの最大試行回数を、10 に設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられた UM が有効なユーザーの場合、Outlook Voice Access ユーザーの PIN をリセットするまでに許容されるサインインの失敗回数を 3、サインインの最大試行回数を 5、PIN の最小の長さを 9 に設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9

