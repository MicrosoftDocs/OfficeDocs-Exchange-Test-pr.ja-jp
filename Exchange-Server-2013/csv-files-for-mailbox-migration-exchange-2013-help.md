---
title: 'メールボックス移行用の CSV ファイル: Exchange Online Help'
TOCTitle: CSV files for mailbox migration
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54651693
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス移行用の CSV ファイル

 

_**適用先:** Exchange Online, Exchange Server 2013_

CSV ファイルを使って、大量のユーザー メールボックスを一括移行することができます。Exchange 管理センター (EAC) または Exchange 管理シェル で **New-MigrationBatch** コマンドレットを使用して移行バッチを作成し、CSV ファイルを指定することができます。CSV ファイルを使用して、移行バッチで移行する複数ユーザーの指定は、次の移行シナリオでサポートされています。

  - **社内の Exchange 組織の移動**
    
      - **ローカル移動:**  ローカル移動は、1 つのメールボックス データベースから別のメールボックス データベースにメールボックスを移動します。ローカル移動は単一のフォレスト内で行われます。
    
      - **フォレスト間エンタープライズ移動:**  フォレスト間エンタープライズ移動では、メールボックスは別のフォレストに移動されます。フォレスト間移動は、メールボックスの移動先フォレストまたはメールボックスを現在ホストしている移動元フォレストのいずれかから開始されます。

  - **Exchange Online** でのオンボードとオフボード
    
      - **オンボード リモート移動/移行:**  Exchange ハイブリッド展開では、社内 Exchange 組織から Exchange Online にメールボックスを移動できます。これは、メールボックスを Exchange Online にオンボードするため、*オンボード* リモート移動/移行とも呼ばれます。
    
      - **オフボード リモート移動/移行:**  *オフボード* リモート移動/移行を実行することもできます。この移動/移行では、Exchange Online メールボックスを社内 Exchange 組織に移行します。
        

        > [!NOTE]
        > オンボードとオフボードの両方のリモート移動/移行は、Exchange Online 組織から開始します。

    
      - **段階的な Exchange 移行:**  メールボックスの一部を、社内 Exchange 組織から Exchange Online に移行することもできます。これはオンボード移行とは種類が異なります。段階的な Exchange 2003 移行を使用して移行できるのは、Exchange 2007 メールボックスおよび Exchange メールボックスだけです。段階的な移行によって Exchange 2010 メールボックスと Exchange 2013 メールボックスを移行することはできません。段階的な移行を実行する前に、Exchange Online 組織内のメール ユーザーをプロビジョニングするため、ディレクトリ同期またはその他の方法を使用する必要があります。
    
      - **IMAP 移行:**  このオンボード移行では、IMAP サーバー (Exchange を含む) から Exchange Online にメールボックス データを移行します。IMAP 移行の場合、メールボックス データを移行する前に、Exchange Online のメールボックスをプロビジョニングする必要があります。


> [!NOTE]
> すべてのオンプレミスのユーザー メールボックスが単一の移行バッチで Exchange Online に移行するので、Exchange 一括移行では、CSV ファイルの使用はサポートされません。



## 両方の移動または移行でサポートされる CSV 属性

移行に使われる CSV ファイルの最初の行、つまりヘッダー行には、後続の行で指定される属性 (つまり、フィールド) の名前が示されます。各属性名はコンマで区切ります。ヘッダー行の下の各行は個々のユーザーを表し、これらの行には、移行に必要な情報が含まれます。個々のユーザー行の属性は、ヘッダー行の属性名と同じ順序で並んでいる必要があります。各属性値はコンマで区切ります。特定のレコードの属性値が null の場合、その属性については何も入力しないでください。ただし、null 値と次の属性を区切るコンマを必ず追加してください。

EAC または Exchange 管理シェル で移行バッチを作成する際に同じパラメーターが使われる場合、CSV ファイルの属性値は対応するパラメーターの値より優先されます。詳細と例については、「CSV ファイルの属性値は、移行バッチの値よりも優先されます」をご覧ください。


> [!TIP]
> CSV ファイルの作成には任意のテキスト エディターが使用できますが、Microsoft&nbsp;Excel などのアプリケーションを使用すると、データのインポートおよび CSV ファイルの構成と整理が簡単になります。必ず CSV ファイルまたは .txt ファイルとして保存します。



以下のセクションでは、移行タイプごとの CSV ファイルの見出し行のサポート属性について説明します。各セクションには、各サポート属性、必須かどうか、属性に使われる値の例、説明を一覧表示した表が含まれています。


> [!NOTE]
> 以下のシナリオでは、<EM>ソース環境</EM>は、ユーザーのメールボックスまたはデータベースの現在の位置を示しています。<EM>ターゲット環境</EM>は、メールボックスが移行される場所、またはメールボックスが移動されるデータベースの場所を示しています。



## ローカル移動

次の表は、ローカル移動に対する CSV ファイルのサポート属性を示しています。詳細については、「[社内の移動の管理](manage-on-premises-moves-exchange-2013-help.md)」を参照してください。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必須かどうか</th>
<th>指定できる値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必須かどうか</p></td>
<td><p>ユーザーの SMTP アドレス</p></td>
<td><p>移動対象のユーザーを指定します。</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>省略可能</p></td>
<td><p>データベース名</p></td>
<td><p>ユーザーのプライマリ メールボックスが移動されるメールボックス データベースを指定します。CSV ファイルの別の行に別のデータベースを指定できます。これにより、同じ移行バッチで別のデータベースにメールボックスを移動することができます。</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>省略可能</p></td>
<td><p>データベース名</p></td>
<td><p>ユーザーのアーカイブ メールボックス (もし存在する場合) が移動されるメールボックス データベースを指定します。CSV ファイルの別の行に別のデータベースを指定できます。これにより、同じ移行バッチで別のデータベースにアーカイブ メールボックスを移動することができます。</p>

> [!NOTE]
> アーカイブ データベースを指定しない場合、アーカイブ メールボックスがプライマリ メールボックスと同じデータベースに移動されます。


</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>省略可能</p></td>
<td><p><code>Unlimited</code>、または <code>0</code> (既定値) から最大値 <code>2147483647</code> までの負ではない整数になります。</p></td>
<td><p>移行サービスでメールボックス内のアイテムの破損が検出された場合にスキップする不良アイテム数を指定します。CSV ファイルにこの属性を含める場合、EAC または Exchange 管理シェル を使って移行バッチを作成した際に <em>BadItemLimit</em> パラメーターを指定すると、既定値またはユーザーの指定値よりも優先されます。</p>

> [!TIP]
> 既定値の 0 を使用し、特定のユーザーの移動または移行が失敗した場合にのみ、そのユーザーの不良アイテムの上限を増やすことをお勧めします。


<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>省略可能</p></td>
<td><p>次のいずれかの値を使用します。</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (既定値)</p></li>
</ul></td>
<td><p>ユーザーのプライマリ メールボックス、アーカイブ メールボックスのいずれかまたは両方を移動するかどうかを指定します。</p></td>
</tr>
</tbody>
</table>


## ハイブリッド展開でのオンボード リモート移動/移行

ハイブリッド展開では、社内 Exchange 組織から Exchange Online にメールボックスを移動できます。オンボード メールボックスの場合、移行バッチは Exchange Online 組織で作成され、Exchange Online 管理者によって継承されます。詳細については、「[ハイブリッド展開においてオンプレミスの組織と Exchange Online 組織間でメールボックスを移動する](https://technet.microsoft.com/ja-jp/library/jj906432\(v=exchg.150\))」を参照してください。

次の表は、オンボード移動/移行に対する CSV ファイルのサポート属性を示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必須かどうか</th>
<th>指定できる値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必須かどうか</p></td>
<td><p>ユーザーの SMTP アドレス</p></td>
<td><p>Exchange Online 組織内でメールが有効なユーザーの電子メールアドレスを指定します。これは、移行対象の社内ユーザーのメールボックスに対応します</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>省略可能</p></td>
<td><p><code>Unlimited</code>、または <code>0</code> (既定値) から最大値 <code>2147483647</code> までの負ではない整数になります。</p></td>
<td><p>移行サービスでメールボックス内のアイテムの破損が検出された場合にスキップする不良アイテム数を指定します。CSV ファイルにこの属性を含める場合、EAC または Exchange 管理シェル を使って移行バッチを作成した際に <em>BadItemLimit</em> パラメーターを含めると、既定値またはユーザーの指定値よりも優先されます。</p>

> [!TIP]
> 既定値の 0 を使用し、特定のユーザーの移動または移行が失敗した場合にのみ、そのユーザーの不良アイテムの上限を増やすことをお勧めします。


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>省略可能</p></td>
<td><p><code>Unlimited</code>、または <code>0</code> (既定値) から最大値までの負ではない整数になります。</p></td>
<td><p>ユーザーのメールボックス内の、サイズが大きく、スキップされるアイテムの数を指定します。サイズの大きいアイテムの数がこの値を超えると、そのメールボックスの移行が失敗します。</p>
<p>既定値は 0 です。これは、メールボックスにサイズの大きいアイテムがあると、その移行は失敗するということです。</p>
<p>メールボックスを Exchange Online にオンボードで移行する場合、35 MB までのアイテムが移行されます。</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>省略可能</p></td>
<td><p>次のいずれかの値を使用します。</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (既定値)</p></li>
</ul></td>
<td><p>ユーザーのプライマリ メールボックス、アーカイブ メールボックスのいずれかまたは両方を移動するかどうかを指定します。</p></td>
</tr>
</tbody>
</table>


## フォレスト間エンタープライズ移動とハイブリッド展開のオフボード リモート移動/移行

前述のように、フォレスト間移動は、ターゲット フォレストまたはソース フォレストのいずれかから開始されます。オフボード リモート移動/移行は、Exchange Online 組織から開始します。詳細については、次のトピックを参照してください。

  - [メールボックスでフォレスト間の移動要求の準備を行う](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [ハイブリッド展開においてオンプレミスの組織と Exchange Online 組織間でメールボックスを移動する](https://technet.microsoft.com/ja-jp/library/jj906432\(v=exchg.150\))

次の表は、フォレスト間エンタープライズ移動と Exchange ハイブリッド展開のオフボード リモート移動/移行に対する CSV ファイルのサポート属性を示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必須かどうか</th>
<th>指定できる値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必須かどうか</p></td>
<td><p>ユーザーの SMTP アドレス</p></td>
<td><p>フォレスト間エンタープライズ移動の場合、この属性は、ソース フォレスト内のメールボックスまたはメールが有効なユーザーの指定します。</p>
<p>オフボード リモート移動/移行の場合は、Exchange Online メールボックスを指定します。</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>オフボード リモート移動/移行と、ソース フォレストから開始されたフォレスト間エンタープライズ移動で必要です。またこの属性は、EAC または Exchange 管理シェル を使って移行バッチを作成する場合に指定することもできます。</p>
<p>この属性は、ターゲット フォレストから開始されたフォレスト間エンタープライズ移動では省略可能です。</p></td>
<td><p>データベース名</p></td>
<td><p>ユーザーのプライマリ メールボックスが移動される、ターゲット フォレスト内のメールボックス データベースを指定します。CSV ファイルの別の行に別のデータベースを指定できます。これにより、同じ移行バッチで別のデータベースにメールボックスを移動することができます。</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>省略可能</p></td>
<td><p>データベース名</p></td>
<td><p>ユーザーのアーカイブ メールボックスが移動される、ターゲット フォレスト内のメールボックス データベースを指定します。CSV ファイルの別の行に別のデータベースを指定できます。これにより、同じ移行バッチで別のデータベースにアーカイブ メールボックスを移動することができます。</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>省略可能</p></td>
<td><p><code>Unlimited</code>、または <code>0</code> (既定値) から最大値 <code>2147483647</code> までの負ではない整数になります。</p></td>
<td><p>移行サービスでメールボックス内のアイテムの破損が検出された場合にスキップする不良アイテム数を指定します。CSV ファイルにこの属性を含める場合、EAC または Exchange 管理シェル を使って移行バッチを作成した際に <em>BadItemLimit</em> パラメーターを含めると、既定値またはユーザーの指定値よりも優先されます。</p>

> [!TIP]
> 既定値の 0 を使用し、特定のユーザーの移動または移行が失敗した場合にのみ、そのユーザーの不良アイテムの上限を増やすことをお勧めします。


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>省略可能</p></td>
<td><p><code>Unlimited</code>、または <code>0</code> (既定値) から最大値までの負ではない整数になります。</p></td>
<td><p>ユーザーのメールボックス内の、サイズが大きく、スキップされるアイテムの数を指定します。サイズの大きいアイテムの数がこの値を超えると、そのメールボックスの移行が失敗します。</p>
<p>既定値は 0 です。これは、メールボックスにサイズの大きいアイテムがあると、その移行は失敗するということです。</p>
<p>メールボックスを Exchange Online にオンボードで移行する場合、35 MB までのアイテムが移行されます。</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>省略可能</p></td>
<td><p>次のいずれかの値を使用します。</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (既定値)</p></li>
</ul></td>
<td><p>ユーザーのプライマリ メールボックス、アーカイブ メールボックスのいずれかまたは両方を移動するかどうかを指定します。</p></td>
</tr>
</tbody>
</table>


## Exchange の段階的移行

段階的な Exchange 移行を使って、Exchange 2003 と Exchange 2007 の社内メールボックスを Exchange Online に移行する場合に、移行バッチのユーザー グループを特定するために CSV ファイルを使用する必要があります。Exchange の段階的移行を使用して、クラウドに移行できるメールボックスの数に制限はありません。ただし、移行バッチ用の CSV ファイルに含めることができる行数は、最大 1,000 行までです。1,000 を超えるメールボックスを移行するには、追加の CSV ファイルを作成し、各ファイルを使用して新しい移行バッチを作成する必要があります。段階的な Exchange 移行の詳細については、「[段階的な移行を使用してメールボックスを Exchange Online に移行する](https://technet.microsoft.com/ja-jp/library/jj874018\(v=exchg.150\))」を参照してください。

次の表は、段階的 Exchange 移行に対する CSV ファイルのサポート属性を示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必須かどうか</th>
<th>指定できる値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必須かどうか</p></td>
<td><p>ユーザーの SMTP アドレス</p></td>
<td><p>Exchange Online 内でメールが有効なユーザーの電子メール アドレス (または移行を再試行している場合はメールボックス) を指定します。これは、移行対象のオンプレミスのユーザーのメールボックスに対応します。ディレクトリ同期処理または別のプロビジョニング処理の結果、メールが有効なユーザーが Exchange Online に作成されます。メールが有効なユーザーの電子メール アドレスは、対応するオンプレミスのメールボックスの <em>WindowsEmailAddress</em> プロパティと一致する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>Password</p></td>
<td><p>省略可能</p></td>
<td><p>パスワードは最低 8 文字の長さで指定し、Office 365 組織に適用されるパスワード制限を満たす必要があります。</p></td>
<td><p>このパスワードは、移行中にExchange Online 内の対応するメールが有効なユーザーがメールボックスに変換された場合にユーザー アカウントに対して設定されます。</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>省略可能</p></td>
<td><p><code>True</code> または<code>False</code></p></td>
<td><p>ユーザーが Exchange Online メールボックスに初めてサインインする場合に、パスワードを変更する必要があるかどうかを指定します。</p>

> [!NOTE]
> Active Directory フェデレーション サービス 2.0 (AD FS 2.0) をオンプレミスの組織に展開してシングル サインオン ソリューションを実装した場合、この属性の値には <CODE>False</CODE> を使用する必要があります。


</td>
</tr>
</tbody>
</table>


## IMAP 移行

IMAP 移行バッチ用の CSV ファイルには、50,000 行まで入力できます。しかし、ユーザーの移行は小さなバッチに分割して実行することをお勧めします。IMAP 移行の詳細については、以下のトピックを参照してください。

  - [電子メールを IMAP サーバーから Exchange Online メールボックスに移行する](https://technet.microsoft.com/ja-jp/library/jj874015\(v=exchg.150\))

  - [IMAP 移行バッチ用の CSV ファイル](https://technet.microsoft.com/ja-jp/library/jj200730\(v=exchg.150\))

次の表は、IMAP 移行に対する CSV ファイルのサポート属性を示しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必須かどうか</th>
<th>指定できる値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必須かどうか</p></td>
<td><p>ユーザーの SMTP アドレス。</p></td>
<td><p>ユーザーの Exchange Online メールボックスのユーザー ID を指定します。</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>必須かどうか</p></td>
<td><p>IMAP メッセージング システム上のユーザーを特定する、IMAP サーバーがサポートしている形式の文字列。</p></td>
<td><p>IMAP メッセージング システム (ソース環境) でユーザーのアカウントのログイン名を指定します。ユーザー名に加えて、IMAP サーバー上のメールボックスへのアクセスに必要なアクセス許可が割り当てられているアカウントの資格情報を使用できます。詳細については、「<a href="https://technet.microsoft.com/ja-jp/library/jj200730(v=exchg.150)">IMAP 移行バッチ用の CSV ファイル</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>Password</p></td>
<td><p>必須かどうか</p></td>
<td><p>パスワード文字列。</p></td>
<td><p>UserName 属性で指定された ユーザー アカウントのパスワードを指定します。</p></td>
</tr>
</tbody>
</table>


## CSV ファイルの属性値は、移行バッチの値よりも優先されます。

EAC または Exchange 管理シェル で移行バッチを作成する際に同じパラメーターが使われる場合、CSV ファイルの属性値は対応するパラメーターの値より優先されます。移行バッチの値をユーザーに適用する場合は、CSV ファイルでこのセルを空白のままにします。これにより、1 つの移行バッチで、選んだ複数のユーザーに対して、特定の属性値に異なる値を指定することができます。

たとえば、フォレスト間エンタープライズ移動用のバッチを Exchange 管理シェル で作成し、次の Exchange 管理シェル コマンドでユーザーのプライマリおよびアーカイブ メールボックスをターゲット フォレストに移動するとします。

```powershell
New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart
```


> [!NOTE]
> 既定ではプライマリおよびアーカイブ メールボックスを移動するため、Exchange 管理シェル コマンドでこのことを明示的に指定する必要はありません。



この移行バッチの CrossForestBatch1.csv ファイルは部分的に次のようになります。

```powershell
EmailAddress,TargetDatabase,TargetArchiveDatabase
user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
user2@contoso.com,,
user3@contoso.com,EXCH-MBX-01,
...
```

CSV ファイルの値は移行バッチの値よりも優先されるため、user1 のプライマリおよびアーカイブ メールボックスはそれぞれ、ターゲット フォレスト内の EXCH-MBX-01 と EXCH-MBX-A01 に移動されます。user2 のプライマリおよびアーカイブ メールボックスは EXCH-MBX-02 または EXCH-MBX-03 に移動されます。user3 のプライマリ メールボックスは EXCH-MBX-01 に、アーカイブ メールボックスは EXCH-MBX-A02 または EXCH-MBX-A03 のいずれかに移動されます。

別の例では、ハイブリッド展開のオンボード リモート移動/移行用のバッチを作成し、次のコマンドでアーカイブ メールボックスを Exchange Online に移動するとします。

```powershell
New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart
```

ただし、選択したユーザーのプライマリ メールボックスも移動したいため、この移行バッチの OnBoarding1.csv ファイルは部分的に次のようになります。

```powershell
EmailAddress,MailboxType
user1@contoso.com,
user2@contoso.com,
user3@cloud.contoso.com,PrimaryAndArchive
user4@cloud.contoso.com,PrimaryAndArchive
...
````

CSV ファイルのメールボックス タイプの値はバッチを作成するコマンド内の *MailboxType* パラメーターの値よりも優先されるため、user1 と user2 のアーカイブ メールボックスだけが Exchange Online に移行されます。しかし、user3 と user4 のプライマリおよびアーカイブ メールボックスは Exchange Online に移動されます。

