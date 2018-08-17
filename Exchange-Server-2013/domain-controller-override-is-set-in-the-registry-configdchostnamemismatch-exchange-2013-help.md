---
title: 'レジストリにドメイン コントローラーのオーバーライドが設定されている'
TOCTitle: レジストリにドメイン コントローラーのオーバーライドが設定されている_ConfigDCHostNameMismatch
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 48269376
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# レジストリにドメイン コントローラーのオーバーライドが設定されている\_ConfigDCHostNameMismatch

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-15_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

指定されたドメイン コントローラーを使用しようとして失敗したため、Microsoft Exchange Server 2007 のセットアップ プログラムを続行できません。ドメイン コントローラーはレジストリで静的にマップされていました。

Exchange 2007 セットアップ プログラムを実行するには、setup コマンドで指定したドメイン コントローラーが、レジストリの上書きを使用して静的にマップされているドメイン コントローラーと一致する必要があります。

この問題を解決するには、セットアップ プログラムを再度実行して、**/DomainController: \<***FQDN of thestatically mapped domain controller***\>** パラメーターで静的に割り当てられたドメイン コント ローラーを指定します。

DSAccess およびディレクトリ サービスの検出の詳細については、Microsoft サポート技術情報の文書番号 250570「ディレクトリ サービス サーバーの検出と DSAccess の使用法」([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052&kbid=250570)) を参照してください。

