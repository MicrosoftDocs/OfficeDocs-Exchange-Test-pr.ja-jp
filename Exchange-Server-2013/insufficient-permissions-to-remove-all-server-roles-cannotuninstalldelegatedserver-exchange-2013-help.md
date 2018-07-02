---
title: 'すべてのサーバー役割を削除するにはアクセス許可が不十分_CannotUninstallDelegatedServer: Exchange 2013 Help'
TOCTitle: すべてのサーバー役割を削除するにはアクセス許可が不十分_CannotUninstallDelegatedServer
ms:assetid: 214ae6f3-15e7-4337-99e8-40f9547c8e0c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.cannotuninstalldelegatedserver(v=EXCHG.150)
ms:contentKeyID: 48269266
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# すべてのサーバー役割を削除するにはアクセス許可が不十分\_CannotUninstallDelegatedServer

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

すべてのサーバーの役割をアンインストールしようとして失敗したため、Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムを実行するには、すべてのサーバーの役割をアンインストールためにログオンするユーザーが、Exchange Organization Administrators グループまたは Enterprise Admins グループのメンバーである必要があります。

この問題を解決するには、ログオン ユーザーに Exchange Organization Administrator のアクセス許可を与えるか、このユーザーを Enterprise Admins グループに登録します。または、これらのアクセス許可を持つアカウントを使用してログオンした後、Exchange 2007 セットアップ プログラムを再実行します。

Microsoft Exchange に必要な Active Directory アクセス許可の詳細については、Exchange Server における Active Directory アクセス許可の操作についてのページ ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)) を参照してください (このサイトは英語の場合があります)。

