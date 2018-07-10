---
title: 'ユニファイド メッセージング言語パックをアンインストールする_AdditionalUMLangPackExists: Exchange 2013 Help'
TOCTitle: ユニファイド メッセージング言語パックをアンインストールする_AdditionalUMLangPackExists
ms:assetid: 3a7e2621-0553-44f5-8029-c72fea25af3c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.additionalumlangpackexists(v=EXCHG.150)
ms:contentKeyID: 48269373
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユニファイド メッセージング言語パックをアンインストールする\_AdditionalUMLangPackExists

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

ユニファイド メッセージング サーバーの役割のアップグレードに失敗したため、Microsoft Exchange Server 2007 セットアップ プログラムを続行できません。

Exchange のセットアップ時には、ユニファイド メッセージング サーバーの役割の言語パックを、US 英語の言語パックを除いてすべてアンインストールしてから、ユニファイド メッセージング サーバーの役割のアップグレードを続行する必要があります。

Exchange 2007 に付属するユニファイド メッセージング (UM) 言語パックには、特定言語用の録音済みのプロンプトと、音声合成 (TTS) 変換サポートが含まれています。

Exchange 2007 UM 言語パックにより、発信者と Outlook Voice Access ユーザーは、複数の言語でユニファイド メッセージング システムと対話できます。

新しい言語パックをインストールできるように、既存の US 英語以外の言語パックをアンインストールする必要があります。

この問題を解決するには、ユニファイド メッセージング サーバーの役割の言語パックを、US 英語の言語パック以外はすべてアンインストールしてから、Exchange 2007 セットアップ プログラムを再実行します。

ユニファイド メッセージング サーバーの役割言語パックのアンインストールの詳細については、Exchange 2007 製品ドキュメントの「[ユニファイド メッセージング サーバーからユニファイド メッセージング言語パックを削除する方法](https://go.microsoft.com/fwlink/?linkid=85973)」を参照してください。

