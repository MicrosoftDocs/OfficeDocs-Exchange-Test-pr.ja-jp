---
title: 'プライマリ DNS サーバーに接続できない_PrimaryDNSTestFailed: Exchange 2013 Help'
TOCTitle: プライマリ DNS サーバーに接続できない_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 48269541
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# プライマリ DNS サーバーに接続できない\_PrimaryDNSTestFailed

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

プライマリ ドメイン ネーム システム (DNS) サーバーとの通信を確立できないため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムでは、ローカル コンピューターが、ドメインに対して権限のある DNS データベースと通信する必要があります。

Microsoft Exchange は、内部または外部にある次の送信先サーバーの IP アドレスを解決するために DNS を使用します。

以下の理由によって、プライマリ DNS サーバーとの通信が失敗することがあります。

  - ローカルの TCP/IP 構成が正しい DNS サーバーを示していない。

  - ネットワーク障害やその他の原因により DNS サーバーが停止しているか、または DNS サーバーに到達できない。

この問題を解決するには

  - ローカルの TCP/IP 構成が正しい DNS サーバーを示していることを確認します。

**ローカルの TCP/IP 構成を確認するには、次の操作を行います。**

1.  ローカルの TCP/IP 構成を見直します。
    
    詳細については、DNS を使用する場合の TCP/IP 構成についてのページ ([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094)) を参照してください (このサイトは英語の場合があります)。

<!-- end list -->

  - DNS サーバーが稼働しており、接続可能なことを確認します。

**DNS サーバーが稼働しており、接続可能なことを確認するには、次の操作を行います。**

1.  次の 1 つ以上のチェックを行うことにより、DNS サーバーが稼働していることを確認します。
    
      - DNS サーバー上の DNS 管理プログラムから、DNS サーバーの状態を調べます。
    
      - DNS サーバーを再起動します。
        
        詳細については、DNS サーバーの起動、停止、一時停止、または再起動についてのページ ([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999)) を参照してください (このサイトは英語の場合があります)。
    
      - **nslookup** コマンドを使用して、DNS サーバーが応答するかどうかを確認します。
        
        詳細については、nslookup コマンドを使用して DNS サーバーの応答を確認する方法についてのページ ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)) を参照してください (このサイトは英語の場合があります)。

