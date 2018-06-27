---
title: 'IIS ログおよび Log Parser Studio レポート: Exchange 2013 Help'
TOCTitle: IIS ログおよび Log Parser Studio レポート
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63907301
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS ログおよび Log Parser Studio レポート

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

## Log Parser Studio のレポートの分析

Log Parser Studio は、IIS (Internet Information Services) を含むさまざまな種類のログ ファイルからレポートを検索し、作成するためのユーティリティです。Log Parser Studio は Log Parser 2.2 に基づいて構築され、関連する SQL クエリを簡単に作成および管理するための完全なユーザー インターフェイスが用意されています。

[Log Parser Studio をダウンロード](https://go.microsoft.com/fwlink/p/?linkid=524244) し、ブログの投稿「[Log Parser Studio をお使いになる前に](https://go.microsoft.com/fwlink/p/?linkid=524243)」を参照してください。

Exchange 2013 では、すべてのトラフィックが IIS で処理される必要があることに注意してください。つまり、IIS ログの分析が、サーバーに当たる接続の数、接続に関するプロトコル固有の情報量、およびパフォーマンスに最も影響を及ぼすユーザー数の全体像をつかむ最善の方法です。Exchange 2013 のパフォーマンスの問題のトラブルシューティングを目的として、20 を超える新しいレポートが Log Parser Studio 用に開発されました。

## Exchange 2013 のパフォーマンスの問題のための Log Parser Studio レポート

Exchange 2013 環境内の全体的な負荷について包括的に理解するため、次のレポートを使用し、それぞれのサーバーに対する番号を比較します。

ここに示した Log Parser Studio のレポートが格納されている .zip ファイルおよび他のトラブルシューティングに関連するレポートは、[ここからダウンロード](https://go.microsoft.com/fwlink/p/?linkid=524245)できます。

  - **IIS:1 時間あたりの要求**。同時に両方ではなく、既定の Web サイト (W3SVC1 ディレクトリ) またはバックエンド Web サイト (W3SVC2 ディレクトリ) のいずれかから IIS ログにフィードします。

  - **ACTIVESYNC\_WP:割合ごとのクライアント**。ユーザー エージェントおよび要求の総数に対する各クライアントの割合によって区分されたすべての ActiveSync 要求を計算します。

  - **ACTIVESYNC\_WP:1 時間あたりの要求 (CSV)**。1 時間あたりの ActiveSync 要求を一覧表示し、CSV ファイルにその結果を送信します。

  - **ACTIVESYNC\_WP:ユーザーごとの要求 (CSV)**。ユーザーごとの ActiveSync 要求を一覧表示し、CSV ファイルにその結果を送信します。

  - **ACTIVESYNC\_WP:ユーザーごとの要求 (上位 10k)**。上位 10,000 ユーザーの各ユーザーごとの ActiveSync 要求を一覧表示します。

  - **ACTIVESYNC\_WP:上位の話者 (CSV)**。上位の ActiveSync クライアントを、要求回数の多い方から順に一覧表示し、CSV ファイルにその結果を送信します。

  - **EWS\_WP:割合ごとのクライアント**。ユーザー エージェントおよび要求の総数に対する各クライアントの割合によって区分されたすべての EWS 要求を計算します。

  - **EWS\_WP:1 時間あたりの要求 (CSV)**。1 時間あたりの EWS 要求の総数を一覧表示します。

  - **EWS\_WP:ユーザーごとの要求 (CSV)**。ユーザーごとの EWS 要求を一覧表示し、CSV ファイルにその結果を送信します。

  - **EWS\_WP:ユーザーごとの要求 (上位 10k)**。上位 10,000 ユーザーの各ユーザーごとの EWS 要求を一覧表示します。

  - **EWS\_WP:上位の話者 (CSV)**。上位の EWS クライアントを、要求回数の多い方から順に一覧表示します。

  - **OLA\_WP:ユーザーごとのエラー、1 時間あたりのエラー、1 日あたりのエラー**。要求の数ごとの Outlook Anywhere ユーザー。

  - **OLA\_WP:1 時間あたりの要求**。1 時間あたりの Outlook Anywhere 要求を一覧表示します。

  - **OLA\_WP:1 時間あたりの要求、ユーザーごとの要求**。Outlook Anywhere の 1 時間あたりの要求と、ユーザーごとの要求を一覧表示します。

  - **OLA\_WP:ユーザーごとの要求 (CSV)**。ユーザーごとの Outlook Anywhere 要求を一覧表示します。

  - **OLA\_WP:ユーザーごとの要求 (上位 10k)**。上位 10,000 ユーザーの各ユーザーごとの Outlook Anywhere 要求を一覧表示します。

  - **OLA\_WP:上位の話者**。上位の Outlook Anywhere クライアントを、要求回数の多い方から順に一覧表示します。

  - **OWA\_WP:割合ごとのクライアント**。ユーザー エージェントおよび要求の総数に対する各クライアントの割合によって区分されたすべての OWA 要求を計算します。

  - **OWA\_WP:1 時間あたりの要求 (CSV)**。1 時間あたりの OWA 要求を一覧表示し、CSV ファイルにその結果を送信します。

  - **OWA\_WP:ユーザーごとの要求 (CSV)**。ユーザーごとの OWA 要求を一覧表示し、CSV ファイルにその結果を送信します。

  - **OWA\_WP:ユーザーごとの要求 (上位 10k)**。上位 10,000 ユーザーの各ユーザーごとの OWA 要求を一覧表示します。

  - **OWA\_WP:上位の話者 (CSV)**。上位の OWA クライアントを、要求回数の多い方から順に一覧表示し、CSV ファイルにその結果を送信します。

