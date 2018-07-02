---
title: 'トランスポート ルールのアクション: Exchange 2013 Help'
TOCTitle: メール フロー ルールの処理
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 49896273
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート ルールのアクション

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-05-03_

メール フロー ルール (別名トランスポート ルール) 内のアクションは、ルールの条件に一致するメッセージをどうしたいかを指定します。たとえば、特定の送信者からメッセージをモデレーターに転送したり、またはすべての送信メッセージに免責事項や個人の署名を追加するルールを作成できます。

アクションには通常、追加のプロパティが必要になります。たとえば、ルールがメッセージをリダイレクトする場合、その宛先を指定する必要があります。アクションによっては、利用可能な、または必要とされるプロパティが複数あります。たとえば、ルールがメッセージ フィールドにヘッダー フィールドを追加する場合、ヘッダーの名前と領域の両方を指定する必要があります。ルールがメッセージに免責事項を追加する場合、免責事項のテキストを指定する必要がありますが、テキストを挿入する位置やメッセージに免責事項を追加できない場合の対処方法を指定することもできます。通常、一つのルールに複数のアクションを設定することができますが、アクションのいくつかは排他的です。たとえば、一つのルールで同じメッセージの拒否とリダイレクトを行うことはできません。

Exchange Server 2013 におけるメール フロー ルールの詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)」を参照してください。

メール フロー ルールにおける条件と例外の詳細については、[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) をご覧ください。

Exchange Online におけるメール フロー ルールのアクションの詳細については、「Exchange Online Protection、[Exchange Online でのメール フロー ルールの処理](https://technet.microsoft.com/ja-jp/library/jj919237\(v=exchg.150\))」、または「[メール フロー ルールの処理 (Exchange Online Protection 向け)](https://technet.microsoft.com/ja-jp/library/jj920117\(v=exchg.150\))」を参照してください。

## メールボックス サーバー上のメール フロー ルールのアクション

メールボックス サーバー上のメール フロー ルールで使用可能なアクションについて、次の表で解説します。各プロパティの有効な値については、「プロパティ値」に説明があります。

**注**:

  - Exchange 管理センター (EAC) 内のアクションを選択した後、最終的に **次の操作を実行** フィールドに示される値は、自分で選択したクリック パスとは異なることがよくあります。また、新しいルールを作成する場合、時として (選択によっては) クリック パスのすべてをなぞる代わりに、テンプレート (アクションのフィルター済みリスト) から短いアクション名を選択できる場合があります。短い名前と完全なクリック パスの値は、表の EAC 列に示されています。

  - **Get-TransportRuleAction** コマンドレットによって戻されたアクションの名前のいくつかは、対応するパラメーター名とは違っており、一つのアクションに複数のパラメーターが必要となることがあります。


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
<th>EAC でのアクション</th>
<th>Exchange 管理シェル でのアクション パラメーター</th>
<th>プロパティ</th>
<th>説明</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>[次のユーザーにメッセージを転送して承認を受ける]</strong></p>
<p><strong>[メッセージを転送して承認を受ける]</strong> &gt; <strong>[次のユーザーに]</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>メッセージを承認要求でラップされた添付ファイルとして特定のモデレーターに転送します。詳細については <a href="common-message-approval-scenarios-exchange-2013-help.md">一般的なメッセージの承認シナリオ</a> をご覧ください。配布グループをモデレーターとして使用することはできません。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[送信者の上司にメッセージを転送して承認を受ける]</strong></p>
<p><strong>[メッセージを転送して承認を受ける]</strong> &gt; <strong>[送信者の上司に]</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>該当なし</p></td>
<td><p>送信者の上司にメッセージを転送して承認を受けます。</p>
<p>このアクションは、送信者の <strong>Manager</strong> 属性が Active Directory で定義されている場合のみ有効です。でなければ、メッセージは受信者にもレートなしで送信されます。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[メッセージを受信者にリダイレクトする]</strong></p>
<p><strong>[メッセージをリダイレクトする]</strong> &gt; <strong>[これらの受信者に]</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>特定の受信者にメッセージをリダイレクトします。元の受信者にメッセージを配信せず、送信者や元の受信者に通知を送信しません。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[説明を示してメッセージを拒否する]</strong></p>
<p><strong>[メッセージをブロックする]</strong> &gt; <strong>[メッセージを拒否して説明を含める]</strong></p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>指定されたテキストを却下の理由として含む配信不能レポート (別名 NDR またはバウンス メッセージ) で、送信者にメッセージを返します。受信者は元のメッセージも通知も受信しません。</p>
<p><code>5.7.1</code> で使用される既定拡張状態コードです。</p>
<p>Exchange 管理シェル でのルールを作成または修正する場合、<em>RejectMessageEnhancedStatusCode</em> パラメーターを使用することで DSN コードを指定できます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[拡張状態コードのメッセージを拒否する]</strong></p>
<p><strong>[メッセージをブロックする]</strong> &gt; <strong>[次の拡張状態コードのメッセージを拒否する]</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>指定した拡張配信状態通知 (DSN) コード付きの NDR でメッセージを送信者に返します。受信者は元のメッセージも通知も受信しません。</p>
<p>有効な DSN コードは、<code>5.7.1</code> または <code>5.7.900</code> から <code>5.7.999</code> です。</p>
<p>使用される既定の理由のテキストは <code>Delivery not authorized, message refused</code> です。</p>
<p>Exchange 管理シェル でのルールを作成または修正する場合、<em>RejectMessageReasonText</em> パラメーターを使用することで拒否理由のテキストを指定できます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[だれにも通知せずにメッセージを削除する]</strong></p>
<p><strong>[メッセージをブロックする]</strong> &gt; <strong>[だれにも通知せずにメッセージを削除する]</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>該当なし</p></td>
<td><p>受信者や送信者に通知を送信することなく、確認なしにメッセージを削除します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[受信者を BCC ボックスに追加する]</strong></p>
<p><strong>[受信者を追加する]</strong> &gt; <strong>[Bcc ボックスに]</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>メッセージの <strong>Bcc</strong> フィールドに一人以上の受信者を追加します。元の受信者は通知を受けず、追加のアドレスを見ることもできません。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[受信者を宛先ボックスに追加する]</strong></p>
<p><strong>[受信者を追加する]</strong> &gt; <strong>[宛先ボックスに]</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>メッセージの <strong>To</strong> フィールドに一人以上の受信者を追加します。元の受信者は追加のアドレスを見ることができます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[受信者を CC ボックスに追加する]</strong></p>
<p><strong>[受信者を追加する]</strong> &gt; <strong>[CC ボックスに]</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>メッセージの <strong>Cc</strong> フィールドに一人以上の受信者を追加します。元の受信者は追加のアドレスを見ることができます。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[送信者のマネージャーを受信者として追加する]</strong></p>
<p><strong>[受信者を追加する]</strong> &gt; <strong>[送信者の上司を受信者として追加する]</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>送信者の上司を指定の受信者タイプ (<strong>To</strong>、<strong>Cc</strong>、<strong>Bcc</strong>) としてメッセージに追加したり、送信者や受信者に通知することなくメッセージを送信者の上司にリダイレクトします。</p>
<p>このアクションは、送信者の <strong>Manager</strong> 属性が Active Directory で定義されている場合のみ有効です。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>免責事項の追加</strong></p>
<p><strong>[メッセージに免責事項を適用する]</strong> &gt; <strong>[末尾に免責事項を追加する]</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>最初のプロパティ:<code>DisclaimerText</code></p>
<p>2 番目のプロパティ: <code>DisclaimerFallbackAction</code></p>
<p>3 番目のプロパティ (Exchange 管理シェル のみ)。<code>DisclaimerTextLocation</code></p></td>
<td><p>メッセージの末尾に指定した HTML 免責事項を適用します。</p>
<p>Exchange 管理シェル 内のルールを作成または修正する場合、<code>Append</code> の値を持つ <em>ApplyHtmlDisclaimerTextLocation</em> パラメーターを使用します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[先頭に免責事項を追加]</strong></p>
<p><strong>[メッセージに免責事項を適用する]</strong> &gt; <strong>[先頭に免責事項を追加]</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>最初のプロパティ:<code>DisclaimerText</code></p>
<p>2 番目のプロパティ: <code>DisclaimerFallbackAction</code></p>
<p>3 番目のプロパティ (Exchange 管理シェル のみ)。<code>DisclaimerTextLocation</code></p></td>
<td><p>メッセージの先頭に指定した HTML 免責事項を適用します。</p>
<p>Exchange 管理シェル 内のルールを作成または修正する場合、<code>Prepend</code> の値を持つ <em>ApplyHtmlDisclaimerTextLocation</em> パラメーターを使用します。</p>
<p></p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[このヘッダーを削除する]</strong></p>
<p><strong>[メッセージのプロパティを変更する]</strong> &gt; <strong>[メッセージのヘッダーを削除する]</strong></p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>指定されたヘッダー フィールドをメッセージから削除します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[メッセージ ヘッダーをこの値に設定する]</strong></p>
<p><strong>[メッセージのプロパティを変更する]</strong> &gt; <strong>[メッセージ ヘッダーを設定する]</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>最初のプロパティ: <code>MessageHeaderField</code></p>
<p>2 番目のプロパティ: <code>String</code></p></td>
<td><p>メッセージ ヘッダーで指定されたヘッダー フィールドを追加または変更し、ヘッダー フィールドを指定した値に設定します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>メッセージ分類の適用</strong></p>
<p><strong>[メッセージ プロパティを変更する]</strong> &gt; <strong>[メッセージ分類を適用する]</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>メッセージに指定のメッセージ分類を適用します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[Spam Confidence Level (SCL) を次の値に設定する]</strong></p>
<p><strong>[メッセージ プロパティを変更する]</strong> &gt; <strong>[spam confidence level (SCL) を設定する]</strong></p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>メッセージの spam confidence level (SCL) を指定の値に設定します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[メッセージに権利保護を適用する]</strong></p>
<p><strong>[メッセージのセキュリティを変更する]</strong> &gt; <strong>[権利保護を適用する]</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>指定された RMS (Rights Management Services) テンプレートをメッセージに適用します。</p>
<p>RMS では Exchange Enterprise クライアント アクセス ライセンス (CALs) が、各メールボックス毎必要になります。CAL の詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange のライセンスについてよく寄せられる質問 (FAQ)</a>を参照してください。</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[TLS 暗号化を要求する]</strong></p>
<p><strong>[メッセージのセキュリティを変更する]</strong> &gt; <strong>[TLS 暗号化を要求する]</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>送信メッセージの TLS 暗号化接続経由でのルーティングを強制します。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[メッセージの件名の先頭に追加する]</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>メッセージの <strong>Subject</strong> フィールドの冒頭に指定のテキストを追加します。元の件名のテキストを区別するために、指定されたテキストの最後の文字としてスペースまたはコロン (:) を使用してください。</p>
<p>メッセージの件名内のテキストにすでに含まれているものと同じ文字列 (例、返信) が追加されることを防ぐため、<strong>[件名に含む]</strong> (<em>ExceptIfSubjectContainsWords</em>) の例外を規則に追加します。</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[ポリシー ヒントを使用して送信者に通知する]</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em> (Exchange 管理シェル のみ)</p></td>
<td><p>最初のプロパティ: <code>NotifySenderType</code></p>
<p>2 番目のプロパティ: <code>String</code></p>
<p>3 番目のプロパティ (Exchange 管理シェル のみ)。<code>DSNEnhancedStatusCode</code></p></td>
<td><p>メッセージが DLP ポリシーに一致する場合、送信者に通知したりメッセージをブロックしたりします。</p>
<p>このアクションを使用する場合は、<strong>[メッセージに機密情報が含まれる]</strong> (<em>MessageContainsDataClassification</em>条件を使用する必要があります。</p>
<p>Exchange 管理シェル 内のルールを作成または修正する場合、<em>RejectMessageReasonText</em> パラメーターはオプションになります。このパラメーターを使用しない場合、既定テキストは <code>Delivery not authorized, message refused</code> です。</p>
<p>Exchange 管理シェル において、拡張状態コードを指定するために <em>RejectMessageEnhancedStatusCode</em> パラメーターを使用することもできます。このパラメーターを使用しない場合、既定拡張状態コード <code>5.7.1</code> が使用されます。</p>
<p>このアクションは、ルールで設定可能な他の条件、例外、およびアクションを制限します。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[インシデント レポートを生成し送信する]</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>最初のプロパティ:<code>Addresses</code></p>
<p>2 番目のプロパティ:<code>IncidentReportContent</code></p></td>
<td><p>指定された受信者に指定されたコンテンツを含むインシデント レポートを送信します。</p>
<p>インシデント レポートは、組織のデータ紛失防止 (DLP) ポリシーに一致するメッセージに対して生成されます。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>受信者にメッセージで通知します。</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>メッセージの受信者に送信される通知メッセージに含まれるテキスト、HTML、およびメッセージのキーワードを指定します。たとえば、受信者に対して、ルールによってメッセージが拒否されたことや、スパムとしてマークが付けられ、迷惑メール フォルダーに送信されたことなどを通知します。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="odd">
<td><p><strong>[このルールのプロパティ]</strong> セクション &gt; <strong>[重大度レベルでこのルールを監査する]</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>以下のいずれかを指定します:</p>
<ul>
<li><p>インシデント レポートおよび対応する入力の、メッセージ追跡ログ内の生成を防止する。</p></li>
<li><p>インシデント レポートおよび対応する入力を、指定の重大度レベル (低、中、または高) 付でメッセージ追跡ログ内に生成する。</p></li>
</ul></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
<tr class="even">
<td><p><strong>[このルールのプロパティ]</strong> セクション &gt; <strong>[ルールの処理を中止する]</strong></p>
<p><strong>その他のオプション</strong> &gt; <strong>[このルールのプロパティ]</strong> セクション &gt; <strong>[ルールの処理を中止する]</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>該当なし</p></td>
<td><p>メッセージがルールにより影響された後、そのメッセージが他のルールによる処理から除外されるよう指定します。</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
</tbody>
</table>


\[トップに戻る\]

## エッジ トランスポート サーバー上のメール フロー ルールのアクション

メールボックス サーバーで使用可能なアクションの小さなサブセットはエッジ トランスポート サーバーでも利用可能ですが、エッジ トランスポート サーバー上のみで使用可能なアクションもいくつかあります。エッジ トランスポート サーバー上には EAC が存在しないので、ローカルのエッジ トランスポート サーバー上の Exchange 管理シェル でしかメール フロー ルールを管理できません。アクションについては以下の表を参照してください。プロパティの種類については、プロパティの値 のセクションで説明します。


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
<th>Exchange 管理シェル でのアクション パラメーター</th>
<th>プロパティ</th>
<th>説明</th>
<th>使用可能な場所</th>
<th>使用できる場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>メッセージの <strong>To</strong> フィールドに一人以上の受信者を追加します。元の受信者は追加のアドレスを見ることができます。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>メッセージの <strong>Bcc</strong> フィールドに一人以上の受信者を追加します。元の受信者は通知を受けず、追加のアドレスを見ることもできません。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>メッセージの <strong>Cc</strong> フィールドに一人以上の受信者を追加します。元の受信者は追加のアドレスを見ることができます。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>該当なし</p></td>
<td><p>受信者や送信者に通知を送信することなく、確認なしにメッセージを削除します。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>該当なし</p></td>
<td><p>NDR メッセージを生成することなく、送信側サーバーとエッジ トランスポート サーバー間の SMTP 接続を終了します。</p></td>
<td><p>エッジ トランスポート サーバーのみ</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>ローカルのエッジ トランスポート サーバーのアプリケーション ログに、指定されたテキストでイベントを生成します。入力には次の情報が含まれます。</p>
<ul>
<li><p><strong>レベル</strong> <code>Information</code></p></li>
<li><p><strong>ソース</strong> <code>MSExchange Messaging Policies</code></p></li>
<li><p><strong>イベント ID</strong> <code>4000</code></p></li>
<li><p><strong>タスク カテゴリ</strong> <code>Rules</code></p></li>
<li><p><strong>EventData</strong> <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>エッジ トランスポート サーバーのみ</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>メッセージの <strong>Subject</strong> フィールドの冒頭に指定のテキストを追加します。元の件名と区別するために、指定されたテキストの最後の文字としてスペースまたはコロン (:) を使用してください。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>該当なし</p></td>
<td><p>エッジ トランスポート サーバー上のコンテンツ フィルター設定で定義されている検疫メールボックスに、メッセージを配信します。詳細については、<a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">スパム検疫メールボックスの構成</a> をご覧ください。</p>
<p>検疫メールボックスが設定されていない場合、メッセージは送信者に NDR で返されます。</p></td>
<td><p>エッジ トランスポート サーバーのみ</p></td>
<td><p>Exchange 2010 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>特定の受信者にメッセージをリダイレクトします。元の受信者にメッセージを配信せず、送信者や元の受信者に通知を送信しません。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>指定されたヘッダー フィールドをメッセージから削除します。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>最初のプロパティ: <code>MessageHeaderField</code></p>
<p>2 番目のプロパティ: <code>String</code></p></td>
<td><p>メッセージ ヘッダーで指定されたヘッダー フィールドを追加または変更し、ヘッダー フィールドを指定した値に設定します。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>メッセージの (SCL) を指定の値に設定します。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>最初のプロパティ: <code>String</code></p>
<p>2 番目のプロパティ: <code>SMTPStatusCode</code></p></td>
<td><p>指定された SMTP 状態コードおよび指定された拒否テキストで、送信側サーバーとエッジ トランスポート サーバーの間の SMTP 接続を終了します。受信者は元のメッセージも通知も受信しません。</p>
<p>SMTP 状態コードの有効な値は、RFC 3463 で定義されているように、<code>400</code> から <code>500</code> の整数です。</p>
<p>SMTP 状態コードを指定せずに拒否のテキストを指定すると、既定のコード <code>550</code> が使用されます。</p>
<p>拒否テキストを指定せずに SMTP 状態コードを指定する場合、使用されるテキストは <code>Delivery not authorized, message refused</code> です。</p></td>
<td><p>エッジ トランスポート サーバーのみ</p></td>
<td><p>Exchange 2007 以降</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>該当なし</p></td>
<td><p>メッセージがルールにより影響された後、そのメッセージが他のルールによる処理から除外されるよう指定します。</p></td>
<td><p>メールボックス サーバーとエッジ トランスポート サーバー</p></td>
<td><p>Exchange 2013 以降</p></td>
</tr>
</tbody>
</table>


## プロパティ値

メール フロー ルール内のアクション用に使用されるプロパティ値を以下の表で説明します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ</th>
<th>有効な値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>次のいずれかの値になります。</p>
<ul>
<li><p><strong>To</strong></p></li>
<li><p><strong>Cc</strong></p></li>
<li><p><strong>Bcc</strong></p></li>
<li><p><strong>リダイレクト</strong></p></li>
</ul></td>
<td><p>メッセージに送信者の上司を含める方法を指定します。</p>
<ul>
<li><p><strong>To</strong>、<strong>Cc</strong>、または <strong>Bcc</strong> を選択した場合、送信者の上司が指定のフィールドに受信者として追加されます。</p></li>
<li><p><strong>リダイレクト</strong> を指定する場合、メッセージは送信者や受信者への通知なしに送信者の上司のみに送信されます</p></li>
</ul>
<p>このアクションは、送信者の <strong>Manager</strong> 属性が Active Directory で定義されている場合のみ有効です。</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 受信者</p></td>
<td><p>アクションによって、組織内の任意のメール有効化オブジェクトを指定できる場合や、特定のオブジェクト タイプに限定される場合があります。通常、複数の受信者を選択可能ですが、インシデント レポートは一人の受信者のみに送信できます。</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>次のいずれかの値になります。</p>
<ul>
<li><p><strong>[重大度レベルでこのルールを監査する]</strong> のチェックを外す、または <strong>[重大度のレベルでこのルールを監査する]</strong> を、値 <strong>指定なし</strong> (<code>DoNotAudit</code>) で選択する</p></li>
<li><p><strong>低</strong></p></li>
<li><p>[<strong>Medium</strong>]</p></li>
<li><p><strong>高</strong></p></li>
</ul></td>
<td><p>値 <strong>低</strong>、<strong>中</strong>、または <strong>高</strong> は、インシデント レポートとメッセージ追跡ログ内の対応する入力の重大度レベルを指定します。</p>
<p>その他の値はインシデント レポートの生成を防止し、対応する入力がメッセージ追跡ログに書き込まれることを防ぎます。</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>次のいずれかの値になります。</p>
<ul>
<li><p><strong>ラッピング</strong></p></li>
<li><p><strong>無視</strong></p></li>
<li><p><strong>拒否</strong></p></li>
</ul></td>
<td><p>メッセージに免責事項を適用できない場合にすべきことを指定できます。メッセージの内容を変更できない場合があります (例、メッセージが暗号化されている場合)。利用可能なフォールバック オプションは以下のとおりです:</p>
<ul>
<li><p><strong>ラッピング</strong>   元のメッセージを新しいメッセージのエンベロープでラッピングし、免責事項のテキストを新しいメッセージに挿入します。これは既定値です。</p>
<p><strong>注</strong>:</p>
<ul>
<li><p>以降のメール フロー ルールは、元のメッセージではなく新しいメッセージのエンベロープに適用されます。したがって、これらのルールは他のルールよりも低い優先度で構成します。</p></li>
<li><p>元のメッセージを新しいメッセージ エンベロープでラップできない場合、元のメッセージは配信されません。メッセージは NDR で送信者に返されます。</p></li>
</ul></li>
<li><p><strong>無視</strong>   ルールは無視され、メッセージは免責事項なしで配信されます。</p></li>
<li><p><strong>拒否</strong>   メッセージは NDR で送信元に返されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>HTML 文字列</p></td>
<td><p>HTML タグ、インラインのカスケード スタイル シート (CSS) のタグ、および IMG タグを使用した画像を含めることが可能な、免責事項テキストを指定します。最大の長さはタグを含めて 5000 文字です。</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>単一の値: <code>Append</code> または <code>Prepend</code></p></td>
<td><p>Exchange 管理シェル において、メッセージ内の免責事項テキストの位置を指定するには <em>ApplyHtmlDisclaimerTextLocation</em> を使用します:</p>
<ul>
<li><p><code>Append</code>   免責事項をメッセージ本文の末尾に追加します。これは既定値です。</p></li>
<li><p><code>Prepend</code>   免責事項をメッセージ本文の冒頭に追加します。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>単一 DSN コード値:</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p><code>5.7.900</code> through <code>5.7.999</code></p></li>
</ul></td>
<td><p>使用される DSN コードを指定します。<strong>New-SystemMessage</strong> コマンドレットを使用してカスタム DSN を作成することができます。</p>
<p>DSN コードと拒否理由テキストを指定しない場合、<code>Delivery not authorized, message refused</code> が既定の理由テキストとして使用されます。</p>
<p>Exchange 管理シェル でのルールを作成または修正する場合、<em>RejectMessageReasonText</em> パラメーターを使用することで拒否理由のテキストを指定できます。</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>次のいずれか、または複数の値を指定します。</p>
<ul>
<li><p><strong>送信者</strong></p></li>
<li><p><strong>受信者</strong></p></li>
<li><p><strong>件名</strong></p></li>
<li><p><strong>Cc された受信者</strong> (<code>Cc</code>)</p></li>
<li><p><strong>Bcc された受信者</strong> (<code>Bcc</code>)</p></li>
<li><p><strong>重大度</strong></p></li>
<li><p><strong>送信者の優先情報</strong> (<code>Override</code>)</p></li>
<li><p><strong>一致するルール</strong> (<code>RuleDetections</code>)</p></li>
<li><p><strong>誤検出の報告</strong> (<code>FalsePositive</code>)</p></li>
<li><p><strong>検出されたデータ分類</strong> (<code>DataClassifications</code>)</p></li>
<li><p><strong>一致するコンテンツ</strong> (<code>IdMatch</code>)</p></li>
<li><p><strong>元のメール</strong> (<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>インシデント レポートに含む元のメッセージ プロパティを指定します。これらのプロパティの任意の組み合わせを選択可能です。指定したプロパティに加え、メッセージ ID が常に含まれます。以下は利用可能なプロパティです:</p>
<ul>
<li><p><strong>[送信者]</strong>   元のメッセージの送信者。</p></li>
<li><p><strong>[受信者]</strong>、<strong>[Cc された受信者]</strong>、および <strong>[Bcc された受信者]</strong>   メッセージの全受信者および <strong>Cc</strong> または <strong>Bcc</strong> フィールド内の受信者のみ。各プロパティごと、最初の 10 名の受信者のみがインシデント レポートに含まれます。</p></li>
<li><p><strong>[件名]</strong>   元のメッセージの <strong>Subject</strong> フィールド</p></li>
<li><p><strong>[重大度]</strong>   トリガーされたルールの監査重大度。メッセージ追跡ログはすべての監査重大度レベルを含み、監査重大度でフィルターすることが可能です。EAC において、<strong>[このルールを重大度レベルで監査する]</strong> のチェックボックス (Exchange 管理シェル 内、<em>SetAuditSeverity</em> [パラメーター値] <code>DoNotAudit</code>) を外すと、一致するルールはルール レポートに表示されなくなります。メッセージが一つ以上のルールで処理されている場合、最高中大度が任意のインシデント レポートに含まれます。</p></li>
<li><p><strong>[送信者優先情報]</strong>   送信者がポリシー ヒントを上書きする選択をした場合の上書き。送信者が理由を提示した場合、理由の最初の 100 文字も含まれます。</p></li>
<li><p><strong>[一致するルール]</strong>   メッセージがトリガーしたルールの一覧。</p></li>
<li><p><strong>[誤検出報告]</strong>   送信者がメッセージをポリシー ヒント用に誤検出とマークした場合の誤検出。</p></li>
<li><p><strong>[検出されたデータ分類]</strong>   メッセージに検出された機密情報の種類の一覧。</p></li>
<li><p><strong>一致するコンテンツ</strong>   検出された機密情報の種類、メッセージ内の完全に一致したコンテンツ、および検出された機密情報の前後 150 文字</p></li>
<li><p><strong>元のメール</strong>   ルールをトリガーした全メッセージがインシデント レポートに添付されます。</p></li>
</ul>
<p>Exchange 管理シェル において、複数の値をコンマで区切って指定します。</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>単一のメッセージ分類オブジェクト</p></td>
<td><p>EAC で、使用可能なメッセージの分類の一覧から選択します。</p>
<p>Exchange 管理シェル 内では、<strong>Get-MessageClassification</strong> コマンドレットを使用して利用可能なメッセージ分類オブジェクトを確認します。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>単一の文字列</p></td>
<td><p>追加、削除、または変更する SMTP メッセージ ヘッダーを指定します。</p>
<p><em>メッセージ ヘッダー</em>は、メッセージの必須および省略可能のヘッダー フィールドの集合です。ヘッダー フィールドの例は <strong>To</strong>、<strong>From</strong>、<strong>Received</strong>、および <strong>Content-Type</strong> です。公式のヘッダー フィールドは RFC 5322 で定義されています。非公式のヘッダー フィールドは <strong>X-</strong> で始まり、<em>X ヘッダー</em> とも呼ばれます。</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>プレーン テキスト、HTML タグ、およびキーワードの任意の組み合わせ</p></td>
<td><p>受信者の通知メッセージで使用するテキストを指定します。</p>
<p>プレーン テキスト、HTML タグだけでなく、元のメッセージからの値を使用する次のキーワードを指定できます。</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>次のいずれかの値になります。</p>
<ul>
<li><p><strong>[送信者に通知するが、送信を許可]</strong> (<code>NotifyOnly</code>)</p></li>
<li><p><strong>メッセージをブロックする</strong> (<code>RejectMessage</code>)</p></li>
<li><p><strong>[誤検知である場合を除いてメッセージをブロックする]</strong> (<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>[メッセージをブロックするが、送信者に上書きと送信を許可する]</strong> (<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>[メッセージをブロックするが、送信者が業務上の理由を示して上書きし、送信することを許可する]</strong> (<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>メッセージが DLP ポリシーに違反する場合、送信者が受信するポリシー ヒントの種類を指定します。次のリストで設定を説明します。</p>
<ul>
<li><p><strong>[送信者に通知するが、送信を許可する]</strong> 送信者が通知されるが、メッセージは通常どおり送信されます。</p></li>
<li><p><strong>[メッセージをブロックする]</strong> メッセージは拒否され、送信者に通知されます。</p></li>
<li><p><strong>[誤検出以外、メッセージをブロックする]</strong> 送信者により誤検出とマークされていない限り、メッセージを拒否します。</p></li>
<li><p><strong>[メッセージをブロックするが、送信者に上書きと送信を許可する]</strong> 送信者がポリシー規制を上書きする選択をしない限り、メッセージを拒否します。</p></li>
<li><p><strong>[メッセージをブロックするが、送信者が業務上の理由を示して上書きし、送信することを許可する</strong> これは <strong>[メッセージをブロックするが、送信者に上書きと送信を許可する</strong> タイプと似ていますが、送信者はポリシー規制を上書きする理由も提示します。</p></li>
</ul>
<p>このアクションを使用する場合は、<strong>[メッセージに機密情報が含まれる]</strong> (<em>MessageContainsDataClassification</em>) 条件を使用する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>単一 RMS テンプレート オブジェクト</p></td>
<td><p>メッセージに適用された Rights Management Services (RMS) テンプレートを指定します。</p>
<p>EAC では、リストから RMS テンプレートを選択します。</p>
<p>Exchange 管理シェル では、<strong>Get-RMSTemplate</strong> コマンドレットを使用して利用可能な RMS テンプレートを参照してください。</p>
<p>RMS では Exchange Enterprise クライアント アクセス ライセンス (CALs) が、各メールボックス毎必要になります。CAL の詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange のライセンスについてよく寄せられる質問 (FAQ)</a>を参照してください。</p></td>
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
<td><p><code>String</code></p></td>
<td><p>単一の文字列</p></td>
<td><p>指定されたメッセージのヘッダー フィールド、NDR、またはイベント ログ エントリに適用されているテキストを指定します。</p>
<p>Exchange 管理シェル において、値がスペースを含む場合、値を二重引用符 (&quot;) で囲んでください。</p></td>
</tr>
</tbody>
</table>


\[トップに戻る\]

## 詳細情報

[メール フロー ルールを管理します](manage-mail-flow-rules-exchange-2013-help.md)

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Exchange Online でのメール フロー ルールの処理](https://technet.microsoft.com/ja-jp/library/jj919237\(v=exchg.150\)) 呼出し時間Exchange Online

[メール フロー ルールの処理 (Exchange Online Protection 向け)](https://technet.microsoft.com/ja-jp/library/jj920117\(v=exchg.150\)) (Exchange Online Protection 向け)

[Office 365 における組織全体のメッセージの免責事項、署名、フッター、ヘッダー](https://technet.microsoft.com/ja-jp/library/dn600323\(v=exchg.150\))

