---
title: 'クライアント アクセス サーバーで通話応答を許可または禁止する: Exchange 2013 Help'
TOCTitle: クライアント アクセス サーバーで通話応答を許可または禁止する
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50555808
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセス サーバーで通話応答を許可または禁止する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2012-11-18_

クライアント アクセス サーバー上の Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスに対して、新しい呼び出しの応答を許可または禁止できます。既定では、インストール後にクライアント アクセス サーバーは有効な状態になります。音声、ファックス、自動応答、および Outlook Voice Access の着信呼び出しを受け付けるようにクライアント アクセス サーバーを設定する場合は、**Set-ServerComponentState** コマンドレットを使用します。

クライアント アクセス サーバーの保守モードを構成すると、サーバーをサービス停止にできます。クライアント アクセス サーバーの場合、サービス停止は、サーバーが VoIP ゲートウェイ、IP PBX、SIP 対応 PBX、またはセッション ボーダー コントローラー (SBC) からのすべての着信呼び出しを受け付けないことを意味します。

Exchange 2007 および Exchange 2010 では、ユニファイド メッセージング サーバーの運用状態の制御に使用できる状態パラメーターがありました。Exchange 2013 には、クライアント アクセス サーバー上での **Set-UMCallRouterSettings** コマンドレットで、この目的として使用できる状態パラメーターはありません。


> [!IMPORTANT]
> UM を Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server と統合する場合を除き、ユニファイド メッセージングのコールを処理できるように、事前にクライアント アクセス サーバーまたはメールボックス サーバーを UM ダイヤル プランに追加する必要はありません。既定では、組織内のクライアント アクセス サーバーおよびメールボックス サーバーを使用して着信呼び出しに応答できます。



クライアント アクセス サーバーに関連する追加の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「Exchange サーバー構成設定」。

  - クライアント アクセス サーバーが、メールボックス サーバーと同じコンピューターまたは個別のコンピューターのどちらにインストールされているかを確認します。

  - クライアント アクセス サーバーを保守モードに切り替える場合は、クライアント アクセス アレイにおいて、サーバーをサービス停止にするための十分かつ正常な容量があることを確認します。

  - サーバーの保守モードを終了する前に、サーバーの正常性を確認し、サービスを開始する準備ができていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用してクライアント アクセス サーバー上での呼び出し応答を許可または禁止する

この例では、クライアント アクセス サーバー `UMCallRouter-05x.contoso.com` において、VoIP ゲートウェイ、IP PBX、SIP 対応 PBX、または SBC からの音声、FAX、自動応答、および Outlook Voice Access の着信呼び出しへの応答を有効にし、UMCallRouter-05x サーバー上のレジストリに変更を書き込みます。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

この例では、クライアント アクセス サーバー `UMCallRouter-05x.contoso.com` において、VoIP ゲートウェイ、IP PBX、SIP 対応 PBX、または SBC からの音声、FAX、自動応答、および Outlook Voice Access の着信呼び出しへの応答を禁止し、Active Directory にのみ変更を書き込みます。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

