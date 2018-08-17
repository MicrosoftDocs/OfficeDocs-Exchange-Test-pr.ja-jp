---
title: '最大通話時間の構成: Exchange Online Help'
TOCTitle: 最大通話時間の構成
ms:assetid: 01aa40d2-f918-472b-bace-158222143484
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423535(v=EXCHG.150)
ms:contentKeyID: 49895212
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 最大通話時間の構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

着信呼び出しが通話の途中で有効な内線番号に転送されずに、システムに接続していることができる最大時間 (分単位) を指定できます。大部分の組織では、この値は既定の 30 分に設定する必要があります。この設定は、着信 Outlook Voice Access 呼び出し、組織内部への音声呼び出し、ユニファイド メッセージング (UM) 自動応答への音声呼び出し、および組織外部からの FAX 呼び出しなど、すべての呼び出しに適用されます。

この値は 10 ～ 120 の値に設定できます。この値が小さすぎると、通話が終了する前に切断される可能性があります。たとえば、大量の FAX メッセージを受信することが多い組織では、FAX メッセージのすべてのページが受信されるように、この値を既定値から増やす方が良い場合があります。

UM ダイヤル プランに関連するその他のタスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して最大通話時間を構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>設定</strong> で、<strong>最大通話時間 (分)</strong> の下に分単位で数字を入力します。

5.  <strong>保存</strong> をクリックします。

## シェルを使用して最大通話時間を構成する

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランで、最大通話時間を 10 分に設定します。

    Set-UMDialPlan -identity MyUMDialPlan -MaxCallDuration 10

