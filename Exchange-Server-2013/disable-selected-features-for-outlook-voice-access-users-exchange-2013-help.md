---
title: 'Outlook Voice Access ユーザー用に選択した機能を無効にする: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザー用に選択した機能を無効にする
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50555759
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザー用に選択した機能を無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access には、次の 2 つのインターフェイスが含まれています。電話ユーザー インターフェイス (TUI) と音声ユーザー インターフェイス (VUI) です。既定では、ユーザーが Outlook Voice Access にダイヤルインすると、予定表、電子メール、および個人用連絡先にアクセスし、ディレクトリを検索できます。シェルを使用すると、ユーザーが Outlook Voice Access を使用して自分のメールボックスにアクセスするときに、これらの 1 つ以上の機能にアクセスしないようにできます。ユニファイド メッセージング (UM) メールボックス ポリシーで Outlook Voice Access 機能を変更すると、その UM メールボックス ポリシーに関連付けられているすべてのユーザーにその変更が影響を及ぼします。

UM メールボックス ポリシーで次の Outlook Voice Access 機能へのユーザーのアクセスを無効にできます。

  - 予定表

  - ディレクトリ

  - Email

  - 個人用連絡先

UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

また、シェルを使用して、UM が有効な 1 人のユーザーのメールボックスで Outlook Voice Access 機能を無効にすることもできます。これを行うと、そのユーザーに対してのみ機能が無効になります。1 人のユーザーの UM メールボックス ポリシーにあるすべての Outlook Voice Access 機能を無効にすることはできませんが、その予定表と電子メールへのアクセスを無効にすることはできます。

UM メールボックスに関連する追加の管理タスクについては、「[ユーザーのボイス メール](voice-mail-for-users-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> UM メールボックス ポリシーまたは UM が有効な 1 人のユーザーのメールボックスで、UM が有効なユーザーの Outlook&nbsp;Voice Access 機能を変更する場合は、シェルしか使用できません。



## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、ユーザーに対して UM が有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して、UM メールボックス ポリシーで UM が有効なユーザーに対して選択した Outlook Voice Access 機能を無効にする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられているユーザーが、Outlook Voice Access へのダイヤルイン時に自分の予定表にアクセスできないようにします。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられているユーザーが、Outlook Voice Access へのダイヤルイン時にディレクトリにアクセスできないようにします。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられているユーザーが、Outlook Voice Access へのダイヤルイン時に電子メールにアクセスできないようにします。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられているユーザーが、Outlook Voice Access へのダイヤルイン時に個人用連絡先にアクセスできないようにします。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## シェルを使用して、UM が有効な 1 人のユーザーのメールボックスで選択した Outlook Voice Access 機能を無効にする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

この例では、ユーザーが Outlook Voice Access へのダイヤルイン時に、tony@contoso.com という名前の UM メールボックスの予定表へのアクセスを無効にします。

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

この例では、ユーザーが Outlook Voice Access へのダイヤルイン時に、tony@contoso.com という名前の UM メールボックスの電子メールへのアクセスを無効にします。

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false

