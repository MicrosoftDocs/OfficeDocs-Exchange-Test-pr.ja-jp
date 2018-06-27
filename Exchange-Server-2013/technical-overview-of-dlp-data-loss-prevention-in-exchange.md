---
title: 'データ損失防止: Exchange Online Help'
TOCTitle: データ損失防止
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 48269052
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# データ損失防止

 

_**適用先:**Exchange Online, Exchange Server 2013_

Exchange Server 2013 と Exchange Online の DLP ポリシーについて説明し、これらのポリシーに含まれている機能と、それらの機能をテストする方法を示します。また、Exchange の DLP の新機能について説明します。

データ損失防止 (DLP) は、エンタープライズ メッセージ システムにとって重要な問題です。機密データを含むビジネスに不可欠な通信において、電子メールが広範に使用されているためです。作業者の生産性を阻害せずに、このようなデータに準拠要件を適用して電子メールの使用を管理するために、DLP 機能では機密データをかつてないほど容易に管理できます。DLP の概念の概要を理解するには、次のビデオをご覧ください。

> [!VIDEO https://www.microsoft.com/ja-jp/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

DLP ポリシーは、トランスポート ルール、アクション、および例外から構成される一連の条件を含む単純なパッケージです。これらを管理者が Exchange 管理センター (EAC) で作成し、電子メール メッセージと添付ファイルをフィルター処理するためにアクティブにします。管理者は DLP ポリシーを作成できますが、アクティブにしないように選択できます。これにより、メール フローに影響を与えずにポリシーをテストすることができます。DLP ポリシーでは、既存のトランスポート ルールの全機能を使用できます。実際 DLP の新機能を実現するために、Microsoft Exchange Server 2013 および Exchange Online には、いくつかの新しい種類のトランスポート ルールが作成されています。トランスポート ルールの重要な新機能の 1 つに、メール フロー処理に組み込むことができる、機密情報を分類するための新しい方法があります。この新しい DLP 機能は、キーワード一致、辞書一致、正規表現評価、その他のコンテンツ検査を通じて深いコンテンツ分析を実行し、組織の DLP ポリシーに違反するコンテンツを検出します。最新リリースの Exchange Online および Exchange 2013 SP1 は [ドキュメント フィンガープリンティング](overview-of-document-fingerprinting-in-exchange.md) を追加するので、標準フォームの機密情報を検出するために役立ちます。トランスポート ルールの詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)」または「[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\)) (Exchange Online)」および「[機密情報ルールとトランスポート ルールの統合](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)」を参照してください。Exchange 管理シェル コマンドレットを使用して、DLP ポリシーを管理することもできます。ポリシーと準拠のコマンドレットの詳細については、「[ポリシーとコンプライアンスのコマンドレット](https://technet.microsoft.com/ja-jp/library/dd298082\(v=exchg.150\))」を参照してください。

カスタマイズ可能な DLP ポリシー自身に加えて、電子メール送信者が違反メッセージを送信する前でも、送信者に管理のポリシーに違反する可能性があることを通知することもできます。これは、ポリシー ヒントを構成することで実現できます。ポリシー ヒントはメール ヒントに似ていて、メッセージを作成しているユーザーにそれがポリシー違反の可能性があることを通知する短いメモを、Microsoft Outlook 2013 クライアントで提示するように構成できます。最新リリースの Exchange Online および Exchange 2013 SP1 では、ポリシー ヒントが Outlook Web App および OWA for Devices にも表示されます。詳細については、「[ポリシー ヒント](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)」を参照してください。


> [!NOTE]
> Exchange Online:DLP は、Exchange Online プラン 2 サブスクリプションが必要なプレミアム機能です。詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online プランの比較</A>」を参照してください。<BR>Exchange 2013: DLP は、Exchange エンタープライズ クライアント アクセス ライセンス (CAL) が必要なプレミアム機能です。CAL とサーバー ライセンスの詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Project のヘルプ</A>」を参照してください。<BR><STRONG>Exchange Enterprise CAL とサービス：</STRONG> メールボックスの一部が社内に置かれ、一部が Exchange Online に置かれているハイブリッド展開を持つ Exchange Enterprise CAL とサービスのお客様の場合、注目する必要がある特徴的な動作があります。それは DLP ポリシーが Exchange Online に適用されることです。このため、ある社内ユーザーから別の社内ユーザーに送信されたメッセージには DLP ポリシーが適用されません。メッセージは社内インフラストラクチャから外部に発信されないためです。



データ損失防止に関連する管理タスクについては、「[DLP の手順](dlp-procedures-exchange-2013-help.md) (Exchange 2013)」または「[DLP に関する手順](https://technet.microsoft.com/ja-jp/library/jj938003\(v=exchg.150\)) (Exchange Online)」を参照してください。

**目次**

機密データを保護するポリシーの確立

DLP ポリシー内の機密情報の種類

従来のメッセージ分類に沿った機密情報の検出

ドキュメントの指紋による機密フォーム データの検出

機密コンテンツの可能性についてユーザーに通知するポリシー ヒント

DLP 処理メッセージに関する情報

インストールの前提条件

詳細情報

## 機密データを保護するポリシーの確立

データ損失防止機能を使用すると、ポリシーの条件内で定義した多数のカテゴリの機密情報 (個人識別番号やクレジット カード番号など) の特定と監視に役に立ちます。独自のカスタム ポリシーやトランスポート ルールを定義したり、Microsoft によって提供される事前に定義された DLP ポリシー テンプレートを使用してすぐに作業を開始したりできます。付属のポリシー テンプレートの詳細については、「[Exchange で提供される DLP ポリシー テンプレート](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)」を参照してください。*ポリシー テンプレート*には、メッセージの検査に役立つ実際の DLP ポリシーを作成および保存するために選択できる一連の条件、ルール、アクションが含まれています。ポリシー テンプレートとは、データ損失防止のニーズを満たすポリシーを作成するために、その中から独自の特定のルールを選択または作成できるモデルです。

DLP の使用を開始するには、次の 3 つの異なる方法があります。

1.  **Microsoft が提供する定義済みテンプレートを適用する。**   DLP ポリシーの使用を開始する最も早い方法は、テンプレートを使用して新しいポリシーを作成および実装することです。テンプレートを使用することで、新しいルールのセットを一から作成する手間を省けます。確認するデータの種類や対応する法令遵守規定を把握しておく必要があります。このようなデータの処理に関する組織の要望を把握しておくことも必要です。詳細については、「[Exchange で提供される DLP ポリシー テンプレート](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)」および「[テンプレートからの DLP ポリシーの作成](how-to-new-dlp-data-loss-prevention-policy-template.md)」を参照してください。

2.  **組織外から事前に作成済みのポリシー ファイルをインポートする。**   独立ソフトウェア ベンダーによってユーザーのメッセージング環境外で作成されたポリシーをインポートできます。こうすることで、ユーザーのビジネス環境に合うように DLP ソリューションを拡張できます。詳細については、「[Microsoft パートナーからのポリシー テンプレート](policy-templates-from-microsoft-partners-exchange-2013-help.md)」、「[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)」、および「[ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)」を参照してください。

3.  **既存の条件がないカスタム ポリシーを作成する。**   企業によっては、メッセージング システム内に特定の種類のデータが存在し、このようなデータを監視する独自の要件がある可能性があります。まったく独力でカスタム ポリシーを作成して、固有のメッセージ データのチェックと処理を開始することができます。このようなカスタム ポリシーを作成するために DLP ポリシーを適用する環境の要件と制約を把握する必要があります。詳細については、「[カスタム DLP ポリシーの作成](create-a-custom-dlp-policy-exchange-2013-help.md)」を参照してください。

ポリシーを追加したら、そのルールの確認と変更、ポリシーの非アクティブ化、ポリシーの完全な削除を行うこともできます。これらの操作の手順については、「[DLP ポリシーの管理](manage-dlp-policies-exchange-2013-help.md)」を参照してください。

## DLP ポリシー内の機密情報の種類

DLP ポリシーを作成または変更する際には、機密情報を確認するルールを含めることができます。「[Exchange での機密情報の種類の検索基準：](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)」に記載されている機密情報の種類がポリシー内で使用できます。アクションの実行をトリガする検出回数や実行するアクションなど、ポリシー内に設定する条件は、特定のポリシー要件に合わせて独自の新しいポリシー内でカスタマイズできます。DLP ポリシーの作成の詳細については、「[カスタム DLP ポリシーの作成](create-a-custom-dlp-policy-exchange-2013-help.md)」を参照してください。各種トランスポート ルールの詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)」、または「[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\)) (Exchange Online)」を参照してください。

機密情報に関連するルールを簡単に利用できるようにするために、Microsoft ではいくつかの機密情報の種類を含めたポリシー テンプレートを用意しました。ただし、このポリシー テンプレートは、組織内で最も一般的な種類のコンプライアンス関連データに重点を置くように設計されているため、ここで示す機密情報の種類の中にはポリシー テンプレートに含めることができないものもあります。あらかじめ組み込まれているテンプレートの詳細については、「[Exchange で提供される DLP ポリシー テンプレート](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)」を参照してください。組織用の DLP ポリシーを数多く作成し、さまざまな種類の情報を調査できるようにすべてを有効にすることができます。既存のテンプレートに基づかない DLP ポリシーを作成することもできます。このようなポリシーを作成する場合は、「[カスタム DLP ポリシーの作成](create-a-custom-dlp-policy-exchange-2013-help.md)」を参照してください。機密情報の種類の詳細については、「[Exchange での機密情報の種類の検索基準：](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)」を参照してください。

## ドキュメントの指紋による機密フォーム データの検出

Exchange 2013 SP1 および最新バージョンの Exchange Online では、標準フォームに基づく機密情報の種類を [ドキュメント フィンガープリンティング](overview-of-document-fingerprinting-in-exchange.md) を使用して容易に作成できます。フォームのデータを保護する方法については、「[ドキュメント フィンガープリンティングを使用してフォーム データを保護する](protect-form-data-with-document-fingerprinting-exchange-2013-help.md)」を参照してください。

## 機密コンテンツの可能性についてユーザーに通知するポリシー ヒント

ポリシー ヒントの通知メッセージを使用すると、電子メール送信者が電子メール メッセージを作成しているときに、その送信者にコンプライアンスに関する潜在的な問題について通知できます。DLP ポリシー内でポリシー ヒントを構成すると、送信者の電子メール メッセージがポリシーに記載された条件を満たす場合にのみ、通知メッセージが表示されます。ポリシー ヒントは、Microsoft Exchange 2010 で導入されたメール ヒントに似ています。詳細については、「[ポリシー ヒント](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)」を参照してください。

## 従来のメッセージ分類に沿った機密情報の検出

Exchange 2013 および Exchange Online では、従来のメッセージ分類と異なる、新しい方法によるメッセージおよび添付ファイル データの管理を提供します。DLP ソリューションの主要な長所としては、組織、規制ニーズ、地理、またはその他のビジネス ニーズに固有の機密コンテンツを正しく識別できることにあります。Exchange 2013 では、コンテンツを詳細に分析するための新しいアーキテクチャと DLP ポリシー内のルールを通じて確立する検出条件を使用してこれを実現できます。Exchange 2013 でのデータ損失を防止するには、適切な一連の機密情報ルールを構成して、偽陽性と偽陰性の不適切なメール フローの中断を最小化しながら、高度な保護を提供する必要があります。これらの種類のルールは DLP 情報全体を通じて機密情報検出と呼ばれ、トランスポート ルールによって提供されるフレームワーク内で機能し、DLP 機能を有効にします。

これらの新機能の詳細については、「[機密情報ルールとトランスポート ルールの統合](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)」を参照してください。従来のメッセージ分類フィールドは、今までどおり Exchange 内のメッセージに適用でき、1 つの DLP ポリシー内で新しい機密情報検出と連動させるか、同時に実行することで、Exchange 内で別々に評価することができます。従来の Exchange 2010 メッセージ分類の詳細については、TechNet ライブラリの「[メッセージ分類について](https://go.microsoft.com/fwlink/?linkid=266612)」を参照してください。

## DLP 処理メッセージに関する情報

Exchange 2013 の場合、環境内のメッセージと DLP ポリシー検出に関する情報を取得するには、「[DLP ポリシー検出のレポートの表示](view-dlp-policy-detection-reports-exchange-2013-help.md)」および「[DLP ポリシー検出のインシデント レポートの作成](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)」を参照してください。DLP 検出に関連するデータは、Exchange 2013 の配信レポート メッセージ追跡ツールに高度に統合されています。

Exchange Online の場合は、「[DLP ポリシー検出のレポート](https://technet.microsoft.com/ja-jp/library/dn904484\(v=exchg.150\))」および「[DLP ポリシー検出のインシデント レポートの作成](https://technet.microsoft.com/ja-jp/library/dn904486\(v=exchg.150\))」を参照してください。

## インストールの前提条件

DLP 機能を使用するには、Exchange 2013 または Exchange Online を少なくとも 1 つの送信者メールボックスを使用して構成する必要があります。データ損失防止は、エンタープライズ クライアント アクセス ライセンス (CAL) が必要なプレミアム機能です。Exchange 2013 の使用開始の詳細については、「[計画と展開](planning-and-deployment-for-exchange-2013-installation-instructions.md)」を参照してください。Exchange Online の使用開始の詳細については、「[Exchange Online](https://technet.microsoft.com/ja-jp/library/jj200580\(v=exchg.150\))」を参照してください。

## 詳細情報

Exchange 2013

  - [メッセージングのポリシーと準拠](messaging-policy-and-compliance-exchange-2013-help.md)

  - [DLP の手順](dlp-procedures-exchange-2013-help.md)

  - [DLP ポリシー検出のレポートの表示](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [ドキュメント フィンガープリンティング](overview-of-document-fingerprinting-in-exchange.md)

  - [ポリシーとコンプライアンスのコマンドレット](https://technet.microsoft.com/ja-jp/library/dd298082\(v=exchg.150\))

Exchange Online

  - [Exchange Online のセキュリティとコンプライアンス](https://technet.microsoft.com/ja-jp/library/jj200706\(v=exchg.150\))

  - [DLP に関する手順](https://technet.microsoft.com/ja-jp/library/jj938003\(v=exchg.150\))

  - [DLP ポリシー検出のレポート](https://technet.microsoft.com/ja-jp/library/dn904484\(v=exchg.150\))

  - [ドキュメント フィンガープリンティング](overview-of-document-fingerprinting-in-exchange.md)

