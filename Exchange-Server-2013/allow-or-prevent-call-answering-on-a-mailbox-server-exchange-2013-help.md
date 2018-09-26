---
title: 'メールボックス サーバーで通話応答を許可または禁止する: Exchange 2013 Help'
TOCTitle: メールボックス サーバーで通話応答を許可または禁止する
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50555774
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス サーバーで通話応答を許可または禁止する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2012-11-18_

メールボックス サーバー上の Microsoft Exchange Unified Messaging サービスが新しい呼び出しに応答することを許可したり、応答を禁止したりすることができます。既定では、メールボックス サーバーは、インストール後に有効な状態になります。メールボックス サーバーが着信音声、FAX、自動応答、および Outlook Voice Access 呼び出しを受け入れるように設定する場合、**Set-ServerComponentState** コマンドレットを使用します。

メールボックス サーバーにメンテナンス モードを構成すると、サーバーをサービス停止の状態にできます。メールボックス サーバーの場合、サービス停止とはサーバーがアクティブなデータベースをホストせず、すべてのトランスポート キューが空であり、サーバーがクライアント アクセス サーバー、VoIP ゲートウェイ、IP PBX、SIP が有効な PBX、またはセッション ボーダー コントローラー (SBC) からの着信呼び出しを受け入れないことを意味します。

Exchange 2007 および Exchange 2010 では、ユニファイド メッセージング サーバーの動作状態を制御するために使用できる状態パラメーターがありました。Exchange 2013 では、メールボックス サーバーの **Set-UMService** コマンドレットに、その目的に使用できる状態パラメーターはありません。


> [!IMPORTANT]
> UM を Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server と統合する場合を除き、ユニファイド メッセージングのコールを処理できるように、事前にクライアント アクセス サーバーまたはメールボックス サーバーを UM ダイヤル プランに追加する必要はありません。既定では、組織内のクライアント アクセス サーバーおよびメールボックス サーバーを使用して着信呼び出しに応答できます。



メールボックス サーバーに関するその他の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「Exchange サーバー構成設定」。

  - メールボックス サーバーがクライアント アクセス サーバーと同じコンピューターにインストールされているか、または別のコンピューターにインストールされているかを確認します。

  - メールボックス サーバーをメンテナンス モードにしている場合、サーバーをサービス停止の状態にするためにすべてのデータベース コピーに十分な冗長性があることを確認します。

  - サーバーの保守モードを終了する前に、サーバーの正常性を確認し、サービスを開始する準備ができていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して、メールボックス サーバー上で呼び出し応答を許可または禁止する

この例では、メールボックス サーバー `UMMBXr-05x.contoso.com` が VoIP ゲートウェイ、IP PBX、SIP が有効な PBX、および SBC からの着信ボイス、FAX、自動応答、および Outlook Voice Access 呼び出しに応答できるようにし、UMMBX-05x サーバー上のレジストリに変更を書き込みます。

```powershell
Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly
```

この例では、メールボックス サーバー `UMMBX-05x.contoso.com` が VoIP ゲートウェイ、IP PBX、SIP が有効な PBX、および SBC からの着信ボイス、FAX、自動応答、および Outlook Voice Access 呼び出しに応答できないようにして、Active Directory のみに変更を書き込みます。

```powershell
Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly
```

