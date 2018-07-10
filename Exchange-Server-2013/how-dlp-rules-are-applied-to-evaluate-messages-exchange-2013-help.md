---
title: 'メッセージの評価に DLP ルールを適用する方法: Exchange Online Help'
TOCTitle: メッセージの評価に DLP ルールを適用する方法
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56270027
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージの評価に DLP ルールを適用する方法

 

_**適用先:** Exchange Online, Exchange Server 2013_

秘匿性の高い情報のルールを Microsoft Exchange データ損失対策 (DLP) ポリシーに設定して、電子メール メッセージの固有のデータを検出します。このトピックによって、これらのルールが適用される方法とメッセージが評価される方法が理解できるようになります。ルールが実施される方法を理解すれば、電子メール ユーザーのワークフローの中断を回避したり、高精度の DLP 検出を実現したりすることができます。例として、Microsoft が提供するクレジット カード情報ルールを使用します。トランスポート ルールまたは DLP ポリシーを有効にした場合、Exchange トランスポート ルール エージェントは、ユーザーが送信したすべてのメッセージに対して、作成したルール セットと比較します。

## 正確にニーズを把握する

メッセージのクレジット カード情報に基づいて処理する必要があるとします。いったん明らかになった内容に応じて実行するアクションは、このトピックの主題ではありませんが、それらの詳細は「[Exchange Online でのメール フロー ルールの処理](https://technet.microsoft.com/ja-jp/library/jj919237\(v=exchg.150\))」で知ることができます。メッセージから検出されるデータが本当にクレジット カードのデータであり、単にクレジット カードのデータに似た予約コードや車両識別番号など、別の正規の数字の並びではないことを可能な限り確認する必要があります。　　この必要から、次の情報がクレジット カードに分類されることを明確にしてください。

**    Margie’s Travel  
    Spencer の更新されたクレジット カード情報を受信しました。  
    Spencer Badillo  
    Visa:4111 1111 1111 1111  
    有効期限:2/2012  
    旅行プロファイルを更新してください。**

次の情報がクレジット カードに分類されないことも明確にしてください。

**    こんにちは Alex,  
    私もハワイを楽しみにしています。予約コードは、1234 1234 1234 1234 です。2012 年 3 月の予定です。  
    よろしくお願いします、Lisa**

次の XML スニペットは、前出のニーズが、Exchange が提供する秘匿性の高い情報ルールでは、現在どのように定義されているか、また提供された DLP ポリシー テンプレートの 1 つにどのように埋め込まれているかを示します。

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## ソリューションでのパターンマッチング

前出の XML ルール定義にはパターンマッチングが含まれており、これにより、あいまいな関連情報ではなく重要な情報のみをルールが検出する可能性が向上します。DPL ルールおよびテンプレート用の XML スキーマについての詳細は、「[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)」を参照してください。

クレジット カード ルールには、パターン用の XML コードのセクションがあり、ここには主識別子の一致および追加の補強証拠が含まれます。これらの要件は全部で 3 つですが、それらを次に説明します。

1.  `<IdMatch idRef="Func_credit_card" />  ` — 内部定義関数 (関数名は「credit card」) が一致する必要があります。この関数には、次の検証が含まれます。
    
    1.  正規表現の一致。ここでの 16 桁のインスタンスでは、**4111 1111 1111 1111** にもマッチするようにスペース区切り文字、あるいは **4111-1111-1111-1111** にもマッチするようにハイフン区切り文字のバリエーションも含めることができます。
    
    2.  その数字がクレジット カード番号である確率が高いかを確認するために、16 桁の数に対して Lhun のチェックサム アルゴリズムで評価します。
    
    3.  これは一致が必須で、その後に補強証拠が評価されます。

2.  `<Any minMatches="1">  ` — このセクションは、次の証拠項目の少なくとも 1 つが存在することが必要であることを示します。

3.  補強証拠は、次の 3 つのうちのいずれかにマッチすればかまいません。
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    これらの 3 つは単に、クレジット カードのキーワードのリスト、クレジット カードの名前または有効期限を意味しています。有効期限は、別の関数として内部定義および評価されます。

## ルールに対してコンテンツを評価するプロセス

ここでの 5 つのステップは、ルールと電子メール メッセージを比較する際に Exchange が実行するアクションを示します。クレジット カード ルールの例では、次のステップを実行します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>手順</th>
<th>アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. コンテンツを取得</p></td>
<td><p>Spencer Badillo</p>
<p>Visa:4111 1111 1111 1111</p>
<p>有効期限:2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. 正規表現解析</p></td>
<td><p>4111 1111 1111 1111 -&gt; 16 桁の数値を検出</p></td>
</tr>
<tr class="odd">
<td><p>3. 関数解析</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; チェックサムが一致</p></li>
<li><p>1234 1234 1234 1234 -&gt; 一致しない</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. 追加の証拠</p></td>
<td><ol>
<li><p>キーワード Visa は番号の近くにあります。</p></li>
<li><p>日付 (2/2012) の正規表現は番号の近くにあります。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. 評決</p></td>
<td><ol>
<li><p>チェックサムと一致する正規表現があります。</p></li>
<li><p>追加の証拠により信頼度が上がります。</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


Microsoft が設定したこのルールでは、ルールにマッチするためには、キーワードなどの補強証拠が電子メール メッセージのコンテンツの一部となることが必須です。したがって、次の電子メール コンテンツはクレジット カードを含むものとして検出されません。

**    Margie’s Travel  
    Spencerの更新された情報を受信しました。  
    Spencer Badillo  
    4111 1111 1111 1111  
    旅行プロファイルを更新してください。**

次の例に示すように、追加の証拠がなくてもパターンを定義するカスタム ルールを使用することができます。クレジット カード番号のみで補強証拠がなくてもメッセージを検出します。

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

この記事にあるクレジット カードの説明は、その他の秘匿性の高い情報ルールに展開することもできます。Exchangeで Microsoft が提供するルールの完全なリストを表示するには、Exchange 管理シェルで [Get-ClassificationRuleCollection](https://technet.microsoft.com/ja-jp/library/jj218696\(v=exchg.150\)) コマンドレットを次のように使用します。
```
$rule_collection = Get-ClassificationRuleCollection
```
```
$rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte
```

## 詳細情報

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))

[Exchange 2013 で Powershell を使用する (Exchange 管理シェル)](https://technet.microsoft.com/ja-jp/library/bb123778\(v=exchg.150\))

[Exchange Online の PowerShell](https://technet.microsoft.com/ja-jp/library/jj200677\(v=exchg.150\))

