---
title: 'セットアップで Exchange を読み取り専用ドメイン コントローラーにインストールできない_ComputerRODC: Exchange 2013 Help'
TOCTitle: セットアップで Exchange を読み取り専用ドメイン コントローラーにインストールできない_ComputerRODC
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 48269450
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# セットアップで Exchange を読み取り専用ドメイン コントローラーにインストールできない\_ComputerRODC

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 セットアップ プログラムは、インストール先のコンピューターが読み取り専用ドメイン コントローラー (RODC) であるため、インストールを続行できません。

読み取り専用ドメイン コントローラーは、Windows Server 2008 Active Directory の機能です。RODC は、ドメイン コントローラー インストール オプションの 1 つの種類で、物理セキュリティのレベルが低い可能性があるリモート サイトにインストールできます。

Exchange セットアップ プログラムは、インストール先のコンピューターへの書き込みアクセスを必要とします。

この問題を解決するには、RODC として指定されていないコンピューターをインストール先として選択し、セットアップを再度実行します。

