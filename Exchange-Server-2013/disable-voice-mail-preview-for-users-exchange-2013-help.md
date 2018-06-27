---
title: 'ユーザーのボイス メール プレビューを無効にする: Exchange Online Help'
TOCTitle: ユーザーのボイス メール プレビューを無効にする
ms:assetid: 362fed13-3a9c-4111-bfa4-8c45ab6a3a01
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335199(v=EXCHG.150)
ms:contentKeyID: 51407521
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのボイス メール プレビューを無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーに関連付けられたユーザーのボイス メール プレビュー機能を無効にすることができます。この設定を無効にすることで、ユーザーは電子メールやテキスト メッセージのメッセージ本文でボイス メール メッセージのテキストを受信できなくなります。既定の設定は有効です。

UM メールボックス ポリシーに関連する追加の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してボイス メール プレビューを無効にする

1.  EAC で **\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** の順に移動し、変更する UM ダイヤル プランを選択して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページの **\[全般\]** で、**\[ボイス メールのプレビューを許可する\]** の横にあるチェック ボックスをオフにします。

4.  **\[保存\]** をクリックします。

## シェルを使用してボイス メール プレビューを無効にする

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` に関連付けられているユーザーがボイス メールのプレビュー機能を使用できないようにします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - AllowVoiceMailPreview $false

