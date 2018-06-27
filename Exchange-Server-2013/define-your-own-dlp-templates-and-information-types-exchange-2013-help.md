---
title: '独自の DLP テンプレートおよび情報の種類の定義: Exchange Online Help'
TOCTitle: 独自の DLP テンプレートおよび情報の種類の定義
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 49896554
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 独自の DLP テンプレートおよび情報の種類の定義

 

_**適用先:**Exchange Online, Exchange Server 2013_

データ損失防止 (DLP)ポリシー テンプレートを、Microsoft Exchange Server 2013 からは切り離して XML ファイルとして開発し、Exchange 管理センターまたは Exchange 管理シェルを使用してインポートできます。ここでは、DLP ソリューション内部で使用するための DLP XML ファイルの作成とチューニングのプロセスおよび詳細について説明します。Exchange 管理センターから既存の DLP ポリシー テンプレートを使用してただちに作業を開始しルールをトランスポートしてメッセージをスキャンする方法が提供されているため、独自の DLP XML ファイルの開発は必須ではありません。

DLP ポリシー テンプレートに関連する管理タスクについては、「[DLP の手順](dlp-procedures-exchange-2013-help.md)」(Exchange Server 2013) または 「[DLP に関する手順](https://technet.microsoft.com/ja-jp/library/jj938003\(v=exchg.150\))」(Exchange Online) をご覧ください。


> [!NOTE]
> Exchange 2013: DLP は、Exchange エンタープライズ クライアント アクセス ライセンス (CAL) が必要なプレミアム機能です。CAL とサーバー ライセンスの詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Project のヘルプ</A>」を参照してください。<BR>Exchange Online:DLP は、Exchange Online プラン 2 サブスクリプションが必要なプレミアム機能です。詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online プランの比較</A>」を参照してください。




> [!IMPORTANT]
> このドキュメントでは、ビジネス モデルや、機密情報ルールを対象にしたファイル パッケージの作成や展開のガイドラインに関する情報についての推奨は行いません。また、そのようなルールの配布方法についても扱いません。また、カスタム開発ルールについての暗号化などの保護メカニズムやそのようなメカニズムの導入方法についても取り扱いません。



## ユーザーのニーズを満たすために情報タイプを拡張する

ここでは、Exchange 2013 にインポートして DLP ポリシーとして使用できる DLP ポリシー テンプレートと機密情報ルール パッケージ用の独自の XML ファイルの作成を開始するに当たって理解しておく必要があるコンセプトと XML スキーマ定義について説明します。

Microsoft Exchange の DLP を使用すると、組織固有のポリシーを機密情報に円滑に適用できます。DLP ソリューションの強さの主要な要因は、組織、規制ニーズ、地理またはその他のビジネス局面に固有の機密情報を正しく識別できることです。Microsoft は、ユーザーが簡単に操作を開始できるように製品内部でポリシー テンプレートや機密情報タイプを提供していますが、固有のビジネス ニーズによりカスタム データ損失防止ソリューションが必要になる場合があります。このため、Microsoft はユーザー独自の DLP ポリシー テンプレートを作成してインポートする方法や分類ルール パッケージ内部で独自の機密情報定義を作成してインポートする方法を提供しています。DLP ソリューションの精度は、誤検知 (正常なメッセージを異常と判断するか、異常なメッセージを正常と判断する) を最小化しながら高度な保護を提供する、機密情報検出エンジン用に正しいルール セットが構成されるかどうかによって決まります。

## 独自のDLP ポリシー テンプレートを開発する

独自の DLP ポリシー テンプレート XML ファイルを作成してインポートできます。Exchange で提供される DLP ソリューション拡張のためのこのアプローチにより、自身の DLP 要件をより完璧に満たす DLP ポリシーを作成できます。

カスタム テンプレートとそれに関連したポリシーを管理することは、Microsoft 提供のテンプレートに基づいて作成した DLP ポリシーを管理することに似ています。標準的な DLP ポリシー ライフサイクルでは、次の操作が行われます。

1.  独自の DLP ポリシー テンプレート、つまり、カスタム XML ファイルを作成します。詳しくは、「[DLP ポリシー テンプレート ファイルの作成](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)」を参照してください。

2.  カスタム テンプレートをインポートします。詳しくは、「[ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)」を参照してください。

3.  カスタム テンプレートに基づいて DLP ポリシーを作成します。詳しくは、「[テンプレートからの DLP ポリシーの作成](how-to-new-dlp-data-loss-prevention-policy-template.md)」を参照してください。

4.  手順 1 と 2 を繰り返すことによって、カスタム テンプレートを更新します。

5.  カスタム テンプレートを削除します。詳しくは、「[Remove-DlpPolicyTemplate](https://technet.microsoft.com/ja-jp/library/jj215739\(v=exchg.150\))」を参照してください。

独自のテンプレート開発に関わる XML スキーマ定義とコンセプトの詳細については、「[DLP ポリシー テンプレート ファイルの作成](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)」を参照してください。

## 分類ルール パッケージで独自の機密情報タイプと照合ロジックを開発する

分類ルール パッケージ内部で独自の機密情報定義を XML ファイルで作成して、独自の DLP ソリューションの一部としてインポートできます。機密情報検出エンジンは、クレジット カード番号、社会保障番号、企業の知的財産など、機密情報を識別するための洞察力に優れたコンテンツ分析機能を提供します。エンジンは、構成可能な命令セット、すなわちルールで制御され、内容をスキャンして分析します。ルールは、1 つにまとめられ分類ルールパッケージに組み込まれます。分類ルール パッケージは、標準化されたルール パッケージ XML スキーマ定義に準拠する XML ドキュメントです。独自の機密情報タイプと照合ロジックを開発する方法を次に示します。

1.  独自の機密情報タイプ、つまり、カスタム XML ファイルを作成します。詳しくは、「[機密情報のルール パッケージの作成](technical-description-of-xml-schema-for-dlp-rule-packages.md)」を参照してください。

2.  機密情報タイプをインポートします。詳しくは、「[New-ClassificationRuleCollection](https://technet.microsoft.com/ja-jp/library/jj218619\(v=exchg.150\))」を参照してください。

3.  情報タイプに基づいてカスタム テンプレートを作成します。詳しくは、「[機密情報のルール パッケージの作成](technical-description-of-xml-schema-for-dlp-rule-packages.md)」を参照してください。

4.  手順 1 と 2 を繰り返すことによって、カスタム テンプレートを更新します。

5.  カスタム テンプレートを削除します。詳しくは、「[Remove-ClassificationRuleCollection](https://technet.microsoft.com/ja-jp/library/jj218670\(v=exchg.150\))」を参照してください。

ルール パッケージの詳細については、「[機密情報のルール パッケージの作成](technical-description-of-xml-schema-for-dlp-rule-packages.md)」および「[ルール パッケージの照合の方法と手法](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md)」を参照してください。

## ルール パッケージでのルール タイプの理解

ルール パッケージ内部のルールは、ドライバーの免許証番号の検索ルールなど、内容に含まれる明確に定義された特性を検出するためのプロセスを構成します。ルールには、次の 2 つの主要タイプがあります。エンティティとアフィニティ。

*エンティティ* ルールは、米国の社会保障番号など、(多くの場合、法的に規定され) 明確に定義された識別子を対象にしています。エンティティは、カウントが可能なパターンの集まりで表現されます。パターンは、明示的なプライマリ照合識別子との一致の集合を定義します。エンティティの例は、ドライバーの免許です。

*アフィニティ* ルールは、企業の財務報告など特定のタイプのドキュメントを対象にしています。アフィニティは、独立した証拠の集合で表現されます。証拠は、特定の近さになっている、必要な一致物の集計です。アフィニティの例としては、米国のサーベンス・オクスリー法があります。

## 詳細情報

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/ja-jp/library/jj218619\(v=exchg.150\))

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange Server 2013

[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))Exchange Online

[Exchange での機密情報の種類の検索基準：](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

