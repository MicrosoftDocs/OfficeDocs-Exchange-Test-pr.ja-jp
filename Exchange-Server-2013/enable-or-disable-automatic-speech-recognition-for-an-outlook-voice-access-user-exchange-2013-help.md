---
title: 'Outlook Voice Access ユーザーの自動音声認識を有効または無効にする: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザーの自動音声認識を有効または無効にする
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50555783
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザーの自動音声認識を有効または無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) とボイス メールが有効なユーザーに自動音声認識 (ASR) を構成できます。Outlook Voice Access ユーザーのメールボックスで ASR が有効になると、ユーザーは音声コマンドを使用してメールボックス メニューを操作できます。ASR は既定で有効になっています。ASR が無効になると、メニュー間を移動するには、タッチトーンと呼ばれるデュアル トーン多重周波数 (DTMF) 入力を使用する必要があります。


> [!NOTE]
> EAC を使用してこの機能を構成することはできません。シェルを使用して、ボイス メール ユーザーの ASR を有効または無効にする必要があります。



UM またはボイス メール ユーザーに関連する追加の管理タスクについては、「[ユーザーのボイス メール設定の管理](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM メールボックス」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM メールボックス ポリシーが作成されていることを確認してください。詳細な手順については、「[UM メールボックス ポリシーの作成](create-a-um-mailbox-policy-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、ユーザーのメールボックスの UM が有効になっていることを確認してください。詳細な手順については、「[ボイス メール用にユーザーを有効にする](enable-a-user-for-voice-mail-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して UM が有効なユーザーの ASR を有効または無効にする

この例では、`tonysmith` という名前の UM が有効なユーザーの ASR を有効にします。

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

この例では、`tonysmith` という名前の UM が有効なユーザーの ASR を無効にします。

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false

