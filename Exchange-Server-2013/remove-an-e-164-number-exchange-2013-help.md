---
title: 'E.164 番号の削除: Exchange Online Help'
TOCTitle: E.164 番号の削除
ms:assetid: 17941918-7dc5-41a0-b540-09f2f907362b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ662759(v=EXCHG.150)
ms:contentKeyID: 50555735
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# E.164 番号の削除

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユーザーの UM を有効にして E.164 ダイヤル プランにリンクすると、2 つの EUM プロキシ アドレスが作成されます。一方にはユーザーの内線番号が含まれ、もう一方にはユーザーの E.164 番号が含まれています。内線番号は、ユーザーが Outlook Voice Access 番号で呼び出すときに使用されます。

ユーザーの UM を有効にしたときに追加されたプライマリ E.164 番号、または後から追加されたセカンダリ E.164 番号は、ユーザーの EUM プロキシ アドレスとともに削除できます。ユーザーの UM を有効にしたときに追加されたプライマリ E.164 番号は、プライマリ EUM プロキシ アドレスとして表示されます。E.164 番号を追加した場合、その番号はセカンダリ EUM プロキシ アドレスとして表示されます。E.164 番号が削除された場合、発信者は削除された E.164 番号のユーザーにボイス メールを残すことができなくなります。

プライマリ E.164 番号を削除すると、UM はユーザーのメールボックスにボイス メールを送信できなくなり、通話応答ルールは処理されなくなります。プライマリ E.164 番号を削除した場合、EAC ではユーザーのメールボックスでユーザーの EUM プロキシ アドレスが **Null** と表示され、シェルでは **Get-Mailbox** コマンドレットを実行したときにユーザーの EUM プロキシ アドレスが Null と表示されます。また、**Get-UMMailbox** コマンドレットを実行したときには、*Extensions*、*PhoneNumber*、および *CallAnsweringRulesExtensions* パラメーターが空白または Null になります。

ユーザーのプライマリまたはセカンダリの E.164 番号を削除するには、EAC またはシェルを使用します。EAC ではユーザーのメールボックスの **\[電子メール アドレス\]** ページを使用して、プライマリまたはセカンダリの E.164 番号を削除できます。EAC で **\[UM メールボックス\]** ページを使用して、プライマリまたはセカンダリの E.164 番号を削除することはできません。

シェルでは **Get-UMMailbox** コマンドレットまたは **Get-Mailbox** コマンドレットを使用して、ユーザーのプライマリとセカンダリの E.164 番号を表示できます。

ボイス メールが有効なユーザーに関連するその他の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - この手順を実行する前に、E.164 の UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する際には、前もってユーザーのメールボックスで UM が有効に設定され、メールボックスが E.164 ダイヤル プランにリンクされていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する際には、前もってユーザーに対してプライマリおよびセカンダリの E.164 番号が構成されていることを確認してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してプライマリまたはセカンダリの E.164 番号を削除する

1.  EAC で、**\[受信者\]** \> **\[メールボックス\]**に移動します。

2.  リスト ビューで、E.164 番号を削除するメールボックスを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[ユーザー メールボックス\]** ページの **\[電子メール アドレス\]** で、リストから削除する E.164 番号を選択して **\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。プライマリ EUM プロキシ アドレスまたは E.164 番号は、太字の文字と数字で表示されます。

4.  **\[保存\]** をクリックします。

## シェルを使用してプライマリまたはセカンダリの E.164 番号を削除する

この例では、UM が有効なユーザー Tony Smith のメールボックスから E.164 番号 +14255551010 を削除します。


> [!NOTE]
> シェルを使用して E.164 を削除する際には、事前に変更する EUM プロキシ アドレスの位置を特定する必要があります。位置を特定するには、<STRONG>$mbx.EmailAddresses</STRONG> コマンドを使用します。一覧の最初の EUM プロキシ アドレスは 0 になります。



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:+14255551010;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

