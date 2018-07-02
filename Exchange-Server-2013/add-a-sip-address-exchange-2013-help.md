---
title: 'SIP アドレスの追加: Exchange Online Help'
TOCTitle: SIP アドレスの追加
ms:assetid: 40295bcf-c62b-4f26-95ca-a8c4bd210fb3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ662760(v=EXCHG.150)
ms:contentKeyID: 50555760
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# SIP アドレスの追加

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーの UM を有効にして SIP URI ダイヤル プランにリンクすると、2 つの EUM プロキシ アドレスが作成されます。一方にはユーザーの内線番号が含まれ、もう一方にはユーザーの SIP アドレスが含まれています。内線番号は、ユーザーが Outlook Voice Access 番号で呼び出すときに使用されます。

SIP URI ダイヤル プランと SIP アドレスは、UM と Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server を統合する際に使用されます。SIP アドレスは、Communications Server または Lync Server が着信呼び出しをルーティングしてユーザーにボイス メールを送信するため使用します。既定では、UM で使用される SIP アドレスが Communications Server または Lync Server で使用される SIP アドレスになります。

ユーザーの UM を有効にしたときに追加されたプライマリ SIP アドレスは、プライマリ EUM プロキシ アドレスとして表示されます。プライマリ SIP アドレスが削除された場合、ユーザーの SIP アドレスを含む EUM プロキシ アドレスのうちで最初に追加したものが、プライマリ EUM プロキシ アドレスとして一覧に表示されます。追加されたその他の SIP アドレスは、セカンダリ EUM プロキシ アドレスとして一覧に表示されます。セカンダリ SIP アドレスが追加されると、発信者は SIP アドレスを使用してユーザーがサインインした SIP エンドポイントでユーザーにボイス メールを残すことができます。すべての音声メッセージは、同じユーザーのメールボックスに配信されます。

EAC またはシェルを使用して、ユーザー用にプライマリまたはセカンダリ SIP アドレスを追加できます。EAC でユーザーのメールボックスの **\[メール アドレス\]** ページを使用して、プライマリまたはセカンダリ SIP アドレスを追加できます。EAC の **\[UM メールボックス\]** ページを使用して、プライマリまたはセカンダリ SIP アドレスを追加することはできません。

シェルでは **Get-UMMailbox** コマンドレットまたは **Get-Mailbox** コマンドレットを使用して、ユーザーのプライマリ SIP アドレスとセカンダリ SIP アドレスを表示できます。

ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、SIP URI UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、既存のユーザーの UM が有効になっていて、SIP URI ダイヤル プランにリンクされていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、ユーザーに割り当てられる SIP アドレスが有効で、正しい形式であることを確認してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、プライマリまたはセカンダリの SIP アドレスを追加する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  リスト ビューで、SIP アドレスを追加するメールボックスを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[ユーザー メールボックス\]** ページの **\[電子メール アドレス\]** の下で、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン")をクリックします。

4.  **\[メール アドレスの新規作成\]** ページで、**\[EUM\]** を選択し、**\[アドレス/内線番号\]** ボックスにユーザーの新しい SIP アドレスを入力します。

5.  **\[メール アドレスの新規作成\]** ページの **\[ダイヤル プラン\]** の下で、**\[参照\]** をクリックして SIP URI ダイヤル プランを選択し、**\[OK\]** をクリックします。

6.  **\[保存\]** をクリックします。

## シェルを使用して SIP アドレスを追加する

この例では、UM が有効なユーザーである Tony Smith の SIP アドレスを追加します。


> [!NOTE]
> シェルを使用して SIP アドレスを追加する前に、追加する EUM プロキシ アドレスの位置を決定する必要があります。位置を決定するには、<STRONG>$mbx.EmailAddresses</STRONG> コマンドを使用します。一覧の最初のプロキシ アドレスは 0 になります。



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:tsmit@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

