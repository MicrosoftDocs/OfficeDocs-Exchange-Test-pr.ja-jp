---
title: 'セットアップを続行するために COM+ イベント システム サービスを開始する必要がある_EventSystemStopped: Exchange 2013 Help'
TOCTitle: セットアップを続行するために COM+ イベント システム サービスを開始する必要がある_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 48269382
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# セットアップを続行するために COM+ イベント システム サービスを開始する必要がある\_EventSystemStopped

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。インストール先のコンピューターで COM+ イベント システム サービスが開始されていないため、クライアント アクセス サーバーの役割またはエッジ トランスポート サーバーの役割をインストールしようとして失敗したことが原因です。

Exchange 2007 のセットアップ プログラムを実行するには、Microsoft Exchange をインストールしようとしているコンピューターで、COM+ イベント システム サービスの状態が **"開始"** に設定されている必要があります。

COM+ イベント システム サービスは、購読する側の COM コンポーネントにイベントの自動配信を行う COM+ コンポーネントのために、システム イベント通知をサポートしています。

クライアント アクセス サーバーの役割とエッジ トランスポート サーバーの役割はどちらも、COM+ イベント システム サービスを購読する COM+ コンポーネントを必要とします。

この問題を解決するには、ローカル コンピューターで COM+ イベント システム サービスの状態が **"開始"** に設定されていることを確認してから、Microsoft Exchange セットアップ プログラムを再実行します。

**COM+ イベント システム サービスの状態を "開始" に設定するには、次の操作を行います。**

1.  **\[マイ コンピューター\]** を右クリックし、**\[管理\]** をクリックします。

2.  **\[サービスとアプリケーション\]** ノードを展開し、**\[サービス\]** ノードをクリックします。

3.  右側のウィンドウで、**\[Com+ Event System\]** を見つけます。

4.  **\[Com+ Event System\]** を右クリックし、**\[プロパティ\]** をクリックします。

5.  **\[スタートアップの種類\]** を **\[自動\]** に設定し、**\[サービスの状態\]** を **\[開始\]** に設定します。

6.  **\[適用\]** をクリックし、**\[OK\]** をクリックします。

