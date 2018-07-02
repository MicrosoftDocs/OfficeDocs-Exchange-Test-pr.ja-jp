---
title: 'ユーザーへの音声メッセージの送信を有効または無効にする: Exchange Online Help'
TOCTitle: ユーザーへの音声メッセージの送信を有効または無効にする
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52057508
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーへの音声メッセージの送信を有効または無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

発信者がユニファイド メッセージング (UM) 自動応答から音声メッセージをユーザーに送信することを許可または禁止することができます。既定では、このオプションは有効になっており、発信者は UM 自動応答に関連付けられている UM ダイヤル プランのユーザーに音声メッセージを送信することができます。このオプションを無効にすると、自動応答は、システム プロンプトで発信者に音声メッセージを送信するように案内しなくなります。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、発信者による音声メッセージの送信を許可または禁止する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で管理する UM 自動応答を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM 自動応答\]** ページ \> **\[アドレス帳とオペレーター アクセス\]** にある **\[ユーザーに連絡するためのオプション\]** で、**\[ユーザーに音声メッセージを残すことを発信者に許可する\]** の横のチェックボックスをオンにし、発信者が音声メッセージを残すことができるようにします。発信者が音声メッセージを残せないようにするには、チェックボックスをオフにします。

4.  **\[保存\]** をクリックします。


> [!NOTE]
> このオプションと <STRONG>[ユーザーへのダイヤルを発信者に許可する]</STRONG> オプションを無効にした場合は、<STRONG>[アドレス帳の検索のオプション]</STRONG> も無効になります。



## シェルを使用して、発信者が音声メッセージを送信することを許可または禁止する

この例では、`MyUMAutoAttendant` という名前の UM 自動応答に呼び出しを行う発信者が音声メッセージを送信できないようにします。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

この例では、`MyUMAutoAttendant` という名前の UM 自動応答に呼び出しを行う発信者が音声メッセージを送信できるようにします。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

