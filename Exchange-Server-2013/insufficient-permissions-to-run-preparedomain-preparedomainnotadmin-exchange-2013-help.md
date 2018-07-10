---
title: '/PrepareDomain_PrepareDomainNotAdmin を実行するための十分なアクセス許可がない: Exchange 2013 Help'
TOCTitle: /PrepareDomain_PrepareDomainNotAdmin を実行するための十分なアクセス許可がない
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 48270030
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# /PrepareDomain\_PrepareDomainNotAdmin を実行するための十分なアクセス許可がない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

**/PrepareDomain** プロセスの実行が失敗したため、Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。ログオンしたユーザーに、**/PrepareDomain** プロセスを実行するための十分なアクセス許可がありません。

Exchange 2007 セットアップ プログラムでは、**/PrepareDomain** プロセスの実行時にログオンするユーザーは、準備するドメインの Domain Admins グループのメンバーである必要があります。また、Enterprise Admins グループのメンバーである必要があります。

この問題を解決するには、準備するドメインの Domain Admins グループのアクセス許可をログオン ユーザーに与え、ログオン ユーザーを Enterprise Admins グループに登録します。または、これらのアクセス許可を持つアカウントを使用してログオンし、Exchange 2007 セットアップ プログラムを再実行します。

Microsoft Exchange に必要な Active Directory アクセス許可の詳細については、Exchange Server における Active Directory アクセス許可の操作についてのページ ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)) を参照してください (このサイトは英語の場合があります)。

