---
title: 'Exchange Search: Exchange 2013 Help'
TOCTitle: Exchange Search
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52057849
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Search

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-09-17_

メールボックスのサイズが大きくなり、メッセージや添付ファイルなど、メッセージボックスに保存されるデータ量が増加している中で、ユーザーが必要なメッセージを素早く検索できることが不可欠になっています。[Exchange 2013 のインプレース アーカイブ](in-place-archiving-in-exchange-2013-exchange-2013-help.md) は、頻繁にアクセスする古いアイテムをアーカイブに移動することによって, .pst ファイルの使用頻度を減らすか、または不要にします。その結果、ユーザーはメールボックスにより多くのデータを保存できるようになり、ユーザーのプライマリ メールボックスとアーカイブ メールボックス全体の検索機能が重要な生産性向上ツールになります。[インプレース電子情報開示 (eDiscovery)](in-place-ediscovery-exchange-2013-help.md) によって、権限のあるユーザーが社内およびクラウドベースの Exchange 組織全体にわたってメールボックスの内容を検索し、電子情報開示 (eDiscovery) 要求、法的監査、または内部調査に対応できるようになります。インプレース電子情報開示では、Exchange Search によって作成されたコンテンツ インデックスも使用します。

Exchange Search は、Exchange Server 2003 で利用可能なフルテキスト インデックス処理とは異なります。パフォーマンス、コンテンツ インデックス処理、および検索で機能強化が行われました。新しいアイテムが作成されるか、またはメールボックスに配信されると即座にトランスポート パイプラインにインデックスが作成され、ユーザーが速く、安定した、そしてより信頼できる方法でメールボックス データを検索できる方法が提供されます。コンテンツ インデックス作成は、既定で有効になっているため、初期のセットアップや構成は不要です。

Exchange Search に関連する管理タスクについては、「[Exchange Search の手順](exchange-search-procedures-exchange-2013-help.md)」を参照してください。

## 新機能

Exchange 2013 では、Exchange Search に次の変更が加えられています。

  - 基盤となるコンテンツ インデックス作成エンジンが Microsoft Search Foundation に置き換えられたことで、パフォーマンスと機能が向上し、これが Exchange と SharePoint 共通の基盤となるコンテンツ インデックス作成エンジンとして機能します。ただし、管理インターフェイスは同じです。

  - Search Foundation は、既定では、電子メールの添付ファイルとして最も一般的なファイル形式を処理します。Exchange Search のために Microsoft Office フィルター パックをインストールする必要はありません。Exchange Search によって処理されるファイル形式の一覧については、「[Exchange Search によってインデックス処理されるファイル形式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)」を参照してください。
    
    IFilter をインストールすることによって、Exchange 2010 のようにあらゆるファイル形式をサポートすることができます。

  - コンテンツ インデックス作成は、トランスポート パイプラインでメッセージを処理するため、より効率的です。その結果、複数の受信者または配信グループに宛てるメッセージが 1 回で処理されます。メッセージに注釈ストリームを添付することで、リソース消費を削減しながらコンテンツ インデックス作成を大幅に高速化することができます。

