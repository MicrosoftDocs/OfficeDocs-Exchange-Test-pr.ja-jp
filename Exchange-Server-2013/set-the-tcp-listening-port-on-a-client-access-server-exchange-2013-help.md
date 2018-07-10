---
title: 'クライアント アクセス サーバーで TCP リスニング ポートを設定する: Exchange 2013 Help'
TOCTitle: クライアント アクセス サーバーで TCP リスニング ポートを設定する
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50555791
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセス サーバーで TCP リスニング ポートを設定する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-04-09_

Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバー上では、SIP 要求を待機する TCP ポートを構成できます。既定では、クライアント アクセス サーバーをインストールすると、SIP TCP リスニング ポート番号は 5060 に設定され、クライアント アクセス サーバーは TCP モードで起動します。SIP TCP リスニング ポートは、EAC を使用して構成することはできません。SIP TCP リスニング ポート番号は、**Set-UMCallRouterSettings** コマンドレットを使用して構成する必要があります。

VoIP ゲートウェイ、IP PBX、またはセッション ボーダー コントローラー (SBC) が SIP 標準の 5060 以外の TCP ポートを使用するように構成されている場合、TCP リスニング ポートを 5061 に構成する必要があります。

クライアント アクセス サーバーの TCP および TLS ポートのみを構成できます。Exchange 2013 メールボックス サーバーのポートを構成することはできません。ただし、**Set-UMService** コマンドレットを使用することで、Exchange 2010 UM サーバーの TCP および TLS のリスニング ポートを構成できます。

ユニファイド メッセージング サーバーおよびクライアント アクセス サーバーに関連する追加のタスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 1 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「クライアント アクセス サーバー (UM 呼び出しルーター サービス)」。

  - クライアント アクセス サーバーおよびメールボックス サーバーが正常にインストールされていることを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して、クライアント アクセス サーバー上で TCP リスニング ポートを構成する

1.  EAC で **\[サーバー\]** \> **\[サーバー\]** に移動します。

2.  リスト ビューで、変更する Exchange サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[Exchange Server\]** ページで、**\[ユニファイド メッセージング\]** をクリックします。

4.  **\[UM 呼び出しルーターの設定\]** の **\[TCP リスニング ポート\]** に TCP ポートの番号を入力し、**\[保存\]** をクリックします。

## シェルを使用して、クライアント アクセス サーバー上で TCP リスニング ポートを構成する

この例では、`MyClientAccessServer` というクライアント アクセス サーバー上の TCP リスニング ポートを 5566 に設定します。

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566

