---
title: 'ドメインの準備が必要 _DomainPrepRequired: Exchange 2013 Help'
TOCTitle: ドメインの準備が必要 _DomainPrepRequired
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 48270253
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ドメインの準備が必要 \_DomainPrepRequired

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

サーバーの役割をインストールしようとして失敗したため、Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。

Microsoft Exchange セットアップ プログラムを実行するには、特定のサーバーの役割をインストールする前にローカル ドメインを Exchange Server 2007 のために準備する必要があります。

Exchange Server 2007 に向けたドメインの準備には、以下の作業が含まれます。

  - Exchange Servers、Exchange Organization Administrators、Authenticated Users、および Exchange Mailbox Administrators のドメイン コンテナーに対するアクセス許可の設定。

  - Microsoft Exchange システム オブジェクト コンテナーの作成 (存在しない場合) と、Exchange Servers、Exchange Organization Administrators、Authenticated Users の各 Microsoft Exchange システム オブジェクト コンテナーに対するアクセス許可の設定。

  - 現在のドメインでの Exchange Install Domain Servers という新しいドメイン グローバル グループの作成。

  - ルート ドメインの Exchange Server USG に対する Exchange Install Domain Servers グループの追加。

この問題を解決するには、**setup /PrepareDomain** を実行してローカル ドメインを準備してから、サーバーの役割のインストールを再度試みます。

PrepareDomain プロセスの実行方法の詳細については、Active Directory とドメインを準備する方法に関するページ ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)) を参照してください (このサイトは英語の場合があります)。

