---
title: 'ユーザーが FAX を受信できるようにする: Exchange Online Help'
TOCTitle: ユーザーが FAX を受信できるようにする
ms:assetid: a0505001-aac0-41ef-824f-76e5e56d7675
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201712(v=EXCHG.150)
ms:contentKeyID: 52057476
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーが FAX を受信できるようにする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ユーザーの FAX 受信を有効にできます。既定では、ユーザーのユニファイド メッセージングを有効にした場合、そのユーザーにリンクされた UM メールボックス ポリシーで FAX 送受信を有効にし、FAX パートナーの URI を構成することで、そのユーザーが FAX を受信できるようになります。UM ダイヤル プラン、UM メールボックス ポリシー、または UM が有効なユーザーのメールボックスで、FAX を有効または無効にできます。

既定では、ユーザーのメールボックスと、ユーザーにリンクされたダイヤル プランにより、FAX 受信が可能になります。ただし、FAX を受信するユーザーについて、UM が有効なユーザーに関連付けられている UM メールボックス ポリシーで最初に FAX 受信を有効にし、FAX パートナーの URI を入力する必要があります。


> [!NOTE]
> UM メールボックス ポリシーの FAX の設定は、EAC を使用して構成できます。ただし、ダイヤル プランまたは個々のユーザーについては、シェルを使用して FAX 設定を構成する必要があります。



FAX パートナーの詳細は、「[Microsoft PinPoint の FAX パートナー](https://go.microsoft.com/fwlink/?linkid=190238)」を参照してください。

FAX に関するその他の管理タスクについては、「[FAX 送受信の手順](faxing-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、ユーザーに割り当てられている UM メールボックス ポリシーで FAX が有効になっていることと、FAX パートナーの URL が適切に構成されていることを確認してください。

  - これらの手順を実行する前に、ユーザーのユニファイド メッセージングが有効になっていることをご確認ください。詳しい手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」をご覧ください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して UM ユーザーの FAX 受信を有効にする

この例では、Tony Smith の 着信 FAX の受信を有効にします。

    Set-UMMailbox -Identity tonysmith@contoso.com -FaxEnabled $true

