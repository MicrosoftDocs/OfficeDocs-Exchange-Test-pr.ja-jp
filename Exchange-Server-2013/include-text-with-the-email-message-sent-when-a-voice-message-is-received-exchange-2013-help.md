---
title: '音声メッセージの受信時に送信される電子メール メッセージにテキストを含める: Exchange Online Help'
TOCTitle: 音声メッセージの受信時に送信される電子メール メッセージにテキストを含める
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 51407564
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 音声メッセージの受信時に送信される電子メール メッセージにテキストを含める

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ボイス メールが有効なユーザーがボイス メール メッセージを受信したときに送信される電子メール メッセージに追加テキストを含めることができます。既定では、音声メッセージに追加されるテキストは、そのユーザーが音声メッセージを受信したことだけを示します。ただし、UM メール ボックス ポリシーの <strong>ユーザーが音声メッセージを受信したとき</strong> ボックスにテキストを追加することにより、カスタム メッセージを作成できます。たとえば、テキストにシステム セキュリティ ポリシーに関する情報を含めたり、組織内で音声メッセージを正しく扱う方法を記述することができます。このテキストを入力すると、UM メールボックス ポリシーに関連付けられている UM が有効なユーザーが音声メッセージを受信したときに送信されるそれぞれの電子メールに、そのテキストが追加されます。


> [!NOTE]
> 音声メッセージに追加されるカスタム テキストは最大 512 文字で、簡単な HTML テキストを含めることができます。



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

## EAC を使用して音声メッセージに含まれるテキストを変更する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> で管理する UM メールボックス ポリシーを選択してから、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM メールボックス ポリシー</strong> ページの <strong>メッセージ テキスト</strong> にある <strong>ユーザーが音声メッセージを受信したとき</strong> のテキスト ボックスに、ユーザーが音声メッセージを受信したときに送信される電子メール メッセージに含めるテキストを入力します。

4.  <strong>保存</strong> をクリックします。

## シェルを使用して音声メッセージに含まれるテキストを変更する

この例では、`MyUMMailboxPolicy` という UM メールボックス ポリシーに関連付けられたユーザーに送信される音声メッセージに、"この組織外部のユーザーには音声メッセージを転送しないでください" という追加テキストを含めます。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."

