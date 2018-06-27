---
title: 'UM 自動応答を無効にする: Exchange Online Help'
TOCTitle: UM 自動応答を無効にする
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 49896414
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 自動応答を無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

既定では、ユニファイド メッセージング (UM) 自動応答を作成すると、UM 自動応答は無効な状態に設定されます。 UM 自動応答を作成した後、その状態を変更して着信呼び出しに応答するかどうかを管理できます。 たとえば、カスタマイズされたプロンプトやメッセージを記録または再記録するときに UM 自動応答を無効にすることができます。

UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答の管理](manage-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。 詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。 また、UM 自動応答の状態が有効に設定されていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM 自動応答を無効にする

1.  EAC で、**\[ユニファイド メッセージング\]** \> **\[UM ダイヤル プラン\]** に移動します。 リスト ビューで、変更するダイヤル プランを選択し、ツール バーで **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  **\[UM ダイヤル プラン\]** ページの**\[UM 自動応答\]** で、無効にする UM 自動応答を選択します。 ツール バーの **\[下方向キー\]**![下矢印アイコン](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "下矢印アイコン") をクリックします。

3.  **\[警告\]** ページで **\[はい\]** をクリックします。

## シェルを使用して UM 自動応答を無効にする

この例では、`MyUMAutoAttendant` という名前の UM 自動応答を無効にします。

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

構文およびパラメーターの詳細については、「[Disable-UMAutoAttendant](https://technet.microsoft.com/ja-jp/library/aa997565\(v=exchg.150\))」を参照してください。

