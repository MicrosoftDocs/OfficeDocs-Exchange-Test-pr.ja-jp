---
title: 'E.164 番号の変更: Exchange Online Help'
TOCTitle: E.164 番号の変更
ms:assetid: 2a3da11b-bb9b-4d4d-9238-6a1a47ef63f2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335162(v=EXCHG.150)
ms:contentKeyID: 50555754
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# E.164 番号の変更

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーの UM を有効にして E.164 ダイヤル プランにリンクすると、2 つの EUM プロキシ アドレスが作成されます。一方にはユーザーの内線番号が含まれ、もう一方にはユーザーの E.164 番号が含まれています。内線番号は、ユーザーが Outlook Voice Access 番号で呼び出すときに使用されます。

ユーザーの UM を有効にしたときに追加されたプライマリ E.164 番号、または後から追加されたセカンダリ E.164 番号は、ユーザーの EUM プロキシ アドレスとともに変更できます。ユーザーの UM を有効にしたときに追加されたプライマリ E.164 番号は、プライマリ EUM プロキシ アドレスとして表示されます。追加したセカンダリ E.164 番号は、セカンダリ EUM プロキシ アドレスとして表示されます。E.164 番号が変更された場合、発信者は設定されたすべての新しい E.164 番号でユーザーにボイス メールを残すことができます。すべての音声メッセージは、同じユーザーのメールボックスに配信されます。

ユーザーのプライマリまたはセカンダリ E.164 番号を変更するには、EAC またはシェルを使用します。ユーザーのメールボックスの <strong>電子メール アドレス</strong> ページを使用して、プライマリまたはセカンダリ E.164 番号を変更できます。ただし、EAC で <strong>UM メールボックス</strong> ページを使用して、プライマリまたはセカンダリ E.164 番号を変更することはできません。

シェルでは **Get-UMMailbox** コマンドレットまたは **Get-Mailbox** コマンドレットを使用して、ユーザーのプライマリとセカンダリの E.164 番号を表示できます。

ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、E.164 の UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)」を参照してください。

  - これらの手順を実行する際には、前もってユーザーのメールボックスで UM が有効に設定され、メールボックスが E.164 ダイヤル プランにリンクされていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)」を参照してください。

  - これらの手順を実行する際には、前もって UM が有効なユーザーに割り当てられる E.164 番号が有効であることを確認してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してプライマリまたはセカンダリ E.164 番号を変更する

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  リスト ビューで、E.164 番号を変更するメールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>ユーザー メールボックス</strong> ページの <strong>電子メール アドレス</strong> で、変更する E.164 番号を選択して <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。プライマリ E.164 番号は、太字の文字と数字で表示されます。

4.  <strong>電子メール アドレス</strong> ページで、<strong>アドレス/内線番号</strong> ボックスにユーザーの新しい E.164 番号を入力し、<strong>OK</strong> をクリックします。新しい UM ダイヤル プランを選択する場合は、<strong>参照</strong> をクリックします。

5.  <strong>保存</strong> をクリックします。

## シェルを使用してプライマリまたはセカンダリ E.164 番号を変更する

この例では、Tony Smith という名前の UM が有効なユーザーの E.164 番号を変更します。


> [!NOTE]
> シェルを使用して E.164 を変更する際には、事前に変更する EUM プロキシ アドレスの位置を特定する必要があります。位置を特定するには、<STRONG>$mbx.EmailAddresses</STRONG> コマンドを使用します。最初の EUM プロキシ アドレスは既定の (プライマリ) E.164 番号で、リスト内の 0 になります。



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:+14255550123;phone-context=MyE.164DialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

