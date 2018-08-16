---
title: 'ダイヤル プランの既定言語を設定する: Exchange Online Help'
TOCTitle: ダイヤル プランの既定言語を設定する
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50555802
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ダイヤル プランの既定言語を設定する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランの既定の言語を設定できます。ユーザーが作成した各ダイヤル プランでは、既定の言語として米国英語 (en-US) が使用されます。米国英語 (en-US) 言語パックは、どのバージョンの MicrosoftExchange Server 2013 にもインストールされ、削除することはできません。

ドイツ語 (de-DE) などの別の言語を既定の言語として選択する場合は、まず「[Exchange Server 2013 UM Language Packs](https://go.microsoft.com/fwlink/p/?linkid=266542)」(Exchange Server 2013 UM 言語パック) から German UM language pack .exe ファイルをダウンロードし、UMLanguagePack.de-de.exe インストール ファイルを使用してメールボックス サーバー上に言語パックをインストールします (このサイトは英語の場合があります)。言語パックをインストールした後には、UM ダイヤル プランの既定の言語を米国英語 (en-US) 以外の言語に設定できます。

UM 言語に関連した追加タスクについては、「[UM 言語、プロンプト、および案内応答の手順](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM ダイヤル プランの既定の言語を設定する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、修正する UM ダイヤル プランを選択し、ツール バーで、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>設定</strong> ページの <strong>音声の言語</strong> で、ドロップダウン リストから設定する言語を選択します。

5.  <strong>保存</strong> をクリックして、変更を承認します。

## シェルを使用して UM ダイヤル プランの既定の言語を設定する

この例では、`MyUMDialPlan` という UM ダイヤル プランの既定の言語をドイツ語に設定します。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

この例では、`MyUMDialPlan` という UM ダイヤル プランの既定の言語を日本語に設定します。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

この例では、`MyUMDialPlan` という UM ダイヤル プランの既定の言語を英語 (オーストラリア) に設定します。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

