---
title: 'DLP ポリシー テンプレート: Exchange Online Help'
TOCTitle: DLP ポリシー テンプレート
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 49896466
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DLP ポリシー テンプレート

 

_**適用先:** Exchange Online, Exchange Server 2013_

データ損失防止 (DLP) ポリシー テンプレートを使用して、Microsoft Exchange 2013 の DLP ソリューションを開始することができます。DLP ポリシー テンプレートは、ポリシーのためのモデルです。テンプレートを選択して、独自のカスタマイズされた DLP ポリシーを構築するプロセスを開始できます。DLP ポリシー内で、事業上のデータ損失防止ニーズに合うようルールをカスタマイズできます。Microsoft からいくつかのポリシー テンプレートが提供されていますが、Exchange でデータ損失防止ソリューションを実施する方法は他にもあります。

DLP ポリシー テンプレートに関連する管理タスクについては、「[DLP の手順](dlp-procedures-exchange-2013-help.md)」を参照してください。

**目次**

ニーズに合わせてテンプレートと情報の種類を拡張する

分類ルール パッケージに新しい DLP ポリシー テンプレートまたは機密情報の種類を作成する

既存のトランスポート ルールに DLP 機能を含める

Microsoft によって作成された DLP ポリシーを使用する

詳細情報

## ニーズに合わせてテンプレートと情報の種類を拡張する

機密コンテンツの定義とポリシー テンプレートを、Microsoft パートナーから、または Exchange 2013 ですでに提供されているDLP ポリシー テンプレート、情報の種類、ルールに付加して作成したファイルから組み込むことができます。ここでは、固有の DLP コンテンツを追加し、DLP 機能を拡張する方法をいくつか示します。Microsoft からすでに提供されているテンプレートは、DLP ソリューションを開始するのに便利な方法です。固有のDLP ポリシー テンプレート ファイルで DLP 機能を拡張するには、Exchange から独立して作成されるポリシー テンプレートの XML スキーマ要件を理解する必要があります。DLP ポリシー テンプレートに関連する Exchange 管理シェル コマンドレットの詳細については、「[ポリシーとコンプライアンスのコマンドレット](https://technet.microsoft.com/ja-jp/library/dd298082\(v=exchg.150\))」で `Get-DlpPolicyTemplate` に関連するコマンドレットを参照してください。また、機密コンテンツの種類を組み込むための形式と手順を理解した上で、その種類を定義できます。DLP ポリシー テンプレートに関連する Exchange 管理シェル コマンドレットの詳細については、「[ポリシーとコンプライアンスのコマンドレット](https://technet.microsoft.com/ja-jp/library/dd298082\(v=exchg.150\))」で `Get-ClassificationRuleCollection` に関連するコマンドレットを参照してください。


> [!NOTE]
> DLP ポリシーは、運用環境での適用の前に、テスト モードで有効にする必要があります。このようなテストの間に、サンプルのユーザー メールボックスを構成して、結果を確認するためにテスト ポリシーを呼び出すテスト メッセージを送信することをお勧めします。



## 分類ルール パッケージに新しい DLP ポリシー テンプレートまたは機密情報の種類を作成する

Exchange 以外に、Microsoft が提供する特定の XML スキーマ定義に合うDLP ポリシー テンプレート ファイルを作成し、そのファイルをシステムにインポートしてこれを基に DLP ポリシーを作成することができます。固有のテンプレート ファイルを作成することにより、Microsoft がまだ提供していない DLP ポリシーのモデルを定義できます。これは、Exchange 管理センターを使用して DLP ポリシーを作成する手順（通常、ポリシー テンプレートが利用可能となった後に発生）とは異なります。Exchange から独立してポリシー テンプレートを作成した場合、これを使用してメッセージのスキャンを行うにはポリシー テンプレートのインポートが必要です。また、Exchange で Microsoft が定義するもの以外に、固有の機密情報の定義を作成できます。DLP ポリシー テンプレート ファイルと分類ルール パッケージには別々の XML スキーマ定義があります。これを開始するには、次の情報を参照してください。

  -  [独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  [ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## 既存のトランスポート ルールに DLP 機能を含める

新しい DLP ポリシーを作成せずに、DLP 検出機能を従来のトランスポート ルールに組み込むことができます。以前のバージョンの Exchange で複雑なルール セットが作成されており、Exchange 2013 にこれらを複製、または機密情報の検出を追加したい場合は、Exchange 管理センターまたは Exchange 管理シェルのトランスポート ルール エディターを使用してこれら 2 つの機能を組み込むことができます。これを開始するには、次の情報を参照してください。

  -  [メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  [Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  [メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)
    
  -  [ポリシーとコンプライアンスのコマンドレット](https://technet.microsoft.com/ja-jp/library/dd298082\(v=exchg.150\))

## Microsoft によって作成された DLP ポリシーを使用する

Microsoft から多数の DLP ポリシーが提供されています。これは、柔軟かつ単純に実施できる DLP ソリューションを開始するもっとも簡単な方法です。いつでもこれら提供されたポリシーを開始点として使用して、自らの要件に合わせてカスタマイズすることができます。これを開始するには、次の情報を参照してください。

  - [Exchange で提供される DLP ポリシー テンプレート](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/dlp-policy-templates)

  - [テンプレートからの DLP ポリシーの作成](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/create-dlp-policy-from-template)

## 詳細情報

[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

