---
title: '自動応答の内線番号の追加: Exchange Online Help'
TOCTitle: 自動応答の内線番号の追加
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 49896551
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動応答の内線番号の追加

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) 自動応答の 1 つまたは複数の内線番号を構成できます。 UM 自動応答に内線番号を追加すると、発信者はその番号を使用して自動応答を呼び出しできます。 また、発信者が自動応答へのアクセスに使用できる内線番号が複数あるために、内線番号の追加が必要になる場合があります。 既定では、自動応答の作成時に内線番号は構成されません。

新しい自動応答を作成するときには、自動応答の内線番号を設定しなくてもかまいません。 また、1 つの自動応答に複数の電話番号または内線番号を関連付けることもできます。 内線番号の追加は、UM 自動応答を作成するときに、または自動応答を構成した後で行うことができます。 UM 自動応答に構成した内線番号の桁数は、UM 自動応答に関連付けられている UM ダイヤル プランで構成されている内線番号の桁数に一致している必要があります。


> [!NOTE]
> 内線番号を追加する代わりに、セッション開始プロトコル (SIP) アドレスを追加することもできます。 一部の IP 構内交換機 (PBX) および Office Communications Server 2007 R2 または Microsoft Lync Server は SIP アドレスを使用します。



UM 自動応答に関連する追加の管理タスクについては、「[UM 自動応答の管理](manage-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。 詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM 自動応答の内線番号または電話番号を追加する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。 リスト ビューで、編集する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> で、内線番号または電話番号を追加する UM 自動応答を選択します。

3.  ツール バーの <strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

4.  <strong>UM 自動応答</strong> ページ \> <strong>全般</strong> の <strong>アクセス番号</strong> のテキストボックスに、使用する内線番号または電話番号を入力して、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  <strong>保存</strong> をクリックして、番号を追加します。

## シェル を使用して UM 自動応答の内線番号を構成する

この例では、複数の内線番号を持つ "`MyUMAutoAttendant`" という名前の UM 自動応答を構成します。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"

