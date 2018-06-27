---
title: 'このサーバーは送信コネクタのソースである_ServerIsSourceForSendConnector: Exchange 2013 Help'
TOCTitle: このサーバーは送信コネクタのソースである_ServerIsSourceForSendConnector
ms:assetid: 151c0014-c90c-4c52-8e74-4b3f1bc7aaf1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.serverissourceforsendconnector(v=EXCHG.150)
ms:contentKeyID: 48269198
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# このサーバーは送信コネクタのソースである\_ServerIsSourceForSendConnector

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

ハブ トランスポート サーバーの役割の削除が失敗したため、Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。このローカル コンピューターは、Exchange 組織内の 1 つ以上の送信コネクタのソースになっています。

送信コネクタは、そこを通過して送信メッセージが送信される論理ゲートウェイを表します。

Exchange 2007 セットアップ プログラムを実行するには、サーバーの役割を削除する前に、ハブ トランスポート サーバー コンピューターから Exchange 組織のすべての送信コネクタを移動または削除する必要があります。

この問題を解決するには、ローカル コンピューターからすべての送信コネクタを移動または削除してから、セットアップ プログラムを再実行します。

送信コネクタの変更や削除の詳細については、Exchange Server 2007 製品ドキュメントの次のトピックを参照してください。

  - 送信コネクタを削除する方法についてのページ ([https://go.microsoft.com/fwlink/?LinkId=86655](https://go.microsoft.com/fwlink/?linkid=86655)) (このサイトは英語の場合があります)

  - 送信コネクタの構成を変更する方法についてのページ ([https://go.microsoft.com/fwlink/?LinkId=86656](https://go.microsoft.com/fwlink/?linkid=86656)) (このサイトは英語の場合があります)

