---
title: '組織全体の免責事項、署名、フッター、またはヘッダー: Exchange 2013 Help'
TOCTitle: 組織全体の免責事項、署名、フッター、またはヘッダー
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61060497
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織全体の免責事項、署名、フッター、またはヘッダー

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

電子メール免責事項、法的免責事項、重要事項説明、署名、またはその他の情報を、組織で送受信される電子メール メッセージの上部または下部に追加することができます。法的要件、ビジネス要件、規制要件を満たすため、あるいは危険性があり得る電子メール メッセージを見分けるため、あるいはその組織特有の他の理由により、これが必要になる可能性があります。

免責事項をセットアップするにはトランスポート ルールを作成し、条件 (送信者が特定のグループに含まれている場合や、メッセージに特定のテキスト パターンが含まれている場合など) と、追加するテキストを指定します。複数の免責事項を 1 つの電子メール メッセージに適用するには、複数のトランスポート ルールを使用します。


> [!IMPORTANT]
> <UL>
> <LI>
> <P>送信メッセージにのみ情報を追加するためには、受信者が組織の外部に存在するなどの条件を追加する必要があります。既定では、トランスポート ルールは受信と送信の両方のメッセージに適用されます。</P></LI></UL>



**目次**

例

免責事項のスコープ設定

免責事項の書式設定

免責事項を追加できなかった場合のフォールバック オプション

詳細情報

手順の詳細については、「[Office 365 における組織全体のメッセージの免責事項、署名、フッター、ヘッダー](https://technet.microsoft.com/ja-jp/library/dn600323\(v=exchg.150\))」を参照してください。

## 例

ここでは、免責事項を使用する方法についていくつかのアイデアを示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>追加するサンプル テキスト</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>法的 - 送信メッセージ</p></td>
<td><p>この電子メールおよびメールと共に送信されるすべてのファイルは機密情報です。これらは宛先に指定された個人または組織のみが使用できます。この電子メールを誤って受け取った場合、システム マネージャーにお知らせください。</p></td>
</tr>
<tr class="even">
<td><p>法的 - 受信メッセージ</p></td>
<td><p>従業員は、電子メールのやりとりで、中傷的な陳述をしないこと、著作権侵害またはその他の法的権利を侵したり、許可したりしないことが明確に求められています。このような電子メールを受け取った従業員は、すぐに管理者に通知しなければなりません。</p></td>
</tr>
<tr class="odd">
<td><p>メッセージがエイリアスに送信されたことの表示</p></td>
<td><p>このメッセージは、Sales ディスカッション グループに送信されました。</p></td>
</tr>
<tr class="even">
<td><p>署名 - 各従業員のデータの取り出し</p></td>
<td><p>Kathleen Mayer<br />
営業部<br />
Contoso<br />
www.contoso.com<br />
kathleen@contoso.com<br />
携帯電話: 111-222-1234111-222-1234</p></td>
</tr>
<tr class="odd">
<td><p>広告</p></td>
<td><p>3 月のお薦めはこちらをクリックしてください</p></td>
</tr>
</tbody>
</table>


この記事の例は、そのまま使用することを意図していません。必要に応じて変更してください。

## 免責事項のスコープ設定

免責事項について作業する際に、適用対象となるメッセージについて考慮します。たとえば、内部メッセージおよび外部メッセージ、または特定の部門のユーザーによって送信されたメッセージに対して、異なる免責事項を指定できます。スレッドの最初のメッセージのみに免責事項を記載するには、免責事項の固有のテキストを探す例外を追加します。

使用できる条件および例外の例を以下に示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>説明</th>
<th>EAC における条件と例外</th>
<th>シェルにおける条件と例外</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織外部であり、元のメッセージに「CONTOSO LEGAL NOTICE」のような免責事項のテキストが含まれていない場合</p></td>
<td><p>条件: <strong>[受信者の場所が次の場合]</strong> &gt; <strong>[組織外部]</strong></p>
<p>例外: <strong>[件名または本文]</strong> &gt; <strong>[件名または本文が次のテキスト パターンと一致する]</strong> &gt; <strong>CONTOSO LEGAL NOTICE</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches &quot;CONTOSO LEGAL NOTICE&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>実行可能ファイルが添付された受信メッセージ</p></td>
<td><p>条件 1: <strong>[送信者の場所が次の場合]</strong> &gt; <strong>[組織外部]</strong></p>
<p>条件 2: <strong>[すべての添付ファイル]</strong> &gt; <strong>[実行可能なコンテンツが含まれる]</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -AttachmentHasExecutableContent</code></pre></td>
</tr>
<tr class="odd">
<td><p>送信者がマーケティング部門である</p></td>
<td><p>条件: <strong>[送信者]</strong> &gt; <strong>[このグループのメンバーである]</strong> &gt; <strong>group name</strong></p></td>
<td><pre><code>-FromMemberOf &quot;Marketing Team&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>外部の送信者から Sales ディスカッション グループに送信されるすべてのメッセージ</p></td>
<td><p>条件 1: <strong>[送信者の場所が次の場合]</strong> &gt; <strong>[組織外部]</strong></p>
<p>条件 2: <strong>[メッセージ]</strong> &gt; <strong>[[宛先] ボックスまたは [CC] ボックスにこの人物を含む]</strong> &gt; <strong>group name</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -SentTo &quot;Sales Discussion Group&quot; -PrependSubject &quot;Sent to Sales Discussion Group: &quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>1 か月間送信メッセージの先頭に広告を追加する</p></td>
<td><p>条件 1: <strong>[受信者の場所が次の場合]</strong> &gt; <strong>[組織外部]</strong></p>
<p><strong>[新しいルール]</strong> ダイアログの下部で日付を指定します。</p></td>
<td><p>-ApplyHtmlDisclaimerLocation 'Prepend' -SentToScope 'NotInOrganization' –ActivationDate ‘03/1/2014’ –ExpiryDate ‘03/31/2014’</p></td>
</tr>
</tbody>
</table>


免責事項を対象とするために使用できるトランスポート ルール条件の完全な一覧については、以下のいずれかを参照してください。

  - [Exchange Online でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [Exchange Online でのメール フロー ルールの条件と例外 (述語)](https://technet.microsoft.com/ja-jp/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## 免責事項の書式設定

必要に応じて免責事項の書式を設定できます。免責事項のテキストに含めることができる内容を以下に示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>情報のタイプ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>テキスト</p></td>
<td><p>最大で 5,000 文字です。これには HTML タグおよびインラインのカスケード スタイル シート (CSS) が含まれます。</p></td>
</tr>
<tr class="even">
<td><p>HTML およびインラインの CSS</p></td>
<td><p>HTML およびインラインの CSS スタイルを使用してテキストの形式を設定できます。たとえば、<code>&lt;HR&gt;</code> タグを使用して、免責事項の前に線を追加します。</p>
<p>テキスト形式のメッセージに免責事項を追加する場合、免責事項の HTML は無視されます。</p></td>
</tr>
<tr class="odd">
<td><p>イメージの追加</p></td>
<td><p><code>&lt;IMG&gt;</code> タグを使用して、インターネット上で使用可能なイメージをポイントします。たとえば、<code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code> のように指定します。</p>
<p>既定では、Outlook Web App および Outlook は外部 Web コンテンツ (イメージを含む) をブロックすることに注意してください。ブロックされた外部コンテンツを表示するには、ユーザーが特別の操作を実行する必要があります。つまり、<code>IMG</code> タグを使用して追加されたイメージは、既定では表示されない可能性があります。受信者が使用する可能性の高い電子メール クライアントで、<code>IMG</code> タグを使用した免責事項をテストして、正しく表示されるか確認することをお勧めします。</p></td>
</tr>
<tr class="even">
<td><p>個人用署名に情報を追加する</p></td>
<td><p>すべての電子メールに同じ方法で書式設定された同じ情報の署名を含めたい場合、<code>DisplayName</code>、<code>FirstName</code>、<code>LastName</code>、<code>PhoneNumber</code>、<code>Email</code>、<code>FaxNumber</code>、<code>Department</code> などの各従業員に関する固有の情報を追加することができます。これらの情報は、その両側を 2 つのパーセント記号 (%%) で囲む必要があります。たとえば、<code>DisplayName</code> を使用する場合、免責事項で <strong>%%DisplayName%%</strong> を使用する必要があります。</p>
<p>免責事項のルールがトリガーされると、そのユーザーの対応する値が挿入されます。データは、送信者の Active Directory ユーザー アカウント (社内 Exchange Server の場合)、または Exchange Online では送信者の Office 365 アカウントから取られます。</p>
<p>免責事項および個人用署名で使用できる属性の完全な一覧については、<a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">トランスポート ルールの条件 (述語)</a> (Exchange Server)、<a href="https://technet.microsoft.com/ja-jp/library/jj919235(v=exchg.150)">Exchange Online でのメール フロー ルールの条件と例外 (述語)</a> (Exchange Online)、または <a href="https://technet.microsoft.com/ja-jp/library/jj919234(v=exchg.150)">Exchange Online Protection でのメール フロー ルールの条件と例外 (述語)</a> (Exchange Online Protection) の <code>ADAttribute</code> プロパティの説明を参照してください。</p></td>
</tr>
</tbody>
</table>


たとえば、署名、`IMG` タグ、および埋め込み CSS を含む HTML の免責事項の例を以下に示します。

    <div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
    %%displayname%%</br>
    %%title%%</br>
    %%company%%</br>
    %%street%%</br>
    %%city%%, %%state%% %%zipcode%%</div>
    &nbsp;</br>
    <div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
    <div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
    <span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
    <p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
    <span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
    </div>

## 免責事項を追加できなかった場合のフォールバック オプション

暗号化されたメッセージなど、一部のメッセージでは Exchange で元のメッセージの内容を変更することができません。このような変更できないメッセージを組織でどのように処理するかを制御できます。免責事項を含むメッセージ エンベロープで変更できないメッセージをラップするか、免責事項を付加できない場合はメッセージを拒否するか、または免責事項アクションを無視してメッセージを免責事項なしで配信するかを指定します。

次の一覧で、各フォールバック アクションについて説明します。

  - **ラップ**   元のメッセージに免責事項を挿入できない場合、Exchange は、新しいメッセージ エンベロープで元のメッセージを包む、つまり "ラップ" します。そのうえで、免責事項が新しいメッセージに挿入されます。元のメッセージを新しいメッセージ エンベロープでラップできない場合、元のメッセージは配信されません。メッセージの送信者は、メッセージが配信されなかった理由を説明する配信不能レポート (NDR) を受信します。
    

    > [!IMPORTANT]
    > 元のメッセージが新しいメッセージ エンベロープでラップされると、以降のトランスポート ルールは元のメッセージではなく新しいメッセージ エンベロープに適用されます。したがって、元のメッセージを新しいメッセージの本文でラップする免責事項アクションを含むトランスポート ルールは、他のトランスポート ルールを構成した後で構成する必要があります。



  - **拒否**   免責事項を元のメッセージに挿入できない場合、Exchange はメッセージを配信しません。メッセージの送信者は、メッセージが配信されなかった理由を説明する NDR を受信します。

  - **無視**   免責事項を元のメッセージに挿入できない場合、Exchange は元のメッセージを変更せずに配信します。免責事項は付加されません。

## 詳細情報

[Office 365 における組織全体のメッセージの免責事項、署名、フッター、ヘッダー](https://technet.microsoft.com/ja-jp/library/dn600323\(v=exchg.150\))

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Exchange Online Protection のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

