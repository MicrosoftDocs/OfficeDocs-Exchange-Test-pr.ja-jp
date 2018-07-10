---
title: 'Active Directory サイトの名前を確認できない_InvalidADSite: Exchange 2013 Help'
TOCTitle: Active Directory サイトの名前を確認できない_InvalidADSite
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 48270225
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory サイトの名前を確認できない\_InvalidADSite

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

有効な Active Directory® ディレクトリ サービス サイトにサーバーが属していないように見えるため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Microsoft Exchange セットアップ プログラムを実行するには、Exchange 2007 のインストールに使用するサーバーが有効な Active Directory サイトに属している必要があります。

この問題を解決するには、ローカル サーバーが有効な Active Directory サイトのメンバーであることを確認してから、Exchange Server 2007 セットアップ プログラムを再実行します。

Nltest.exe コマンド ライン ツールの **/DsGetSite** オプションを使用すると、サイト メンバーシップを確認および表示できます。詳細については、*Windows Server 2003 テクニカル リファレンスのページ* ([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734)) の NLTest (Nltest.exe) の概要に関するセクションを参照してください (このサイトは英語の場合があります)。

Active Directory のトラブルシューティングの詳細については、*Windows Server 2003 の運用についてのページ* (<https://go.microsoft.com/fwlink/?linkid=68099>) の Active Directory の運用のトラブルシューティングに関するセクションを参照してください (このサイトは英語の場合があります)。

