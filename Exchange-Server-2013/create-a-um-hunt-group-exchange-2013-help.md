---
title: 'UM ハント グループを作成する: Exchange Online Help'
TOCTitle: UM ハント グループを作成する
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50555768
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: HT
---

# UM ハント グループを作成する

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ハント グループは、構内交換機 (PBX) または IP PBX のハント グループを示す論理的な表現です。UM ハント グループは、UM IP ゲートウェイと UM ダイヤル プランの間の接続またはリンクとして機能します。


> [!NOTE]
> UM IP ゲートウェイを作成するときに、UM IP ゲートウェイに UM ダイヤル プランを関連付けると、UM ハント グループも作成されます。




> [!NOTE]
> UM ハント グループの設定を変更する必要がある場合は、そのハント グループを削除して、適切な設定を持つ別のハント グループを作成する必要があります。



UM ハント グループに関連する追加の管理タスクについては、「[UM ハント グループ手順](um-hunt-group-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ハント グループ」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM IP ゲートウェイが作成されていることを確認してください。詳細な手順については、「[UM IP ゲートウェイを作成する](create-a-um-ip-gateway-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM ハント グループを作成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM ハント グループ\]** で、**\[新規作成\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

3.  **\[UM ハント グループの新規作成\]** ページで、次の情報を入力します。
    
      - **\[名前\]**   UM ハント グループの表示名を作成するには、このボックスを使用します。UM ハント グループ名は必須で、一意である必要があります。ただし、この名前は、EAC とシェルでの表示のためにのみ使用されます。ハント グループを作成した後にその表示名を変更する必要が生じた場合は、まず既存のハント グループを削除し、その後で適切な名前を持つ別のハント グループを作成する必要があります。
        
        組織で複数のハント グループを使用する場合は、ハント グループに対してわかりやすい名前を使用することをお勧めします。UM ハント グループ名の長さの上限は 64 文字で、スペースも使用できます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **\[UM IP ゲートウェイ\]**   このボックスは、使用する UM IP ゲートウェイを指定するために使用します。**\[参照\]** をクリックして UM IP ゲートウェイを選択してから、**\[OK\]** をクリックします。
    
      - **\[パイロット ID\]**   このボックスは、PBX または IP PBX 上に構成されたパイロット識別子を一意に識別する文字列を指定するために使用します。
        
        このボックスでは、内線番号または SIP (セッション開始プロトコル) URI (Uniform Resource Identifier) を使用できます。このボックスは英数字の入力に対応しています。従来の PBX では数字のパイロット ID が使用されますが、IP PBX では SIP URI が使用される場合もあります。

4.  
    
    **\[保存\]** をクリックします。

## シェルを使用して UM ハント グループを作成する

この例は、`MyUMHuntGroup` という名前の、パイロット ID が 12345 の UM ハント グループを作成します。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

この例は、`MyUMHuntGroup` という名前の、複数のパイロット ID を持つ UM ハント グループを作成します。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

