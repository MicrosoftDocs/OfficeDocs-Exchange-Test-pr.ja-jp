---
title: 'データベースの移植性: Exchange 2013 Help'
TOCTitle: データベースの移植性
ms:assetid: 387b727a-ce51-4910-b5c4-613c693fa5bd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876873(v=EXCHG.150)
ms:contentKeyID: 51407517
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データベースの移植性

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2017-01-30_

データベースの移植性は、同じデータベース スキーマ バージョンを使用したデータベースがあり、Exchange 2013 を実行している同じ組織の他のメールボックス サーバーに、Microsoft Exchange Server 2013 メールボックス データベースを移動またはマウントできる機能です。以前のバージョンの Exchange のメールボックス データベースは、Exchange 2013 を実行しているメールボックス サーバーに移動できません。データベースの移植性を使用すると、回復プロセスでのいくつかのエラーの発生しやすい手動による手順をなくすことで、信頼性が強化されます。また、さまざまな障害のシナリオで、データベースの移植性によって回復時間全体が短縮されます。

データベースの移植性を使用してメールボックス データベースを回復する場合は、ソースとターゲットの Exchange サーバー上のオペレーティング システムのバージョンと Exchange Server のバージョンが同じである必要があります。 たとえば、以前に Exchange 2013 メールボックス データベースが Windows Server 2012 を実行するサーバーにマウントされていた場合、データベースの移植性は、Windows Server 2012 と Exchange 2013 の両方を実行するサーバーにデータベースを移行する場合にのみ機能します。

データベースの移植性機能を使用してデータベースを回復する方法については、「[データベースの移植性を使用して、メールボックス データベースを移動する](move-a-mailbox-database-using-database-portability-exchange-2013-help.md)」を参照してください。

