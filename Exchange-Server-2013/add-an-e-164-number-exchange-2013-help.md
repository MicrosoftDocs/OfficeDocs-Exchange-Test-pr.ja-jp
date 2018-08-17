---
title: 'E.164 番号の追加: Exchange Online Help'
TOCTitle: E.164 番号の追加
ms:assetid: fab86207-be03-40ef-9fea-045a50f3d122
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ662762(v=EXCHG.150)
ms:contentKeyID: 50555902
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# E.164 番号の追加

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーの UM を有効にして E.164 ダイヤル プランにリンクすると、2 つの EUM プロキシ アドレスが作成されます。一方にはユーザーの内線番号が含まれ、もう一方にはユーザーの E.164 番号が含まれています。内線番号は、ユーザーが Outlook Voice Access 番号で呼び出すときに使用されます。

ユーザーの UM を有効にしたときに追加したプライマリ E.164 番号は、プライマリ EUM プロキシ アドレスとして表示されます。プライマリ E.164 番号が削除された場合は、そのユーザーの内線番号を含む最初の EUM プロキシ アドレスがプライマリ EUM プロキシ アドレスとして一覧表示されます。E.164 番号を追加した場合、その E.164 番号はセカンダリ EUM プロキシ アドレスとして一覧表示されます。セカンダリ E.164 番号が追加されている場合、発信者は設定済みのすべての E.164 番号でユーザーにボイス メールを残すことができます。すべての音声メッセージは、同じユーザーのメールボックスに配信されます。

ユーザーのプライマリまたはセカンダリの E.164 番号を追加するには、EAC またはシェルを使用します。EAC ではユーザーのメールボックスの <strong>電子メール アドレス</strong> ページを使用して、プライマリまたはセカンダリの E.164 番号を追加できます。EAC で <strong>UM メールボックス</strong> ページを使用して、プライマリまたはセカンダリの E.164 番号を追加することはできません。

シェルでは **Get-UMMailbox** コマンドレットまたは **Get-Mailbox** コマンドレットを使用して、ユーザーのプライマリとセカンダリの E.164 番号を表示できます。

ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、E.164 の UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する際には、前もってユーザーのメールボックスで UM が有効に設定され、メールボックスが E.164 ダイヤル プランにリンクされていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、ユーザーに割り当てる E.164 番号が有効で正しく書式設定されていることを確認してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、プライマリまたはセカンダリ E.164 番号を追加する

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  リスト ビューで、E.164 番号を追加するメールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>ユーザー メールボックス</strong> ページの <strong>電子メール アドレス</strong> の下で、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。

4.  <strong>新しい電子メール アドレス</strong> ページで <strong>EUM</strong> を選択し、<strong>アドレス/内線番号</strong> ボックスにユーザーの新しい E.164 番号を入力します。

5.  <strong>新しい電子メール アドレス</strong> ページの <strong>ダイヤル プラン</strong> の下で、<strong>参照</strong> をクリックし、E.164 ダイヤル プランを選択して <strong>OK</strong> をクリックします。

6.  <strong>保存</strong> をクリックします。

## シェルを使用して、E.164 番号を追加する

この例では、Tony Smith という名前の UM が有効なユーザーの E.164 番号を追加します。


> [!NOTE]
> シェルを使用して E.164 番号を追加する際には、事前に追加する EUM プロキシ アドレスの位置を特定する必要があります。位置を特定するには、<STRONG>$mbx.EmailAddresses</STRONG> コマンドを使用します。一覧の最初のプロキシ アドレスは 0 になります。



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(2)="eum:+14255550123;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

