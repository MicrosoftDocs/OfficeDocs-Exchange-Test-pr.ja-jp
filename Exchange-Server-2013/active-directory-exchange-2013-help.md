---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 49896358
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange Server 2013 では、Active Directory を使用して、ディレクトリ情報を格納して Windows と共有します。Exchange 2013 用の Active Directory フォレスト設計は、次に説明するいくつかの点を除き、Exchange Server 2010 に似ています。

## Active Directory ドライバー

Active Directory ドライバーは Microsoft Exchange のコア コンポーネントであり、Exchange サービスでの Active Directory ドメイン サービス (AD DS) データの作成、変更、削除、およびクエリを可能にします。Exchange 2013 では、Active Directory へのすべてのアクセスは Active Directory ドライバー自体を使用して行います。これまで Exchange 2010 では、DSAccess が SMTP、MTA (メッセージ転送エージェント)、および Exchange ストアなどのコンポーネントに対するディレクトリ参照サービスを提供していました。

また、Active Directory ドライバーは Microsoft ExchangeActive Directory トポロジ (MSExchangeADTopology) を利用しています。このトポロジは、Active Directory ドライバーでディレクトリ サービス アクセス (DSAccess) トポロジ データを使用できるようにします。このデータには、利用できるドメイン コントローラーと Exchange 要求を処理できるグローバル カタログ サーバーの一覧が含まれています。Active Directory ドライバーの詳細については、「[Active Directory ドメイン サービス](https://go.microsoft.com/fwlink/p/?linkid=110942)」を参照してください。

## Active Directory のスキーマの変更点

Exchange 2013 により、新しい属性が Active Directory ドメイン サービス スキーマに追加され、既存のクラスおよび属性も変更されています。Exchange 2013 をインストールする際の Active Directory の変更点の詳細については、「[Exchange 2013 Active Directory スキーマの変更](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)」を参照してください。

## 詳細情報

Active Directory へのアクセスを計画できるように、Exchange 2013 が Active Directory に情報を格納し、Active Directory から情報を取得する方法については、「[Active Directory へのアクセス](access-to-active-directory-exchange-2013-help.md)」を参照してください。

Active Directory フォレスト設計の詳細については、「[Active Directory ドメイン サービスの展開を計画する](https://go.microsoft.com/fwlink/p/?linkid=264957)」を参照してください。

Active Directory ドメイン内で Windows を実行するコンピューターおよび名前空間に不整合があるドメイン内での Exchange 2013 の展開の詳細については、「[名前空間の不整合のシナリオ](disjoint-namespace-scenarios-exchange-2013-help.md)」を参照してください。

