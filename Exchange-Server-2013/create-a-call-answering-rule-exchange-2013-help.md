---
title: '通話応答ルールを作成する: Exchange Online Help'
TOCTitle: 通話応答ルールを作成する
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 51407499
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通話応答ルールを作成する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

シェルを使用して、ユーザーの通話応答ルールを 1 つ以上作成できます。 Exchange 管理シェル スクリプト内で **New-UMCallAnsweringRule** コマンドレットを使用して、複数のユーザーの通話応答ルールを作成することもできます。

通話応答ルールを着信呼び出しに適用する方法は、受信トレイ ルールを受信電子メール メッセージに適用する方法と似ています。 既定では、ユーザーのユニファイド メッセージング (UM) を有効にしたときに、通話応答ルールは構成されません。 それでも、着信呼び出しはメール システムによって応答され、発信者は音声メッセージを残すように伝えられます。


> [!NOTE]
> UM が有効なユーザーは、Outlook Web App にサインインすることによって、通話応答ルールを作成、管理、削除できます。



通話応答ルールに関連する追加の管理タスクについては、「[通話転送手順](forwarding-calls-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 通話応答ルール」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。 詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。 詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、ユーザーのメールボックスの UM が有効になっていることを確認してください。 詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - この手順を実行するには、シェルを使用する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。 Windows PowerShell を使って Exchange Online に接続する方法については、「[Exchange Online PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=396554)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して通話応答ルールを作成する

この例では、優先順位 2 で Tony Smith のメールボックスに通話応答ルール `MyCallAnsweringRule` を作成します。

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

この例では、Tony Smith のメールボックスに通話応答ルール `MyCallAnsweringRule` を作成し、次のような操作を実行します。

  - 通話応答ルールを 2 つの発信者 ID に設定します。

  - 通話応答ルールの優先順位を 2 に設定します。

  - 発信者に挨拶の中断を許可する通話応答ルールを設定します。

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

この例では、Tony Smith のメールボックスに通話応答ルール `MyCallAnsweringRule` を作成し、次のような操作を実行します。

  -  
    通話応答ルールの優先順位を 2 に設定します。

  -  
    通話応答ルールのキー マッピングを作成します。

  -  
    発信者がユーザーのボイス メールに達し、ユーザーのステータスが「予定あり」に設定されている場合、発信者は次のような操作を行うことができます。
    
      - キー 1 を押して、内線 45678 の受付に転送します。
    
      - キー 2 を押して、緊急用の検索機能を使用し、まず内線 23456 を呼び出し、次に内線 45671 を呼び出します。

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"

