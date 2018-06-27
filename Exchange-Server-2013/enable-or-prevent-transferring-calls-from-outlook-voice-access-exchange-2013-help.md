---
title: 'Outlook Voice Access からの呼び出しの転送を許可または禁止する: Exchange Online Help'
TOCTitle: Outlook Voice Access からの呼び出しの転送を許可または禁止する
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52057511
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access からの呼び出しの転送を許可または禁止する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access のユーザーがユニファイド メッセージング (UM) ダイヤル プランに関連付けられているユーザーに電話を転送することを許可または禁止できます。既定では、上記のオプションと **\[ユーザーの電話を呼び出さずに音声メッセージを残す\]** オプションがともに有効になっています。そのため、Outlook Voice Access のユーザーは同じ UM ダイヤル プランの ユーザーに電話を転送したり音声メッセージを残したりすることができます。この設定が適用されるのは、PIN を入力して承認された Outlook Voice Access ユーザーのみです。

UM ダイヤル プランに関連するその他のタスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Outlook Voice Access ユーザーによる電話の転送を許可または禁止する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

3.  **\[転送と検索\]**で、**\[発信者に許可する\]** の **\[ユーザーへの転送\]** の横にあるチェック ボックスをオンにして、発信者が同じダイヤル プランのユーザーに電話を転送できるようにします。Outlook Voice Access のユーザーによる電話の転送を禁止したい場合は、このチェック ボックスをオフにします。

4.  **\[保存\]** をクリックします。

## シェルを使用して Outlook Voice Access ユーザーによる電話の転送を許可または禁止する

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランに所属する Outlook Voice Access ユーザーに対して、同じダイヤル プランのユーザーへの電話の転送を許可します。

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランに所属する Outlook Voice Access ユーザーに対して、同じダイヤル プランのユーザーへの電話の転送を禁止します。

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

