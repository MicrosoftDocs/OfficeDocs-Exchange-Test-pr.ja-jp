---
title: '録音アイドル タイムアウトの値の構成: Exchange Online Help'
TOCTitle: 録音アイドル タイムアウトの値の構成
ms:assetid: a7fb9a09-fde9-447d-ad2c-95598405e99b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423550(v=EXCHG.150)
ms:contentKeyID: 49896406
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 録音アイドル タイムアウトの値の構成

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

音声メッセージを録音するとき、通話を終了するまでにシステムで許可する無音の秒数を指定できます。大部分の組織では、この値は既定の 5 秒に設定してください。

2 ～ 10 の値を指定できます。この値が小さすぎると、発信者が音声メッセージを残している途中で通話が切断される可能性があります。この値が大きすぎると、音声メッセージの無音時間が長くなることがあります。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して録音アイドル タイムアウト値を構成するには

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>設定</strong> の <strong>録音アイドル タイムアウト (秒)</strong> で、秒数を入力します。

5.  <strong>保存</strong> をクリックします。

## シェルを使用して録音アイドル タイムアウト値を構成する

この例では、`MyUMDialPlan` という名前の UM ダイヤル プランの録音アイドル タイムアウト値を 10 に設定します。

    Set-UMDialPlan -identity MyUMDialPlan -RecordingIdleTimeout 10

