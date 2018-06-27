---
title: 'Active Directory が存在しないか接続できない: Exchange 2013 Help'
TOCTitle: Active Directory が存在しないか接続できない
ms:assetid: 56adb6fe-ecb8-4a7f-b440-89aa401c28b7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.cannotaccessad(v=EXCHG.150)
ms:contentKeyID: 48269520
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory が存在しないか接続できない

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2016-12-09_

有効な Active Directory ディレクトリ サービス サイトと連絡できないため、Microsoft Exchange Server 2013 セットアップ プログラムは作業を続行できません。セットアップ プログラムは、Exchange がインストールされているサーバーが Active Directory で構成名前付けコンテキストを検出できることを要求します。

この問題を解決するには、Exchange セットアップ プログラムを実行するユーザー アカウントが Active Directory ユーザーであることを確認してから、セットアップ プログラムを再度実行してください。これで問題が解決されない場合は、以下のトピックに説明がある dcdiag.exe および repadmin.exe サポート ツールの使用に関するガイダンスに従って、さらに問題を診断します。

Active Directory のトラブルシューティングおよび Exchange の構成の詳細については、以下のトピックを参照してください。

  - [Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)

  - [Active Directory ドメイン サービスのトラブルシューティングを行う](https://go.microsoft.com/fwlink/p/?linkid=272144)

  - [トラブルシューティングのためにコンピューターを構成する](https://go.microsoft.com/fwlink/p/?linkid=272141)

  - [Active Directory レプリケーションの問題に関するトラブルシューティングを行う](https://go.microsoft.com/fwlink/p/?linkid=272142)

  - [Repadmin を使用して Active Directory レプリケーションの監視とトラブルシューティングを行う](https://go.microsoft.com/fwlink/p/?linkid=272143)

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

