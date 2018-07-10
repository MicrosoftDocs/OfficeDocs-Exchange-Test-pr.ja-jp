---
title: 'クライアント アクセス サーバーの UM 設定管理: Exchange 2013 Help'
TOCTitle: クライアント アクセス サーバーの UM 設定管理
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50555725
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセス サーバーの UM 設定管理

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-04-09_

Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバーをインストールした後、同時呼び出し数、TCP およびトランスポート層セキュリティ (TLS) リスニング ポート、状態、およびスタートアップ モードなどのサーバー オプションを構成できます。


> [!NOTE]
> UM を Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server と統合している場合を除いて、クライアント アクセス サーバーがユニファイド メッセージング (UM) の呼び出しを処理するために、クライアント アクセス サーバーを UM ダイヤル プランに追加する必要がありません。既定では、着信呼び出しに応答するために組織内のすべてのクライアント アクセス サーバーが使用可能です。



ユニファイド メッセージングおよびクライアント アクセス サーバーに関連するその他のタスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「クライアント アクセス サーバー (UM 呼び出しルーター サービス)」。

  - クライアント アクセス サーバーがメールボックス サーバーと同じコンピューターにインストールされているか、または別のコンピューターにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して、クライアント アクセス サーバーにユニファイド メッセージング プロパティを構成する

この例では、すべてのセッション開始プロトコル (SIP) ダイヤル プランから `MyClientAccessServer` という名前のクライアント アクセス サーバーを削除します。

    Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer

この例では、`MyClientAccessServer` という名前のクライアント アクセス サーバーを `MySIPDialPlan` という名前の SIP ダイヤル プランに追加し、着信音声呼び出しの最大数も設定しています。

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer

この例では、`MyClientAccessServer` という名前のクライアント アクセス サーバーで SIP TCP リスニング ポートを 5077 に設定し、スタートアップ モードをデュアル モードに設定します。

    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 

## シェルを使用してクライアント アクセス サーバー プロパティを表示する

この例を実行すると、すべてのクライアント アクセス サーバーの一覧が表示されます。

    Get-UMCallRouterSettings

この例では、クライアント アクセス サーバーのプロパティの一覧を書式付きで表示します。

    Get-UMCallRouterSettings | Format-List

