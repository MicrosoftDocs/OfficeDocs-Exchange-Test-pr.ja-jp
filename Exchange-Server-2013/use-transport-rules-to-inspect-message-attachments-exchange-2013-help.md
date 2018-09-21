---
title: 'トランスポート ルールを使用してメッセージの添付を検査する: Exchange 2013 Help'
TOCTitle: トランスポート ルールを使用してメッセージの添付を検査する
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 49896453
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート ルールを使用してメッセージの添付を検査する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-27_

トランスポート ルールを設定すると、組織でメールの添付ファイルを検査できます。Exchange は、メッセージング セキュリティおよび法令遵守のニーズの一環としてメールの添付ファイルを調べるためのトランスポート ルールを提供します。添付ファイルを検査するときには、添付ファイルの内容や特徴に基づいて、検査されたメッセージを処理することができます。トランスポート ルールを使用して実行できる添付ファイル関連タスクをいくつか示します。

  - .zip や .rar ファイルなどの圧縮された添付ファイル内のファイルを検索し、指定するパターンと一致するテキストが存在する場合、メッセージの最後に免責事項を追加する。

  - 添付ファイル内のコンテンツを検査し、指定するキーワードが存在する場合、メッセージを配信する前に承認のためにモデレーターにリダイレクトする。

  - メッセージを確認して検査できない添付ファイルがあった場合、メッセージ全体が送信されないようにする。

  - 特定のサイズを超える添付ファイルがないかどうか確認し、メッセージを送信しない場合は、その問題を送信者に通知する。

  - トランスポート ルールと一致するメッセージを送信した場合に、ユーザーに警告する通知を作成する。

  - 添付ファイルを含むすべてのメッセージをブロックする。例については、「[添付ファイル ブロックの一般的なシナリオ](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)」を参照してください。

Exchange 管理者は、<strong>Exchange 管理センター</strong> \> <strong>メール フロー</strong> \> <strong>ルール</strong> で、トランスポート ルールを作成できます。この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。新しいルールの作成を開始した後、<strong>次の場合にこのルールを適用</strong> で <strong>その他のオプション</strong> \> <strong>いずれかの添付ファイル</strong> をクリックすれば、添付ファイルに関連した条件の完全な一覧を表示できます。次の図に、添付ファイルに関連するオプションを示します。

![添付ファイルに関連するルールを選択するダイアログ ボックス](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "添付ファイルに関連するルールを選択するダイアログ ボックス")

選択できる条件や操作の範囲全般を含むトランスポート ルールの詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)」を参照してください。Exchange Online Protection (EOP) およびハイブリッド環境では、[EOP を構成するためのベスト プラクティス](https://technet.microsoft.com/ja-jp/library/jj723164\(v=exchg.150\)) で提供されるトランスポート ルールのベスト プラクティスを活用できます。ルールの作成を開始する準備ができている場合は、「[メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)」を参照してください。

## 添付ファイル内のコンテンツの検査

次の表にあるトランスポート ルールの条件を使用して、メッセージの添付ファイルのコンテンツを調べることができます。これらの条件では、添付ファイルの最初の 150 KB だけが検査されます。メッセージを検査するときに、これらの条件の使用を開始するためには、トランスポート ルールに条件を追加する必要があります。ルールの作成や変更の詳細については、「[メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)」を参照してください。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件名</th>
<th>シェルにおける条件名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>添付ファイルの内容にこれらの単語のいずれかが含まれている場合</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>この条件は、指定された文字列または文字のグループを含む、サポートされているファイルの種類の添付ファイルがあるメッセージと一致します。</p></td>
</tr>
<tr class="even">
<td><p><strong>添付ファイルの内容がこれらのテキスト パターンと一致する場合</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>この条件は、指定の正規表現と一致するテキスト パターンを含む、サポートされているファイルの種類の添付ファイルがあるメッセージと一致します。</p></td>
</tr>
</tbody>
</table>


ここに一覧表示されている条件の Exchange 管理シェル 名は、`TransportRule` コマンドレットを必要とするパラメーターです。

  -  コマンドレットの詳細については、「[New-TransportRule](https://technet.microsoft.com/ja-jp/library/bb125138\(v=exchg.150\))」を参照してください。

  -  これらの条件のプロパティの種類の詳細については、「[Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)」を参照してください。

トランスポート ルールは、サポートされているファイルの種類のコンテンツのみを検査できます。トランスポート ルール エージェントが、サポートされているファイルの種類の一覧にない添付ファイルを検出すると、`AttachmentIsUnsupported` 条件がトリガーされます。サポートされているファイルの種類を次のセクションに一覧表示します。一覧にないファイルは、`AttachmentIsUnsupported` の条件をトリガーします。

## 圧縮アーカイブ ファイル

メッセージに圧縮アーカイブ ファイル (.zip ファイル, .cab ファイルなど) が含まれている場合、トランスポート ルール エージェントは添付ファイル内に含まれているファイルを検査します。このようなメッセージは、複数の添付ファイルが付いているメッセージと同様に処理されます。圧縮されたアーカイブ ファイルのプロパティは検査されません。たとえば、コンテナー ファイルの種類ではコメントがサポートされる場合、そのフィールドは検査されません。

## トランスポート ルールによるコンテンツ検査でサポートされているファイルの種類

次の表は、トランスポート ルールによってサポートされているファイルの種類を一覧表示しています。システムは、実際のファイル名拡張子ではなくファイルのプロパティを検査してファイル種類を自動的に検出するため、悪意あるハッカーがファイル拡張子の名前を変更してトランスポート ルール フィルターを迂回するのを防ぎます。トランスポート ルールのコンテキスト内でチェックできる、実行可能コードを持つファイルの種類の一覧については、後で説明します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>カテゴリ</th>
<th>ファイル拡張子</th>
<th>注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013、Office 2010、Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>Microsoft OneNote ファイルおよび Microsoft Publisher ファイルは、既定ではサポートされません。IFilter の統合を使用することにより、これらのファイルの種類のサポートを有効にできます。詳細については、「<a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Exchange 2013 でフィルター パック IFilter を登録する</a>」を参照してください。</p>
<p>これらのファイルの種類に含まれるすべての埋め込みパーツの内容も検査されます。ただし、埋め込まれていないオブジェクト (たとえばリンクされたドキュメント) は検査されません。</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>その他の Office ファイル</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>Adobe PDF</p></td>
<td><p>.pdf</p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>テキスト</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, .inf, .ini, .inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>.odf ファイルのパーツは処理されません。たとえば, .odf ファイルに埋め込みドキュメントが含まれている場合、その埋め込みドキュメントの内容は検査されません。</p></td>
</tr>
<tr class="odd">
<td><p>AutoCAD 図面</p></td>
<td><p>.dxf</p></td>
<td><p>AutoCAD 2013 ファイルはサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p>イメージ</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>これらのイメージ ファイルに関連付けられているメタデータのテキストのみが検査されます。光学式文字認識はありません。</p></td>
</tr>
</tbody>
</table>


## 添付ファイルのファイル プロパティの検査

次のトランスポート ルールの条件は、メッセージに添付されているファイルのプロパティを検査します。メッセージを検査するときに、これらの条件の使用を開始するためには、トランスポート ルールに条件を追加する必要があります。トランスポート ルールのコンテキスト内でチェックできる、実行可能コードを持つサポート対象ファイルの種類の一覧は次のとおりです。ルールの作成または変更に関する詳細については、「[メール フロー ルールを管理します](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)」を参照してください。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC における条件名</th>
<th>シェルにおける条件名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任意の添付ファイル名が次のテキスト パターンと一致する場合</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>この条件は、サポートされているファイル種類の添付ファイルの名前に指定した文字が含まれているメッセージと一致します。</p></td>
</tr>
<tr class="even">
<td><p><strong>任意の添付ファイルの拡張子に次の単語が含まれる場合</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>この条件は、サポートされているファイル種類の添付ファイルの拡張子が指定した単語と一致するメッセージと一致します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>添付ファイルのサイズが次の値以上の場合</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>この条件は、サポートされているファイル種類の添付ファイルが指定したサイズより大きいメッセージと一致します。</p></td>
</tr>
<tr class="even">
<td><p><strong>添付ファイルがスキャンを完了しなかった場合</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>この条件は、添付ファイルがトランスポート ルール エージェントによって検査されないメッセージと一致します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>添付ファイルに実行可能なコンテンツがある場合</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>この条件は、添付ファイルとして実行可能ファイルを含むメッセージと一致します。サポートされているファイルの種類は以下のとおりです。</p></td>
</tr>
<tr class="even">
<td><p><strong>すべての添付ファイルがパスワードで保護されている</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>この条件は、サポートされているファイル種類の添付ファイルがパスワードで保護されているメッセージと一致します。</p></td>
</tr>
</tbody>
</table>


ここに一覧表示されている条件の Exchange 管理シェル 名は、`TransportRule` コマンドレットを必要とするパラメーターです。

  -  コマンドレットの詳細については、「[New-TransportRule](https://technet.microsoft.com/ja-jp/library/bb125138\(v=exchg.150\))」を参照してください。

  -  これらの条件のプロパティの種類の詳細については、「[Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)」を参照してください。

## トランスポート ルールによる検査でサポートされている実行可能ファイルの種類

トランスポート エージェントは、ファイル拡張子だけではなくファイル プロパティを検査することによって、実際の種類の検出を使用します。これは、悪意のあるハッカーがファイル拡張子の名前を変更してルールを迂回することがないようにするうえで助けになります。次の表は、これらの条件によってサポートされている実行可能ファイルの種類の一覧です。ここに一覧表示されていないファイルが見つかった場合、その `AttachmentIsUnsupported` 条件がトリガーされます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ファイルの種類</th>
<th>ネイティブの拡張子</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WinRAR アーカイバを使用して作成された自己解凍アーカイブ ファイル。</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>ダイナミック リンク ライブラリの拡張子を持つ 32 ビット Windows の実行可能ファイル。</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>自己解凍形式の実行可能プログラム ファイル。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Java アーカイブ ファイル。</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>アンインストール実行可能ファイル。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>プログラムのショートカット ファイル。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>コンパイルされたソース コード ファイル、3D オブジェクト ファイル、シーケンス ファイル。</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>32 ビット Windows 実行可能ファイル。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Visio の XML 図面ファイル。</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>OS/2 のオペレーティング システム ファイル。</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>16 ビット Windows 実行可能ファイル。</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>ディスク オペレーティング システムのファイル。</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>European Institute for Computer Antivirus Research 規格のウイルス対策テスト ファイル。</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>Windows のプログラム情報ファイル。</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>Windows プログラムの実行可能ファイル。</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## サポートされているファイルの種類の数を拡張

いつでも IFilter で統合し、このトピックで一覧表示されているサポートされているファイルの種類を変更できます。詳細については、「[Exchange 2013 でフィルター パック IFilter を登録する](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md)」を参照してください。

このプロセスを使用して追加したファイルの種類は、サポートされているファイルの種類となり、`AttachmentIsUnsupported` の条件をトリガーすることはなくなります。

## データ損失防止ポリシーと添付ファイルのトランスポート ルール

メールの重要なビジネス情報を管理する助けとして、データ損失防止 (DLP) ポリシーのルールとともに添付ファイルに関連する条件のいずれかを含めることができます。たとえば、パスポート番号がパスワード保護された添付ファイルに含まれる場合にのみ、パスポート番号を含むメッセージを送信できるようにすることも可能です。このためには、次のことを実行します。

  - パスポート関連の機密情報がないかどうかメールを検査する DLP ポリシーを作成します。詳細については、「[DLP の手順](dlp-procedures-exchange-2013-help.md)」を参照してください。

  - <strong>\[ただし次の場合を除く\]</strong>トランスポート ルール領域に <strong>すべての添付ファイルがパスワードで保護されている</strong> 例外を追加します。

  - 保護されたファイル以外のところパスポート番号が存在するメールに対して実行するアクションを定義します。

DLP ポリシーおよび添付ファイル関連の条件は、ビジネスのニーズをトランスポート ルール条件、例外、アクションとして定義することで、それらのニーズを満たすのに役立ちます。DLP ポリシーに機密情報の検査を含めた場合、メッセージの添付ファイルはその情報についてだけスキャンされます。ただし、サイズやファイル種類などの添付ファイルに関連する条件は、このトピックに一覧表示されている条件を追加するまでは含まれません。DLP はすべてのバージョンの Exchange で利用できるわけではありません。詳しくは、「[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)」を参照してください。

## 詳細情報

[データ損失防止](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[トランスポート ルールの条件 (述語)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Office 365 で、メール フロー ルールを使用してメッセージの添付ファイルを検査する](https://technet.microsoft.com/ja-jp/library/jj919236\(v=exchg.150\)) の Exchange Online

