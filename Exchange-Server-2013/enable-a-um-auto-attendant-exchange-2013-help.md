---
title: 'UM 自動応答を有効にする: Exchange Online Help'
TOCTitle: UM 自動応答を有効にする
ms:assetid: 16667a8f-50ab-4bb8-9a05-0389511974b1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996379(v=EXCHG.150)
ms:contentKeyID: 49895264
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 自動応答を有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

既定では、ユニファイド メッセージング (UM) 自動応答を作成すると、UM 自動応答は無効な状態に設定されます。UM 自動応答を作成すると、その状態を、着信呼び出しに応答できる状態に変更できます。

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

## EAC を使用して UM 自動応答を有効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> の下で、有効にする UM 自動応答を選択します。ツール バーの **上矢印**![上矢印アイコン](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "上矢印アイコン") をクリックします。

3.  <strong>警告</strong> ページで <strong>はい</strong> をクリックします。

## シェルを使用して UM 自動応答を有効にする

この例では、着信呼び出しに応答する `MyUMAutoAttendant` という名前の UM 自動応答を有効にします。

    Enable-UMAutoAttendant -Identity MyUMAutoAttendant

