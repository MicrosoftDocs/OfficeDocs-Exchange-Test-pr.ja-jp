---
title: 'Exchange Server 2013 のパフォーマンスに関する推奨事項: Exchange 2013 Help'
TOCTitle: Exchange Server 2013 のパフォーマンスに関する推奨事項
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63892234
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 のパフォーマンスに関する推奨事項

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Exchange Server 2013 のパフォーマンスのチューニングとトラブルシューティングは、環境が適切にサイズ設定され、計画されているときに最も効果的です。Exchange 2013 は、基盤となるリソース インフラストラクチャを簡略化するために設計されましたが、メモリ、記憶域容量、および CPU 容量などのシステム リソースを大幅に消費する場合があります。

このセクションにある記事は、Exchange のパフォーマンス チームによって作成されました。これらの記事は、Exchange 製品グループからの専門知識およびカスタマー サポートの事例から学んだベスト プラクティスについて説明しています。これらの記事の目的は、Exchange 2013 で導入された変更の影響と、Exchange 2013 インフラストラクチャの適切なサイズ変更の重要性を理解していただくことです。さらに、お勧めの最適化機能やパフォーマンスの問題点を突き止めるためのガイダンスについても説明されています。

## Exchange 2013 および他のリソースにおけるアーキテクチャ上の変更

Exchange 2013 のアーキテクチャ上の変更については、TechNet および [Exchange チームのブログ](https://go.microsoft.com/fwlink/p/?linkid=35786) に既に記載されています。最初に、パフォーマンス コストとサイズ設定についてより深く理解するうえで考慮する必要のあるいくつかの高レベルの変更を取り上げます。次に、これらの重要な分野のより深い内容や背景に関する推奨された参照の一覧が下に記載されています。


> [!NOTE]
> 仮想環境における Exchange Server 2013 の展開に関するパフォーマンス最適化のガイダンスについては、「<A href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 仮想化</A>」を参照してください。



Exchange 2013 では、クライアント アクセス サーバーの役割は、ステートレス プロキシ サーバーです。クライアント アクセス サーバーの役割の主要な機能は、受信要求を認証し、それぞれの要求を適切なメールボックス サーバー (ユーザー メールボックスのアクティブ コピーをホストしているサーバー) にプロキシ処理することです。つまり、特定のプロトコルのために、クライアント アクセス サーバーと負荷分散装置の間の類似性を構成する必要がなくなりました。

Exchange 2013 のもう 1 つの注目すべき変更は、インフォメーション ストアにあります。インフォメーション ストアは現在 2 種類のプロセス、ホストとワーカーで構成しています。各データベース インスタンスは、独自の Microsoft.Exchange.Store.Worker.exe プロセスに関連付けられています。これにより、問題のあるデータベースの問題の分離を強化し、データベースの問題がパフォーマンスに及ぼす影響を、そのデータベースの 1 つのワーカー インスタンスだけに減らすことができます。

Microsoft Exchange Replication サービスは、メールボックス サーバーの役割に関連するすべての高可用性サービスを管理します。このレプリケーション サービスは、障害の監視や修正処理を実行する Active Manager コンポーネントをホストします。

以前のバージョンから Exchange 2013 環境をサイズ変更した影響を含む、アーキテクチャ上の変更に関する詳しい投稿については、「[Exchange 2013 Server の役割のアーキテクチャ](https://go.microsoft.com/fwlink/p/?linkid=523735)」を参照してください。

Exchange 2013 のアーキテクチャ上の変更や、関連する他の分野の背景情報の詳細については、次の項目を参照してください。

[Exchange Server 2013 アーキテクチャ](https://go.microsoft.com/fwlink/p/?linkid=523769)

[適切な計画: Exchange Server 2013 のサイズ設定シナリオ](https://go.microsoft.com/fwlink/p/?linkid=523773)

[Microsoft Exchange Server 2013 のパフォーマンスの監視とチューニング](https://go.microsoft.com/fwlink/p/?linkid=523774)

[Exchange Server 2013 の実装:(01) Exchange Server 2013 のアップグレードと展開](https://go.microsoft.com/fwlink/p/?linkid=523775)

[Exchange Server 2013 の実装:(02) 適切な計画:Exchange Server 2013 のサイズ設定](https://go.microsoft.com/fwlink/p/?linkid=523776)

[Exchange Server 2013 の実装:(03) Exchange Server 2013 の仮想化のベスト プラクティス](https://go.microsoft.com/fwlink/p/?linkid=523777)

[Exchange Server 2013 の実装:(04) Exchange アーキテクチャ:高可用性とサイトの復元](https://go.microsoft.com/fwlink/p/?linkid=523779)

[Exchange Server 2013 の実装:(05) Outlook 接続](https://go.microsoft.com/fwlink/p/?linkid=523781)

[優先するアーキテクチャ](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Exchange 2013 クライアント アクセス サーバーの役割](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Exchange Server 2013 の仮想化のベスト プラクティス](https://go.microsoft.com/fwlink/p/?linkid=523783)

[負荷分散](load-balancing-exchange-2013-help.md)

[Exchange Server 更新プログラム: ビルド番号とリリース日](https://technet.microsoft.com/ja-jp/library/hh135098\(v=exchg.150\))

[Exchange 2013 のリリース ノート](release-notes-for-exchange-2013-exchange-2013-help.md)

[Exchange 2013 の更新プログラム](updates-for-exchange-2013-exchange-2013-help.md)

[IIS 7.5、IIS 7.0、および IIS 6.0 での ASP.NET スレッドの使用量](https://go.microsoft.com/fwlink/p/?linkid=169626)

