---
title: 'ユーザーのボイス メール設定の管理: Exchange Online Help'
TOCTitle: ユーザーのボイス メール設定の管理
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 49896312
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーのボイス メール設定の管理

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) とボイス メール、および UM とボイス メールが有効なユーザーの構成設定を表示または設定できます。たとえば、次の操作を実行できます。

  - Outlook Voice Access PIN をリセットする。

  - オペレーターの個人内線番号を追加する。

  - 他の内線番号を追加する。

  - 自動音声認識 (ASR) を有効または無効にする。

  - 通話応答ルールを有効または無効にする。

  - 電子メールや予定表へのアクセスを有効または無効にする。


> [!NOTE]
> 一部の設定と機能は、シェルを使用してのみ構成できます。



ボイス メールが有効なユーザーに関連する追加の管理タスクについては、「[ボイス メールが有効なユーザーの手順](voice-mail-enabled-user-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、既存のユーザーがユニファイド メッセージングで現在有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM が有効なユーザーのプロパティを表示または構成する

1.  EAC で、<strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。

2.  リスト ビューで、UM メールボックス ポリシーを変更するメールボックスを選択します。

3.  \[詳細\] ウィンドウの <strong>電話機能と音声機能</strong> \> <strong>ユニファイド メッセージング</strong> で <strong>詳細の表示</strong> をクリックします。

4.  <strong>UM メールボックス</strong> ページで、<strong>UM メールボックスの設定</strong> をクリックして、UM が有効な既存のユーザーの次の UM のプロパティを表示または変更します。
    
      - <strong>PIN の状態</strong>   この表示専用フィールドには、ユーザーのメールボックスの状態が表示されます。既定では、ユーザーの UM が有効になっている場合、PIN の状態は <strong>ロックされていません</strong> と表示されます。ただし、ユーザーが正しくない Outlook Voice Access PIN を複数回入力した場合、状態は <strong>ロックアウト済み</strong> と表示されます。
    
      - <strong>UM メールボックス ポリシー</strong>   このボックスには、UM が有効なユーザーに関連付けられている UM メールボックス ポリシーの名前が表示されます。<strong>参照</strong> をクリックすると、この UM メールボックスに関連付ける UM メールボックス ポリシーを見つけて指定することができます。
    
      - <strong>オペレーターの個人内線番号</strong>   ユーザーに対するオペレーターの個人内線番号を指定するには、このボックスを使用します。既定では、内線電話番号は構成されていません。内線電話番号は 1 ～ 20 文字の長さで指定できます。このオプションを有効にすると、UM が有効になっているユーザーに対する着信呼び出しは、このボックスに指定した内線番号に転送されます。
        
        ダイヤル プランと自動応答には、別の種類のオペレーター内線番号を構成することができます。ただし、それらの内線番号は通常、企業全体にわたる受付またはオペレーター用のものです。オペレーターの個人内線番号設定は、特定のユーザーが応答する前に、管理者のアシスタントまたは個人秘書が着信呼び出しに応答するような場合に使用することができます。

5.  <strong>UM メールボックス</strong> ページの <strong>その他の内線番号</strong> で、ユーザーの内線番号を追加、変更、および表示できます。
    
      - 内線番号を追加するには、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。<strong>内線番号の追加</strong> ページで、<strong>参照</strong> を使用して UM ダイヤル プランを選択し、<strong>内線番号</strong> ボックスに内線番号を入力します。
    
      - 内線番号を削除するには、削除する内線番号を選択し、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックします。

6.  変更を加えた場合は、<strong>保存</strong> をクリックします。

## シェルを使用して UM が有効なユーザーの機能を構成する

この例では、電話での再生機能と、不在着信通知機能を無効にしますが、テキスト メッセージによる通知 (SMS) を有効にします。


> [!NOTE]
> 社内展開およびハイブリッド展開の場合、ユニファイド メッセージングと Lync Server を統合すると、Exchange 2007 または Exchange 2010 メールボックス サーバーに配置されたメールボックスを持つユーザーは、不在着信通知を使用できません。不在着信通知は、通話がメールボックス サーバーに送信される前に切断された場合に生成されます。



    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

この例では、ユーザーが Outlook Voice Access を使用しているときに、予定表にアクセスできず、電子メールにアクセスできるようにします。

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

この例では、ユーザーが Outlook Voice Access を使用しているときに、予定表と電子メールにアクセスできないようにします。

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

この例では、ユーザーが通話応答ルールの作成、着信ファックスの受信、および Outlook Voice Access の使用をできないようにしますが、自動音声認識 (ASR) を有効にします。

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## シェルを使用して UM が有効なユーザーのプロパティを表示する

この例では、フォレスト内の UM が有効なメールボックスすべてを、書式化された一覧で表示します。

    Get-UMMailbox | Format-List

この例は、tonysmith@contoso.com の UM メールボックス プロパティを表示します。.

    Get-UMMailbox -Identity tonysmith@contoso.com


> [!IMPORTANT]
> Exchange 2007 と Exchange 2013 を実行中に、ユーザーのメールボックスが Exchange 2007 メールボックス サーバー上にある場合、<STRONG>Get-UMMailbox</STRONG> コマンドレットを実行しても、正しく動作しません。この問題を解決するには、Exchange 2007 サーバーまたは Exchange 2007 管理ツールを実行しているコンピューターから <STRONG>Get-UMMailbox</STRONG> コマンドレットを実行します。


