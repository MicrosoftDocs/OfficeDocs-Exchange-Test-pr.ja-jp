---
title: '自動応答で使う言語を選択する: Exchange Online Help'
TOCTitle: 自動応答で使う言語を選択する
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50555757
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動応答で使う言語を選択する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答の音声ガイダンスの既定の言語設定を構成できます。UM 自動応答の言語設定を使用すると、自動応答の音声ガイダンスに使用する既定の言語を構成できます。システムの既定の音声ガイダンスを自動応答に使用している場合、自動応答が着信呼び出しに応答したときに発信者が聞く音声ガイダンスにはこの言語が使用されます。この言語設定が影響するのは、Microsoft Exchange Unified Messaging サービスを実行しているメールボックス サーバーをインストールした後に提供されるシステムの既定の音声ガイダンスだけです。この設定は、自動応答で構成されるカスタムの音声ガイダンスには影響しません。使用可能な言語は、メール サーバーにインストールされたユニファイド メッセージング言語パックに基づきます。

ユーザーが作成した自動応答には、最初に既定の言語として米国英語 (en-US) が使用されます。米国英語 (en-US) 言語パックは、Microsoft Exchange 2013 のすべてのバージョンに既定でインストールされ、削除することはできません。たとえばドイツ語 (de-DE) など別の言語を選択する場合は、まず「[Exchange Server 2013 UM Language Packs](https://go.microsoft.com/fwlink/?linkid=266542)」から German UM language pack .exe ファイルをダウンロードし、UMLanguagePack.de-de.exe インストール ファイルを使用してメールボックス サーバーに UM 言語パックをインストールします。UM 言語パックをインストールすると、UM 自動応答の既定の言語を英語 (en-US) 以外の言語に設定できるようになります。

UM 言語に関連した追加タスクについては、「[UM 言語、プロンプト、および案内応答の手順](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して既定の言語の設定を構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、修正する UM ダイヤル プランを選択し、ツール バーで、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** の下で変更したい UM 自動応答を選択してから、ツール バーで **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  **\[全般\]** ページの **\[自動音声インターフェイスの言語\]** の下で、必要な言語をドロップダウン リストから選択します。

5.  **\[保存\]** をクリックして、変更を承認します。

## シェルを使用して既定の言語の設定を構成する

この例では、UM 自動応答 `MyUMAutoAttendant` の既定言語を英語 (英国) に設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

この例では、UM 自動応答 `MyUMAutoAttendant` の既定言語をドイツ語に設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

