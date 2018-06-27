---
title: 'SIP アドレスの変更: Exchange Online Help'
TOCTitle: SIP アドレスの変更
ms:assetid: 33f4f464-9baa-48af-bf5e-a0d55bb45f60
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335189(v=EXCHG.150)
ms:contentKeyID: 50555752
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# SIP アドレスの変更

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーの UM を有効にして SIP URI ダイヤル プランにリンクすると、2 つの EUM プロキシ アドレスが作成されます。一方にはユーザーの内線番号が含まれ、もう一方にはユーザーの SIP アドレスが含まれています。内線番号は、ユーザーが Outlook Voice Access 番号で呼び出すときに使用されます。

SIP URI ダイヤル プランと SIP アドレスは、UM と Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server を統合する際に使用されます。SIP アドレスは、Communications Server または Lync Server が着信呼び出しをルーティングしてユーザーにボイス メールを送信するため使用します。既定では、UM で使用される SIP アドレスが Communications Server または Lync Server で使用される SIP アドレスになります。

ユーザーの UM を有効にしたときに追加されたプライマリ SIP アドレス、または後から追加されたセカンダリ SIP アドレスは、ユーザーの EUM プロキシ アドレスとともに変更できます。ユーザーの UM を有効にしたときに追加されたプライマリ SIP アドレスは、プライマリ EUM プロキシ アドレスとして表示されます。追加したセカンダリ SIP アドレスは、セカンダリ EUM プロキシ アドレスとして表示されます。セカンダリ SIP アドレスが変更された場合、発信者は新しい SIP アドレスを使用してユーザーがサインインしているすべての SIP エンドポイントでユーザーにボイス メールを残すことができます。すべての音声メッセージは、同じユーザーのメールボックスに配信されます。

プライマリまたはセカンダリ SIP アドレスを変更するには、EAC またはシェルを使用します。EAC ではユーザーのメールボックスの **\[電子メール アドレス\]** ページを使用して、プライマリまたはセカンダリ SIP アドレスを変更できます。EAC で **\[UM メールボックス\]** ページを使用して、プライマリまたはセカンダリ SIP アドレスを変更することはできません。

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

## EAC を使用してプライマリまたはセカンダリ SIP アドレスを変更する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  リスト ビューで、SIP アドレスを変更するメールボックスを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[ユーザー メールボックス\]** ページの **\[電子メール アドレス\]** で、変更する SIP アドレスを選択して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。プライマリ SIP アドレスは、太字の文字と数字で表示されます。

4.  **\[電子メール アドレス\]** ページで、**\[アドレス/内線番号\]** ボックスにユーザーの新しい SIP アドレスを入力し、**\[OK\]** をクリックします。新しい UM ダイヤル プランを選択する場合は、**\[参照\]** をクリックします。

5.  **\[保存\]** をクリックします。

## シェルを使用してプライマリまたはセカンダリ SIP アドレスを変更する

この例では、Tony Smith の SIP アドレスを変更します。


> [!NOTE]
> シェルを使用して SIP アドレスを変更する際には、事前に変更する EUM プロキシ アドレスの位置を特定する必要があります。位置を特定するには、<STRONG>$mbx.EmailAddresses</STRONG> コマンドを使用します。最初の EUM プロキシ アドレスは既定の (プライマリ) SIP アドレスで、リスト内の 0 になります。



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:tsmith@contoso.com;phone-context=MySIPDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

