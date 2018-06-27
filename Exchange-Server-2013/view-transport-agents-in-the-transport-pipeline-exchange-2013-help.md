---
title: 'トランスポート パイプライン内のトランスポート エージェントを表示する: Exchange 2013 Help'
TOCTitle: トランスポート パイプライン内のトランスポート エージェントを表示する
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51407568
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート パイプライン内のトランスポート エージェントを表示する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

Exchange 管理シェルを使用することで、Microsoft Exchange Server 2013 メールボックス サーバーおよびクライアント アクセス サーバー上のトランスポート パイプラインのトランスポート エージェントの一覧を確認できます。具体的には、**Get-TransportPipeline** コマンドレットを使用して、トランスポート パイプラインの以下の種類のトランスポート エージェントに関する情報を表示できます。

  - メールボックス サーバー上のトランスポート サービスの **SmtpReceiveAgent**、**RoutingAgent**、**DeliveryAgent**、および **StorageAgent** クラスに基づくエージェント。

  - メールボックス サーバー上のメールボックス トランスポート配信サービスの **SmtpReceiveAgentClass** に基づくエージェント。

  - クライアント アクセス サーバー上のフロント エンド トランスポート サービスの **SmtpReceiveAgentClass** に基づくエージェント。

トランスポート パイプライン内でメッセージに遭遇する有効なすべてのトランスポート エージェントと登録している SMTP イベントの一覧を表示できます。トランスポート エージェントの詳細については、「[トランスポート エージェント](transport-agents-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート エージェント」。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してトランスポート パイプラインのトランスポート エージェントの一覧を表示する

シェルを使用して Exchange サーバー上のトランスポート パイプラインのトランスポート エージェントを表示するには、次のコマンドを実行します。

    Get-TransportPipeline | Format-List

結果を C:\\My Documents\\Transport Agents.txt という名前のテキスト ファイルにエクスポートするには、次のコマンドを実行します。

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## 正常な動作を確認する方法

トランスポート サービスが開始されてから **Get-TransportPipeline** コマンドレットが実行される間に、メッセージがトランスポート パイプラインを通過したトランスポート エージェントのみが、コマンドレットによって表示されます。トランスポート パイプラインでメッセージに遭遇したトランスポート エージェントは、トランスポート エージェントが有効になっていても、**Get-TransportPipeline** コマンドレットが表示する結果には表示されません。

