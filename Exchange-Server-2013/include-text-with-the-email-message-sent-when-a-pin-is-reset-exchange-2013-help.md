---
title: 'PIN リセット時に送信される電子メール メッセージにテキストを含める: Exchange Online Help'
TOCTitle: PIN リセット時に送信される電子メール メッセージにテキストを含める
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51407600
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# PIN リセット時に送信される電子メール メッセージにテキストを含める

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーのユニファイド メッセージング (UM) またはボイス メールの PIN のリセット時に、そのユーザーに対して送信される電子メール メッセージにテキストを追加することができます。これは、UM メールボックス ポリシーで、**\[ユーザーの Outlook Voice Access PIN がリセットされたとき\]** ボックスにカスタム テキストを入力することで実行できます。カスタマイズされたテキストには、たとえば UM が有効なユーザー向けのセキュリティ関連情報を含めることができます。

既定では、Outlook Voice Access で使用される PIN は、失敗したサインイン試行の回数が 5 回を超えた場合に、ユニファイド メッセージングまたはボイス メール システムによってリセットされます。またユーザーが、Outlook Web App あるいは Outlook 2010 以降に含まれる UM 機能を使用するか、電話から Outlook Voice Access を使用して、PIN をリセットすることもできます。


> [!NOTE]
> このボックスに入力するテキストは 512 文字に制限されており、シンプルな HTML テキストを含めることができます。



Outlook Voice Access の PIN セキュリティに関連するその他のタスクについては、「[PIN セキュリティ手順](pin-security-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EMC を使用して、PIN のリセット時にユーザーに送信される電子メール メッセージにテキストを追加する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックスポリシー\]** ページの **\[メッセージ テキスト\]** にある **\[ユーザーの Outlook Voice Access PIN がリセットされたとき\]** のテキスト ボックスに、ユーザーの PIN がリセットされたときに送信される電子メール メッセージに含めるテキストを入力します。

4.  **\[保存\]** をクリックします。

## シェルを使用して、PIN のリセット時にユーザーに送信される電子メール メッセージにテキストを追加する

この例では、"PIN を他のユーザーと共有しないでください。共有するとポリシーに違反する行為につながる恐れがあります" というテキストを、PIN がリセットされたときに、UM メールボックス ポリシー `MyUMMailboxPolicy` に関連付けられたユーザーに送信される電子メール メッセージに追加します。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

