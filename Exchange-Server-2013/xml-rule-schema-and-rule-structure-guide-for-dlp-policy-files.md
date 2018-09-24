---
title: DLP ポリシー ファイルの XML ルール スキーマとルール構造ガイド
TOCTitle: DLP ポリシー テンプレート ファイルの作成
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 49896238
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DLP ポリシー テンプレート ファイルの作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

この概要では、データ損失防止 (DLP) ポリシー テンプレート ファイルの XML スキーマ定義のコンポーネントを説明し、さらに XML 形式のポリシー ファイル例も示します。作業を開始する前に、全体的な DLP のアーキテクチャとルール開発プロセスを理解するために役立ちます。詳細については、「[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)」および「[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)」を参照してください。

データ損失防止ソリューションを容易に適用し、管理するために、Microsoft Exchange Server 2013 では、DLP ポリシーとポリシー テンプレートとして認識されている概念モデルが導入されています。DLP ポリシー テンプレートには、目的とする DLP ポリシーの予備的なデザインが備えられています。DLP ポリシー テンプレートを有用なものにするには、このテンプレートが、規則やビジネス上の要求などの特定のポリシーの目的を実現するために必要なすべてのディレクティブおよびデータ オブジェクトをカプセル化する必要があります。テンプレートは、環境に依存するものではありません。DLP ポリシー テンプレートは、製品構成の一部として提供されたり、独立系ソフトウェア ベンダーとパートナーによって提供されたりする単なるポリシーの定義またはモデルです。その一方で DLP ポリシーは、展開環境に依存するテンプレートの実行時のインスタンス化でもあります。トランスポート ルールを使用することで、既存のメッセージング ポリシーのフレームワークに DLP ポリシーを組み込むことができます。トランスポート ルールは、ユーザーの DLP ソリューションに柔軟に適応し、多様な DLP ソリューションに対応します。

## ポリシー テンプレートのソースと構造

DLP ポリシー テンプレートは通常、次の画像で示すように、サーバーベースの処理ディレクティブやクライアント コンピューター ポリシー、その他のポリシー コンストラクタなどの複数のソースから影響を受けます。

![ポリシー テンプレートに影響する要因](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "ポリシー テンプレートに影響する要因")

DLP ポリシー テンプレートでは、Exchange 管理シェルと、Exchange 管理センターなどのインポート、エクスポート、削除、クエリといった機能を備えたインターネットベースのインターフェイスの両方を使用して、シンプルな管理操作を使用できます。DLP ポリシーは、作成プロセスで DLP ポリシー テンプレートを参照することで作成されます。参照されるこれらの DLP ポリシー テンプレートは、システムにインストールされているポリシー テンプレートを参照する場合もあります。これらのテンプレートには、アクティブ ディレクトリ ドメイン サービスに保存されているものや、外部から提供されたポリシーから直接入力として提供されるものがあります。

DLP ポリシー テンプレートは、XML ドキュメントとして表されます。Exchange 内に備えられているポリシーであっても、外部から提供されたポリシーであっても、単一の XML スキーマが使用されます。以下の表に、XML ドキュメントの概念的な構造を示します。この表には主要な要素を示します。一連のポリシー コンポーネント定義は、規則やビジネス上の要求などの特定のポリシーの目的を達成するのに有用です。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>構造要素</th>
<th>意味または例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Publisher</p></td>
<td><p>マイクロソフトまたはパートナー</p></td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>Policy Name</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>Description</p></td>
<td><p>PCI-DSS DLP ポリシーは、PCI データ セキュリティ基準 (PCI DSS) の対象となる情報 (クレジット カード番号やデビット カード番号など) の存在を検出する際に役立ちます。このポリシーを使用しても、何らかの法令の遵守が保証されることはありません。テストを完了したら、情報伝送が組織のポリシーに準拠するように、Exchange で必要な構成変更を行なってください。たとえば、既知のビジネス パートナーとの TLS を構成したり、この種のデータを含むメッセージに対する権利保護を追加して、より制限の多いトランスポート ルール アクションを追加します。</p></td>
</tr>
<tr class="odd">
<td><p>Metadata</p></td>
<td><p>地方の条例、国/地域、キーワードなどを記述するタグ。</p></td>
</tr>
<tr class="even">
<td><p>Set of policy constructs</p></td>
<td><ol>
<li><p>条件やアクションなどのトランスポート ルール定義。</p></li>
<li><p>インタラクティブな通知を介したクライアント エクスペリエンスを制御する電子メール クライアントの動作定義。</p></li>
<li><p>(必要な場合) クライアント環境固有の設定および調整する必要がある構成参照。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Set of data classifications</p></td>
<td><ol>
<li><p>分類エンティティまたはアフィニティを指定します。</p></li>
<li><p>エンティティには数と信頼度があり、アフィニティには信頼度しかありません。</p></li>
<li><p>プロパティと分類スキーマの独自のセットが付属しています。</p></li>
</ol></td>
</tr>
</tbody>
</table>


## ポリシー テンプレート書式定義

DLP ポリシー テンプレートは、次のスキーマに従う XML ドキュメントとして表されます。XML は大文字と小文字が区別されることに注意してください。たとえば、`dlpPolicyTemplates` は機能しますが、`DlpPolicyTemplates` は機能しません。

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <dlpPolicyTemplates>
    <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
      <contentVersion>4</contentVersion>
      <publisherName>Microsoft</publisherName>
      <name>
        <localizedString lang="en">PCI-DSS</localizedString>
      </name>
      <description>
        <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
      </description>
      <keywords></keywords>
      <ruleParameters></ruleParameters>
      <ruleParameters/>
      <policyCommands>
        <!-- The contents below are applied/executed as rules directly in PS - -->
        <commandBlock>
          <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
        </commandBlock>
        <commandBlock>
          <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
        </commandBlock>
      </policyCommands>
      <policyCommandsResources></policyCommandsResources>
    </dlpPolicyTemplate>
  </dlpPolicyTemplates>
  ```

XML ファイルに含まれるいずれかの要素に対するパラメーターに空白を含める場合、そのパラメーターを二重引用符で囲む必要があり、そうしないと適切に動作しません。以下の例では、`-SentToScope` の後に続くパラメーターを使用できますが、これはスペースを含まない連続した文字列であるため、二重引用符は使用しません。ただし、–`Comments` に指定するパラメーターには二重引用符がなくスペースが含まれるため、Exchange 管理センターには表示されません。

  ```powershell
  <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
  ```

## localizedString 要素

テンプレート形式には、たとえば、どの DLP ポリシー テンプレートをインストールするかを選択するような場合に、エンドユーザーに提示するテンプレート内の文字列をローカライズする機能が備えられています。localizedString 要素は、名前と説明の各フィールドに対して複数の定義を提供するのに使用できます。

## ruleParameters ノード

これは、パラメーターのオプション セットで、このオプション セットは DLP ポリシーを作成して展開固有のオブジェクトに対応付ける際のテンプレートのインスタンス化フェーズ中に提供される必要があります。たとえば、展開で利用可能な実際の配布グループなどがあります。

## dlpPolicyTemplate 要素

これは、DLP ポリシー テンプレートのルート要素で、すべてのテンプレートに不可欠です。以下の表に、使用可能な属性を示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>○</p></td>
<td><p>この DLP ポリシー テンプレート ドキュメントで使用されるバージョン番号。</p></td>
</tr>
<tr class="even">
<td><p>State</p></td>
<td><p>X</p></td>
<td><p>ポリシーの状態の既定の構成 (オプション)。</p></td>
</tr>
<tr class="odd">
<td><p>Mode</p></td>
<td><p>X</p></td>
<td><p>ポリシーのモードの既定の構成 (オプション)。</p></td>
</tr>
<tr class="even">
<td><p>Id</p></td>
<td><p>X</p></td>
<td><p>この DLP ポリシー テンプレート定義を一意に識別するための GUID で、&quot;A29C69BF-4F98-47F1-9A99-5771DFD2C27F&quot; という形式になります。</p></td>
</tr>
</tbody>
</table>


子要素には、次の要素シーケンスが含まれます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>子の要素</th>
<th>(最小、最大)</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>テンプレートの発行者のメタデータ</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>(1, 1)</p></td>
<td><p>このテンプレートのローカライズ可能な名前。</p></td>
</tr>
<tr class="odd">
<td><p>Description</p></td>
<td><p>(1, 1)</p></td>
<td><p>このテンプレートのローカライズ可能な説明。</p></td>
</tr>
<tr class="even">
<td><p>Keywords</p></td>
<td><p>(1, 1)</p></td>
<td><p>このテンプレートに適用するキーワード リスト。テンプレートのキーワード リストは空欄にすることができます。</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>ポリシー定義に使用されるテンプレート パラメーターのリスト。</p></td>
</tr>
<tr class="even">
<td><p>PolicyCommands</p></td>
<td><p>(0, 1)</p></td>
<td><p>このポリシーのトランスポート ルール定義のリスト。この要素は省略可能です。</p></td>
</tr>
</tbody>
</table>


## DLP ポリシー テンプレート: ポリシー コマンド

ポリシー テンプレートのこの部分には、ポリシー定義のインスタンス化に使用される Exchange 管理シェル コマンドのリストが含まれます。インポート プロセスでは、インスタンス化プロセスの一部として各コマンドが実行されます。以下に、ポリシー コマンドの例を示します。

  ```powershell
  <PolicyCommands>
      <!-- The contents below are applied/executed as rules directly in PS - -->
        <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
        <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
    </PolicyCommands> 
  ```

コマンドレットの形式は、使用されるコマンドレットの標準的な Exchange 管理シェルのコマンドレット構文です。コマンドは順番に実行されます。各コマンド ノードには、複数のコマンドで構成されるスクリプト ブロックを含めることができます。以下の例では、DLP ポリシー テンプレート内に分類ルール パックを埋め込む方法と、ポリシーの作成プロセスでルール パックをインストールする方法を示しています。分類ルール パックはポリシー テンプレートに埋め込まれ、次にテンプレート内のコマンドレットにパラメーターとして渡されます。

```powershell 
<CommandBlock>
<![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

<RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
<Version major="1" minor="0" build="0" revision="0"/>
<Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
<Details defaultLangCode="en-us">
  <LocalizedDetails langcode="en-us">
    <PublisherName>Contoso</PublisherName>
    <Name>Contoso Sample Rule Pack</Name>
    <Description>This is a sample rule package</Description>
  </LocalizedDetails>
</Details>
</RulePack>

<Rules>
<Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

  <Pattern confidenceLevel="85">
    <IdMatch idRef="Regex_Contoso" />
    <Any minMatches="1">
      <Match idRef="Regex_conf" />
    </Any>
  </Pattern>
</Entity>

<Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
<Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

<LocalizedStrings>
  <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
    <Name default="true" langcode="en-us">
      Confidential Information Rule
    </Name>
    <Description default="true" langcode="en-us">
      Sample rule pack - Detects Contoso confidential information
    </Description>
  </Resource>
</LocalizedStrings>
</Rules>

</RulePackage>

')


New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

子の要素には、次の順序で要素シーケンスが含まれます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>子の要素</th>
<th>(最小、最大)</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1, n)</p></td>
<td><p>PowerShell 内で実行されるコマンド ブロック。各コマンド ブロックはそれぞれ順番に実行されます。</p></td>
</tr>
</tbody>
</table>


## 詳細情報

[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[独自の DLP テンプレートおよび情報の種類の定義](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[ファイルからカスタムの DLP ポリシー テンプレートをインポートする](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

