---
title: '通話応答ルールの表示と管理: Exchange Online Help'
TOCTitle: 通話応答ルールの表示と管理
ms:assetid: de6d9fa1-7878-49a9-bddb-e3317d94f4d8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn140251(v=EXCHG.150)
ms:contentKeyID: 54651688
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通話応答ルールの表示と管理

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

シェルを使用して、ユーザーの 1 つ以上の通話応答ルールを表示または構成できます。また、Exchange 管理シェル スクリプトで **Get-UMCallAnsweringRule** または **Set-UMCallAnsweringRule** コマンドレットを使って、複数のユーザーの通話応答ルールの表示または管理を行うこともできます。

通話応答ルールを着信呼び出しに適用する方法は、受信トレイ ルールを受信電子メール メッセージに適用する方法と似ています。既定では、ユーザーのユニファイド メッセージング (UM) を有効にした場合、通話応答ルールは構成されません。その場合でも、メール システムが着信呼び出しに応答し、発信者は音声メッセージを残すように求められます。


> [!IMPORTANT]
> UM が有効なユーザーは Outlook Web App にサインインして、通話応答ルールの作成、管理、および削除を行うことができます。



着信応答ルールに関連する追加の管理タスクについては、「[通話転送手順](forwarding-calls-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 通話応答ルール」。

  - この手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、ユーザーのメールボックスの UM が有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - この手順を実行するには、シェルを使用する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。 Windows PowerShell を使って Exchange Online に接続する方法については、「[Exchange Online PowerShell への接続](https://go.microsoft.com/fwlink/p/?linkid=396554)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して、通話応答ルールを表示する

UM が有効なユーザーのメールボックスの単一の通話応答ルール、または通話応答ルール一覧のプロパティを取得できます。

この例では、ユーザーの UM が有効なメールボックスの通話応答ルールの書式設定された一覧を返します。

    Get-UMCallAnsweringRule-Mailbox tonysmith | Format-List

この例では、通話応答ルール `MyUMCallAnsweringRule` のプロパティを表示します。

    Get-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

## シェルを使用して、通話応答ルールを構成する

ユーザーのメールボックスに保存されている通話応答ルールの構成または変更を行うことができます。以下の条件を指定できます。

  - 着信呼び出し元

  - 時刻

  - 予定表の空き時間状態

  - 電子メールに対する自動返信の有無

次の操作も指定できます。

  - 私を探す

  - 発信者を他の連絡先に転送する

  - 音声メッセージを残す

この例では、Tony Smith のメールボックスにある通話応答ルール `MyCallAnsweringRule` に優先度 2 を設定します。

    Set-UMCallAnsweringRule -Mailbox tonysmith -Name MyCallAnsweringRule -Priority 2

この例では、Tony Smith のメールボックスで通話応答ルール `MyCallAnsweringRule` に次の操作を実行します。

  - 通話応答ルールを 2 つの発信者 ID に設定します。

  - 通話応答ルールの優先順位を 2 に設定します。

  - 発信者に挨拶の中断を許可する通話応答ルールを設定します。

<!-- end list -->

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

この例では、Tony Smith のメールボックスの通話応答ルール `MyCallAnsweringRule` の空き時間ステータスを不在に変更し、優先度を 2 に設定します。

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith@contoso.com -ScheduleStatus 0x8

