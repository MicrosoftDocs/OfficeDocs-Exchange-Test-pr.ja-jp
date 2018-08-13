---
title: 'リモート ドメインのメッセージ レポート作成の構成: Exchange 2013 Help'
TOCTitle: リモート ドメインのメッセージ レポート作成の構成
ms:assetid: 73dc686a-e7a3-44c7-b82f-f52ff9273199
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ649325(v=EXCHG.150)
ms:contentKeyID: 49896314
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# リモート ドメインのメッセージ レポート作成の構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

Exchange 管理シェルを使用して、リモート ドメイン経由での電子メールの送受信方法を構成できます。次に、Exchange 管理シェルを使用して、Exchange で配信レポートと配信不能レポートを処理する方法を示します。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分

  - この手順を実行するには、シェルを使用する必要があります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「リモート ドメイン」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してメッセージ レポートを構成する

リモート ドメインのプロパティを構成するには、**Set-RemoteDomain** コマンドレットを使用できます。

この例では、Contoso という名前のリモート ドメインへの配信レポートを無効にします。既定では、この設定は有効になっています。

    Set-RemoteDomain Contoso -DeliveryReportEnabled $false

この例では、リモート ドメインへの配信不能レポートを無効にします。既定では、この設定は有効になっています。

    Set-RemoteDomain Contoso -NDREnabled $false

