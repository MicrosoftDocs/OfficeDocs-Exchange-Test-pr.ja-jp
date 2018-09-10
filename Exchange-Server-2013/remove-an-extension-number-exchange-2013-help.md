---
title: '内線番号の削除: Exchange Online Help'
TOCTitle: 内線番号の削除
ms:assetid: c2b896cf-21f7-4453-a4e6-b23d236a6dd3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351124(v=EXCHG.150)
ms:contentKeyID: 50555866
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 内線番号の削除

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーの UM を有効にし、内線電話番号ダイヤル プランにリンクすると、ユーザーの内線番号を含む、そのユーザーの EUM プロキシ アドレスが作成されます。ボイス メールをユーザーのメールボックスに送信できるようにするには、使用する UM の内線番号を少なくとも 1 つ定義する必要があります。この内線番号は、ユーザーが Outlook Voice Access 番号を呼び出すときにも使用されます。

ユーザーの UM を有効にした際に追加したメインの内線番号、または後で追加した第 2 内線番号は、ユーザーの関連する EUM プロキシ アドレスと共に削除できます。ユーザーの UM を有効にした際に追加したメインの内線番号は、プライマリ EUM プロキシ アドレスとして一覧に表示されます。追加したすべての他の内線番号は、セカンダリ EUM プロキシ アドレスとして一覧に表示されます。内線番号を削除すると、発信者は、削除された内線番号のユーザーに対してボイス メールを残すことができなくなります。

メインの内線番号を削除した場合、UM はユーザーのメールボックスにメールを送信できなくなり、呼び出し応答ルールは処理されなくなります。メインの内線番号を削除した後に、シェルで **Get-Mailbox** コマンドレットを実行すると、ユーザーの EUM プロキシ アドレスは、EAC のユーザーのメールボックス上で **Null** として一覧に表示されます。また、**Get-UMMailbox** コマンドを実行すると、*Extensions*、*PhoneNumber*、および *CallAnsweringRulesExtensions* の各パラメーターは空白または Null になります。

EAC またはシェルを使用して、メインの内線番号または第 2 内線番号を削除できます。また、EAC でユーザーのメールボックスの <strong>電子メール アドレス</strong> ページを使用して、メインの内線番号または第 2 内線番号を削除できます。EAC で <strong>UM メールボックス</strong> ページを使用してメインの内線番号を削除することはできませんが、これを使用して第 2 内線番号を削除できます。

シェルで **Get-UMMailbox** コマンドレットまたは **Get-Mailbox** コマンドレットを使用して、ユーザーのメインの内線番号および第 2 内線番号を表示できます。

ボイス メールが有効なユーザーに関連する追加の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)」を参照してください。

  - これらの手順を実行する際には、前もってユーザーのメールボックスで UM が有効に設定され、メールボックスが内線電話ダイヤル プランにリンクされていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)」を参照してください。

  - これらの手順を実行する前に、メインの内線番号および第 2 内線番号がユーザーに対して設定されていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメインの内線番号または第 2 内線番号を削除する

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  リスト ビューで、内線番号を削除するメールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>ユーザー メールボックス</strong> ページの <strong>電子メール アドレス</strong> で、一覧から削除する内線番号を選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。プライマリ EUM プロキシ アドレスまたはメインの内線番号は、太字の文字と数字で一覧に表示されます。

4.  <strong>保存</strong> をクリックします。

## EAC を使用して第 2 内線番号を削除する

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  リスト ビューで、内線番号を削除するメールボックスを持つユーザーを選択します。

3.  詳細ペインの <strong>Phone and Voice Features (電話と音声の機能)</strong> \> <strong>ユニファイド メッセージング</strong> で <strong>詳細の表示</strong> をクリックします。

4.  <strong>その他の内線番号</strong> ページの <strong>内線番号</strong> ボックスで、削除する内線番号を選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

5.  <strong>保存</strong> をクリックします。

## シェルを使用して内線番号を削除する

この例では、UM が有効なユーザー Tony Smith のメールボックスから内線番号 12345 を削除します。


> [!NOTE]
> シェルを使用して内線番号を削除する前に、変更する EUM プロキシ アドレスの位置を確認する必要があります。位置を確認するには、<STRONG>$mbx.EmailAddresses</STRONG> コマンドを使用します。一覧の最初の EUM プロキシ アドレスは 0 になります。



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.remove("eum:22222;phone-context=MyDialPlan.contoso.com") 
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

