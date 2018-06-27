---
title: 'エッジ トランスポート サーバーでのアドレス書き換えエントリのインポート: Exchange 2013 Help'
TOCTitle: エッジ トランスポート サーバーでのアドレス書き換えエントリのインポート
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61060535
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# エッジ トランスポート サーバーでのアドレス書き換えエントリのインポート

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

コンマ区切り値 (CSV) ファイルを使用することによって、アドレス書き換え情報を一括作成したり、エッジ トランスポート サーバーにインポートしたりすることができます。これを実行する必要がある一般的なシナリオを次に示します。

  - アドレス書き換えソリューションをエッジ トランスポート サーバーによって置き換える場合。

  - 契約したサード パーティのソリューション プロバイダーのため、電子メール アドレスの書き換えが必要になった場合。

  - 別の組織を取得し、取得した組織の電子メール アドレスを一時的に書き換えることが必要な場合。

CSV ファイルを作成するには、メモ帳などの任意のテキスト エディター、または Microsoft Excel のようなアプリケーションを使用できます。このトピックの説明に従ってファイルの形式を設定し, .csv ファイルとしてファイルを保存します。

CSV ファイルの最初の行、つまり*ヘッダー行*には、パラメーターの名前のリストが含まれています。パラメーターとパラメーターの間はコンマで区切られています。必須パラメーターとオプション パラメーターについて、以下の表で説明します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>必須</p></td>
<td><p>アドレス書き換えエントリのための、わかりやすい一意の名前。</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>必須</p></td>
<td><p>変更するアドレス。次の値を使用できます。</p>
<ul>
<li><p>単一の電子メール アドレス (chris@contoso.com)</p></li>
<li><p>単一のドメインまたはサブドメイン (contoso.com や sales.contoso.com)</p></li>
<li><p>ドメインとすべてのサブドメイン (*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>必須</p></td>
<td><p>最終的な電子メール アドレス。次の値を使用できます。</p>
<ul>
<li><p><em>InternalAddress</em> に単一の電子メール アドレスを指定した場合、単一の電子メール アドレス。</p></li>
<li><p><em>InternalAddress</em> の他のすべての値の単一のドメインまたはサブドメイン</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>省略可能</p></td>
<td><p>ドメインおよびすべてのサブドメイン (*.contoso.com) に含まれる電子メール アドレスを書き換える場合のみ使用可能。アドレス書き換えから除外するサブドメインを 1 つ以上指定します。値は二重引用符で囲み、値が複数の場合はそれらをコンマで区切ってください。たとえば、<code>&quot;marketing.contoso.com&quot;</code> または <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>省略可能</p></td>
<td><p><code>False</code> は、着信および発信のメールでアドレスが書き換えられることを意味します。<code>True</code> は、発信メールでのみアドレス書き換えがなされることを意味します。その場合、書き換えられる電子メール アドレスを、関係する受信者のプロキシー アドレスとして手動で構成する必要があります。</p>
<p>既定値は <code>False</code> ですが、<em>InternalAddress</em> にワイルドカード文字が含まれている場合 (*.contoso.com)、<code>True</code> に設定しなければなりません。</p>
<p>CSV ファイルの <em>OutboundOnly</em> パラメーター値は、<code>True</code> または <code>False</code> であって、<code>$True</code> と <code>$False</code> ではありません。</p></td>
</tr>
</tbody>
</table>


ヘッダー行の下の各行は、個々のアドレス書き換えエントリを表しています。各行の値は、ヘッダー行のパラメーター名と同じ順序で並んでいる必要があります。値と値の間はコンマで区切ります。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:30 分

  - アドレス書き換えによる影響について、十分に理解しておいてください。たとえば、書き換えられる電子メール アドレスは、Exchange 組織の中で固有でなければならず、関係する受信者に対してプロキシー アドレスを設定することが必要になるかもしれません。詳細については、「[エッジ トランスポート サーバー上でのアドレス書き換え](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)」および「[エッジ トランスポート サーバー上でアドレス書き換えを管理する](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md)」を参照してください。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「アドレス書き換えエージェント」。

  - 複数のエッジ トランスポート サーバーがある場合は、このトピックにある手順を使用することによって、単一のエッジ トランスポート サーバーにアドレス書き換えエントリをインポートした後、そのエッジ トランスポート サーバーの設定と同一の値を、組織内の他のエッジ トランスポート サーバーにも設定することをお勧めします。エッジ トランスポート サーバーを複製する方法の詳細については、「[エッジ トランスポート サーバーの複製構成](edge-transport-server-cloned-configuration-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:CSV ファイルの作成

CSV ファイルを作成する際には、次の項目を検討してください。

  - CSV ファイルでオプション パラメーターの値を指定する場合、すべての行でその列に値が含まれていなければなりません。作成する複数のアドレス書き換えエントリの中にオプション パラメーターであるものと、そうでないものの両方が存在する場合、それらのアドレス書き換えエントリを分けて別個の 2 つの CSV ファイルを作成し、別々にインポートする必要があります。

  - CSV ファイルに非 ASCII 文字が含まれている場合は、必ず UTF-8 などの Unicode エンコードで CSV ファイルを保存するようにしてください。アプリケーションによって、コンピューターのシステム ロケールが CSV ファイルで使用されている言語と一致する場合に、CSV ファイルを UTF-8 などの Unicode エンコードで保存した方が簡単な場合があります。

次の例では、省略可能な *ExceptionList* および *OutboundOnly* パラメーターを CSV ファイルに指定する方法を示します。

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## 手順 2:CSV ファイルのインポート

CSV ファイルをインポートするには、以下の構文を使用します。

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

次の例では、C:\\My Documents\\ImportAddressRewriteEntries.csv から、アドレス書き換えエントリをインポートします。

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## このステップの検証方法

アドレス書き換えエントリが CSV ファイルから正常にインポートされたことを確認するには、以下のようにします。

1.  すべてのアドレス書き換えエントリを表示するため、コマンド `Get-AddressRewriteEntry` を実行します。

2.  特定のアドレス書き換えエントリについての詳細情報を確認するため、コマンド `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List` を実行します。

