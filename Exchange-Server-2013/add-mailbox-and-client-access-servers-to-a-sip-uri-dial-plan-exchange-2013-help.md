---
title: 'メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する: Exchange 2013 Help'
TOCTitle: メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52057798
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス サーバーとクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-04-16_

クライアント アクセス サーバーとメールボックス サーバーは SIP URI ダイヤル プランに追加できます。クライアント アクセス サーバーとメールボックス サーバーを内線番号や E.164 ダイヤル プランに関連付けることはできませんが、これらのサーバーはすべての着信呼び出しに応答します。

Microsoft Lync Server を展開しているときに、発信呼び出しが正しく動作できるようにするには、Lync Server 用に作成したすべての SIP URI ダイヤル プランに、すべてのクライアント アクセス サーバーとメールボックス サーバーを手動で追加する必要があります。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - これらの手順を実行する前に、SIP URI ダイヤル プランが作成されていることを確認してください。詳細な手順については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス サーバーを SIP URI ダイヤル プランに追加する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  リスト ビューで、変更するメールボックス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>Exchange Server</strong> ページで、<strong>ユニファイド メッセージング</strong> をクリックします。

4.  <strong>UM サービス設定</strong> \> <strong>関連付けられたダイヤル プラン</strong> で、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  <strong>UM ダイヤル プランの選択</strong> ウィンドウで SIP URI ダイヤル プランを選択し、<strong>追加</strong>、<strong>OK</strong>、<strong>保存</strong> の順にクリックします。

## シェルを使用してメールボックス サーバーを SIP URI ダイヤル プランに追加する

この例では `MyMailboxServer` というメールボックス サーバーを `MySIPDialPlan` という SIP URI ダイヤル プランに追加し、新しい呼び出しを受け入れないようにします。また、スタートアップ モードをデュアル モードに設定し、メールボックス サーバーが TCP 要求と TLS 要求を受け付けられるようにします。

```powershell
Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual
```

この例では `MyMailboxServer` というメールボックス サーバーを `MySIPDialPlan` および `MySIPDialPlan2` という 2 つの SIP ダイヤル プランに追加して次の設定を行います。

  - IPv4 と IPv6 の両方のアドレスを許可します。

  - 着信呼び出しの最大数を 50 に設定します。

  - Lync Server の SIP アクセス サービスを構成します。

<!-- end list -->

```powershell
Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com
```

## EAC を使用してクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する

1.  EAC で <strong>サーバー</strong> \> <strong>サーバー</strong> に移動します。

2.  リスト ビューで、変更するクライアント アクセス サーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  <strong>Exchange Server</strong> ページで、<strong>ユニファイド メッセージング</strong> をクリックします。

4.  <strong>UM 呼び出しルーターの設定</strong> \> <strong>関連付けられたダイヤル プラン</strong> で、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  <strong>UM ダイヤル プランの選択</strong> ウィンドウで SIP URI ダイヤル プランを選択し、<strong>追加</strong>、<strong>OK</strong>、<strong>保存</strong> の順にクリックします。

## シェルを使用してクライアント アクセス サーバーを SIP URI ダイヤル プランに追加する

この例では、`MyClientAccessServer` というクライアント アクセス サーバーを `MySIPDialPlan` という SIP URI ダイヤル プランに追加します。また、スタートアップ モードをデュアル モードに設定し、クライアント アクセス サーバーが TCP 要求と TLS 要求を受け付けられるようにします。

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual
```  

この例では、`MyClientAccessServer` というクライアント アクセス サーバーを `MySIPDialPlan` と `MySIPDialPlan2` という 2 つの SIP ダイヤル プランに追加して、サーバーが IPv4 と IPv6 の両方のアドレスを使用できるようにします。

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer
```

