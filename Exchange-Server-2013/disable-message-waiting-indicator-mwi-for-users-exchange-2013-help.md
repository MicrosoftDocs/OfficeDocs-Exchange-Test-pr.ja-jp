---
title: 'ユーザーのメッセージ待機インジケーター (MWI) を無効にする: Exchange Online Help'
TOCTitle: ユーザーのメッセージ待機インジケーター (MWI) を無効にする
ms:assetid: 51cd6dc4-11d1-4eb9-a6c6-1965fcd24267
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673525(v=EXCHG.150)
ms:contentKeyID: 50555780
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのメッセージ待機インジケーター (MWI) を無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) メールボックス ポリシーに関連付けられたユーザーに対して、メッセージ待機インジケーターを有効または無効にできます。メッセージ待機インジケーターは、従来のボイス メール システムに存在する機能です。メッセージ待機インジケーターは一般的に、ボイス メール加入者の電話のランプを点灯させ、新しいボイス メール メッセージがあることを知らせます。メッセージ待機インジケーターは、UM が有効であるユーザーの携帯電話にテキスト メッセージを送信することもできます。既定の設定は有効です。

メッセージ待機インジケーターが UM IP ゲートウェイで無効になっている場合、UM メールボックス ポリシーに関連付けられた UM が有効であるユーザーはこの機能を使用できません。

UM メールボックス ポリシーに関連するその他の管理タスクについては、「[UM メールボックス ポリシー手順](um-mailbox-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、メッセージ待機インジケーターを無効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM メールボックス ポリシー</strong> で管理する UM メールボックス ポリシーを選択してから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM メールボックス ポリシー</strong> ページで、<strong>メッセージ待機インジケーターを許可する</strong> の横にあるチェック ボックスをオフにします。

4.  <strong>保存</strong> をクリックします。

## シェルを使用して、メッセージ待機インジケーターを無効にする

この例では、`MyUMMailboxPolicy` という名前の UM メールボックス ポリシーに関連付けられているユーザーに対して、メッセージ待機インジケーターを無効にします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $false

