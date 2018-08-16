---
title: 'ユーザーのボイス メール プレビューを有効にする: Exchange Online Help'
TOCTitle: ユーザーのボイス メール プレビューを有効にする
ms:assetid: 206a5d2b-27c9-4e9b-a29a-6ddffaa07109
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673514(v=EXCHG.150)
ms:contentKeyID: 51407510
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのボイス メール プレビューを有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ボイス メール プレビュー機能が無効になっている場合は、ユニファイド メッセージング (UM) メールボックス ポリシーに関連付けられているユーザーに対して有効にすることができます。この設定を有効にすることで、ユーザーは電子メールやテキスト メッセージのメッセージ本文にあるボイス メール メッセージのテキストを受信できるようになります。既定の設定は有効です。

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

## EAC を使用してボイス メール プレビューを有効にする

1.  EAC で <strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> の順に移動し、変更する UM ダイヤル プランを選択して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> で管理する UM メールボックス ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM メールボックス ポリシー</strong> ページの <strong>全般</strong> で、<strong>ボイス メールのプレビューを許可する</strong> の横にあるチェック ボックスをオンにします。

4.  <strong>保存</strong> をクリックします。

## シェルを使用してボイス メール プレビューを有効にする

この例では、UM メールボックス ポリシー `MyUMMailboxPolicy` に関連付けられているユーザーがボイス メール プレビュー機能を使用できるようにします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - AllowVoiceMailPreview $true

