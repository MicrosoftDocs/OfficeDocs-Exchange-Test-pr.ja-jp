---
title: 'Exchange 2007 のカスタム音声ガイダンスを Exchange 2013 にインポートする: Exchange 2013 Help'
TOCTitle: Exchange 2007 のカスタム音声ガイダンスを Exchange 2013 にインポートする
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54652973
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2007 のカスタム音声ガイダンスを Exchange 2013 にインポートする

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2015-04-08_

カスタム案内応答、アナウンス、メニュー、および音声ガイダンスを含むオーディオ ファイルを Exchange 2007 ユニファイド メッセージング (UM) から Exchange 2013 ユニファイド メッセージングにインポートできます。音声ガイダンスは、シェル スクリプトを使用して、Microsoft Exchange 2013 のインストール時に作成される {e0dc1c29-89c3-4034-b678-e6c29d823ed9} という名前の Exchange システム メールボックスにインポートされます。このシステム メールボックスは、ユニファイド メッセージングでダイヤル プランと自動応答のカスタム案内応答、アナウンス、メニュー、音声ガイダンス、および UM レポートを保存するためにも使用されます。

.wav または .wma 形式のオーディオ ファイルは次のように使用されます。

  - UM ダイヤル プランでは、オーディオ ファイルがカスタマイズされた案内応答と情報アナウンスに使用されます。Outlook Voice Access ユーザーが Outlook Voice Access 番号に電話をかけるとこのオーディオ ファイルが再生されます。

  - UM 自動応答では、オーディオ ファイルがカスタマイズされた勤務時間外および勤務時間内の案内応答、情報アナウンス、メニュー音声ガイダンス、およびナビゲーション メニューに使用されます。発信者が UM 自動応答に電話をかけるとこのオーディオ ファイルが再生されます。

MigrateUMCustomPrompts.ps1 スクリプトを使用して、すべての Exchange Server 2007 UM カスタム案内応答、アナウンス、メニュー、および音声ガイダンスをすべての Exchange 2007 UM ダイヤル プランと UM 自動応答用の Exchange 2013 UM に移行します。

既定で、MigrateUMCustomPrompts.ps1 スクリプトは、Exchange 2013 サーバー上の \<Program Files\>\\Microsoft\\Exchange Server\\V15\\Scripts フォルダーに配置されています。


> [!NOTE]
> MigrateUMCustomPrompts.ps1 スクリプトは、Exchange 2013 に付属しています。このスクリプトは、Exchange&nbsp;2007 UM サーバーが設置された同じ組織内の Exchange 2013 メールボックス上で実行する必要があります。



UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」トピックの「UM ダイヤル プラン」と「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant)」を参照してください。

  - この手順を実行するには、シェルを使用する必要があります。オンプレミスの Exchange 組織で Exchange 管理シェル を開く方法については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## MigrateUMCustomPrompts.ps1 シェルを使用して、UM ダイヤル プランおよび自動応答用のすべてのカスタム音声ガイダンスのコピーを移行する

1.  <strong>スタート</strong> \> <strong>すべてのプログラム</strong> \> <strong>Microsoft Exchange Server 2013</strong> \> <strong>Exchange 管理シェル</strong> を順にクリックします。

2.  シェルのプロンプトで、スクリプトへのパスを入力します。たとえば、「**cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**」と入力してから、Enter を押します。

3.  シェル プロンプトで、**".\\MigrateUMCustomPrompt"** と入力してから、Enter を押します。

