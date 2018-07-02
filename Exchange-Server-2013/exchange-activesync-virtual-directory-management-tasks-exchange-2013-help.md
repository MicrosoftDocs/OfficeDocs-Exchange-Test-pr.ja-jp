---
title: 'Exchange ActiveSync 仮想ディレクトリの管理タスク: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 仮想ディレクトリの管理タスク
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 49896547
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync 仮想ディレクトリの管理タスク

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-05_

Exchange Server 2013 の Exchange ActiveSync アプリケーション設定のいくつかは、Exchange ActiveSync 仮想ディレクトリを介して管理できます。 仮想ディレクトリは、インターネット インフォメーション サービス (IIS) が Exchange ActiveSync などの Web アプリケーションへのアクセスを許可するために使用します。 Exchange ActiveSync で管理できる仮想ディレクトリ設定には、認証、セキュリティ、レポート作成などがあります。

## Exchange ActiveSync 仮想ディレクトリ設定

Exchange ActiveSync 仮想ディレクトリでは、次のプロパティと設定を変更できます。

  - **InternalURL** InternalURL は、内部クライアントが仮想ディスクへのアクセスに使用できる URL です。 InternalURL は通常、https://servername/Microsoft-Server-ActiveSync の形式で指定されます。 たとえば、サーバーの NetBIOS 名が Sequoia の場合、InternalURL は https://sequoia/Microsoft-Server-ActiveSync になります。

  - **ExternalURL** ExternalURL は、外部クライアントが仮想ディレクトリへのアクセスに使用できる URL です。この URL には、内部ネットワークの外からアクセスします。たとえば、ExternalURL として https://www.contoso.com/ を指定できます。

  - **Authentication settings**Exchange ActiveSync 仮想ディレクトリで構成できる認証方式は 2 つあり、基本認証とクライアント証明書認証です。

