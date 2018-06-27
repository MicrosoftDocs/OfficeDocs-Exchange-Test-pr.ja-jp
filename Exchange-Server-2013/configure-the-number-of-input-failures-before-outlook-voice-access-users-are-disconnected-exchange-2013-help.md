---
title: 'Outlook Voice Access ユーザーが切断されるまでの入力の失敗回数を構成する: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザーが切断されるまでの入力の失敗回数を構成する
ms:assetid: 64c13d17-a26a-4c9b-b495-bd69c716456a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423547(v=EXCHG.150)
ms:contentKeyID: 49896285
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザーが切断されるまでの入力の失敗回数を構成する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access の番号に電話をかけるユーザーが、正しくないデータを何回入力すると切断されるかを構成できます。この設定は、ディレクトリ検索を使用する Outlook Voice Access ユーザーと認証されていない発信者の両方に適用されます。

正しくないと見なされるデータの種類の例を次に示します。

  - 発信者がシステムに見つからない内線番号を要求する。

  - 呼び出しを転送する、ユーザーの内線番号が見つからない。

  - 発信者が、有効ではないメニュー オプションを押す。

この設定には 1 ～ 20 の値を指定できます。大部分の組織においては、この値は既定の試行回数である 3 回に設定してください。この値の設定が低すぎる場合、呼び出しが途中で切断される場合があります。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、入力を何回失敗すると切断されるかを構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

4.  **\[設定\]** の **\[次の回数を越えて入力に失敗した場合は切断\]** の下に、入力の失敗の回数を入力します。

5.  **\[保存\]** をクリックします。

## シェルを使用して、次の回数を超えて失敗した場合は切断を構成する

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランで、次の回数を超えて失敗した場合は切断を 5 に設定します。

    Set-UMDialPlan -identity MyUMDialPlan -InputFailuresBeforeDisconnect 5

