---
title: 'ユーザーの通話応答ルールを有効または無効にする: Exchange Online Help'
TOCTitle: ユーザーの通話応答ルールを有効または無効にする
ms:assetid: f9e40ac3-117f-44f6-9ab1-dc9f4c72e8ac
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn140252(v=EXCHG.150)
ms:contentKeyID: 54651694
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーの通話応答ルールを有効または無効にする

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

シェルを使用して、ユーザーの 1 つ以上の通話応答ルールを有効または無効にできます。また、Exchange 管理シェル スクリプトで **Enable-UMCallAnsweringRule** または **Disable-UMCallAnsweringRule** コマンドレットを使って、複数のユーザーの 1 つ以上の通話応答ルールを有効または無効にすることもできます。

通話応答ルールを着信呼び出しに適用する方法は、受信トレイ ルールを受信電子メール メッセージに適用する方法と似ています。既定では、ユニファイド メッセージング (UM) に対してユーザーを有効にしても、通話応答ルールは構成されません。それでも、着信呼び出しはメール システムによって応答され、発信者は音声メッセージを残すように伝えられます。

通話応答ルールに関連する追加の管理タスクについては、「[通話転送手順](forwarding-calls-procedures-exchange-2013-help.md)」を参照してください。

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

## シェルを使用して通話応答ルールを有効にする

通話応答ルールは有効になった状態で作成されます。シェルを使って、以前無効にされた通話応答ルールを有効にすることができます。通話応答ルールを有効にすると、指定した通話応答ルールの条件とアクションを含む通話応答ルールを取得する **Enable-UMCallAnsweringRule** コマンドレットが有効になります。

この例では、Tony Smith のメールボックスで通話応答ルール `MyUMCallAnsweringRule` を有効にします。

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

この例では、*WhatIf* スイッチを使用して、Tony Smith のメールボックスでの通話応答ルール `MyUMCallAnsweringRule` を有効にできるかどうか、およびコマンドにエラーがあるかどうかをテストします。

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

この例では、Tony Smith のメールボックスで通話応答ルール `MyUMCallAnsweringRule` を有効にし、サインインしてるユーザーに通話応答ルールを有効にすることの確認を求めます。

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

## シェルを使用して通話応答ルールを無効にする

通話応答ルールを無効にすると、着信呼び出しを受信しても、通話応答ルールは取得されず、処理もされなくなります。通話応答ルールを作成する際、条件とアクションのセットアップ時に通話応答ルールを無効にする必要があります。これにより、通話応答ルールを正しく構成するまで、着信呼び出しを受信しても、通話応答ルールが処理されなくなります。

この例では、Tony Smith のメールボックスで通話応答ルール `MyUMCallAnsweringRule` を無効にします。

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

この例では、*WhatIf* スイッチを使用して、Tony Smith のメールボックスで通話応答ルール `MyUMCallAnsweringRule` を無効にできるかどうか、およびコマンドにエラーがあるかどうかをテストします。

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

この例では、Tony Smith のメールボックスで通話応答ルール `MyUMCallAnsweringRule` を無効にし、サインインしているユーザーに通話応答ルールを無効にすることの確認を求めます。

    Disable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

