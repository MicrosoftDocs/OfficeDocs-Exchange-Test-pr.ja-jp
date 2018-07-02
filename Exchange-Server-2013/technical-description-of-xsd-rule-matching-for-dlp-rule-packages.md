---
title: 'ルール パッケージの照合の方法と手法: Exchange Online Help'
TOCTitle: ルール パッケージの照合の方法と手法
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 49895227
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ルール パッケージの照合の方法と手法

 

_**適用先:** Exchange Online, Exchange Server 2013_

このトピックは、自分のカスタム機密情報タイプ ルール パッケージを含むように設計されたデータ損失防止 (DLP) XML ファイル内部でパターンと証拠要素を一致させる手法を説明します。整形式の XML ファイルを作成した後、Microsoft Exchange Server 2013 DLP ソリューションの作成のために、Exchange 管理センター (EAC) または Exchange 管理シェルを使用して、ファイルをインポートできます。ここに示す一致方法を使用するためには、既に DLP XML ファイルを開始している必要があります。自分の DLP テンプレートおよび XML ファイルを定義する詳細については、「[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)」を参照してください。

## Match 要素

`Match` 要素は、`Pattern` および `Evidence` 要素内で使用され、一致させる基本キーワード、regex、または関数を表します。一致自体の定義は、`Rule` 要素の外部に保存され、`idRef` 必須属性によって参照されます。複数の `Match` 要素は、`Pattern` 要素に直接入れることができるパターン定義に入れるか、`Any` 要素を使用して結合して、一致するセマンティックを定義できます。

    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>

## キーワード ベースの一致を定義する

共通ルール要件は、既知のキーワード文字列表現に基づいて一致することです。これは、`Keyword` 要素を使用して実現されます。キーワード要素には、対応するエンティティまたはアフィニティ ルールで参照として使用される “id” 属性があります。単一キーワード要素は、複数のエンティティおよびアフィニティ ルールで参照できます。

一致は、完全一致または単語一致に基づくアルゴリズムを使用して実行できます。完全一致の場合は、大文字と小文字が区別されるアルゴリズムを使用して指定された言語でテキストが検索されます。単語一致では、単語の境界に基づいて一致アルゴリズムが適用されます。一致する用語は、Term サブ要素を使用して Keyword 定義にインラインで入れることができます。


> [!TIP]
> 効率性およびパフォーマンスを向上するために、regex に定数ベースの一致スタイルを使用します。regex 一致は、定数ベースの一致が十分ではなくて正規表現の柔軟性が必要とされる場合のみ使用します。



    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>

## 正規表現ベースの一致を定義する

別の一般的な一致方法は、正規表現に基づきます。正規表現一致に柔軟性があるため、運転免許証番号、住所などのデータの一致を実行するにはこれが一般的な選択になります。一般的な正規表現構文は regex パターンの定義に使用されます。この表に、最も一般的な正規表現トークンの一部を利用可能にする例を示します。


> [!TIP]
> 効率性およびパフォーマンスを向上するために、regex に定数ベースの一致スタイルを使用します。regex 一致は、定数ベースの一致が十分ではなくて正規表現の柔軟性が必要とされる場合のみ使用します。




<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>記号</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>特殊文字のいずれかを除いくリテラル文字 c に 1 回一致します。</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>行頭に一致します。</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>改行ではない任意の文字に一致します。</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>行の末尾に一致します。</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>表現の間の論理 OR。</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>サブ表現をグループ化します。</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>文字クラスを定義します。</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>直前の表現に 0 回以上一致します。</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>直前の表現に 1 回以上一致します。</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>直前の表現に 0 回または 1 回一致します。</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>直前の表現に <em>n</em> 回一致します。</p></td>
</tr>
<tr class="even">
<td><p>{<em>n,</em>}</p></td>
<td><p>直前の表現に少なくとも <em>n</em> 回一致します。</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>直前の表現に少なくとも <em>n</em> 回、多くて <em>m</em> 回一致します。</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>数字に一致します。</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>数字でない文字に一致します。</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>アンダー スコアを含む英字に一致します。</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>英字でない文字に一致します。</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>空白文字 (\t、\n、\r、または \f のいずれか) に一致します。</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>空白以外の文字に一致します。</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>タブ。</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>改行。</p></td>
</tr>
<tr class="even">
<td><p>r</p></td>
<td><p>キャリッジ リターン。</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>フォーム フィード。</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p><em>m</em> をエスケープします。<em>m</em> は前述のメタ文字^, .、$、|、()、[]、*、+、?、\、または / のいずれかです。</p></td>
</tr>
</tbody>
</table>


regex 要素には、対応するエンティティまたはアフィニティ ルールで参照として使用される “id” 属性があります。単一 regex 要素は、複数のエンティティおよびアフィニティ ルールで参照できます。regex 表現は、regex 表現の要素の値として定義されます。

    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-  
         ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>

## 複数の一致要素を組み合わせる

一致する信頼度を増やす一般的な手法は、たとえば 1 つ以上の一致の発生が必要になるなど、複数の Match 要素間のセマンティックを定義することです。Any 要素では、複数の一致間に基づくロジックの定義を許可します。Any 要素は、Pattern 要素のサブ要素として使用できます。これには 1 つ以上の Match 子要素を含み、それらの間の一致ロジックを定義します。すべての一致、"not" ロジック、および完全一致回数が指定された次の Any 要素の XML コード例を参照してください。

オプションの minMatches 属性 (既定は 1) を使用すると、一致を満たすために必要な Match 要素の最小数を定義できます。同様に、オプションの maxMatches 属性 (既定は子の Match 要素数) を使用すると、一致を満たすために必要な Match 要素の最大数を定義できます。これらの条件は、minMatches および maxMatches 属性の使用に基づいて論理演算子により結合され、次のセマンティックを許可します。

  - すべての子 Match 要素と一致する
    
    任意の子 Match 要素と一致しない
    
    任意の子 Match 要素の完全サブセットと一致する

<!-- end list -->

    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

## より多くの証拠で信頼レベルを上げる

エンティティ ベースのルールの場合、信頼度を上げる別のオプションは、複数の Pattern 要素を定義し、それぞれが確証的な証拠の数を増やすことです。これは、Any 要素の minMatches および maxMatches を使用して、ますます多くの確証的な証拠に基づいて信頼レベルを上げた個別のパターンを作成することによって実現します。例:

  - 1 つの確証的な証拠が見つかった場合、信頼レベルは 65 % です

  - 2 つの場合、信頼レベルは 75 % です

  - 3 つの場合、信頼レベルは 85 % です

<!-- end list -->

    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>

## 例: 米国の社会保障ルール

ここでは、米国の社会保障番号に一致するルールの作成について概要を説明します。最初に、社会保障番号を含むコンテンツを識別する方法を説明します。社会保障番号は、次の場合に見つかります。

1.  regex が書式付き SSN と一致する (さらに有効 SSN 範囲内にある)

2.  確証的な証拠   次のいずれかが近接している必要があります。
    
    1.  キーワード一致 {Social Security, Soc Sec, SSN, SSNS, SSN\#, SS\#, SSID}
    
    2.  米国の住所を表すテキスト
    
    3.  日付を表すテキスト
    
    4.  名前を表すテキスト

次に、ルール スキーマ表現に説明を変換します。

    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>

## 詳細情報

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

