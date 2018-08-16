---
title: 'Outlook Voice Access PIN ポリシーの設定: Exchange Online Help'
TOCTitle: Outlook Voice Access PIN ポリシーの設定
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50555787
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access PIN ポリシーの設定

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーの PIN ポリシーは、ユーザー自身で設定することができます。UM メールボックス ポリシーは、Outlook Voice Access を使用する UM が有効になっているユーザーのセキュリティのレベルを強化するように構成することができます。これは、組織で事前に定義された PIN ポリシーに準拠するようユーザーに要求することで可能になります。

Outlook Voice Access ユーザーの PIN ポリシーを設定するには、新しい UM メールボックス ポリシーを作成するか、既存の UM メールボックス ポリシーを変更します。新しい UM メールボックス ポリシーを作成すると、次の PIN 設定を構成して UM メールボックス ポリシーを構成できます。

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

セキュリティ上、UM ユーザーには強力な PIN 要件を実装することをお勧めします。これは、6 桁以上の PIN 設定が必要になる UM PIN ポリシーを作成することにより実現できます。これによって、ネットワークのセキュリティのレベルが上がります。

PIN ポリシーを変更すると、UM メールボックス ポリシーに現在関連付けられているユーザーに対して、新しい PIN 設定が適用されます。たとえば、UM メールボックス ポリシーを変更して PIN の最小桁数を 7 桁から 10 桁に変更した場合、次にユーザーがログオンしたときに、変更された PIN 要件に準拠するよう PIN を変更することが求められます。

Outlook Voice Access の PIN セキュリティに関連するその他のタスクについては、「[PIN セキュリティ手順](pin-security-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、Outlook Voice Access ユーザーの PIN ポリシーを設定する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、編集する UM ダイヤル プランをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> 下で編集したい UM メールボックス ポリシーを選択してから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>プロパティ</strong> をクリックします。

4.  <strong>UM メールボックス ポリシー</strong> ページで、<strong>PIN ポリシー</strong> をクリックします。

5.  <strong>PIN ポリシー</strong> ページで、この UM メールボックス ポリシーに関連付けられている Outlook Voice Access ユーザーの PIN 設定を構成し、<strong>保存</strong> をクリックします。

## シェルを使用して、Outlook Voice Access ユーザーの PIN ポリシーを設定する

この例では、`MyUMMailboxPolicy` という UM メールボックス ポリシーに関連付けられているユーザーの PIN 設定を設定します。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

