---
title: 'ユーザーの通話応答ルールの作成を許可または禁止する: Exchange Online Help'
TOCTitle: ユーザーの通話応答ルールの作成を許可または禁止する
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50555804
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーの通話応答ルールの作成を許可または禁止する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

メールボックス プロパティを構成することによって、個々のユーザーが通話応答ルールを作成および管理できるようにするかどうかを指定できます。既定では、ユーザーは通話応答ルールを作成できます。

UM ダイヤル プランまたは UM メールボックス ポリシーに基づいて通話応答ルールを構成することにより、ユニファイド メッセージング (UM) において有効になっている通話応答ルールを、複数のユーザーに対して有効または無効にできます。


> [!NOTE]
> EAC を使用してこの機能を構成することはできません。シェルを使用して、ボイス メール ユーザーの通話応答ルールを有効または無効にする必要があります。



ユーザーによる通話の転送の許可に関連するその他の管理タスクについては、「[通話転送手順](forwarding-calls-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、ユーザーのメールボックスの UM が有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して UM が有効なユーザーに対する通知応答ルールを有効または無効にする

この例では、ユーザー tony@contoso.com の通話応答ルールを有効にします。

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

この例では、ユーザー tony@contoso.com の通話応答ルールを無効にします。

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false

