---
title: 'カスタム案内応答、アナウンス、メニュー、およびプロンプトのインポートとエクスポート: Exchange 2013 Help'
TOCTitle: カスタム案内応答、アナウンス、メニュー、およびプロンプトのインポートとエクスポート
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54652988
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# カスタム案内応答、アナウンス、メニュー、およびプロンプトのインポートとエクスポート

 

_**適用先:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2015-04-08_

ユニファイド メッセージング (ＵＭ) ダイヤル計画および自動応答で使用する、録音した音声ファイルをインポートおよびエクスポートすることができます。たとえば、以前のバージョンの Exchange からアップグレードする場合、オーディオ ファイルのコピーをエクスポートして保存したい場合があります。また、ダイヤル計画や自動応答を構成する前に、録音したオーディオ プロンプトのコピーをインポートしたい場合もあります。

オーディオ ファイルは次の目的に使われます。

  - UM ダイヤル計画で、オーディオ ファイルはカスタマイズされた応答メッセージや情報アナウンスに使われます。このファイルは、Outlook Voice Access ユーザーが Outlook Voice Access 番号に電話をかけてきた場合に再生されます。

  - UM 自動応答の場合、オーディオ ファイルは、カスタマイズされた勤務時間および勤務時間外の案内応答、情報アナウンス、メニュー プロンプト、およびナビゲーション メニューに使われます。オーディオ ファイルは、送信者が UM 自動応答に電話を掛けた場合に再生されます。

カスタムの案内応答、アナウンス、メニュー、およびプロンプトでは、次のオーディオ ファイル形式がサポートされています。

  - Windows Media Audio 9.2 - 96 kbps/44 kHz/stereo 1-pass CBR でエンコードされた .wma ファイル (Windows サウンド レコーダー)

  - Windows Media Audio Voice 9 - 8 kbps/8 kHz/Mono、およびリニア PCM (16 ビット/サンプル)、8 キロヘルツ (kHz) オーディオ コーデックでエンコードされた .wav ファイル

UM ダイヤル計画と自動応答で使われるオーディオ ファイルを、{e0dc1c29-89c3-4034-b678-e6c29d823ed9} という名前のシステム メールボックスにインポートし、このシステム メールボックスからオーディオ ファイルをエクスポートします。オーディオ ファイルは、**Import-UMPrompt** および **Export-UMPrompt** というコマンドレットを使って、インポートおよびエクスポートすることができます。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」トピックの「UM ダイヤル プラン」と「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して UM ダイヤル プランおよび自動応答のカスタム案内応答、アナウンス、メニュー、およびプロンプトをインポートする

この例では、案内応答ファイル welcomegreeting.wav を d:\\UMPrompts から UM ダイヤル プラン `MyUMDialPlan` にインポートします。

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

この例では、案内応答ファイル welcomegreeting.wav を d:\\UMPrompts から UM 自動応答 `MyUMAutoAttendant` にインポートします。

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## シェルを使用して UM ダイヤル プランおよび自動応答から、カスタム案内応答、アナウンス、メニュー、およびプロンプトをエクスポートする

この例では、UM ダイヤル プラン `MyUMDialPlan` の案内応答をエクスポートし、welcomegreeting.wav というファイルとして保存します。

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

この例では、UM 自動応答 `MYUMAutoAttendant` に使用する勤務時間の案内応答をエクスポートし、BusinessHoursWelcomeGreeting.wav として保存します。

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

