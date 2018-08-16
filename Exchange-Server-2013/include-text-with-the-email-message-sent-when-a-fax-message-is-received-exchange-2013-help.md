---
title: 'FAX メッセージの受信時に送信される電子メール メッセージにテキストを含める: Exchange Online Help'
TOCTitle: FAX メッセージの受信時に送信される電子メール メッセージにテキストを含める
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 51407522
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# FAX メッセージの受信時に送信される電子メール メッセージにテキストを含める

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) のボイス メールおよび FAX が有効なユーザーが FAX メッセージを受信したときと、UM メールボックス ポリシーが FAX パートナー プロバイダーを使用するよう正しく構成されている場合に送信されるメール メッセージにテキストを追加できます。既定では、UM が有効なユーザーが FAX メッセージを受信したときに作成されるテキストは、ユーザーが FAX メッセージを受信したことだけを示しています。ただし、UM メールボックス ポリシーの <strong>ユーザーが FAX メッセージを受信したとき</strong> ボックスにテキストを追加すれば、カスタム メッセージを作成できます。たとえば、テキストにシステム セキュリティ ポリシーに関する情報を追加して、組織内で FAX メッセージを正しく扱う方法を説明することができます。追加したテキストは、UM メールボックス ポリシーに関連付けられた UM が有効なユーザーが FAX メッセージを受信したときに送信される各メール メッセージに追加されます。


> [!NOTE]
> FAX メッセージに追加されるカスタム テキストは最大 512 文字で、簡単な HTML テキストを含めることができます。



FAX パートナーの詳細は、「[Microsoft PinPoint の FAX パートナー](https://go.microsoft.com/fwlink/?linkid=190238)」を参照してください。

FAX に関するその他の管理タスクについては、「[FAX 送受信の手順](faxing-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス ポリシー」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して FAX メッセージに含まれるテキストを変更する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM メールボックス ポリシー</strong> で管理する UM メールボックス ポリシーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM メールボックス ポリシー</strong> ページの <strong>メッセージ テキスト</strong> にある <strong>ユーザーが FAX メッセージを受信したとき</strong> のテキスト ボックスに、ユーザーがメールボックスで FAX メッセージを受信したときに送信される電子メール メッセージに含めるテキストを入力します。

4.  <strong>保存</strong> をクリックします。

## シェルを使用して FAX メッセージに含まれるテキストを変更する

この例では、UM メールボックス ポリシーに関連付けられた、UM が有効になっているユーザーが、メールボックスで受信した FAX メッセージを開く方法に関する詳細手順を受信できるようにします。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."

