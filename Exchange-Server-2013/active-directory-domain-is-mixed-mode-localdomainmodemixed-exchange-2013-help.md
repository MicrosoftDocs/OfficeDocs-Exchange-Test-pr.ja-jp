---
title: 'Active Directory ドメインが混合モードである_LocalDomainModeMixed: Exchange 2013 Help'
TOCTitle: Active Directory ドメインが混合モードである_LocalDomainModeMixed
ms:assetid: a6affcfe-7264-455b-8e5c-683fa87383f1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.localdomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 48269899
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory ドメインが混合モードである\_LocalDomainModeMixed

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

既存の Active Directory ドメインが Microsoft Windows® 2000 Server ネイティブ モード以上に設定されていないため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange 2007 セットアップ プログラムでは、Windows 2000 Server ネイティブ モード以上のドメインにのみ存在できるユニバーサル セキュリティ グループが作成されます。

この問題を解決するには、次の手順に従って、ドメインの機能レベルを Windows 2000 Server ネイティブ レベル以上に上げてから、Exchange 2007 セットアップ プログラムを再実行します。

**ドメインの機能レベルを上げるには**

1.  \[Active Directory ドメインと信頼関係\] を開きます。

2.  コンソール ツリーで、機能を上げるドメインを右クリックし、**\[ドメインの機能レベルを上げる\]** をクリックします。

3.  **\[利用可能なドメインの機能レベルを選択してください\]** で、次のいずれかの手順を使用します。
    
      - ドメインの機能レベルを Windows 2000 Server ネイティブに上げるには、**\[Windows 2000 ネイティブ\]**、**\[上げる\]** の順にクリックします。
    
      - ドメインの機能レベルを Windows Server® 2003 に上げるには、**\[Windows Server 2003\]**、**\[上げる\]** の順にクリックします。


> [!NOTE]
> <BR>Windows NT® 4.0 以前を実行しているドメイン コントローラーを使用している場合、または使用する予定の場合は、ドメインの機能レベルを Windows 2000 Server ネイティブに上げないでください。ドメインの機能レベルを Windows 2000 Server ネイティブに設定した後で、Windows 2000 Server 混在に戻すことはできません。<BR>Windows NT 4.0 以前または Windows 2000 Server を実行しているドメイン コントローラーを使用している場合、または使用する予定の場合は、ドメインの機能レベルを Windows Server 2003 に上げないでください。ドメインの機能レベルを Windows Server 2003 に設定した後で、Windows 2000 Server 混在または Windows 2000 Server ネイティブに戻すことはできません。




