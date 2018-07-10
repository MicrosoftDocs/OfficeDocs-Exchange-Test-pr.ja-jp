---
title: '同じような名前を持つユーザーの自動応答を構成する: Exchange Online Help'
TOCTitle: 同じような名前を持つユーザーの自動応答を構成する
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52057399
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 同じような名前を持つユーザーの自動応答を構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

名前が類似しているユーザーに使用する手法を自動応答の **\[アドレス帳とオペレーター アクセス\]** オプションで構成するか、自動応答で既定の設定を残して、自動応答に関連付けられているダイヤル プランでこの設定を構成できます。既定では、自動応答の既定の設定が **\[ダイヤル プランから継承\]** になっているため、名前が同じであるか類似している複数のユーザーを自動応答で区別できます。


> [!NOTE]
> 名前が類似しているユーザーに含まれる情報を正しく機能させるには、Microsoft Exchange 組織の受信者の役職、部署、および場所に関する情報を提供する必要があります。



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

## EAC を使用して、名前が類似しているユーザーの UM 自動応答を構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で構成する UM 自動応答を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM 自動応答\]** ページで **\[アドレス帳とオペレーター アクセス\]** をクリックし、**\[同じ名前のユーザーに含める情報\]** で次のいずれかを選択します。
    
      - **役職**   自動応答で一致する複数のユーザーが表示されるときに、各ユーザーの役職が含まれます。
    
      - **部署**   自動応答で一致する複数のユーザーが表示されるときに、各ユーザーの部署が含まれます。
    
      - **場所**   自動応答で一致する複数のユーザーが表示されるときに、各ユーザーの場所が含まれます。
    
      - **なし**   自動応答で一致する複数のユーザーが表示されるときに、追加の情報は含まれません。
    
      - **エイリアスを要求**   発信者は自動応答からユーザーのエイリアスを入力するよう要求されます。
    
      - **ダイヤル プランから継承**   自動応答では、その自動応答に関連付けられているダイヤル プランの既定の設定が使用されます。

4.  **\[保存\]** をクリックします。

## シェルを使用して、名前が類似しているユーザーの UM 自動応答を構成する

この例では、名前が類似しているユーザーに含める情報を、`MyUMAutoAttendant` という UM 自動応答に対する "エイリアスを要求" に設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

この例では、名前が類似しているユーザーに含める情報をユーザーの役職に設定し、名前の参照を有効にします。また、自動応答にダイヤルした発信者が \* を押して、`MyUMAutoAttendant` という名前の UM 自動応答に対する Outlook Voice Access 案内応答を聞くことができるようにします。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

