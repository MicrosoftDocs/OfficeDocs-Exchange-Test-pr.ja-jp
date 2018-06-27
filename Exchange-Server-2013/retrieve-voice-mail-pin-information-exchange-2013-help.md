---
title: 'ボイス メール PIN 情報を取得する: Exchange Online Help'
TOCTitle: ボイス メール PIN 情報を取得する
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54651668
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メール PIN 情報を取得する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) が有効になっているユーザーの PIN 情報を取得できます。ユーザーに対して UM が有効にされ、PIN が生成または作成されると、PIN が暗号化されてユーザーのメールボックスに保存されます。

UM が有効になっているユーザーの PIN 情報を取得するときに返される情報は、暗号化されてユーザーのメールボックスに格納されている PIN データを使用して計算されたものです。この情報によって、ユーザーのメールボックスの情報を表示したり、ユーザーがメールボックスからロックアウトされているかどうかを確認したりできます。

PIN セキュリティに関連する追加のタスクについては、「[PIN セキュリティ手順](pin-security-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、ユーザーのメールボックスの UM が有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、UM が有効なユーザーの PIN 情報を取得する

1.  EAC で、**\[受信者\]** に移動します。リスト ビューで、表示するユーザー メールボックスを選択します。

2.  詳細ウィンドウの **\[電話と音声の機能\]** で **\[詳細表示\]** をクリックします。

3.  **\[UM メールボックス\]** ページ \> **\[UM メールボックスの設定\]** で、ユーザーの **\[PIN の状態\]** を確認します。このページでは、ユーザーのボイス メール PIN をリセットすることもできます。

## シェルを使用して、UM が有効なユーザーの PIN 情報を取得する

この例では、ユーザー ID、PIN が期限切れかどうか、UM メールボックスがロックアウトされているかどうか、および Tony が初めてのユーザーかどうかが表示されています。

    Get-UMMailboxPIN -identity tony@contoso.com

