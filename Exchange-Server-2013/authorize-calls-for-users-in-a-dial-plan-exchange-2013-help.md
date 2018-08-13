---
title: 'ダイヤル プランでユーザーの呼び出しを承認する: Exchange Online Help'
TOCTitle: ダイヤル プランでユーザーの呼び出しを承認する
ms:assetid: 7c7fd0c4-4001-408e-b352-c49bac9f78cc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb691175(v=EXCHG.150)
ms:contentKeyID: 51407549
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ダイヤル プランでユーザーの呼び出しを承認する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランでダイヤルの承認を有効にできます。ダイヤル プランのダイヤルの承認を使用して、認証されていない Outlook Voice Access ユーザーによる国内/地域通話または国際電話、もしくは*アウトダイヤル*を禁止できます。アウトダイヤルとは、UM ダイヤル プランで構成された Outlook Voice Access 電話番号に電話を掛けてきたユーザーのためにユニファイド メッセージングが電話を掛けることです。UM ダイヤル プランの設定を構成すると、その設定は、Outlook Voice Access の番号に電話を掛ける認証されていないすべてのユーザーに適用されます。

アウトダイヤルに関するその他の管理タスクについては、「[呼び出しプロシージャの作成をユーザーに許可する](allowing-users-to-make-calls-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - この手順を実行する前に、UM ダイヤル プランで国内/地域用および国際用のダイヤル ルールが作成されていることを確認してください。詳細な手順については、「[ユーザーのダイヤル ルールを作成する](create-dialing-rules-for-users-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、国内/地域通話用のダイヤル ルール グループの UM ダイヤル プランでダイヤルの承認を有効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

3.  **\[UM ダイヤル プラン\]** ページの **\[ダイヤルの承認\]** で、**\[承認された国/地域内ダイヤル ルール グループ\]** の **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  **\[許可するダイヤル ルール グループの選択\]** ページでダイヤル ルール グループを選択し、**\[OK\]**、**\[保存\]** の順にクリックします。

## EAC を使用して、国際通話用のダイヤル ルール グループの UM ダイヤル プランでダイヤルの承認を有効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

3.  **\[UM ダイヤル プラン\]** ページの **\[ダイヤルの承認\]** で、**\[承認された国際ダイヤル ルール グループ\]** の **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  **\[許可するダイヤル ルール グループの選択\]** ページでダイヤル ルール グループを選択し、**\[OK\]**、**\[保存\]** の順にクリックします。

## シェルを使用して、UM ダイヤル プランで国内/地域通話用および国際通話用のダイヤルの承認を有効にする

この例では、`MyUMDialPlan` という UM ダイヤル プランで、InCountry/RegionGroup1、InCountry/RegionGroup2、InternationalGroup1、および InternationalGroup2 の各ダイヤルの承認を有効にします。

    Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

