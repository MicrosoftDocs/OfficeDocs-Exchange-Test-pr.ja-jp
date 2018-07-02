---
title: 'トランスポート ルールの新機能: Exchange 2013 Help'
TOCTitle: トランスポート ルールの新機能
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 48268985
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート ルールの新機能

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2014-10-03_

Microsoft Exchange Server 2013 で、トランスポート ルールにいくつかの改善が行われました。このトピックでは、主な変更点と機能拡張の一部について概要を説明します。トランスポート ルールの詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)」を参照してください。

## データ損失防止ポリシーのサポート

Exchange 2013 のデータ損失防止 (DLP) 機能を使用すると、組織は機密データの過失による公開を減らすことができます。トランスポート ルールは、DLP ポリシーを付帯および適用するルールの作成をサポートするように、更新されました。トランスポート ルールでの DLP サポートの詳細については、次のトピックを参照してください。

[機密情報ルールとトランスポート ルールの統合](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

## 新しい述語とアクション

トランスポート ルールの機能が新しい述語とアクションの追加により拡張されました。下記の各述語は、トランスポート ルールを作成するときに条件または例外として使用できます。

これらの新しい述語とアクションを使用する詳細については、「[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)」および「[トランスポート ルールのアクション](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)」を参照してください。

## 新しい述語

  -  
    **AttachmentExtensionMatchesWords**   特定の拡張子を持つ添付ファイルを含むメッセージを検出するために使用します。

  -  
    **AttachmentHasExecutableContent**   実行可能コンテンツ持つ添付ファイルを含むメッセージを検出するために使用します。

  -  
    **HasSenderOverride** 送信者が DLP ポリシー制限を上書きしたメッセージを検出するのに使用します。

  -  
    **MessageContainsDataClassifications**   メッセージ本文といずれかの添付ファイルの機密メッセージを検出するために使用します。使用できるデータ分類の一覧については、「[Exchange での機密情報の種類の検索基準：](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)」を参照してください。

  -  
    **MessageSizeOver**   全体のサイズが指定した制限以上であるメッセージを検出するために使用します。

  -  
    **SenderIPRanges**   特定の IP アドレス範囲セットから送信されたメッセージを検出するために使用します。

## 新しいアクション

  -  
    **GenerateIncidentReport**   指定した SMTP アドレスに送信されるインシデント レポートを生成します。アクションには、次の 2 つのいずれかの値を受け入れる *IncidentReportOriginalMail* と呼ばれるパラメーターもあります。IncludeOriginalMail または DoNotIncludeOriginalMail。

  -  
    **NotifySender**   DLP ポリシーに反するメッセージの送信者に通知する方法を制御します。送信者にただ単に通知してメッセージを通常どおりにルーティングすることを選択することも、メッセージを拒否して送信者に通知することも選択できます。

  -  
    **StopRuleProcessing**   メッセージに対して後続するすべてのルールの処理を停止します。

  -  
    **ReportSeverityLevel**   インシデント レポートで指定した重大度レベルを設定します。このアクションの値は、次のとおりです。情報、低、中、高、およびオフ。

  -  
    **RouteMessageOutboundRequireTLS**   組織外部にこのメッセージをルーティングするときにトランスポート層セキュリティ (TLS) 暗号化を必要とします。TLS 暗号化をサポートしていない場合、メッセージは拒否され、配信されません。

## トランスポート ルールの他の変更

  - **拡張された正規表現構文のサポート**Exchange 2013 のトランスポート ルールは、Microsoft.NET Framework の正規表現 (regex) 機能に基づいており、拡張された正規表現構文をサポートするようになりました。

  - **トランスポート ルール エージェントの呼び出し**   トランスポート ルールの Exchange 2013 での主なアーキテクチャ変更は、トランスポート ルール エージェントを onResolvedMessage で起動することです。以前のバージョンの Exchange では、ルール エージェントが onRoutedMessage で起動されました。この変更により、メッセージをルーティングする方法を変更できる TLS の要求など、新しいアクションを追加できるようになりました。Exchange 2013 のトランスポート ルール アーキテクチャの詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - **メッセージ追跡ログのトランスポート ルールの詳細情報**   トランスポート ルールの詳細情報は、メッセージ追跡ログに含まれるようになりました。これらの情報には、特定のメッセージに対して起動されたルール、およびこれらのルールの処理結果として実行されたアクションが含まれます。

  - **新しいルール監視機能**Exchange 2013 は、構成されるトランスポート ルールを監視し、ルールの作成時と通常の運用時の両方でこれらのルールを実行するコストを測定します。Exchange は、メール配信遅延の原因となっているルールを検出し、警告を生成できます。

