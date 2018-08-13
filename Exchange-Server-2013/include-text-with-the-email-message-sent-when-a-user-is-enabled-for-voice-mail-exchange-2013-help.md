---
title: 'ボイス メールが有効なときに送信される電子メール メッセージにテキストを含める: Exchange Online Help'
TOCTitle: ボイス メールが有効なときに送信される電子メール メッセージにテキストを含める
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51407520
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メールが有効なときに送信される電子メール メッセージにテキストを含める

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーのメールボックスでユニファイド メッセージング (UM) ボイス メールが有効になっている場合、ユニファイド メッセージングへのアクセス方法が記載された電子メール メッセージが送信されます。このメッセージには、ユーザーがボイス メール システムに最初にアクセスする際に使用する PIN 情報が含まれます。

UM メールボックス ポリシーの **\[ユーザーのユニファイド メッセージングが有効\]** ボックスにテキストを追加することにより、ウェルカム電子メール メッセージで送信されるテキストをカスタマイズできます。UM のテクニカル サポートの電話番号、追加の Outlook Voice Access 番号などの情報を含めることができます。追加したテキストは、UM メールボックス ポリシーに関連付けられているユーザーに対してユニファイド メッセージングが有効になったときに送信される電子メール メッセージに含まれます。


> [!NOTE]
> ウェルカム メッセージに追加するカスタム テキストは 512 文字までで、簡単な HTML テキストを含めることができます。



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

## EAC を使用して、メールボックスでユニファイド メッセージングが有効になったときに送信されるテキストをカスタマイズする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM メールボックス ポリシー\]** で管理する UM メールボックス ポリシーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM メールボックス ポリシー\]** ページの **\[メッセージ テキスト\]** で、**\[ユーザーのユニファイド メッセージングが有効\]** のテキスト ボックスに、ユーザーのユニファイド メッセージング ボイス メールが有効になったときに送信される電子メール メッセージに含めるテキストを入力します。

4.  **\[保存\]** をクリックします。

## シェルを使用してメールボックスでユニファイド メッセージングが有効になっているときに送信されるテキストをカスタマイズする

この例では、UM メールボックス ポリシーと関連付けられた、UM が有効なユーザーが電話によるメールボックスへのアクセスに使用できる UM に関する詳細手順と Outlook Voice Access 番号を受け取ることができます。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."

