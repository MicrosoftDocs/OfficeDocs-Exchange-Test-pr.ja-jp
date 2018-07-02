---
title: 'Outlook Voice Access ユーザーのメールボックス機能を設定する: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザーのメールボックス機能を設定する
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50555731
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザーのメールボックス機能を設定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access には、次の 2 つのインターフェイスが含まれています。電話ユーザー インターフェイス (TUI) と音声ユーザー インターフェイス (VUI) です。ユーザーが Exchange 2013 のユニファイド メッセージング (UM) システムを使用してメールボックスにアクセスする場合、UM が有効なユーザーの TUI 設定を構成できます。UM メールボックス ポリシーで UM が有効なユーザーの TUI 設定を変更すると、その UM メールボックス ポリシーに関連付けられているすべてのユーザーにその変更が影響を及ぼします。UM メールボックス ポリシーでは、次の TUI 設定を変更できます。

  - ボイス メールへの暗証番号 (PIN) のないアクセス

  - 他のメッセージに対する音声応答

  - 予定表への TUI アクセス

  - ディレクトリへの TUI アクセス

  - 電子メールへの TUI アクセス

  - 個人用連絡先への TUI アクセス


> [!NOTE]
> UM が有効なユーザーの Outlook&nbsp;Voice Access TUI 設定を変更するには、シェルのみ使用できます。



UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して UM メールボックス ポリシーの TUI 設定を変更する

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーの TUI 関連設定を設定します。

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true

