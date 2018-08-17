---
title: '自動応答の呼び出し元の呼び出しを承認する: Exchange Online Help'
TOCTitle: 自動応答の呼び出し元の呼び出しを承認する
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 51407577
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動応答の呼び出し元の呼び出しを承認する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) の自動応答でダイヤルの承認を有効にすることができます。自動応答のダイヤルの承認は、自動応答を呼び出した発信者に対して、国内/地域通話や国際通話、または*アウトダイヤル*を禁止するためのものです。アウトダイヤルとは、UM 自動応答に構成された電話番号に電話を掛けてきたユーザーのためにユニファイド メッセージングが電話を掛けることです。

アウトダイヤルに関するその他の管理タスクについては、「[呼び出しプロシージャの作成をユーザーに許可する](allowing-users-to-make-calls-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM 自動応答」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、UM 自動応答が作成されていることを確認してください。詳細な手順については、「[UM 自動応答を作成する](create-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

  - これらの手順を実行する前に、国内/地域用および国際用のダイヤル ルールが UM ダイヤル プランに作成されていることを確認してください。詳細な手順については、「[ユーザーのダイヤル ルールを作成する](create-dialing-rules-for-users-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、国内/地域通話用のダイヤル ルール グループの UM 自動応答でダイヤルの承認を有効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> で、ダイヤルの承認を作成する UM 自動応答を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM 自動応答</strong> ページの <strong>ダイヤルの承認</strong> で、<strong>承認された国/地域内ダイヤル ルール グループ</strong> の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  <strong>許可するダイヤル ルール グループの選択</strong> ページでダイヤル ルール グループを選択し、<strong>OK</strong>、<strong>保存</strong> の順にクリックします。

## EAC を使用して、国際通話用のダイヤル ルール グループの UM 自動応答でダイヤルの承認を有効にする

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

2.  <strong>UM ダイヤル プラン</strong> ページの <strong>UM 自動応答</strong> で、ダイヤルの承認を作成する UM 自動応答を選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM 自動応答</strong> ページの <strong>ダイヤルの承認</strong> で、<strong>承認された国際ダイヤル ルール グループ</strong> の <strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

4.  <strong>許可するダイヤル ルール グループの選択</strong> ページでダイヤル ルール グループを選択し、<strong>OK</strong>、<strong>保存</strong> の順にクリックします。

## シェルを使用して、UM 自動応答で国内/地域通話用および国際通話用のダイヤルの承認を有効にする

この例では、`MyUMAutoAttendant`という名前の UM 自動応答上の InCountry/RegionGroup1、InCountry/RegionGroup2、InternationalGroup1、および InternationalGroup2 ダイヤルの承認を有効にします。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

