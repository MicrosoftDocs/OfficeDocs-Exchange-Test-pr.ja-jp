---
title: 'Outlook Voice Access からの音声メッセージの送信を有効または無効にする: Exchange Online Help'
TOCTitle: Outlook Voice Access からの音声メッセージの送信を有効または無効にする
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52057435
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access からの音声メッセージの送信を有効または無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

Outlook Voice Access ユーザーに対して、同じダイヤル プランに関連付けられた UM が有効な他のユーザーへのボイス メール メッセージの送信を許可または禁止できます。

既定では、この設定は有効になっています。この設定を無効にすると、Outlook Voice Access 番号に電話を掛ける Outlook Voice Access ユーザーは、同じダイヤル プラン内のユーザーにボイス メールを送信できなくなります。

UM ダイヤル プランに関連するその他のタスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して Outlook Voice Access ユーザーによる同じダイヤル プラン内のユーザーへの音声メッセージの送信を許可または禁止する

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[UM ダイヤル プラン\]** ページで、**\[構成\]** をクリックします。

4.  **\[転送 & 検索\]** の **\[ユーザーに許可する\]** で、**\[ユーザーの電話を鳴らさずにボイス メールを残す\]** をオンにし、音声メッセージの送信を許可します。ユーザーが音声メッセージを送信できないようにする場合は、この設定をオフにします。

5.  **\[保存\]** をクリックします。

## シェルを使用して Outlook Voice Access ユーザーによる同じダイヤル プラン内のユーザーへの音声メッセージの送信を許可または禁止する

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランに関連付けられた Outlook Voice Access ユーザーが、同じダイヤル プランに関連付けられたユーザーに音声メッセージを送信できるようにします。

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランに関連付けられた Outlook Voice Access ユーザーが、同じダイヤル プランに関連付けられたユーザーに音声メッセージを送信できないようにします。

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

