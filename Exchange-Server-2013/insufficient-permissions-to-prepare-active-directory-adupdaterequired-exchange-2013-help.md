---
title: 'Active Directory を準備するにはアクセス許可が不十分_ADUpdateRequired: Exchange 2013 Help'
TOCTitle: Active Directory を準備するにはアクセス許可が不十分_ADUpdateRequired
ms:assetid: 1412d8a1-605a-4b1e-bee3-0c97f2cc9e65
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.adupdaterequired(v=EXCHG.150)
ms:contentKeyID: 48269194
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory を準備するにはアクセス許可が不十分\_ADUpdateRequired

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

ドメインの準備を試みて失敗したため、Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange セットアップ プログラムを実行するには、Active Directory ディレクトリ サービスを Exchange Server 2007 用に変更してから、Active Directory 内のドメインを準備する必要があります。

**setup /PrepareAD** コマンドの実行に使おうとしていたアカウントは、Enterprise Admins グループに属しているようですが、このコマンドを実行するために必要なアクセス許可を持っていません。アカウントの有効期限が切れている可能性があります。

この問題を解決するには、ログオン ユーザーのアカウントが有効であり、Enterprise Admins グループに属していることを確認するか、またはこれらのアクセス許可を持つアカウントでログオンし、**setup /PrepareAD** を再実行します。

PrepareAD プロセスの実行方法の詳細については、Active Directory とドメインを準備する方法に関するページ ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)) を参照してください (このサイトは英語の場合があります)。

Microsoft Exchange に必要な Active Directory アクセス許可の詳細については、Exchange Server における Active Directory アクセス許可の操作についてのページ ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)) を参照してください (このサイトは英語の場合があります)。

