---
title: 'スキーマ マスターが Windows Server 2003 Service Pack 1 以上を実行していない_DomainControllerIsOutOfSite: Exchange 2013 Help'
TOCTitle: スキーマ マスターが Windows Server 2003 Service Pack 1 以上を実行していない_DomainControllerIsOutOfSite
ms:assetid: 5edbe0b8-7610-4a52-aaaa-38c6a99e7e53
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.domaincontrollerisoutofsite(v=EXCHG.150)
ms:contentKeyID: 48269564
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# スキーマ マスターが Windows Server 2003 Service Pack 1 以上を実行していない\_DomainControllerIsOutOfSite

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

FSMO (Flexible Single Master Operation) とも呼ばれる、Active Directory ディレクトリ サービス スキーマ マスターの役割が割り当てられたドメイン コントローラーで、Microsoft Windows Server 2003 Service Pack 1 (SP1) 以降のバージョンが実行されていないため、Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムを実行するには、スキーマ FSMO として機能するドメイン コントローラーで Windows Server 2003 SP1 以降のバージョンが実行されている必要があります。

FSMO は、Active Directory スキーマに対するすべての更新と変更を制御します。

この問題を解決するには、次のいずれかの操作を行います。

  - FSMO ドメイン コントローラーを Windows Server 2003 SP1 以降のバージョンにアップグレードした後、Microsoft Exchange セットアップ プログラムを再実行します。

  - Microsoft Windows Server 2003 Service Pack 1 (SP1) 以降のバージョンを実行している FSMO ドメイン コントローラーが Exchange 組織内にある場合は、その FSMO ドメイン コントローラーを指す /domaincontroller パラメーターを指定して Exchange 2007 セットアップ プログラムを実行します。
    
    \[*/DomainController*、または */dc\<FQDN of domain controller\>*\]
    
    */DomainController* パラメーターを使用して、セットアップ時に Active Directory との読み書きに使用するドメイン コントローラーを指定します。NetBIOS 形式または完全修飾ドメイン名 (FQDN) 形式を使用できます。

Windows Server 2003 の最新の Service Pack の入手については、Windows Server TechCenter のページ (英語ページの可能性があります) ([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315)) を参照してください。

Exchange Server 2007 セットアップ プログラムのパラメーターの詳細については、Exchange Server 2007 製品ドキュメントの、Exchange 2007 を無人インストールする方法についてのページ ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)) を参照してください (このサイトは英語の場合があります)。

