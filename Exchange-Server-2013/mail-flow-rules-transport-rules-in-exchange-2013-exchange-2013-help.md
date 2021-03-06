﻿---
title: 'メール フローやトランスポート ルール: Exchange 2013 Help'
TOCTitle: メール フロー ルール (トランスポート ルール)
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 49896460
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール フローやトランスポート ルール

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-04-28_

メール フロー ルール (別名トランスポート ルール) は、Exchange 2013 組織を通過するメッセージを識別し、アクションを実行するために使用できます。メール フロー ルールは、Outlook および Outlook Web App で使用できる受信トレイ ルールに似ています。最大の違いは、メール フロー ルールはメールボックスにメッセージが届いた後ではなく、送信中のメッセージに対しアクションを実行するということです。メール フロー ルールにはより多くの条件、例外、アクションが含まれるため、多種多様なメッセージング ポリシーを柔軟に実装することができます。

この記事では、メール フロー ルールのコンポーネントとその機能について説明します。

Exchange Online におけるメール フロー ルールの情報については、「[Exchange Online のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/jj919238\(v=exchg.150\))」を参照してください。Exchange Online Protection におけるメール フロー ルールの情報については、「[Exchange Online Protection のメール フロー ルール (トランスポート ルール)](https://technet.microsoft.com/ja-jp/library/dn271424\(v=exchg.150\))」を参照してください。

メール フロー ルールを管理するために、Exchange 管理センター (EAC)、または Exchange 管理シェル を使用できます。トランスポート ルールを管理する方法の詳細については、[メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules) を参照してください。

ルールごとに、ルールを適用、ルールをテスト、ルールをテストして送信者に通知するという、いずれかのオプションを選択できます。テストのオプションについては、[メール フロー ルールのテスト](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules) および [ポリシー ヒント](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips)を参照してください。

メール フロー ルールを使用して特定のメッセージング ポリシーを実装するには、次のトピックを参照してください。

  - [トランスポート ルールを使用してメッセージの添付を検査する](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [添付ファイル ブロックの一般的なシナリオ](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)

  - [組織全体の免責事項、署名、フッター、またはヘッダー](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [メッセージが低優先メール機能を迂回できるメール フロー ルールを使用する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/use-rules-to-bypass-clutter)

  - [単語、語句、パターンの一覧に基づいてメールをルーティングするメール フロー ルールの使用](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/use-rules-to-route-email)

  - [一般的なメッセージの承認シナリオ](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/common-message-approval-scenarios)

## メール フロー ルールの構成要素

メール フロー ルールは条件、例外、アクション、プロパティからできています。

  - <strong>条件</strong>   アクションを適用するメッセージを特定します。一部の条件は、メッセージ ヘッダー フィールド (例、宛先、差出人、または CC フィールド) を確認します。その他の条件はメッセージ プロパティ (例、メッセージの件名、本文、添付ファイル、メッセージ サイズ、またはメッセージ分類) を確認します。ほとんどの条件は、比較演算子 (例、次と一致する、次と一致しない、または次が含まれる) と一致する値を指定する必要があります。条件または例外が 1 つもない場合、ルールはすべてのメッセージに適用されます。
    
    Exchange 2013 におけるメール フロー ルール条件の詳細については、「[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - <strong>例外</strong>   アクションが適用されないメッセージを任意で特定します。条件で使用可能なメッセージ識別子と同じものが、例外でも使用可能です。例外は条件より優先され、メッセージが構成されているすべての条件に一致していても、そのメッセージにルール アクションが適用されないようにします。

  - <strong>アクション</strong>   ルールの条件に一致し、いずれの例外にも一致しないメッセージに対して行うことを指定します。使用できるアクションには、メッセージの拒否、削除、またはリダイレクト、受信者の追加、メッセージの件名へのプレフィックスの追加、またはメッセージ本文への免責事項の挿入など、多数のものがあります。
    
    Exchange 2013 におけるメール フロー ルール操作の詳細については、「[トランスポート ルールのアクション](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - <strong>プロパティ</strong> その他のルールの設定で、条件、例外、またはアクションではないものを指定します。たとえば、いつルールを適用するか、ルールを強制するか、あるいはテストするかどうか、およびルールを有効化する期間などです。
    
    詳細に関しては、このトピックの「メール フロー ルールのプロパティ」セクションを参照してください。

## 複数の条件、例外、アクション

次の表は、複数の条件、条件の値、例外、アクションが、ルールでどのように処理されるのかを説明しています。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>ロジック</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>複数の条件</p></td>
<td><p>および</p></td>
<td><p>メッセージは、ルールのすべての条件に一致しなければなりません。別々の条件に一致させる必要がある場合は、条件ごとに個別のルールを使用します。たとえば、ファイルが添付されたメッセージと、特定のテキストを含んでいるメッセージに同じ免責事項を追加するには、それぞれの条件ごとに 1 つのルールを作成します。EAC においては、ルールは簡単にコピーできます。</p></td>
</tr>
<tr class="even">
<td><p>複数の値を持つ 1 つの条件</p></td>
<td><p>または</p></td>
<td><p>条件によっては、複数の値を指定できる場合もあります。メッセージは指定された値の任意の 1 つ (すべてではない) に一致する必要があります。たとえば、メール メッセージの件名が「<strong>株価情報</strong>」で、<strong>[件名に次のいずれかの語が含まれている場合]</strong> という条件が「<strong>Contoso</strong>」または「<strong>株</strong>」のいずれかの単語に一致するよう構成されていたとすると、件名に値が少なくとも 1 つは含まれているので、この条件は満たされています。</p></td>
</tr>
<tr class="odd">
<td><p>複数の例外</p></td>
<td><p>または</p></td>
<td><p>メッセージがいずれか 1 つの例外に一致すると、アクションはメッセージに適用されません。メッセージがすべての例外に一致する必要はありません。</p></td>
</tr>
<tr class="even">
<td><p>複数のアクション</p></td>
<td><p>および</p></td>
<td><p>ルールの条件に一致するメッセージには、ルールに指定されるすべてのアクションが実行されます。たとえば、<strong>[メッセージの件名の先頭に付加する]</strong> というアクションと、<strong>[受信者を BCC ボックスに追加する]</strong> というアクションが選択されている場合、両方のアクションがメッセージに適用されます。</p>
<p><strong>[だれにも通知せずにメッセージを削除する]</strong> などの一部のアクションは、後続のルールがメッセージに適用されないようにします。<strong>[メッセージを転送する]</strong> など、追加のアクションを使用できないアクションもあります。</p>
<p>ルールにアクションを設定して、そのルールが適用されたときに、メッセージにそれ以降のルールの適用されないようにすることもできます。</p></td>
</tr>
</tbody>
</table>


メール フロー ルールの構成要素

## メール フロー ルールのプロパティ

次の表で、メール フロー ルールで使用可能なルールのプロパティについて説明します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC におけるプロパティ名</th>
<th>PowerShell におけるパラメーター名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>[優先度]</strong></p></td>
<td><p><em>Priority</em></p></td>
<td><p>メッセージにルールを適用する順番を示します。優先度の既定値はルールの作成時期に基づいています (古いルールのほうが新しいルールより優先度が高く、優先度の高いルールが優先度の低いルールよりも先に処理されます)。</p>
<p>EAC 内でのルールの優先度は、ルール一覧内でそのルールを上下に移動させることで変更します。PowerShell では、優先度番号を設定します (0 が最高優先度)。</p>
<p>たとえば、クレジット カード番号が含まれるメッセージを拒否するルールと、承認を必要とする別のルールがある場合、拒否のルールを最初に適用して、他のルールの適用を停止する必要があります。</p>
<p>詳細に関しては、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules">メール フロー ルールの優先度の設定</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>[モード]</strong></p></td>
<td><p><em>Mode</em></p></td>
<td><p>ルールにすぐにメッセージの処理を開始させるか、あるいはメッセージの配信に影響を与えずにルールをテストするかどうかを指定することができます (データ紛失防止、DLP ポリシー ヒントの有無を問わず)。</p>
<p>ポリシー ヒントは、メッセージを作成しているユーザーにそれがポリシー違反の可能性があることを通知する短いメモを、Outlook または Web 上の Outlook で提示します。詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/policy-tips">ポリシー ヒント</a>」を参照してください。</p>
<p>モードの詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules">メール フロー ルールのテスト</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>次の日付でこのルールを有効にする</strong></p>
<p><strong>次の日付に、このルールを無効にする</strong></p></td>
<td><p><em>ActivationDate</em></p>
<p><em>ExpiryDate</em></p></td>
<td><p>ルールが有効化される日付の範囲を指定します。</p></td>
</tr>
<tr class="even">
<td><p>選択されているかどうかに関わらず、チェック ボックスを <strong>オン</strong> にします。</p></td>
<td><p>新しいルール: <strong>New-TransportRule</strong> コマンドレットの<em>Enabled</em> パラメーター。</p>
<p>既存のルール:<strong>Enable-TransportRule</strong> または <strong>Disable-TransportRule</strong> コマンドレットを使用します。</p>
<p>値はルールの <strong>State</strong> プロパティに表示されます。</p></td>
<td><p>無効なルールを作成して、それをテストする準備ができたときに有効にすることができます。または、設定を保持するために削除することなくルールを無効にすることができます</p></td>
</tr>
<tr class="odd">
<td><p><strong>[ルール処理が完了しない場合メッセージを優先する]</strong></p></td>
<td><p><em>RuleErrorAction</em></p></td>
<td><p>ルール処理が完了しない場合にメッセージをどのように扱うかを指定することができます。既定値ではルールは無視されますが、処理のためにメッセージを再送信することを選択できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>メッセージの送信者アドレスを一致</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>ルールが送信者のメール アドレスを確認する例外や条件を使用する場合、メッセージ ヘッダー、メッセージのエンベロープ、またはその両方の値を検索できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[ルールの処理を中止する]</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>これはルールのアクションですが、EAC でのプロパティのように見えます。ルールがメッセージを処理した後に、追加のルールが適用されないように選択できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>コメント</strong></p></td>
<td><p><em>Comments</em></p></td>
<td><p>ルールに関する説明的なコメントを入力することができます。</p></td>
</tr>
</tbody>
</table>


メール フロー ルールの構成要素

## メッセージへのメール フロー ルールの適用方法

組織を通過するすべてのメッセージが、組織内の有効にされているメール フロー ルールについて評価されます。ルールが処理される順序は、EAC の <strong>メール フロー</strong> \> <strong>ルール</strong> ページでリストされている順、または PowerShell 内の対応する *Priority* パラメーターの値に基づきます。

各ルールでは、そのルールが一致した場合に、以降のルールの処理を停止するオプションを選択できます。この設定は、メッセージが複数のメール フロー ルールの条件に一致する場合に重要です (メッセージにどのルールを適用しますか?すべてですか?1 つだけですか?)。

## メッセージの種類による処理の違い

組織を通過するメッセージにはいくつかの種類があります。次の表に、メール フロー ルールで処理できるメッセージの種類を示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>メッセージの種類</th>
<th>ルールを適用可能か</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>[通常のメッセージ]</strong> 単一のリッチ テキスト形式 (RTF)、HTML、プレーン テキストのメッセージ本文あるいはメッセージ本文のマルチパートまたは代替セットが含まれるメッセージ。</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 Message Encryption</strong>    Office 365 の Office 365 Message Encryption によって暗号化されたメッセージ。詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=392525">Office 365 での暗号化</a>」を参照してください。</p></td>
<td><p>ルールは常にエンベロープ ヘッダーにアクセスでき、それらのヘッダーを検査する条件に基づいてメッセージを処理できます。</p>
<p>暗号化されたメッセージのコンテンツをルールで検査または変更する場合、トランスポート復号化が有効になっていることを確認する必要があります (必須または省略可能。既定は省略可能です)。詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=848060">トランスポート解読を有効または無効にする</a>」を参照してください。</p>
<p>暗号化されたメッセージを自動的に復号化するルールを作成することもできます。詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=402846">電子メール メッセージの暗号化または暗号化解除ルールの定義</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>S/MIME 暗号化されたメッセージ</strong></p></td>
<td><p>ルールは、エンベロープ ヘッダーにのみアクセスでき、それらのヘッダーを検査する条件に基づいてメッセージを処理できます。</p>
<p>メッセージ コンテンツの検査を必要とする条件を使用したルール、またはメッセージのコンテンツを変更するアクションを処理することはできません。</p></td>
</tr>
<tr class="even">
<td><p><strong>RMS 保護されたメッセージ</strong>   Active Directory Rights Management サービス (AD RMS) または Azure Rights Management (RMS) ポリシーが適用されたメッセージ。</p></td>
<td><p>ルールは常にエンベロープ ヘッダーにアクセスでき、それらのヘッダーを検査する条件に基づいてメッセージを処理できます。</p>
<p>RMS で保護されたメッセージのコンテンツをルールで検査または変更する場合、トランスポート復号化が有効になっていることを確認する必要があります (必須または省略可能。既定は省略可能です)。詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=848060">トランスポート解読を有効または無効にする</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>[クリア署名付きメッセージ]</strong>   署名されているが、暗号化はされていないメッセージ。</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p><strong>[UM メッセージ]</strong> ボイス メール、ファックス、不在着信通知などのユニファイド メッセージング サービスによって作成または処理されたメッセージ、および Microsoft Outlook Voice Access を使用して転送されたメッセージ。</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p><strong>[匿名メッセージ]</strong>   匿名の送信者によって送信されたメッセージ。</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p><strong>[開封済みレポート]</strong>   送信者による開封要求確認を読み取るために生成されたレポート。開封済みレポートには、<code>IPM.Note*.MdnRead</code> または <code>IPM.Note*.MdnNotRead</code> のメッセージ クラスがあります。</p></td>
<td><p>はい</p></td>
</tr>
</tbody>
</table>


## トランスポート ルールとグループ メンバーシップ

配布グループのメンバーシップを展開する条件を使用してトランスポート ルールを定義する場合、ルールを適用するメールボックス サーバー上のトランスポート サービスにより、生成された受信者の一覧がキャッシュされます。これは、*展開されたグループ キャッシュ* と呼ばれ、ジャーナル エージェントでも、ジャーナル ルールに対してグループ メンバーシップを評価する際に使用されます。既定では、展開されたグループ キャッシュはグループ メンバーシップを 4 時間保存します。動的配布グループの受信者フィルターによって返された受信者も保存されます。展開されたグループ キャッシュにより、反復的な Active Directory へのラウンド トリップ、およびグループ メンバーシップの解決によって生じるネットワーク トラフィックが不要になります。

Exchange 2013 では、この間隔および展開されたグループ キャッシュに関連する他のパラメーターを構成することができます。キャッシュ有効期限の間隔を短くしたり、キャッシュをまとめて無効にしたりすると、グループ メンバーシップをより頻繁に更新することが可能になります。配布グループの展開のクエリがやり取りされるので、Active Directory ドメイン コントローラーでその分の負荷が増加することを考慮する必要があります。また、メールボックス サーバー上のキャッシュを、そのサーバーの Microsoft Exchange トランスポート サービスを再起動することで消去することもできます。この処理は、キャッシュを消去する各メールボックス サーバーで実行する必要があります。配布グループ メンバーシップに基づいて条件を使用するトランスポート ルールを作成、テスト、およびトラブルシューティングする場合、展開されたグループ キャッシュの影響も考慮する必要があります。

## ルールの保存とレプリケーション

メールボックス サーバー上に作成、設定するメール フロー ルールで、Active Directory に格納されており、組織のメールボックス サーバー上のトランスポート サービスによって読み取られ、適用されます。メール フロー ルールを作成、変更、または削除すると、変更は組織のドメイン コントローラー間でレプリケートされます。これにより、Exchange は組織全体に、一貫性のあるメール フロー ルールのセットを提供できます。

**注**:

  - ドメイン間のレプリケーションは、Exchange が制御しない要素 (たとえば、Active Directory サイトの数やネットワーク リンクの速度など) によって異なります。したがって、組織でメール フロー ルールを実装する際は、レプリケーションによる遅延を考慮する必要があります。Active Directory レプリケーションの詳細については、「[Windows PowerShell を使用した Active Directory レプリケーションとトポロジの管理](https://go.microsoft.com/fwlink/p/?linkid=274904)」を参照してください。

  - 各メールボックス サーバーは、展開された配布グループをキャッシュして、グループのメンバーシップを特定するために Active Directory クエリが繰り返し実行されないようにします。既定では、拡張されたグループ キャッシュは 4 時間ごとに期限切れになります。したがって、グループのメンバーシップに対する変更は、展開されたグループ キャッシュが更新されるまでメールフロー ルールには検出されません。メールボックス サーバーに対してすぐにキャッシュを更新するように強制するには、Microsoft Exchange トランスポート サービスを再起動します。キャッシュを強制的に更新する各メールボックス サーバーのサービスを再起動する必要があります。

エッジ トランスポート サーバー上で作成、構成されるメール フロー ルールは、サーバー上の AD LDS のローカル インスタンスに格納されます。エッジ トランスポート サーバーでは、メール フロー ルールの自動レプリケーションは発生しません。エッジ トランスポート サーバー上のルールは、そのローカル サーバーを流れるメッセージのみに適用されます。複数のエッジ トランスポート サーバーに同じメール フロー ルールのセットを適用する必要がある場合、エッジ トランスポート サーバーの構成を複製したり、メール フロー ルールをエクスポートおよびインポートすることができます。詳細については、[エッジ トランスポート サーバーの複製構成](edge-transport-server-cloned-configuration-exchange-2013-help.md) と「[メール フロー ルール コレクションのインポートまたはエクスポート](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)」をご覧ください。

メールボックス サーバーまたはエッジ トランスポート サーバー上のトランスポート サービスがメール フロー ルールの変更を検出すると、イベント ビューアーのアプリケーション ログにイベントが記録されます (メールボックス サーバーのイベント ID 4002 と、エッジ トランスポート サーバーのイベント ID 16028)。

## 混在環境におけるルールのレプリケーションと保存

Exchange 2013 の一般的な混在環境のシナリオは 2 つあります。

  - **組織の一部が UNRESOLVED\_TOKEN\_VAL(Office365) に存在するハイブリッド展開**
    
    ハイブリッド環境の場合、社内 Exchange 組織と UNRESOLVED\_TOKEN\_VAL(Office365) の間でルールのレプリケーションは行われません。そのため、Exchange でルールを作成した場合は、それと同じルールを UNRESOLVED\_TOKEN\_VAL(Office365) でも作成する必要があります。UNRESOLVED\_TOKEN\_VAL(Office365) で作成したルールはクラウドに保存される一方、社内組織で作成したルールはローカルの Active Directory に保存されます。ハイブリッド環境でルールを管理する際は、両方の場所で変更を行うか、一つの環境で変更を行ってから、ルールをエクスポートしてもう一つの環境にインポートするなどして、2 つに分かれているルールを常に同期させておく必要があります。
    

    > [!IMPORTANT]
    > 大多数の条件と操作が UNRESOLVED_TOKEN_VAL(Office365) と Exchange Server で共通に利用できますが、異なる点もあります。両方に対して同じルールを作成する場合は、使用するすべての条件と操作がどちらの環境でも利用できることを確認してください。UNRESOLVED_TOKEN_VAL(Office365) で利用できる条件と操作の一覧については、以下のトピックを参照してください。<BR><A href="https://technet.microsoft.com/ja-jp/library/jj919235(v=exchg.150)">Exchange Online でのメール フロー ルールの条件と例外 (述語)</A><BR><A href="https://technet.microsoft.com/ja-jp/library/jj919237(v=exchg.150)">Exchange Online でのメール フロー ルールの処理</A>



  - **Exchange 2010 または Exchange 2007 との共存**
    
    Exchange 2010 または Exchange 2007 と共存させる場合、すべてのメール フロー ルールは Active Directory に保存され、ルールを作成した Exchange Server のバージョンに関係なく組織全体にレプリケートされます。ただし、すべてのメール フロー ルールは作成に使用した Exchange Server サーバーのバージョンと関連付けられており、Active Directory 内のバージョン固有のコンテナーに保存されます。Exchange 2013 を最初に組織に展開する際、セットアップ プロセスの一環として既存のルールはすべて Exchange 2013 にインポートされます。ただし、その後は両方のバージョンに対して変更を加える必要があります。たとえば、Exchange 2013 (Exchange 管理シェル あるいは EAC) 内の既存のルールを変更した場合は、同じ変更を Exchange 2010 (Exchange 管理シェル あるいは UNRESOLVED\_TOKEN\_VAL(exEMC)) でも行う必要があります。または、Exchange 2013 からルールをエクスポートし、それを Exchange 2010 にインポートすることができます。
    
    Exchange 2010 は、**バージョン** または **RuleVersion** 値 15 *n*.*n*.*n*.を持つルールを処理することはできません。すべてのルールが処理されることを確認するため、値が 14 *n*.*n*.*n* を持つルールのみを使用します。

## 詳細情報

[メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)

[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールのアクション](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[トランスポート エージェント](transport-agents-exchange-2013-help.md)

