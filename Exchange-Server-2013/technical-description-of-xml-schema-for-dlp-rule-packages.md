---
title: '機密情報のルール パッケージの作成: Exchange Online Help'
TOCTitle: 機密情報のルール パッケージの作成
ms:assetid: c4ab8707-0839-4855-9390-3dbcb43475a7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ674704(v=EXCHG.150)
ms:contentKeyID: 49896461
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 機密情報のルール パッケージの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

このトピックの XML スキーマとガイダンスは、分類ルール パッケージにおいて、機密情報の種類を定義する基礎的なデータ損失防止（DLP） XML ファイルの作成を開始するのに役立ちます。適切な形式の XML ファイルを作成した後、Exchange 管理センターまたは Exchange 管理シェルを使用して XML ファイルをインポートし、Microsoft Exchange Server 2013 DLP ソリューションの作成に役立てることができます。カスタム DLP ポリシー テンプレートである XML ファイルには、分類ルール パッケージである XML を含めることができます。DLP テンプレートを XML ファイルとして定義する方法の概要については、「[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)」を参照してください。

**目次**

ルール オーサリング プロセスの概要

ルールの説明

基本的なルールの構造

XML ファイルでのローカル言語の使用

分類ルール パック XML スキーマ定義

詳細情報

## ルール オーサリング プロセスの概要

ルール オーサリング プロセスは、次の一般的な手順で構成されます。

1.  ターゲット環境の代表的なテスト ドキュメントのセットを準備します。テスト ドキュメントのセットについて、考慮すべき主な特徴にはたとえば次のものがあります。ドキュメントの 1 つのサブセットには、ルールを作成しようとするエンティティまたはアフィニティが含まれます。ドキュメントの 1 つのサブセットには、ルールを作成しようとするエンティティまたはアフィニティが含まれません。

2.  適格なコンテンツを識別するため、許容要件（適合率と再現率）を満たすルールを識別します。これには、ブール論理と組み合わせ、ルール内の複数の条件の策定が必要な場合もあります。これらの組み合わせにより、ターゲット ドキュメントを識別するための最小合致要件を満足させます。

3.  許容要件（適合率と再現率）に基づき、ルールの推奨信頼度を確立します。推奨信頼要素を、そのルールに対する既定の信頼度と考えることができます。

4.  ポリシーをルールとともに生成し、サンプル テスト コンテンツを監視することによってルールの検証を行います。その結果に基づいてルールまたは信頼度を調整し、検出されるコンテンツを最大化するとともに、誤検知（ポジティブ、ネガティブとも）を最小化します。ポジティブ サンプル、ネガティブ サンプルともコンテンツ検出度が適切な水準に達するまで、上記の検証とルール調整を繰り返します。

ポリシー テンプレート ファイルの XML スキーマ定義の詳細については、「[DLP ポリシー テンプレート ファイルの作成](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)」を参照してください。

## ルールの説明

DLP 機密情報検出エンジンに対しては、主に 2 種類のルールを作成することができます。エンティティとアフィニティ。ルールの種類は、前のセクションで説明したコンテンツの処理に適用される処理ロジックの種類に基づいて選択されます。ルールの定義は、標準化されたルール XSD で説明される形式の XML ドキュメントで構成されます。ルールでは、一致が必要なコンテンツの種類と、説明された一致によってターゲット コンテンツを表す信頼度の両方を説明します。信頼度では、コンテンツ内にあるパターンが検出された場合にエンティティが存在する確率、またはコンテンツ内にエビデンスが検出された場合にアフィニティが存在する確率を指定します。

## 基本的なルールの構造

ルールの定義は、3 つの主要なコンポーネントから構成されます。

1.  **エンティティ** は、そのルールに対するマッチングとカウンティングのロジックを定義します。

2.  **アフィニティ** は、そのルールに対するマッチングのロジックを定義します。

3.  **ローカライズ文字列** ルールの名前とその説明のローカライズ

さらに、処理の詳細を定義するのに 3 つのサポート要素が使用されます。これらは主要コンポーネント内で参照されます。キーワード、正規表現、および関数です。参照を使用することにより、サポート要素に関する 1 つの定義が、たとえば社会保障番号のように複数のエンティティ ルールやアフィニティ ルールに使用できます。基本的なルールの構造を XML 形式では次のとおりに見ることができます。

    <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
    
      <RulePack id="DAD86A92-AB18-43BB-AB35-96F7C594ADAA">
        <Version major="1" minor="0" build="0" revision="0"/>
        <Publisher id="619DD8C3-7B80-4998-A312-4DF0402BAC04"/>
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>DLP by EPG</PublisherName>
            <Name>CSO Custom Rule Pack</Name>
            <Description>This is a rule package for a EPG demo.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
    
      <Rules>
    
        <!-- Employee ID -->
        <Entity id="E1CC861E-3FE9-4A58-82DF-4BD259EAB378" patternsProximity="300" recommendedConfidence="75">
          <Pattern confidenceLevel="75">
            <IdMatch idRef="Regex_employee_id" />
            <Match idRef="Keyword_employee" />
          </Pattern>
        </Entity>
    
        <Regex id="Regex_employee_id">(\s)(\d{9})(\s)</Regex>
        <Keyword id="Keyword_employee">
          <Group matchStyle="word">
            <Term>Identification</Term>
            <Term>Contoso Employee</Term>
          </Group>
        </Keyword>
    
    
        <LocalizedStrings>
    
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB378">
            <Name default="true" langcode="en-us">
              Employee ID
            </Name>
            <Description default="true" langcode="en-us">
              A custom classification for detecting Employee ID's
            </Description>
          </Resource>
    
        </LocalizedStrings>
      </Rules>
    </RulePackage>

## エンティティ ルール

エンティティ ルールは、適切に定義された識別子（たとえば社会保障番号）を対象とし、カウントできるパターンの集合で表されます。エンティティ ルールはカウントおよびマッチの信頼度を返します。「カウント」とは検出されたエンティティのインスタンス総数、「信頼度」とは所定のエンティティが任意のドキュメント内に存在する確率を指します。エンティティには一意の識別子として "id" 属性が含まれています。識別子は、ローカリゼーション、バージョン管理、および照会に使用されます。エンティティ id は必ず GUID であり、他のエンティティやアフィニティと重複しないことが必要です。エンティティ id は \[ローカライズ文字列\] セクションで参照されています。

エンティティ ルールには、任意の "patternsProximity" 属性（既定では 300）が含まれており、ブール論理を適用して、マッチ条件を満たすのに必要な複数のパターンの隣接関係を指定するときに使用されます。エンティティ要素には子パターン要素が 1 つ以上含まれており、パターン 1 つ 1 つがクレジットカード エンティティや運転免許エンティティのようなエンティティを別々に表しています。パターン要素には "confidenceLevel" の必要な属性が含まれます。これは、サンプル データセットに基づくパターンの適合率を表します。パターン要素は、3 つの子要素を持つことができます。

1.  IdMatch - これは必須です。

2.  マッチ（一致）

3.  Any

パターン要素のいずれかが "true" を返すと、パターンが満たされたことになります。エンティティ要素のカウントは、すべての検出されたパターンの合計カウントと等しくなります。

![エンティティ数の計算式](images/JJ674704.25309939-98bc-4460-8f89-8560bbad7981(EXCHG.150).gif "エンティティ数の計算式")

ここで k はエンティティのパターン要素の数です。

1 つのパターン要素には、正確に 1 つの IdMatch 要素が必要です。IdMatch は、パターンがマッチする識別子を表します（たとえば、クレジットカード番号や ITIN 番号）。パターンのカウントとは、パターン要素とマッチする IdMatch の数です。IdMatch 要素は、マッチ要素に対する近接ウィンドウをアンカーします。

パターン要素の他の任意のサブ要素として、マッチ要素があります。これは、IdMatch 要素の検出をサポートするためにマッチングが必要となる補強エビデンスを表します。たとえば、より信頼度の高いルールでは、クレジットカード番号の検出に加えて、ドキュメント内に他のアーティファクトの存在が必要となる場合があります (クレジットカードの近接ウィンドウ内に、たとえば住所と氏名がある)。これらの他のアーティファクトは、マッチ要素または他の要素 (これらの詳細については、「マッチング方法と技術」セクションを参照) によって表されます。1 つのパターン定義に複数のマッチ要素を含めることができます。パターン定義は直接パターン要素に含めることも、マッチング セマンティックスを定義する Any 要素を使用して組み合わせることもできます。IdMatch コンテンツの周囲にアンカーされた近接ウィンドウ内でマッチが検出されると、"true" が返されます。

IdMatch 要素とマッチ要素はどちらも、マッチが必要なコンテンツの詳細を定義するのではなく、idRef 属性を通じてコンテンツを参照します。これにより、複数のパターンの構成要素における定義の再利用性が向上します。

    <Entity id="..." patternsProximity="300" > 
        <Pattern confidenceLevel="85">
            <IdMatch idRef="FormattedSSN" />
            <Any minMatches="1">
                <Match idRef="SSNKeyword" />
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>  
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Match idRef="SSNKeyword" />
            <Any minMatches="1">        
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity> 

エンティティ id 要素は、前の XML では "..." で表され、GUID である必要があります。また、エンティティ id 要素は \[ローカライズ文字列\] セクションで参照されています。

## エンティティ パターン近接ウィンドウ

エンティティは、パターン検出に使用される任意の "patternsProximity" 属性値（整数、既定では 300）を保持しています。各パターンについて、そのパターンに対して指定されたすべての他のマッチに関して、属性値が IdMatch の場所からの距離（Unicode 文字で表示）を定義します。近接ウィンドウは、IdMatch の場所によってアンカーされ、IdMatch の左側と右側にウィンドウが展開されます。

![一致要素が呼び出されるテキスト パターン](images/JJ674704.65d52989-f50f-4097-b39a-9612f860d727(EXCHG.150).gif "一致要素が呼び出されるテキスト パターン")

下の例では、SSN IdMatch 要素において、少なくとも 1 つの住所、名前または日付の補強マッチが必要な場合に、近接ウィンドウがマッチング アルゴリズムに与える影響を示しています。SSN2 と SSN3 は、近接ウィンドウ内に補強エビデンスがない、または部分的でしかないため、マッチが成立するのは SSN1 と SSN4 のみです。

![近接ルールの一致と不一致の例](images/JJ674704.8117deb3-d8c8-4d4e-a011-ac5f9990b08e(EXCHG.150).gif "近接ルールの一致と不一致の例")

メッセージ本文と各添付ファイルは、独立したアイテムとして扱われる点に注意してください。つまり、近接ウィンドウは、これらの各アイテムの終端を超えて延長されないということです。各アイテム (添付ファイルまたは本文) には、それぞれの範囲内に idMatch と補強エビデンスの両方が存在している必要があります。

## エンティティの信頼度

エンティティ要素の信頼度は、満たされるパターンの信頼度をすべて結合したものです。次の方程式を使用して結合されます。

![エンティティ信頼度レベルの計算式](images/JJ674704.9b8bb9c8-3ded-4ea5-a609-71d8034b1017(EXCHG.150).gif "エンティティ信頼度レベルの計算式")

k はエンティティ要素数とし、マッチしないパターンは信頼度 "0" を返すものとします。

例に示したエンティティ要素構造コードのサンプルを参照すると、両方のパターンがマッチした場合、次の計算によりエンティティの信頼度は 94.75% となります。

CLEntity= 1-\[(1-CLPattern1) x (1-CLPattern1)\]

*= 1-\[(1-0.85) x (1-0.65)\]*

*= 1-(0.15 x 0.35)*

*= 94.75%*

同様に、2 つめのパターンのみがマッチする場合、次の計算によりエンティティの信頼度は 65% となります。

CLEntity= 1–\[(1–CLPattern1) X (1–CLPattern1)\]

*= 1–\[(1–0) X (1–0.65)\]*

*= 1–(1 X 0.35)*

*= 65%*

これらの信頼度の値は、ルール オーサリング プロセスの一環として検証されるテスト ドキュメントのセットに基づき、個々のパターンのルールに割り当てられます。

## アフィニティ ルール

アフィニティ ルールは、適切に定義された識別子を持たないコンテンツ（たとえば SOX 法や企業財務コンテンツ）を対象とします。このコンテンツでは、単一の一貫性のある識別子を検出することはできないため、エビデンスの集合が存在するかを分析によって判定する必要があります。アフィニティ ルールではカウントを返さず、検出の有無および関連付けられた信頼度を返します。アフィニティのコンテンツは、独立したエビデンスの集合として表されます。証拠は、特定の近さになっている、必要な一致物の集計です。アフィニティ ルールでは、近接度は "evidencesProximity" 属性（既定では600）によって定義され、最低信頼度は "thresholdConfidenceLevel" によって定義されます。

アフィニティ ルールには、ローカリゼーション、バージョン管理、および照会に使用される一意の識別子に対する id 属性が含まれます。エンティティ ルールと異なり、アフィニティ ルールは適切に定義された識別子に依存しないため、IdMatch 要素を含みません。

各アフィニティ ルールには、1 つ以上の子エビデンス要素が含まれます。これらは検出するエビデンスと、アフィニティ ルールに使用される信頼度を定義します。検出結果の信頼度がしきい値未満の場合、アフィニティを検出したとは見なされません。各エビデンスは、この「種類」のドキュメントに対する補強エビデンスを論理的に表します。"confidenceLevel" 属性は、テスト データセットに対する上記エビデンスの適合率です。

エビデンス要素には、1 つまたは複数のマッチ要素または Any 子要素が含まれます。すべての子マッチ要素および子 Any 要素がマッチした場合、エビデンスが検出され、信頼度はルールの信頼度計算に使用されます。エンティティ ルールと同様の説明が、アフィニティ ルールのマッチ要素または Any 要素にも当てはまります。

    <Affinity id="..." 
              evidencesProximity="1000"
              thresholdConfidenceLevel="65">
        <Evidence confidenceLevel="40">
            <Any> 
                <Match idRef="AssetsTerms" /> 
                <Match idRef="BalanceSheetTerms" /> 
                <Match idRef="ProfitAndLossTerms" /> 
            </Any> 
        </Evidence>
        <Evidence confidenceLevel="40">
            <Any minMatches="2"> 
                <Match idRef="TaxTerms" /> 
                <Match idRef="DollarAmountTerms" /> 
                <Match idRef="SECTerms" /> 
                <Match idRef="SECFilingFormTerms" /> 
                <Match idRef="DollarTotalRegex" /> 
            </Any> 
        </Evidence>
    </Affinity>

## アフィニティ近接ウィンドウ

アフィニティの近接ウィンドウについては、エンティティ パターンと異なる計算をします。アフィニティ近接度は、スライディング ウィンドウ モデルに従います。アフィニティ近接度アルゴリズムは、任意のウィンドウ内でマッチング エビデンスの最大数を検出しようとします。近接ウィンドウ内のエビデンスには、検出対象のアフィニティ ルールについて定義されているしきい値を超える信頼度が必要です。

![アフィニティ ルール一致の近接テキスト](images/JJ674704.2601ec86-0094-43fa-8d22-9d97f7465942(EXCHG.150).gif "アフィニティ ルール一致の近接テキスト")

## アフィニティの信頼度

アフィニティの信頼度は、アフィニティ ルールの近接ウィンドウ内で検出されたエビデンスの合計と等しくなります。エンティティ ルールの信頼度と似ていますが、主な違いは近接ウィンドウの適用です。エンティティ ルールと同様、アフィニティ要素の信頼度は、すべての満たされたエビデンスの信頼度を結合したものですが、アフィニティ ルールの場合は近接ウィンドウ内で検出されたエビデンス要素の合計の最高値だけを表します。エビデンスの信頼度は、次の方程式を使用して結合されます。

![アフィニティ ルールの信頼度の計算式](images/JJ674704.8a5da4ca-af02-4c5a-ab60-0072dc7e7a0f(EXCHG.150).gif "アフィニティ ルールの信頼度の計算式")

ここで k は、近接ウィンドウ内でマッチしたアフィニティのエビデンス要素の数です。

図 4 アフィニティ ルール構造の例を参照すると、近接スライディング ウィンドウ内で 3 つのエビデンスすべてがマッチした場合、次の計算によりアフィニティの信頼度は 85.6% となります。これは、アフィニティ ルールのしきい値 65 を超えているため、ルール マッチングとなります。

CLAffinity= 1 – \[(1 – CLEvidence 1) X (1 – CLEvidence 2) X (1 – CLEvidence 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0.4) X (1 – 0.4)\]*

*= 1 – (0.4 X 0.6 X 0.6)*

*= 85.6%*

![信頼度が高いアフィニティ ルール一致の例](images/JJ674704.e17b2e22-18c3-40c4-8f19-0993bb556675(EXCHG.150).gif "信頼度が高いアフィニティ ルール一致の例")

同じ例のルール定義を使用し、2 番目のエビデンスが近接ウィンドウの外であったため、1 番目のエビデンスのみがマッチする場合、最高アフィニティ信頼度は下の計算により 60% となります。この場合はしきい値 65 に達しないため、アフィニティ ルールはマッチしません。

CLAffinity= 1 – \[(1 – CLEvidence 1) X (1 – CLEvidence 2) X (1 – CLEvidence 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0) X (1 – 0)\]*

*= 1 – (0.4 X 1 X 1)*

*= 60%*

![信頼度が低いアフィニティ ルール一致の例](images/JJ674704.077095b1-6eb0-40df-b254-f33437725720(EXCHG.150).gif "信頼度が低いアフィニティ ルール一致の例")

## 信頼度の調整

ルール オーサリング プロセスの重要な側面の 1 つは、エンティティ ルールとアフィニティ ルール両方の信頼度を調整することです。ルール定義を作成した後、代表的なコンテンツを使わずにルールを実行し、正確性のデータを集めます。各パターンまたはエビデンスについて返ってきた結果を、テスト ドキュメントに期待される結果と比較します。

![ルール一致のエビデンスを比較する表](images/JJ674704.25a7d9a1-d02f-447e-a88b-8e78bdc0413a(EXCHG.150).gif "ルール一致のエビデンスを比較する表")

ルールが許容要件を満たしている場合、そのパターンまたはエビデンスは確立されたしきい値 (例: 75%) を超える信頼度をもち、マッチ式が成立しているため次のステップへ進むことができます。

パターンまたはエビデンスがその信頼度を満たさない場合は、再作成し (例: さらなる補強エビデンスを追加する、他のパターン/エビデンスを削除または追加するなど)、上記のステップを繰り返します。

次に、上記のステップの結果に基づき、ルール内の各パターンまたはエビデンスの信頼度を調整します。各パターンまたはエビデンスについて、真陽性 (TP) 数 (作成しているルールの対象であるエンティティまたはアフィニティを含み、マッチとなったドキュメントのサブセット)、および偽陽性 (FP) 数 (作成しているルールの対象であるエンティティまたはアフィニティを含まず、マッチを返したドキュメントのサブセット) を合計します。各パターン/エビデンスの信頼度を、次の計算式を使用して設定します。

*信頼度 = 真陽性 / (真陽性 + 偽陽性)*


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>パターンまたはエビデンス</th>
<th>真陽性</th>
<th>偽陽性</th>
<th>信頼度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>P1または E1</p></td>
<td><p>4</p></td>
<td><p>1</p></td>
<td><p>80%</p></td>
</tr>
<tr class="even">
<td><p>P2または E2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Pnまたは En</p></td>
<td><p>9</p></td>
<td><p>10</p></td>
<td><p>47%</p></td>
</tr>
</tbody>
</table>


## XML ファイルでのローカル言語の使用

ルール スキーマは、各エンティティ要素およびアフィニティ要素について、ローカライズされた名前と説明の格納をサポートします。各エンティティ要素およびアフィニティ要素は、対応する要素が LocalizedStrings セクションに含まれている必要があります。各要素をローカライズするには、リソース要素を LocalizedStrings 要素の子要素として組み入れ、各要素について複数のロケールに名前と説明を格納します。リソース要素には必要な idRef 属性を組み入れ、ローカライズ対象である各要素について、対応する idRef 属性のマッチングを行います。リソース要素のロケール子要素には、個別の各ロケールに対するローカライズされた名前と説明が含まれます。

    <LocalizedStrings>
        <Resource idRef="guid">
            <Locale langcode="en-US" default="true"> 
                <Name>affinity name en-us</Name> 
                <Description>
                    affinity description en-us
                </Description> 
            </Locale> 
            <Locale langcode="de"> 
                <Name>affinity name de</Name> 
                <Description>
                    affinity description de
                </Description> 
            </Locale> 
        </Resource>
    </LocalizedStrings>

## 分類ルール パック XML スキーマ定義

    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:mce="http://schemas.microsoft.com/office/2011/mce"
               targetNamespace="http://schemas.microsoft.com/office/2011/mce" 
               xmlns:xs="http://www.w3.org/2001/XMLSchema"
               elementFormDefault="qualified"
               attributeFormDefault="unqualified"
               id="RulePackageSchema">
      <xs:simpleType name="LangType">
        <xs:union memberTypes="xs:language">
          <xs:simpleType>
            <xs:restriction base="xs:string">
              <xs:enumeration value=""/>
            </xs:restriction>
          </xs:simpleType>
        </xs:union>
      </xs:simpleType>
      <xs:simpleType name="GuidType" final="#all">
        <xs:restriction base="xs:token">
          <xs:pattern value="[0-9a-fA-F]{8}\-([0-9a-fA-F]{4}\-){3}[0-9a-fA-F]{12}"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulePackageType">
        <xs:sequence>
          <xs:element name="RulePack" type="mce:RulePackType"/>
          <xs:element name="Rules" type="mce:RulesType">
            <xs:key name="UniqueRuleId">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueProcessorId">
              <xs:selector xpath="mce:Regex|mce:Keyword"></xs:selector>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueResourceIdRef">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:key>        
            <xs:keyref name="ReferencedRuleMustExist" refer="mce:UniqueRuleId">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:keyref>
            <xs:keyref name="RuleMustHaveResource" refer="mce:UniqueResourceIdRef">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:keyref>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="RulePackType">
        <xs:sequence>
          <xs:element name="Version" type="mce:VersionType"/>
          <xs:element name="Publisher" type="mce:PublisherType"/>
          <xs:element name="Details" type="mce:DetailsType">
            <xs:key name="UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="mce:LocalizedDetails"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:keyref name="DefaultLangCodeMustExist" refer="mce:UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="."/>
              <xs:field xpath="@defaultLangCode"/>
            </xs:keyref>
          </xs:element>
          <xs:element name="Encryption" type="mce:EncryptionType" minOccurs="0" maxOccurs="1"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="VersionType">
        <xs:attribute name="major" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="minor" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="build" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="revision" type="xs:unsignedShort" use="required"/>
      </xs:complexType>
      <xs:complexType name="PublisherType">
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="LocalizedDetailsType">
        <xs:sequence>
          <xs:element name="PublisherName" type="mce:NameType"/>
          <xs:element name="Name" type="mce:RulePackNameType"/>
          <xs:element name="Description" type="mce:OptionalNameType"/>
        </xs:sequence>
        <xs:attribute name="langcode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="DetailsType">
        <xs:sequence>
          <xs:element name="LocalizedDetails" type="mce:LocalizedDetailsType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="defaultLangCode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="EncryptionType">
        <xs:sequence>
          <xs:element name="Key" type="xs:normalizedString"/>
          <xs:element name="IV" type="xs:normalizedString"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="RulePackNameType">
        <xs:restriction base="xs:token">
          <xs:minLength value="1"/>
          <xs:maxLength value="64"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="NameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="1"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="OptionalNameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="0"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="RestrictedTermType">
        <xs:restriction base="xs:string">
          <xs:minLength value="1"/>
          <xs:maxLength value="512"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulesType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Entity" type="mce:EntityType"/>
            <xs:element name="Affinity" type="mce:AffinityType"/>
          </xs:choice>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Regex" type="mce:RegexType"/>
            <xs:element name="Keyword" type="mce:KeywordType"/>
          </xs:choice>
          <xs:element name="LocalizedStrings" type="mce:LocalizedStringsType"/>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="EntityType">
        <xs:sequence>
          <xs:element name="Pattern" type="mce:PatternType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="patternsProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="recommendedConfidence" type="mce:ProbabilityType"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="PatternType">
        <xs:sequence>
          <xs:element name="IdMatch" type="mce:IdMatchType"/>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="AffinityType">
        <xs:sequence>
          <xs:element name="Evidence" type="mce:EvidenceType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="evidencesProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="thresholdConfidenceLevel" type="mce:ProbabilityType" use="required"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="EvidenceType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="IdMatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="MatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="AnyType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="minMatches" type="xs:nonNegativeInteger" default="1"/>
        <xs:attribute name="maxMatches" type="xs:nonNegativeInteger" use="optional"/>
      </xs:complexType>
      <xs:simpleType name="ProximityType">
        <xs:restriction base="xs:positiveInteger">
          <xs:minInclusive value="1"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="ProbabilityType">
        <xs:restriction base="xs:integer">
          <xs:minInclusive value="1"/>
          <xs:maxInclusive value="100"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="WorkloadType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Exchange"/>
          <xs:enumeration value="Outlook"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RegexType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="id" type="xs:token" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="KeywordType">
        <xs:sequence>
          <xs:element name="Group" type="mce:GroupType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:token" use="required"/>
      </xs:complexType>
      <xs:complexType name="GroupType">
        <xs:sequence>
          <xs:choice>
            <xs:element name="Term" type="mce:TermType" maxOccurs="unbounded"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="matchStyle" default="word">
          <xs:simpleType>
            <xs:restriction base="xs:NMTOKEN">
              <xs:enumeration value="word"/>
              <xs:enumeration value="string"/>
            </xs:restriction>
          </xs:simpleType>
        </xs:attribute>
      </xs:complexType>
      <xs:complexType name="TermType">
        <xs:simpleContent>
          <xs:extension base="mce:RestrictedTermType">
            <xs:attribute name="caseSensitive" type="xs:boolean" default="false"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="LocalizedStringsType">
        <xs:sequence>
          <xs:element name="Resource" type="mce:ResourceType" maxOccurs="unbounded">
            <xs:key name="UniqueLangCodeUsedInNamePerResource">
              <xs:selector xpath="mce:Name"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:key name="UniqueLangCodeUsedInDescriptionPerResource">
              <xs:selector xpath="mce:Description"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="ResourceType">
        <xs:sequence>
          <xs:element name="Name" type="mce:ResourceNameType" maxOccurs="unbounded"/>
          <xs:element name="Description" type="mce:DescriptionType" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="idRef" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="ResourceNameType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="DescriptionType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
    </xs:schema>

## 詳細情報

[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

