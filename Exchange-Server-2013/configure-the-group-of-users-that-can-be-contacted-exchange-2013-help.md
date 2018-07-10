---
title: '連絡可能なユーザーのグループを構成する: Exchange Online Help'
TOCTitle: 連絡可能なユーザーのグループを構成する
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52057416
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 連絡可能なユーザーのグループを構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

発信者がユニファイド メッセージング (UM) 自動応答に電話を掛けたときに連絡できるユーザーのグループを指定できます。既定で、発信者は UM 自動応答に関連付けられた同一ダイヤル プラン内のユーザーに連絡できます。ただし、ユーザーに通話を転送することや、組織のアドレス帳や特定のユーザー セットに属するユーザーに音声メッセージを送信することを発信者に許可するユーザーのグループ化は、変更することができます。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答の管理](manage-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して発信者が連絡できるユーザーのグループを構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの **\[UM 自動応答\]** で構成する UM 自動応答を選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM 自動応答\]** ページの **\[アドレス帳とオペレーター アクセス\]** にある **\[アドレス帳の検索のオプション\]** で、次のオプションを選択します。
    
      - **\[このダイヤル プラン内のみ\]**   このオプションを選択すると、UM 自動応答に接続した発信者は、UM 自動応答に関連付けられているダイヤル プラン内のユーザーを探して、その人に連絡できるようになります。
    
      - **\[組織全体\]**   このオプションを選択すると、UM 自動応答に接続した発信者は、組織のアドレス帳内にあるすべてのユーザーを探して、その人に連絡できるようになります。これには、メールボックスが有効なすべてのユーザーが含まれます。

4.  **\[保存\]** をクリックします。

## シェルを使用して発信者が連絡できるユーザーのグループを構成する

この例では、発信者が連絡できるユーザーの範囲を `MyUMAutoAttendant` という名前の UM 自動応答で組織のアドレス帳の全ユーザーに設定します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

