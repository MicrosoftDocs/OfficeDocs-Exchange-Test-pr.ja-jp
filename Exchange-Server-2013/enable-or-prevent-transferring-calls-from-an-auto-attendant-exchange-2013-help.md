---
title: '自動応答からの呼び出しの転送を許可または禁止する: Exchange Online Help'
TOCTitle: 自動応答からの呼び出しの転送を許可または禁止する
ms:assetid: ca961cc8-cc24-4e05-b72d-79979c155cf9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423558(v=EXCHG.150)
ms:contentKeyID: 52057498
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動応答からの呼び出しの転送を許可または禁止する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

発信者が自動応答を通じてユーザーに通話を転送することを許可または禁止できます。このオプションは既定で有効になっており、発信者は、UM 自動応答に関連付けられているユニファイド メッセージング (UM) ダイヤル プラン内の UM が有効なユーザーに通話を転送できます。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答手順](um-auto-attendant-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、UM 自動応答からユーザーへの通話の転送を許可または禁止する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で、通話の転送を構成する UM 自動応答を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM 自動応答\]** ページの **\[アドレス帳とオペレーター アクセス\]** にある **\[ユーザーに連絡するためのオプション\]** で、**\[ユーザーへのダイヤルを発信者に許可する\]** の横のチェックボックスをオンにして、通話の転送を有効にします。通話の転送を禁止するには、チェック ボックスをオフにします。

4.  **\[保存\]** をクリックします。


> [!NOTE]
> このオプションをオフにし、<STRONG>[ユーザーに音声メッセージを残すことを発信者に許可する]</STRONG> オプションもオフにした場合は、<STRONG>[アドレス帳の検索のオプション]</STRONG> に含まれるオプションは無効になります。



## シェルを使用して、UM 自動応答からユーザーへの通話の転送を許可または禁止する

この例では、`MyUMAutoAttendant` という名前の UM 自動応答で通話の転送を禁止します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $false

この例では、`MyUMAutoAttendant` という名前の UM 自動応答で通話の転送を許可します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $true

