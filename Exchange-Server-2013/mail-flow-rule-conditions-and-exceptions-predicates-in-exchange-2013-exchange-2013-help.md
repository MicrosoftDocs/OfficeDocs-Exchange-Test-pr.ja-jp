---
title: 'トランスポート ルールの条件 (述語): Exchange 2013 Help'
TOCTitle: 'メール フロー ルールの条件と例外 (述語) '
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 49896471
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート ルールの条件 (述語)

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2017-12-20_

メール フロー ルール (別名トランスポート ルール) 内の条件および例外は、メッセージに対するルールの適用、不適用を識別します。たとえば、ルールがメッセージに免責事項を追加する場合、特定の単語を含むメッセージだけに、または特定のユーザーによって送信されたメッセージだけに、あるいは特定のグループのメンバーによって送信されたもの以外すべてのメッセージにルールが適用されるように設定することが可能です。全体として、メール フロー ルール内の条件と例外は、すべての条件に対し、全く同じ設定と構文を使う、対応した例外が存在することから、*述語* とも呼ばれます。唯一の違いは、条件が内包するメッセージを指定するのに対し、例外は除外するメッセージを指定することです。

ほとんどの条件および例外には、1 つまたはそれ以上の値を必要とする 1 つのプロパティが設定されています。たとえば、**この送信者** という条件には、メッセージの送信者が必要となります。プロパティが 2 つある条件もあります。たとえば、**メッセージ ヘッダーにこれらの単語のいずれかが含まれる** という条件には、ヘッダーを指定するプロパティ 1 つと、ヘッダー フィールド内で検索するテキストを指定する 2 つめのプロパティが必要です。いくつかの条件や例外は、プロパティが全くありません。たとえば、**添付ファイルが実行可能なコンテンツを持つ** の条件は、単に実行可能なコンテンツを持つメッセージの添付ファイルを検索します。

Exchange Server 2013 におけるメール フロー ルールの詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)」を参照してください。

Exchange Online Protection または Exchange Online におけるメール フロー ルールにおける条件と例外の詳細については、「[Exchange Online でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919235\(v=exchg.150\))」または「[Exchange Online Protection でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919234\(v=exchg.150\))」を参照してください。

## メールボックス サーバー上のメール フロー ルールの条件と例外

次のセクション内の表では、メールボックス サーバー上のメール フロー ルールで使用可能な条件および例外について説明します。プロパティの種類は、プロパティの種類 セクションで説明されています。

送信者

受信者

メッセージの件名または本文

添付ファイル

任意の受信者

メッセージの機密情報の種類と To および Cc 値、サイズ、および文字セット

送信者と受信者

メッセージのプロパティ

メッセージ ヘッダー

**注**:

  - Exchange 管理センター (EAC) で条件または例外を選択した後、**この場合はこのルールを適用する** または **この場合を除く** フィールドに最終的に示される値が、選択したクリック パスの値と異なる (満たない) 場合が多々あります。また、テンプレート (シナリオのフィルター済みリスト) に基づいて新しいルールを作成する場合、完全なクリック パスに従う代わりに短い条件の名前を選択できます。短い名前と完全なクリック パスの値は、表の EAC 列に示されています。

  - EAC で **\[すべてのメッセージに適用\]** を選択した場合は、それ以外の条件を指定することはできません。Exchange 管理シェル でこれの同意になるものは、条件のパラメーターを全く指定せずにルールを作成することです。

  - 条件と例外において、設定とプロパティは同じため、**Get-TransportRulePredicate** コマンドレットの出力は、例外を個別に表示しません。また、このコマンドレットによって戻された述語の名前のいくつかは、対応するパラメーター名とは違っており、一つの述語に複数のパラメーターが必要となることがあります。

## 送信者

送信者のアドレスを調べる条件と例外においては、ルールが送信者のアドレスを検索する場所を指定できます。

EAC において、**この規則のプロパティ** セクションで、**メッセージの送信者アドレスが一致**をクリックします。この設定を参照するには、**その他のオプション** をクリックする必要があるかもしれないことに注意してください。Exchange 管理シェル において、パラメーターは *SenderAddressLocation* です。使用できる値は次のとおりです。

  - **ヘッダー**   メッセージ ヘッダー内の送信者のみを確認します (たとえば、**From**、**Sender**、または **Reply-To** フィールド)。これは既定値であり、Exchange 2013 累積的な更新プログラム 1 (CU1) の前にメール フロー ルールが作動する方法です。

  - **Envelope**   メッセージ エンベロープ (**Return-Path** フィールドに通常格納されている SMTP 転送に使用された **MAIL FROM** 値) からの送信者のみを確認します。メッセージ エンベロープ検索は以下の条件 (および対応する例外) でのみ利用可能であることに注意してください。
    
      - **送信者が** (*From*)
    
      - **送信者が次のメンバーである** (*FromMemberOf*)
    
      - **送信者のアドレスに次が含まれる場合** (*FromAddressContainsWords*)
    
      - **送信者のアドレスが次と一致する場合** (*FromAddressMatchesPatterns*)
    
      - **送信者のドメインが次の場合** (*SenderDomainIs*)

  - **ヘッダーまたはエンベロープ** (`HeaderOrEnvelope`)   メッセージ ヘッダーおよびメッセージ エンベロープ内の送信者を確認します。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>送信者が次の場合</strong></p>
<p><strong>送信者</strong> &gt; <strong>この人物である</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 組織内の特定のメールボックス、メール ユーザー、あるいはメール連絡先から送信されたメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>送信者の場所が次の場合</strong></p>
<p><strong>送信者</strong> &gt; <strong>外部/内部である</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>内部または外部の送信者によって送信されたメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>送信者が次のメンバーの場合</strong></p>
<p><strong>送信者</strong> &gt; <strong>このグループのメンバーである</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>特定のグループのメンバーによって送信されたメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>送信者のアドレスに次が含まれる場合</strong></p>
<p><strong>送信者</strong> &gt; <strong>アドレスに次のいずれかの単語を含む</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>送信者のメール アドレスに指定の単語が含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>送信者のアドレスが次と一致する場合</strong></p>
<p><strong>送信者</strong> &gt; <strong>アドレスが次のいずれかのテキスト パターンと一致する</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>送信者のメール アドレスに、特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>送信者の指定のプロパティが次の単語のいずれかを含む</strong></p>
<p><strong>送信者</strong> &gt; <strong>次の単語のいずれかを含む特定のプロパティ</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>最初のプロパティ: <code>ADAttribute</code></p>
<p>2 番目のプロパティ: <code>Words</code></p></td>
<td><p>送信者の指定の Active Directory 属性に任意の特定の文字が含まれているメッセージです。</p>
<p><strong>Country</strong> 属性には、2 文字の国コードの値 (たとえば、ドイツの DE) が必要であることに注意してください。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>送信者の指定のプロパティが次のテキスト パターンと一致する</strong></p>
<p><strong>送信者</strong> &gt; <strong>次のテキスト パターンと一致する特定のプロパティを持つ</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>最初のプロパティ: <code>ADAttribute</code></p>
<p>2 番目のプロパティ: <code>Patterns</code></p></td>
<td><p>送信者の指定の Active Directory 属性に、指定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>送信者がポリシー ヒントを上書きした</strong></p>
<p><strong>送信者</strong> &gt; <strong>ポリシー ヒントを上書きした</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>該当なし</p></td>
<td><p>送信者がデータ損失防止 (DLP) ポリシーを上書きすることを選択したメッセージです。DLP ポリシーの詳細については、<a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">データ損失防止</a> を参照してください。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>送信者の IP アドレスが次の範囲内の場合</strong></p>
<p><strong>送信者</strong> &gt; <strong>IP アドレスが、これらのいずれかの範囲、または完全に一致する</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>送信者の IP アドレスが、指定した IP アドレスと一致するか、指定した IP アドレスの範囲内にあるメッセージです。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>送信者のドメインが次の場合</strong></p>
<p><strong>送信者</strong> &gt; <strong>ドメインが</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>送信者のメール アドレスのドメインが指定された値と一致するメッセージです。</p>
<p>指定したドメイン (ドメインの任意のサブドメインなど) を <em>含む</em> 送信者のドメインを見つける必要がある場合、<strong>送信者アドレスが一致</strong> (<em>FromAddressMatchesPatterns</em>) 条件を使用し、構文: <code>'@domain\.com$'</code> を使用してドメインを指定します。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## 受信者


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>受信者が次の場合</strong></p>
<p><strong>受信者</strong> &gt; <strong>この人物である</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>受信者の 1 人が Exchange の組織内の指定されたメールボックス、メール ユーザー、メール連絡先であるメッセージです。受信者はメッセージの <strong>To</strong>、<strong>Cc</strong>、<strong>Bcc</strong> のフィールドにいることが可能です。</p>
<p><strong>注</strong>:配布グループもメールが有効なセキュリティ グループも指定できません。グループに送信されたメッセージに対してアクションを実行する必要がある場合、<strong>[宛先] ボックスに次が含まれている場合</strong> (<em>AnyOfToHeader</em>) という条件を代わりに使用します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>受信者の場所が次の場合</strong></p>
<p><strong>受信者</strong> &gt; <strong>外部/内部である</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>内部受信者、外部受信者、パートナー組織の外部受信者、またはパートナー以外の組織の外部受信者に送信されるメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>受信者が次のメンバーの場合</strong></p>
<p><strong>受信者</strong> &gt; <strong>このグループのメンバーである</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>特定のグループのメンバーである受信者を含むメッセージです。グループはメッセージの <strong>To</strong>、<strong>Cc</strong>、または <strong>Bcc</strong> フィールドにあることが可能です。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>受信者のアドレスに次が含まれる場合</strong></p>
<p><strong>受信者</strong> &gt; <strong>アドレスに次のいずれかの単語を含む</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>受信者のメール アドレスに指定の単語が含まれているメッセージです。</p>
<p><strong>注:</strong> この条件が、受信プロキシ アドレスに送信されるメッセージについて考慮していない点に注意してください。受信者のプライマリ メール アドレスに送信されるメッセージのみを照合します。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>受信者のアドレスが次と一致する場合</strong></p>
<p><strong>受信者</strong> &gt; <strong>アドレスが次のいずれかのテキスト パターンと一致する</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>受信者のメール アドレスに、特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p>
<p><strong>注:</strong> この条件が、受信プロキシ アドレスに送信されるメッセージについて考慮していない点に注意してください。受信者のプライマリ メール アドレスに送信されるメッセージのみを照合します。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>受信者の指定のプロパティが次の単語のいずれかを含む</strong></p>
<p><strong>受信者</strong> &gt; <strong>次の単語のいずれかを含む特定のプロパティを持つ</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>最初のプロパティ: <code>ADAttribute</code></p>
<p>2 番目のプロパティ: <code>Words</code></p></td>
<td><p>受信者の指定の Active Directory 属性に、任意の指定単語が含まれているメッセージです。</p>
<p><strong>Country</strong> 属性には、2 文字の国コードの値 (たとえば、ドイツの DE) が必要であることに注意してください。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>受信者の指定のプロパティが次のテキスト パターンと一致する</strong></p>
<p><strong>受信者</strong> &gt; <strong>次のテキスト パターンと一致する特定のプロパティを持つ</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>最初のプロパティ: <code>ADAttribute</code></p>
<p>2 番目のプロパティ: <code>Patterns</code></p></td>
<td><p>受信者の指定の Active Directory 属性に、指定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>受信者のドメインが次の場合</strong></p>
<p><strong>受信者</strong> &gt; <strong>ドメインが</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>受信者のメール アドレスのドメインが指定された値と一致するメッセージです。</p>
<p>指定したドメイン (ドメインの任意のサブドメインなど) を <em>含む</em> 受信者のドメインを見つける必要がある場合、<strong>受信者アドレスが一致</strong> (<em>RecipientAddressMatchesPatterns</em>) 条件を使用し、構文: <code>'@domain\.com$'</code> を使用してドメインを指定します。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージの件名または本文


> [!NOTE]
> メッセージ内の件名または他のヘッダー フィールドでの単語またはテキスト パターンの検索は、SMTP サーバー間で ASCII テキスト内のバイナリ メッセージ送信に使用された MIME コンテンツ転送エンコーディング方式に基づいてメッセージがデコードされた<EM>後</EM>に行われます。条件または例外を使用して、メッセージ内の件名または他のヘッダー フィールドの未加工 (通常は Base64) のエンコード値を検索することはできません。




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>件名または本文に次が含まれる場合</strong></p>
<p><strong>件名または本文</strong> &gt; <strong>件名または本文に次のいずれかの単語を含む</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> フィールドまたはメッセージ本文に特定の単語を持つメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>件名または本文が次と一致する場合</strong></p>
<p><strong>件名または本文</strong> &gt; <strong>件名または本文が次のテキスト パターンと一致する</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p><strong>Subject</strong> フィールドまたはメッセージ本文に、特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>件名に次が含まれている場合</strong></p>
<p><strong>件名または本文</strong> &gt; <strong>件名に次のいずれかの単語を含む</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> フィールドに特定の単語を持つメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>件名が次と一致する場合</strong></p>
<p><strong>件名または本文</strong> &gt; <strong>件名が次のテキスト パターンと一致する</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p><strong>Subject</strong> フィールドに特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## 添付ファイル

メール フロー ルールがメッセージの添付ファイルを検査する方法の詳細については、[トランスポート ルールを使用してメッセージの添付を検査する](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) をご覧ください。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>添付ファイルのコンテンツに次が含まれる場合</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>内容にこれらの単語のいずれかが含まれている</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>添付ファイルに指定された単語が含まれているメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>任意の添付ファイルの内容が一致</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>内容がこれらのテキスト パターンと一致する</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>添付ファイルに特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p>
<p><strong>注:</strong> 添付ファイルの最初の 150 キロバイト (KB) のみがスキャンされます。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>添付ファイルのコンテンツを検査できない場合</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>コンテンツを検査できない</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>該当なし</p></td>
<td><p>添付ファイルが Exchange でネイティブに認識されず、必要な IFilter がメールボックス サーバーにインストールされていないメッセージ詳細については、<a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Exchange 2013 でフィルター パック IFilter を登録する</a> をご覧ください。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>添付ファイルのファイル名が次と一致する場合</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>ファイル名が次のテキスト パターンと一致する</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>添付ファイル名に特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>添付ファイルのファイル拡張子が次と一致する場合</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>ファイルの拡張子に次の単語が含まれる</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>添付ファイルの拡張子が、以下の指定の単語と一致するメッセージです。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>任意の添付ファイルのサイズが次の値以上</strong></p>
<p><strong>添付ファイル &gt; サイズが次の値以上の場合</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>任意の添付ファイルが指定値以上のメッセージです。</p>
<p>EAC では、サイズはキロバイト (KB) 単位でのみ指定できます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>メッセージのスキャンが完了しなかった場合</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>スキャンを完了しなかった</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>該当なし</p></td>
<td><p>ルール エンジンが添付ファイルのスキャンを完了できなかったメッセージです。内容が完全にスキャンできなかったメッセージを認識し、処理するために協力して作用するルールを作成するために、この条件を使用できます。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>添付ファイルに実行可能なコンテンツがある場合</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>実行可能なコンテンツがある</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>該当なし</p></td>
<td><p>添付ファイルが実行可能ファイルであるメッセージです。システムは、ファイルの拡張子に依存するのではなく、ファイルのプロパティを検査します。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>すべての添付ファイルがパスワードで保護されている</strong></p>
<p><strong>任意の添付ファイル</strong> &gt; <strong>パスワードで保護されている</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>該当なし</p></td>
<td><p>添付ファイルがパスワードで保護された (ゆえにスキャンすることができない) メッセージです。パスワードの検出は、Office ドキュメントと Zip ファイルにのみ利用できます。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## 任意の受信者

このセクションの条件と例外は、メッセージが少なくとも一人の特定受信者を含むときに *すべて* の受信者に影響する、一意の能力を提供します。たとえば、メッセージを拒否するルールがあるとします。受信者 セクションの受信者条件を使用する場合、メッセージはその指定受信者にのみ拒否されます。たとえば、ルールがメッセージ内に指定受信者を発見したのに、他にも 5 名の受信者がメッセージに含まれるとします。メッセージはその 1 人の受信者のみに拒否され、その他 5 名の受信者には配信されます。

このセクションから受信者の条件を追加した場合、同じメッセージは検出された受信者およびその他の 5 人の受信者に拒否されます。

逆に、このセクションの受信者の例外は、ルール アクションがメッセージの検出された受信者だけでなく、*すべて* の受信者に適用されることを *防止* します。

**注:** この条件が、受信プロキシ アドレスに送信されるメッセージについて考慮していない点に注意してください。受信者のプライマリ メール アドレスに送信されるメッセージのみを照合します。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任意の受信者アドレスが次を含む</strong></p>
<p><strong>任意の受信者</strong> &gt; <strong>アドレスが次のいずれかの単語を含む</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>メッセージの <strong>To</strong>、<strong>Cc</strong>、または <strong>Bcc</strong> フィールドに特定の単語が含まれているメッセージです。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>任意の受信者アドレスが次と一致する</strong></p>
<p><strong>任意の受信者</strong> &gt; <strong>アドレスが次のいずれかのテキスト パターンと一致する</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p><strong>To</strong>、<strong>Cc</strong>、または <strong>Bcc</strong> フィールドに特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージの機密情報の種類と To および Cc 値、サイズ、および文字セット

このセクションの **To** フィールドと **Cc** フィールドの値を検索する条件は、の値を検索する、「任意の受信者」セクションの条件のように動作します (検出された受信者だけでなく、メッセージの*すべて*の受信者はルールの影響を受けます)。

**注:** この条件が、受信プロキシ アドレスに送信されるメッセージについて考慮していない点に注意してください。受信者のプライマリ メール アドレスに送信されるメッセージのみを照合します。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>メッセージに機密情報が含まれている場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>以下の種類の機密情報のいずれかが含まれる</strong></p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>データ損失防止 (DLP) のポリシーで定義されている機密情報が含まれるメッセージです。</p>
<p>この条件は、<strong>ポリシー ヒントを使用して送信者に通知する</strong> (<em>NotifySender</em>) アクションを使用するルールに必要です。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[宛先] ボックスに次が含まれている場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>[宛先] ボックスにこの人物を含む</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p><strong>To</strong> フィールドに任意の指定受信者が含まれるメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[宛先] ボックスに次のメンバーが含まれている場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>[宛先] ボックスにこのグループのメンバーを含む</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p><strong>To</strong> フィールドが特定のグループのメンバーである受信者を含むメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[Cc] ボックスに次が含まれている場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>[Cc] ボックスにこの人物を含む</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p><strong>Cc</strong> フィールドに任意の指定受信者が含まれるメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[Cc] ボックスに次のメンバーが含まれている場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>このグループのメンバーを含む</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p><strong>Cc</strong> フィールドが特定のグループのメンバーである受信者を含むメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[宛先] ボックスまたは [Cc] ボックスに次が含まれている場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>[宛先] ボックスまたは [Cc] ボックスにこの人物を含む</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p><strong>To</strong> または <strong>Cc</strong> フィールドが任意の指定受信者を含むメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[宛先] ボックスまたは [Cc] ボックスに次のメンバーが含まれている場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>[宛先] または [Cc] ボックスがこのグループのメンバーを含む</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p><strong>To</strong> または <strong>Cc</strong> フィールドが特定のグループのメンバーである受信者を含むメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>メッセージ サイズが次の値以上の場合</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>サイズが次の値以上の場合</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>合計サイズ (メッセージ プラス添付ファイル) が指定値以上のメッセージです。</p>
<p>EAC では、サイズはキロバイト (KB) 単位でのみ指定できます。</p>
<p><strong>注</strong>:メールボックスのメッセージ サイズの制限は、メール フロー ルールの前に評価されます。この条件を含むルールがメッセージを処理する前に、メールボックスに対して大きすぎるメッセージが拒否されます。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>メッセージの文字セット名に次の単語のいずれかが含まれる:</strong></p>
<p><strong>メッセージ</strong> &gt; <strong>文字セット名に以下の単語のいずれかが含まれる</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>指定した文字セット名のいずれかを含むメッセージです。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## 送信者と受信者


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>送信者が受信者の 1 人</strong></p>
<p><strong>送信者と受信者</strong> &gt; <strong>送信者の受信者に対する関係が</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>送信者が受信者の管理者か、送信者が受信者によって管理されているか、どちらかのメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>次のグループのメンバー間のメッセージである</strong></p>
<p><strong>送信者と受信者</strong> &gt; <strong>メッセージは次のグループのメンバー間</strong></p></td>
<td><p><em>BetweenMemberOf1</em> と <em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em> と <em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>特定のグループのメンバー間で送信されたメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>送信者または受信者のマネージャーが次である場合</strong></p>
<p><strong>送信者と受信者の</strong> &gt; <strong>送信者または受信者のマネージャーがこの人物</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em> と <em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em> と <em>ExceptIfManagerAddress</em></p></td>
<td><p>最初のプロパティ: <code>EvaluatedUser</code></p>
<p>2 番目のプロパティ: <code>Addresses</code></p></td>
<td><p>特定のユーザーが送信者の管理者、または特定のユーザーが受信者の管理者であるメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>送信者および任意の受信者のプロパティを次のように比較する場合</strong></p>
<p><strong>送信者と受信者</strong> &gt; <strong>送信者と受信者のプロパティを比較する</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em> と <em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em> と <em>ExceptIfADComparisonOperator</em></p></td>
<td><p>最初のプロパティ: <code>ADAttribute</code></p>
<p>2 番目のプロパティ: <code>Evaluation</code></p></td>
<td><p>送信者と受信者の指定した Active Directory 属性が一致する、あるいは一致しないメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージのプロパティ


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>メッセージの種類が次である場合</strong></p>
<p><strong>メッセージのプロパティ</strong> &gt; <strong>次のメッセージの種類を含む</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>指定の種類のメッセージです。</p>

> [!NOTE]
> Outlook または Outlook Web App がメッセージを転送するように設定されている場合、<STRONG>ForwardingSmtpAddress</STRONG> プロパティがメッセージに追加されます。メッセージの種類は <CODE>AutoForward</CODE> に変更されません。


</td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>メッセージが次のように分類される場合</strong></p>
<p><strong>メッセージのプロパティ</strong> &gt; <strong>この分類を含む</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>指定したメッセージ分類を持つメッセージです。これは、<strong>New-MessageClassification</strong> コマンドレットを使用して組織内に作成できるカスタムのメッセージ分類です。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>メッセージに分類がマークされていない場合</strong></p>
<p><strong>メッセージのプロパティ</strong> &gt; <strong>分類を一切含まない</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>該当なし</p></td>
<td><p>メッセージ分類のないメッセージです。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>メッセージの SCL が次の値以上の場合</strong></p>
<p><strong>メッセージのプロパティ</strong> &gt; <strong>次の値以上の SCL を含む</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>指定値と一致するか、それを超える Spam Confidence Level (SCL) が割り当てられているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>メッセージの重要度が次に設定されている場合</strong></p>
<p><strong>メッセージのプロパティ</strong> &gt; <strong>重要度レベルを含む</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>指定された重要度レベルでマークされたメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## メッセージ ヘッダー


> [!NOTE]
> メッセージ内の件名または他のヘッダー フィールドでの単語またはテキスト パターンの検索は、SMTP サーバー間で ASCII テキスト内のバイナリ メッセージ送信に使用された MIME コンテンツ転送エンコーディング方式に基づいてメッセージがデコードされた<EM>後</EM>に行われます。条件または例外を使用して、メッセージ内の件名または他のヘッダー フィールドの未加工 (通常は Base64) のエンコード値を検索することはできません。




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件または例外</th>
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>メッセージ ヘッダーに次が含まれている場合</strong></p>
<p><strong>メッセージ ヘッダー</strong> &gt; <strong>これらの単語のいずれかを含む</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em> と <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> と <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>最初のプロパティ: <code>MessageHeaderField</code></p>
<p>2 番目のプロパティ: <code>Words</code></p></td>
<td><p>指定したヘッダー フィールドを含むメッセージであり、そのヘッダー フィールドの値には指定した単語が含まれています。</p>
<p>ヘッダー フィールドの名前とヘッダー フィールドの値は、常に一緒に使用されます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>メッセージ ヘッダーが次と一致する場合</strong></p>
<p><strong>メッセージ ヘッダー</strong> &gt; <strong>次のテキスト パターンと一致する</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em> と <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> と <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>最初のプロパティ: <code>MessageHeaderField</code></p>
<p>2 番目のプロパティ: <code>Patterns</code></p></td>
<td><p>指定したヘッダー フィールドを含むメッセージであり、そのヘッダー フィールドの値には指定した正規表現が含まれています。</p>
<p>ヘッダー フィールドの名前とヘッダー フィールドの値は、常に一緒に使用されます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## エッジ トランスポート サーバー上のメール フロー ルールの条件と例外

エッジ トランスポート サーバー上のメール フロー ルールで使用可能な条件および例外は、メールボックス サーバーで使用できるもの小さなサブセットです。エッジ トランスポート サーバー上には EAC が存在しないので、ローカルのエッジ トランスポート サーバー上の Exchange 管理シェル でしかメール フロー ルールを管理できません。次の表で、これらの条件と例外について説明します。プロパティの種類は、プロパティの種類 セクションで説明されています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 管理シェル における条件と例外のパラメーター</th>
<th>プロパティの種類</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>To</strong>、<strong>Cc</strong>、または <strong>Bcc</strong> フィールドに特定の単語が含まれているメッセージです。</p>
<p>メッセージに指定された受信者が含まれている場合、ルールのアクションはメッセージの <em>すべて</em> の受信者に適用されます (またはされません)。たとえば、メッセージは特定の受信者だけでなく、メッセージのすべての受信者に拒否されます。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p><strong>To</strong>、<strong>Cc</strong>、または <strong>Bcc</strong> フィールドに特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p>
<p>メッセージに指定された受信者が含まれている場合、ルールのアクションはメッセージの <em>すべて</em> の受信者に適用されます (またはされません)。たとえば、メッセージは特定の受信者だけでなく、メッセージのすべての受信者に拒否されます。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>任意の添付ファイルが指定値以上の添付ファイル付きメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>送信者のメール アドレスに指定の単語が含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>送信者のメール アドレスに、特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>内部または外部の送信者によって送信されたメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em> と <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> と <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>最初のプロパティ: <code>MessageHeaderField</code></p>
<p>2 番目のプロパティ: <code>Words</code></p></td>
<td><p>指定したヘッダー フィールドを含むメッセージであり、そのヘッダー フィールドの値には指定した単語が含まれています。</p>
<p>ヘッダー フィールドの名前とヘッダー フィールドの値は、常に一緒に使用されます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em> と <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> と <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>最初のプロパティ: <code>MessageHeaderField</code></p>
<p>2 番目のプロパティ: <code>Patterns</code></p></td>
<td><p>指定したヘッダー フィールドを含むメッセージであり、そのヘッダー フィールドの値には指定した正規表現が含まれています。</p>
<p>ヘッダー フィールドの名前とヘッダー フィールドの値は、常に一緒に使用されます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>合計サイズ (メッセージ プラス添付ファイル) が指定値以上のメッセージです。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>指定値と一致するか、それを超える SCL が割り当てられているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> フィールドに特定の単語が含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p><strong>Subject</strong> フィールドに特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> フィールドまたはメッセージ本文に特定の単語が含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p><strong>Subject</strong> フィールドまたはメッセージ本文に、特定の正規表現と一致するテキスト パターンが含まれているメッセージです。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## プロパティの種類

次の表で、条件と例外で使用されているプロパティ タイプについて説明します。


> [!NOTE]
> プロパティが文字列の場合、末尾のスペースは使用できません。




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティの種類</th>
<th>有効な値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>定義済みの Active Directory の属性一覧から選択</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>EAC では、同一の属性に複数の単語やテキスト パターンを指定する場合、値をコンマで区切ります。たとえば、<strong>市</strong> 属性の <strong>サンフランシスコ、パロアルト</strong> という値は、「City イコール サン フランシスコ」あるいは「City イコール パロアルト」を探します。</p>
<p>Exchange 管理シェル において、<code>Value</code>が一致させたい単語またはテキスト パターンであるとき、構文 <code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code> を使用します。</p>
<p>たとえば、<code>&quot;City:San Francisco,Palo Alto&quot;</code> または <code>&quot;City:San Francisco,Palo Alto&quot;</code>、<code>&quot;Department:Sales,Finance&quot;</code> です。</p>
<p>複数の属性、または同一の属性の複数の値を指定する場合、<strong>or</strong> 演算子を使用します。前後にスペースのある値を使用しないでください。</p>
<p><strong>Country</strong> 属性には、2 文字の ISO 3166-1 国コードの値 (たとえば、ドイツの DE) が必要であることに注意してください。値を検索するには、<a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a> を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 受信者</p></td>
<td><p>条件や例外の性質(たとえば、受信者関連条件) によって、組織内の任意のメール有効化オブジェクトを指定できることもあれば、特定のオブジェクト タイプ (たとえば、グループ メンバーシップの条件のグループ) に限定されることもあります。そして、条件や例外は単一の値を必要としたり、複数の値を許可することがあります。</p>
<p>Exchange 管理シェル においては、コンマを使用して複数の値を区切ります。</p>
<p><strong>注:</strong> この条件が、受信プロキシ アドレスに送信されるメッセージについて考慮していない点に注意してください。受信者のプライマリ メール アドレスに送信されるメッセージのみを照合します。</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>文字セット名の配列</p></td>
<td><p>メッセージ内に存在する 1 つまたは複数のコンテンツの文字セットです。以下に例を示します。</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>SMTP ドメインの配列</p></td>
<td><p>たとえば、<code>contoso.com</code> または <code>eu.contoso.com</code> などです。</p>
<p>Exchange 管理シェル において、複数のドメインをコンマで区切って指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p><strong>送信者</strong> または <strong>受信者</strong> の単一の値</p></td>
<td><p>ルールが送信者の管理者か受信者の管理者のどちらを探しているかを指定します。</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p><strong>Equal</strong> または <strong>Not equal</strong> (<code>NotEqual</code>) の単一の値</p></td>
<td><p>送信者と受信者の Active Directory 属性を比較する場合、これは値が一致するかしないかを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p><strong>低</strong>、<strong>通常</strong>、または <strong>高</strong> の単一の値</p></td>
<td><p>Outlook または Outlook Web App の送信者によってメッセージに割り当てられた重要度レベルです。</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>IP アドレスやアドレスの範囲の配列</p></td>
<td><p>次の構文を使用して IPv4 アドレスを入力します。</p>
<ul>
<li><p><strong>単一の IP アドレス</strong>   例、<code>192.168.1.1</code>。</p></li>
<li><p><strong>IP アドレス範囲</strong>   例、<code>192.168.0.1-192.168.0.254</code>。</p></li>
<li><p><strong>クラスレス ドメイン間ルーティング (CIDR) IP アドレス範囲</strong>   例、<code>192.168.0.1/25</code>。</p></li>
</ul>
<p>Exchange 管理シェル において、複数の IP アドレスまたは範囲をコンマで区切って指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p><strong>マネージャー</strong> または <strong>直属の部下</strong>(<code>DirectReport</code>) の単一の値</p></td>
<td><p>送信者と任意の受信者の間の関係を指定します。ルールは Active Directory の <strong>Manager</strong> 属性を確認して、送信者が受信者の管理者か、あるいは送信者が受信者によって管理されているかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>単一メッセージ分類</p></td>
<td><p>EAC で、作成したメッセージ分類の一覧から選択します。</p>
<p>Exchange 管理シェル において、<strong>Get-MessageClassification</strong> コマンドレットを使用してメッセージ分類を識別します。たとえば、次のコマンドを使用して <code>Company Internal</code> 分類を持つメッセージを検索し、メッセージの件名の先頭に値 <code>CompanyInternal</code> を追加します。</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>単一の文字列</p></td>
<td><p>ヘッダー フィールドの名前を指定します。ヘッダー フィールドの名前は、常にヘッダー フィールドの値とペアになっています (単語またはテキスト パターンの一致)。</p>
<p><em>メッセージ ヘッダー</em>は、メッセージの必須および省略可能のヘッダー フィールドの集合です。ヘッダー フィールドの例は <strong>To</strong>、<strong>From</strong>、<strong>Received</strong>、および <strong>Content-Type</strong> です。公式のヘッダー フィールドは RFC 5322 で定義されています。非公式のヘッダー フィールドは <strong>X-</strong> で始まり、<em>X ヘッダー</em> とも呼ばれます。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>単一メッセージ種類の値</p></td>
<td><p>次のうちいずれかのメッセージの種類を指定できます。</p>
<ul>
<li><p><strong>自動応答</strong> (<code>OOF</code>)</p></li>
<li><p><strong>自動転送</strong> (<code>AutoForward</code>)</p></li>
<li><p><strong>暗号化</strong></p></li>
<li><p><strong>予定表管理</strong></p></li>
<li><p><strong>アクセス許可制御</strong> (<code>PermissionControlled</code>)</p></li>
<li><p><strong>ボイスメール</strong></p></li>
<li><p><strong>署名済み</strong></p></li>
<li><p><strong>承認要求</strong> (<code>ApprovalRequest</code>)</p></li>
<li><p><strong>開封確認メッセージ</strong> (<code>ReadReceipt</code>)</p></li>
</ul>

> [!NOTE]
> Outlook または Outlook Web App がメッセージを転送するように設定されている場合、<STRONG>ForwardingSmtpAddress</STRONG> プロパティがメッセージに追加されます。メッセージの種類は <CODE>AutoForward</CODE> に変更されません。


</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>正規表現の配列</p></td>
<td><p>値のテキスト パターンの識別に使用されている、1 つかそれ以上の正規表現を指定します。詳細情報は、「<a href="https://go.microsoft.com/fwlink/p/?linkid=180327">正規表現構文</a>」を参照してください。</p>
<p>Exchange 管理シェル において、コンマで区切られた複数の正規表現を指定して、各正規表現を二重引用符 (&quot;) で囲みます。</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>次のいずれかの値になります。</p>
<ul>
<li><p><strong>スパム フィルターをバイパスする</strong> (<code>-1</code>)</p></li>
<li><p>整数 0 から 9</p></li>
</ul></td>
<td><p>メッセージに割り当てられた spam confidence level (SCL) を指定します。SCL 値が高いほど、メッセージがスパムである可能性が高くなります。</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>機密情報の種類の配列</p></td>
<td><p>組織において定義された、1 つかそれ以上の機密情報の種類を指定します。組み込み機密情報種類の一覧に関しては、<a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">Exchange での機密情報の種類の検索基準：</a> を参照してください。</p>
<p>Exchange 管理シェル では、構文 <code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code> を使用します。たとえば、2 つ以上のクレジット カード番号と、少なくとも 1 つの ABA ルーティング番号を含むコンテンツを検索する場合、<code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code> 値を使用します。</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>単一サイズ値</p></td>
<td><p>添付ファイルまたはメッセージ全体のサイズを指定します。</p>
<p>EAC では、サイズはキロバイト (KB) 単位でのみ指定できます。</p>
<p>Exchange 管理シェル において、値を入力するときは、値に以下の単位のいずれかを付加した形式で記述します。</p>
<ul>
<li><p><code>B</code> (バイト)</p></li>
<li><p><code>KB</code> (キロバイト)</p></li>
<li><p><code>MB</code> (メガバイト)</p></li>
<li><p><code>GB</code> (ギガバイト)</p></li>
</ul>
<p>たとえば、<code>20MB</code> のように指定します。</p>
<p>通常、単位なしの値はバイトとして扱われますが、小さい値は最も近いキロバイトの値に切り上げられます。</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p><strong>組織内</strong> (<code>InOrganization</code>) または <strong>組織外</strong> (<code>NotInOrganization</code>) の単一値</p></td>
<td><p>以下の条件のいずれかに当てはまる場合、送信者は組織内の人物と見なされます。</p>
<ul>
<li><p>送信者が、組織の Active Directory 内に存在するメールボックス、メール ユーザー、グループ、またはメール有効化パブリック フォルダーである。</p></li>
<li><p>送信者のメール アドレスが、権限のあるドメインまたは内部の中継ドメインとして構成されている承認済みドメインに属していて、<strong>かつ</strong> メッセージが認証済み接続経由で送信または受信された。承認済みドメインの詳細については、<a href="accepted-domains-exchange-2013-help.md">承認済みドメイン</a> を参照してください。</p></li>
</ul>
<p>以下の条件のいずれかに当てはまる場合、送信者は組織外の人物と見なされます。</p>
<ul>
<li><p>送信者の電子メール アドレスが承認済みドメインにない。</p></li>
<li><p>送信者の電子メール アドレスが、外部の中継ドメインとして構成されている承認済みドメインに属している。</p></li>
</ul>

> [!NOTE]
> メールの連絡先が組織の内部であるか外部であるかを判断するため、送信者アドレスが組織の承認済みドメインと比較されます。


</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>次のいずれかの値になります。</p>
<ul>
<li><p><strong>組織内</strong> (<code>InOrganization</code>)</p></li>
<li><p><strong>組織外</strong> (<code>NotInOrganization</code>)</p></li>
<li><p><strong>外部パートナー組織内</strong> (<code>ExternalPartner</code>)</p></li>
<li><p><strong>外部非パートナー組織内</strong> (<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>以下の条件のいずれかに当てはまる場合、受信者は組織内の人物と見なされます。</p>
<ul>
<li><p>受信者が、組織の Active Directory 内に存在するメールボックス、メール ユーザー、グループ、またはメール有効化パブリック フォルダーである。</p></li>
<li><p>受信者のメール アドレスが、権限のあるドメインまたは内部の中継ドメインとして構成されている承認済みドメインに属していて、<strong>かつ</strong> メッセージが認証済み接続経由で送信または受信された。</p></li>
</ul>
<p>以下の条件のいずれかに当てはまる場合、受信者は組織外の人物と見なされます。</p>
<ul>
<li><p>受信者の電子メール アドレスが承認済みドメインにない。</p></li>
<li><p>受信者の電子メール アドレスが、外部の中継ドメインとして構成されている承認済みドメインに属している。</p></li>
</ul>
<p>外部パートナー組織は、メールを送信するドメイン セキュリティ (相互 TLS 認証) が設定されている外部ドメインです。</p>
<p>外部非パートナー組織は、パートナーのドメインとは見なされないその他すべての外部ドメインです。</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>文字列の配列</p></td>
<td><p>検索する 1 つまたは複数の単語を指定します。大文字と小文字は区別されず、前後にスペースと句読点記号があっても大丈夫です。ワイルドカードおよび部分一致の機能はサポートされていません。</p>
<p>たとえば、&quot;contoso&quot; と &quot;Contoso&quot; は一致します。ただし、テキストが他の文字で囲まれている場合、一致と見なされません。たとえば、&quot;contoso&quot; は次の値とは一致しません。</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>アスタリスク (*) はリテラル文字として扱われ、ワイルドカード文字としては使用されません。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## 詳細情報

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールのアクション](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[メール フローやトランスポート ルールの手順](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

[Exchange Online でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919235\(v=exchg.150\)) (Exchange Online 向け)

[Exchange Online Protection でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919234\(v=exchg.150\)) (Exchange Online Protection 向け)

