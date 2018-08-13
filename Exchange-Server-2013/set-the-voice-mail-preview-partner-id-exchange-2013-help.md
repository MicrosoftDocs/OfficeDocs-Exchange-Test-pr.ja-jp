---
title: 'ボイス メール プレビュー パートナーの ID を設定する: Exchange Online Help'
TOCTitle: ボイス メール プレビュー パートナーの ID を設定する
ms:assetid: ab98c320-9952-47a7-b141-ddfc2c0ad419
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff630924(v=EXCHG.150)
ms:contentKeyID: 51407562
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メール プレビュー パートナーの ID を設定する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーにボイス メール プレビュー パートナー ID を設定できます。UM メールボックス ポリシーにボイス メール プレビュー パートナー ID を設定すると、そのメールボックス ポリシーとリンクしている UM が有効なすべてのユーザーに適用されます。


> [!NOTE]
> ボイス メール プレビュー パートナー ID を設定するには、シェルを使用する必要があります。



ボイス メール プレビュー パートナー プログラムの詳細については、「[ボイス メール プレビュー アドバイザー](voice-mail-preview-advisor-exchange-2013-help.md)」を参照してください。

ボイス メール プレビューに関連するその他の管理タスクについては、「[ボイス メール プレビューの手順](voice-mail-preview-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して UM メールボックス ポリシーにボイス メール プレビュー パートナー ID を設定する

この例では、*MyUMMailboxPolicy* という名前の UM メールボックス ポリシーで、ボイス メール プレビュー パートナー ID を CON123-2010 に設定します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy 
    -VoiceMailPreviewPartnerAssignedID CON123-2010

