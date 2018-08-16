---
title: 'SIP アドレスの削除: Exchange Online Help'
TOCTitle: SIP アドレスの削除
ms:assetid: eaaff0b0-7d85-4845-a7b8-ac22b42bc415
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ662761(v=EXCHG.150)
ms:contentKeyID: 50555890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# SIP アドレスの削除

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

UM に対してユーザーを有効にして、そのユーザーを SIP URI ダイヤル プランにリンクすると、2 つの EUM プロキシ アドレスが作成されます。一方のアドレスはユーザーの内線番号を、もう一方のアドレスはユーザーの SIP アドレスを含みます。内線番号は、ユーザーが Outlook Voice Access 番号を呼び出す際に使用されます。

SIP URI ダイヤル プランおよび SIP アドレスは、UM と Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server を統合する際に使用されます。SIP アドレスは、Communications Server または Lync Server が着信呼び出しのルーティングやボイス メールのユーザーへの送信に使用します。既定では、UM が使用する SIP アドレスは、Communications Server または Lync Server が使用する SIP アドレスになります。

UM に対してユーザーを有効にしたときに追加したプライマリ SIP アドレスや後で追加したセカンダリ SIP アドレスを、ユーザーの EUM プロキシ アドレスと連動して削除できます。UM に対してユーザーを有効にしたときに追加したプライマリ SIP アドレスは、プライマリ EUM プロキシ アドレスとして一覧に表示されます。追加した SIP アドレスは、セカンダリ EUM プロキシ アドレスとして一覧に表示されます。SIP アドレスを削除すると、ユーザーが Communications Server または Lync Server でユーザーに割り当てられた SIP アドレスでサインインしている場合でも、発信者が削除された SIP アドレスでユーザーにボイス メールを残すことはできなくなります。

プライマリ SIP アドレスを削除すると、UM はボイス メールをそのユーザーのメールボックスに送信できなくなり、通話応答ルールは処理されなくなります。プライマリ SIP アドレスの削除後、EAC のユーザーのメールボックスでは、ユーザーの EUM プロキシ アドレスは **Null** として一覧に表示されます。シェルで **Get-Mailbox** コマンドレットを実行する場合の結果も同じです。また、**Get-UMMailbox** コマンドレットを実行すると、*Extensions*、*PhoneNumber*、および *CallAnsweringRulesExtensions* パラメーターは空白または null になります。

プライマリおよびセカンダリ SIP アドレスは、EAC またはシェルを使用して削除できます。プライマリおよびセカンダリ SIP アドレスは、EAC でユーザーのメールボックスの <strong>電子メール アドレス</strong> ページを使用して削除できます。プライマリおよびセカンダリ SIP アドレスを、EAC の <strong>UM メールボックス</strong> ページを使用して削除することはできません。

ユーザーのプライマリおよびセカンダリ SIP アドレスは、シェルで **Get-UMMailbox** コマンドレットまたは **Get-Mailbox** コマンドレットを使用して表示できます。

ボイス メールが有効なユーザーに関連する追加の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM に対してユーザーのメールボックスが有効になっており SIP URI ダイヤル プランにリンクされていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、このユーザーを対象にプライマリおよびセカンダリ SIP アドレスが構成されていることを確認してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してプライマリまたはセカンダリ SIP アドレスを削除する

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong>に移動します。

2.  リスト ビューで、SIP アドレスを削除するメールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>ユーザー メールボックス</strong> ページの <strong>電子メール アドレス</strong> の下で、一覧から削除する SIP アドレスを選択し、<strong>削除</strong>![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。プライマリ EUM プロキシ アドレスまたは SIP アドレスは、太字と数字で一覧表示されます。

4.  <strong>保存</strong> をクリックします。

## シェルを使用してプライマリまたはセカンダリ SIP アドレスを削除する

この例では、UM が有効なユーザー Tony Smith のメールボックスから、SIP アドレス tsmith@contoso.com を削除します。


> [!NOTE]
> シェルを使用して SIP アドレスを削除する前に、変更する EUM プロキシ アドレスの位置を確認する必要があります。位置を確認するには、<STRONG>$mbx.EmailAddresses</STRONG> コマンドを使用します。一覧の最初の EUM プロキシ アドレスは 0 になります。



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:tsmith@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

