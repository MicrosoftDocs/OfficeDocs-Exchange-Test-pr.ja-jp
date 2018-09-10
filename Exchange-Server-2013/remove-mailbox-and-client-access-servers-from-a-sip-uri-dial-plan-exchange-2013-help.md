---
title: 'メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランから削除する: Exchange 2013 Help'
TOCTitle: メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランから削除する
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54652962
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランから削除する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-04-16_

クライアント アクセス サーバーとメールボックス サーバーを SIP URI ダイヤル プランから削除できます。Microsoft Lync Server を展開しているときに、発信呼び出しが正しく動作できるようにするには、Lync Server 用に作成した SIP URI ダイヤル プランに、すべてのクライアント アクセス サーバーとメールボックス サーバーを手動で追加する必要があります。ただし、保守の実行中やサーバーのオフライン中などは、クライアント アクセス サーバーまたはメールボックス サーバーを Lync 展開から削除する必要がある場合があります。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、SIP URI ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス サーバーを SIP URI ダイヤル プランから削除する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  リスト ビューで、変更するメールボックス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>Exchange Server</strong> ページで、<strong>ユニファイド メッセージング</strong> をクリックします。

4.  <strong>UM サービス設定</strong> \> <strong>関連付けられたダイヤル プラン</strong> で、削除する SIP URI ダイヤル プランを探して、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックしてから、<strong>保存</strong> をクリックします。複数の SIP URI ダイヤル プランを削除する場合は、CTRL キーを押しながら、削除するダイヤル プランを選択してから、<strong>保存</strong> をクリックします。

## シェルを使用してメールボックス サーバーを SIP URI ダイヤル プランから削除する

この例では、`MyMailboxServer` という名前のメールボックス サーバーを `MySIPDialPlan` という名前の SIP URI ダイヤル プランから削除します。

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMService MyMailboxServer
    $s.dialplans-=$dp.identity
    Set-UMService -id MyMailboxServer -dialplans:$s.dialplans

この例では、SipDP1、SipDP2、および SipDP3 という 3 つの SIP URI ダイヤル プランがあります。この例は、SipDP3 ダイヤル プランから `MyMailboxServer` という名前のメールボックス サーバーを削除します。

    Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2

この例では、SipDP1 と SipDP2 という 2 つの SIP URI ダイヤル プランがあります。この例は、SipDP2 ダイヤル プランから `MyMailboxServer` という名前のメールボックス サーバーを削除します。

    Set-UMService -id MyMailboxServer -DialPlans SipDP1

この例は、すべての SIP ダイヤル プランから `MyMailboxServer` という名前のメールボックス サーバーを削除します。

    Set-UMService -id MyUMServer -DialPlans $null

## EAC を使用してクライアント アクセス サーバーを SIP URI ダイヤル プランから削除する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  リスト ビューで、変更するクライアント アクセス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>Exchange Server</strong> ページで、<strong>ユニファイド メッセージング</strong> をクリックします。

4.  <strong>UM 呼び出しルーターの設定</strong> \> <strong>関連付けられたダイヤル プラン</strong> で、削除する SIP URI ダイヤル プランを探して、<strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックしてから、<strong>保存</strong> をクリックします。複数の SIP URI ダイヤル プランを削除する場合は、CTRL キーを押しながら、削除するダイヤル プランを選択してから、<strong>保存</strong> をクリックします。

## シェルを使用してクライアント アクセス サーバーを SIP URI ダイヤル プランから削除する

この例では、`MyClientAccessServer` というクライアント アクセス サーバーを `MySIPDialPlan` という SIP URI ダイヤル プランから削除します。

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMCallRouterSettings MyClientAccessServer
    $s.dialplans-=$dp.identity
    Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans

この例では、SipDP1、SipDP2、および SipDP3 という 3 つの SIP URI ダイヤル プランがあります。この例は、SipDP3 ダイヤル プランから `MyClientAccessServer` という名前のクライアント アクセス サーバーを削除します。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2

この例では、SipDP1 と SipDP2 という 2 つの SIP URI ダイヤル プランがあります。この例は、SipDP2 ダイヤル プランから `MyClientAccessServer` という名前のクライアント アクセス サーバーを削除します。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1

この例は、すべての SIP ダイヤル プランから `MyClientAccessServer` という名前のクライアント アクセス サーバーを削除します。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null

