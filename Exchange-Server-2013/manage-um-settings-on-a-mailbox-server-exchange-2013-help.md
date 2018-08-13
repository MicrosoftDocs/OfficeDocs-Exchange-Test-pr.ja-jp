---
title: 'メールボックス サーバーの UM 設定の管理: Exchange 2013 Help'
TOCTitle: メールボックス サーバーの UM 設定の管理
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50555807
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: HT
---

# メールボックス サーバーの UM 設定の管理

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-11_

Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーをインストールしたら、同時呼び出し数、TCP およびトランスポート層セキュリティ (TLS) のリスニング ポート、状態、UM スタートアップ モードを含むいくつかのオプションを構成できます。


> [!IMPORTANT]
> UM と Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server を統合している場合を除き、ユニファイド メッセージング (UM) の呼び出しを処理する前に、メールボックス サーバーを UM ダイヤル プランに追加する必要はありません。既定では、組織内のすべてのメールボックス サーバーは、着信呼び出しに応答できます。



ユニファイド メッセージングとメールボックス サーバーに関するその他の管理タスクについては、「[UM サービス手順](um-services-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「メールボックス サーバー (UM サービス)」。

  - メールボックス サーバーがクライアント アクセス サーバーと同じコンピューターにインストールされているか、または別のコンピューターにインストールされているかを確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用してメールボックス サーバー上のユニファイド メッセージングのプロパティを構成する

この例では、セッション開始プロトコル (SIP) のすべてのダイヤル プランから `MyMailboxServer` という名前のメールボックス サーバーを削除します。

    Set-UMService -Identity MyMailboxServer -DialPlans $null

この例では、`MyMailboxServer` という名前のメールボックス サーバーを `MySIPDialPlanName` という名前の UM SIP ダイヤル プランに追加し、着信の音声呼び出しの最大数も設定しています。

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

この例では、`MyUMServer` という名前のメールボックス サーバーでスタートアップ モードをデュアル モードに設定します。

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## シェルを使用して、メールボックス サーバーのプロパティを表示する

この例では、すべてのメールボックス サーバーの一覧を表示します。

    Get-UMService

この例では、`MyMailboxServer` という名前のメールボックス サーバーのプロパティの一覧を書式付きで表示します。

    Get-UMService -Identity MyMailboxServer | Format-List

