---
title: 'ユーザー用にボイス メールのプレビューのパートナー サービスを構成する: Exchange Online Help'
TOCTitle: ユーザー用にボイス メールのプレビューのパートナー サービスを構成する
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51407547
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザー用にボイス メールのプレビューのパートナー サービスを構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーでボイス メール プレビュー パートナーを構成できます。ボイス メール プレビュー パートナー ID やボイス メール プレビュー パートナー アドレスなどのボイス メール プレビュー パートナー設定を構成すると、UM メールボックス ポリシーで、構成した設定が UM メールボックス ポリシーにリンクされている UM が有効なすべてのユーザーに適用されます。


> [!NOTE]
> ボイス メール プレビュー パートナーを構成するには、シェルを使用する必要があります。



UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 実行方法

## 手順 1: パートナー サービスにサインアップする

認定パートナー一覧とサインアップ方法の詳細については、「[ボイス メール プレビュー アドバイザー](voice-mail-preview-advisor-exchange-2013-help.md)」または「[Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966)」の Web サイトを参照してください。サインアップが完了すると、ボイス メール プレビュー パートナーによってパートナー ID およびボイス メッセージを転送する際に使用する SMTP アドレスが提供されます。

手順 2 で、手順 1 で取得したパートナー ID と SMTP アドレスを、必要な UM メールボックス ポリシーに適用します。

## 手順 2: ボイス メール プレビュー パートナーのアドレスと ID を設定する

この例では、*MyUMMailboxPolicy* という名前の UM メールボックス ポリシーで、ボイス メール プレビュー パートナー アドレスを exumvmp@fabrikam.com に、ボイス メール プレビュー パートナー ID を CON123-2010 に設定します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## 手順 3: 高度なボイス メール プレビュー パートナー設定を構成する

パートナーに独自の設定が必要な場合、ボイス メール プレビュー パートナーに対して次の 2 つの追加パラメーターを設定できます。

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

この例では、*MyUMMailboxPolicy* という名前の UM メールボックス ポリシーで、最大メッセージ時間を 300 秒 (5 分)、最大配信遅延時間を 600 秒 (10 分) に設定します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## 手順 4: UM が有効なユーザーをボイス メール プレビュー パートナーの UM メールボックス ポリシーに割り当てる

UM ダイヤル プラン内の一部の (ただし全員ではない) UM が有効なユーザーに対して、ボイス メール プレビュー パートナー サービスを構成する場合は、新しい UM メールボックス ポリシーを作成し、パートナー設定を構成する必要があります。構成が完了したら、選択した UM が可能なユーザーに新しいポリシーを適用できます。UM が有効なユーザーを UM メールボックス ポリシーに割り当てる方法の詳細については、次のトピックを参照してください。

  - [UM メールボックス ポリシーの割り当て](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/ja-jp/library/bb124893\(v=exchg.150\))

ボイス メール プレビュー パートナー プログラムの詳細については、「[ボイス メール プレビュー アドバイザー](voice-mail-preview-advisor-exchange-2013-help.md)」を参照してください。

