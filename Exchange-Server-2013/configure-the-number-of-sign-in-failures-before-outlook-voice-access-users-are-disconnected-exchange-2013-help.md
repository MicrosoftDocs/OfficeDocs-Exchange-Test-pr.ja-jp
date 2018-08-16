---
title: 'Outlook Voice Access ユーザーが切断されるまでのサインインの失敗回数を構成する: Exchange Online Help'
TOCTitle: Outlook Voice Access ユーザーが切断されるまでのサインインの失敗回数を構成する
ms:assetid: 02f93888-168c-44bb-8cf6-17f5fcc3d733
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee423537(v=EXCHG.150)
ms:contentKeyID: 49895216
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Voice Access ユーザーが切断されるまでのサインインの失敗回数を構成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

発信者が切断されるまでにサインインの試行を連続して失敗できる回数を指定することができます。この設定には 1 ～ 20 の値を指定できます。この値が小さすぎると、ユーザーがフラストレーションを感じる可能性があります。大部分の組織では、この値は既定の 3 回に設定する必要があります。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、UM ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してユーザーが切断されるまでのサインイン失敗回数を構成する

1.  EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> に移動します。

2.  リスト ビューで、変更する UM ダイヤル プランを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>UM ダイヤル プラン</strong> ページで、<strong>構成</strong> をクリックします。

4.  <strong>設定</strong> で、<strong>次の回数を超えてサインインに失敗した場合は切断</strong> の下にサインイン失敗回数を入力します。

5.  <strong>保存</strong> をクリックします。

## シェルを使用して、ユーザーが切断されるまでのサインイン失敗回数を構成する

この例では、UM ダイヤル プラン `MyUMDialPlan` のユーザーが切断されるまでのサインイン失敗回数を 5 に設定します。

    Set-UMDialPlan -identity MyUMDialPlan -LogonFailuresBeforeDisconnect 5

