---
title: 'Outlook ボイス アクセス ユーザーが連絡できるユーザーのグループの構成: Exchange Online Help'
TOCTitle: Outlook ボイス アクセス ユーザーが連絡できるユーザーのグループの構成
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 49896408
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook ボイス アクセス ユーザーが連絡できるユーザーのグループの構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access ユーザーから転送された電話またはボイス メール メッセージを受信するユーザーを指定できます。 既定では、**\[このダイヤル プラン内のみ\]** オプションが選択されます。 Outlook Voice Access ユーザーから組織全体のユーザー、既存のUM自動応答、または特定の内線番号への電話を転送したりボイス メッセージを送信できるよう、上記の設定を変更できます。

UM ダイヤル プランに関連するその他のタスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。 詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC 使用して、Outlook Voice Access ユーザーが連絡できるユーザーグループを構成する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで変更したい UM ダイアル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン").

3.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

4.  **\[転送&検索\]**の**\[ユーザーを名前やエイリアスで検索することを発信者に許可する\]**で、次のいずれかのオプションを選択します。
    
      - **\[このダイヤル プランのみ\]** このオプションを使用すると、Outlook Voice Access 番号に発信する Outlook Voice Access ユーザーが同じダイヤル プランのユーザーを見つけて連絡するようにできます。
    
      - **\[組織全体\]** このオプションを使用すると、Outlook Voice Access 番号に発信する Outlook Voice Access ユーザーが組織全体からユーザーを見つけて連絡するようにできます。 これには、メールボックスが有効なすべてのユーザーが含まれます。
    
      - **\[この自動応答のみ\]** このオプションを使用すると、Outlook Voice Access 番号に発信する Outlook Voice Access ユーザーが特定の自動応答に接続するようにできます。 ここで指定する前に、自動応答を作成する必要があります。 これにより、Outlook Voice Access ユーザーを他の自動応答に転送できます。 ここでは、音声認識が有効な自動応答または音声認識が無効な自動応答どちらでも選択できます。
    
      - **\[この内線番号のみ\]** このオプションを使用すると、Outlook Voice Access ユーザーが指定した内線番号に接続するようにできます。 使用できるのは内線番号の数字桁のみです。 このテキスト ボックスに入力する桁数と、UM ダイヤル プランで構成されている内線番号の桁数とが一致する必要があります。

5.  **\[保存\]** をクリックします。

## シェルを使用して、Outlook Voice Access ユーザーが連絡できるユーザーグループを構成する

この例では、`MyUMDialPlan` という UM ダイヤル プランで Outlook Voice Access ユーザーが連絡できるユーザーグループを「組織全体」に設定しています。

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

この例では、`MyUMDialPlan` という UM ダイヤル プランで Outlook Voice Access ユーザーが連絡できるユーザーグループを `DialPlan`に設定しています。

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false

