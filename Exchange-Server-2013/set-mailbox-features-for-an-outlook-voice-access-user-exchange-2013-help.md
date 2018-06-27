---
title: 'Outlook Voice Access ユーザー用メールボックスの機能を設定する: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザー用メールボックスの機能を設定する
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50555840
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザー用メールボックスの機能を設定する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

電話ユーザー インターフェイス (TUI) 設定は、ユーザーが Outlook Voice Access を使用してユニファイド メッセージング (UM) システムにアクセスする場合に使用されます。UM が有効なユーザーの TUI 構成設定を変更する場合は、その UM が有効なユーザーのメールボックスでプロパティとその値を変更します。

UM が有効なユーザーに対して、次の TUI 設定を変更できます。

  - サブスクライバー アクセスの許可

  - 予定表への TUI アクセスの許可

  - 電子メールへの TUI アクセスの許可

  - 自動音声認識の許可

UM ユーザーに関連する追加の管理タスクについては、「[Outlook Voice Access ユーザー用メールボックスの機能を設定する](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、既存の Exchange 受信者のユニファイド メッセージングおよびボイス メールが有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して UM が有効な単一のユーザーの TUI 設定を変更する

この例では、Tony Smith という名前の UM が有効なユーザーの TUI を使用して予定表と電子メールにアクセスできるようにします。

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True


> [!NOTE]
> ユーザーの TUI 設定は、UM メールボックス ポリシーでもアクセスできます。UM メールボックス ポリシーでの TUI 設定の変更は、その UM メールボックス ポリシーに関連付けられたすべてのユーザーに影響します。UM メールボックス ポリシーで TUI 設定を変更する方法の詳細については、「<A href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">Outlook Voice Access ユーザーのメールボックス機能を設定する</A>」を参照してください。


