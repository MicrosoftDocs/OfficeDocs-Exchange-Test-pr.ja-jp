---
title: 'コマンドレット拡張エージェント: Exchange 2013 Help'
TOCTitle: コマンドレット拡張エージェント
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50555722
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# コマンドレット拡張エージェント

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

コマンドレット拡張エージェントは、 Exchange 2013 コマンドレットの実行時にコマンドレットによって呼び出される Microsoft Exchange Server 2013 のコンポーネントです。コマンドレット拡張エージェントは、その名前が示すように、コマンドレットの要求に基づいてデータの処理または追加操作の実行を支援することで、それらを呼び出すコマンドレットの機能を拡張します。コマンドレット拡張エージェントは、任意のサーバーの役割で使用可能です。

エージェントは、Exchange 管理シェル コマンドレットの機能を変更、置き換え、または拡張できます。また、コマンド上で提供されない必須パラメーターの値の提供、ユーザーが入力した値の上書き、コマンドレットの実行中にコマンドレット ワークフロー外の他の操作の実行などを行うことができます。

たとえば、**New-Mailbox** コマンドレットは、新しいメールボックスを作成するメールボックス データベースを指定する、*Database* パラメーターを受け入れます。Microsoft Exchange Server 2007 では、**New-Mailbox** コマンドレットの実行時に *Database* パラメーターを指定しない場合、コマンドは失敗します。ただし、Exchange 2013 では、**New-Mailbox** コマンドレットは、その実行時に `Mailbox Resources Management` エージェントを呼び出します。*Database* パラメーターが指定されていない場合、`Mailbox Resources Management` エージェントは、自動的に新しいメールボックスを作成する適切なメールボックス データベースを特定し、その値を *Database* パラメーターに挿入します。

コマンドレット拡張エージェントは、Exchange 2013 コマンドレットおよび Microsoft Exchange Server 2010 コマンドレットによってのみ起動できます。Exchange 2007 コマンドレットおよび他の Microsoft/サード パーティ製品によって提供されるコマンドレットは、コマンドレット拡張エージェントを呼び出すことができません。スクリプトもコマンドレット拡張エージェントを直接呼び出すことはできません。ただし、スクリプトに Exchange 2013 コマンドレットが含まれている場合、これらのコマンドレットはコマンドレット拡張エージェントを呼び出し続けます。

コマンドレット拡張子エージェントに関連する管理タスクについては、「[コマンドレット拡張エージェントの管理](manage-cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

## エージェントの優先度

エージェントの優先度によって、コマンドレットの実行中にエージェントが呼び出される順序が決まります。優先度が高い、つまり 0 に近いエージェントが最初に呼び出されます。2 つ以上のエージェントが同じプロパティの値を設定しようとする場合に、エージェントの優先度が重要になります。優先度が最も高いエージェントによるプロパティ値の設定試行は成功し、優先度の低いエージェントによる同じプロパティ設定に対する後続の試行は無視されます。たとえば、オブジェクトの **Name** プロパティが優先度 3 のエージェントと優先度 6 の別のエージェントによって変更される場合、優先度 6 のエージェントによる変更は無視されます。

`Scripting agent` を使用して、他の優先度の高いエージェントによって設定される可能性があるプロパティの値を設定する場合、次のオプションがあります。

  - 現在プロパティを設定しているエージェントを無効にします。

  - `Scripting agent` を置き換える既存のエージェントより高い優先度に設定します。

  - エージェントの優先度を同じ値のままにして、`Scripting agent` の下で実行するスクリプトによって他のエージェントが提供する値が重視されることを確認します。


> [!NOTE]
> 優先度の変更またはビルトイン エージェントの機能の置き換えは、高度な操作です。変更について完全に理解するようにしてください。



エージェントの優先度の変更の詳細については、「[コマンドレット拡張エージェントの管理](manage-cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

## ビルトイン エージェント

Exchange 2013 には、コマンドレットの実行時に呼び出すことができるいくつかのエージェントが含まれています。次の表に、エージェント、その順序、および既定でそのエージェントが有効になっているかどうかの一覧を示します。Exchange 2013 を実行しているサーバーから、エージェントを追加または削除することはできません。ただし、`Scripting agent` を使用して Windows PowerShell スクリプトを実行することにより、これを使用するコマンドレットの機能を拡張できます。`Scripting agent` の詳細については、このトピックの後半の「Scripting agent」を参照してください。

特定のエージェントの機能を、`Scripting agent` を使用して呼び出すカスタム スクリプトで提供する機能で置き換える場合、ほとんどのエージェントを有効または無効にしたり、エージェントの優先度を変更したりできます。ただし、一部のエージェントは無効にできません。無効にできないエージェントは*システム エージェント*と呼ばれ、これらの *IsSystem* プロパティは `$True` に設定されています。次の表に、Exchange 2013 コマンドレット拡張エージェント (システム エージェントを含む) の詳細を示します。

エージェントの構成は、組織レベルで格納されます。エージェントを有効または無効にするか、その優先度を設定する場合、組織内のすべてのサーバーにわたってエージェントの構成を設定します。例外は、スクリプトを `Scripting agent` に追加する場合です。各サーバー上のスクリプトは個別に更新する必要があります。`Scripting agent` で使用するスクリプトの構成の詳細については、このトピックの後半の「Scripting agent」を参照してください。


> [!NOTE]
> 各エージェントの機能およびエージェントと Exchange コマンドレットのやり取りを十分に理解していない場合、エージェントの優先度を変更したり、エージェントを有効または無効にすると、予期しない結果が発生する可能性があります。エージェントの構成を変更する前に、目的の変更内容と結果を十分に理解した上で、カスタム スクリプトが意図したとおりに動作することを確認してください。



### Exchange 2013 コマンドレット拡張子エージェント

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>エージェント名</th>
<th>優先度</th>
<th>既定で有効</th>
<th>システム エージェント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Scripting agent

Exchange 2013 の `Scripting agent` コマンドレット拡張エージェントを使用すると、Exchange コマンドレットの実行に独自のスクリプト ロジックを挿入できます。`Scripting agent` を使用すると、条件の追加、値の上書き、およびレポートの設定を行うことができます。


> [!NOTE]
> <CODE>Scripting agent</CODE> コマンドレット拡張エージェントを有効にすると、Exchange 2013 を実行するサーバーでコマンドレットを実行するたびにこのエージェントが呼び出されます。Exchange 管理シェルで直接コマンドレットを実行する場合だけでなく、Exchange サービスおよび Exchange 管理コンソール (EAC) でコマンドレットを実行する場合も、このエージェントが呼び出されます。更新した構成ファイルを Exchange 2013 サーバーにコピーして、<CODE>Scripting agent</CODE> コマンドレット拡張エージェントを有効にする場合、事前にスクリプトと構成ファイルへの変更をテストしておくことを強くお勧めします。



Exchange コマンドレットを実行するたびに、`Scripting agent` コマンドレット拡張エージェントがコマンドレットによって呼び出されます。このエージェントが呼び出されると、コマンドレットによって呼び出されるようにスクリプトが構成されているかどうかがコマンドレットによってチェックされます。コマンドレットに対してスクリプトを実行する必要がある場合、コマンドレットによってスクリプトで定義されている API の呼び出しが試行されます。利用可能な API は次のとおりです。これらの API は以下の順序で呼び出されます。

1.  **ProvisionDefaultProperties**   この API は、オブジェクトの作成時にオブジェクトに対してプロパティ値を設定するために使用します。値を設定すると、設定した値はコマンドレットに返され、その値がコマンドレットによってプロパティに対して設定されます。ユーザーが値を指定しなかった場合はプロパティに対して値を入力できます。また、ユーザーが指定した値を上書きすることも可能です。この API は、より優先度の高いエージェントによって設定された値を使用します。`Scripting agent` コマンドレット拡張エージェントは、より優先度の高いエージェントによって設定された値を上書きできません。

2.  **UpdateAffectedIConfigurable**   この API は、`Validate` API の呼び出しを除く他のすべての処理が完了した後で、オブジェクトのプロパティ値を設定するために使用します。この API は、より優先度の高いエージェントによって設定された値を使用します。`Scripting agent` コマンドレット拡張エージェントは、より優先度の高いエージェントによって設定された値を上書きできません。

3.  **Validate**   この API は、コマンドレットによって設定されようとしているオブジェクトのプロパティ値を検証するために使用します。この API は、コマンドレットがデータを書き込む直前に呼び出されます。コマンドレットが成功、または失敗する検証チェックを構成できます。コマンドレットがこの API 内の検証チェックをパスすると、コマンドレットはデータの書き込みを許可されます。コマンドレットが検証チェックに失敗すると、この API で定義されているエラーが返されます。

4.  **OnComplete**   この API は、すべてのコマンドレット処理が完了した後に使用します。この API は、外部データベースへのデータの書き込みなどの処理後のタスクを実行するために使用します。


> [!NOTE]
> <CODE>Scripting agent</CODE> コマンドレット拡張エージェントは、<CODE>Get</CODE> コマンドを指定したコマンドレットを実行したときには呼び出されません。



## Scripting agent 構成ファイル

`Scripting agent` 構成ファイルには、`Scripting agent` で実行するすべてのスクリプトが含まれています。構成ファイル内のスクリプトは、スクリプトの開始と終了、およびスクリプトにデータを渡すのに必要な各種入力パラメーターを定義する XML タグ内に格納されています。スクリプトは、Windows PowerShell 構文に従って記述されます。構成ファイルは、次の表の要素または属性を使用する 1 つの XML ファイルです。

### Scripting agent 構成ファイルの属性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>属性</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>該当なし</p></td>
<td><p>この要素には、<code>Scripting agent</code> コマンドレット拡張エージェントが実行可能なスクリプトがすべて含まれます。<code>Feature</code> タグは、このタグの子です。</p>
<p>構成ファイルには <code>Configuration</code> タグは 1 つしかありません。</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>該当なし</p></td>
<td><p>この要素には、機能に関連するすスクリプト セットが含まれます。<code>ApiCall</code> 子タグで定義されている各スクリプトは、コマンドレットの実行パイプラインの特定の部分を拡張します。このタグには、<code>Name</code> および <code>Cmdlets</code> 属性が含まれます</p>
<p><code>Feature</code> タグの下には、<code>Configuration</code> タグを複数含めることができます。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>この属性には、機能の名前が含まれます。この属性を使用すると、タグ内に格納されているスクリプトによって拡張される機能を特定しやすくなります。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>この属性には、この機能拡張内のスクリプト セットによって使用される Exchange コマンドレットの一覧が含まれます。複数のコマンドレットを指定する場合は、各コマンドレットをコンマで区切ります。</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>該当なし</p></td>
<td><p>この要素には、コマンドレット実行パイプラインの一部を拡張できるスクリプトが含まれます。各スクリプトは、拡張するコマンドレット実行パイプライン内で API 呼び出し名で定義されます。拡張できる API 名は以下のとおりです。</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>この属性には、コマンドレット実行パイプラインを拡張している API 呼び出しの名前が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>該当なし</p></td>
<td><p>この要素には、構成ファイル内のすべてのスクリプトから使用できる機能が含まれます。</p></td>
</tr>
</tbody>
</table>


すべての Exchange 2013 サーバーでは \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents フォルダーに ScriptingAgentConfig.xml.sample ファイルが保存されています。Scripting Agent コマンドレット拡張エージェントを有効にする場合は、すべての Exchange 2013 サーバーで、このファイルの名前を ScriptingAgentConfig.xml に変更する必要があります。サンプル構成ファイルには、構成ファイルにスクリプトを追加する方法を理解するのに役立つサンプル スクリプトが含まれています。

構成ファイルにスクリプトを追加した後、または構成ファイルを変更した場合は、組織内のすべての Exchange 2013 サーバーの構成ファイルを更新する必要があります。このためには、`Scripting Agent` コマンドレット拡張エージェントを実行するスクリプトの最新バージョンを各サーバーに置く必要があります。

スクリプト内で通常使用される文字の中には、XML 内で特殊な意味を持つものがあります。スクリプトでこれらの文字を使用する場合は、エスケープ シーケンスを使用します。たとえば、エスケープ シーケンスを使用する文字には以下があります。

  - 大なり記号 (`>`) の代わりに、`&gt;` を使用します。

  - 小なり記号 (`<`) の代わりに、`$lt;` を使用します。

  - アンパサンド (`&`) の代わりに、`&amp;` を使用します。

## Scripting agent を有効にする

`Scripting agent` コマンドレット実行エージェントは既定で無効になっています。`Scripting agent` を有効にすると、このエージェントは Exchange 2013 組織全体に対して有効になります。`Scripting agent` を有効にする際は、すべての Exchange 2013 サーバーで `Scripting agent` 構成ファイルを、独自のスクリプトで正しく名前変更および更新していることを事前に確認してください。構成ファイルの名前を正しく変更していない場合、または構成ファイルを別の Exchange 2013 サーバーからこのコンピューターにコピーしていない場合は、コマンドレットが実行されるごとにエラー メッセージが受信されます。

`Scripting agent` を有効にするには、次の手順を実行します。

1.  組織内のすべての Exchange 2013 サーバーで、**\<インストール パス\>\\V15\\Bin\\CmdletExtensionAgents** 内のScriptingAgentConfig.xml.sample ファイルを、ScriptingAgentConfig.xml に名前変更します。
    

    > [!NOTE]
    > 構成ファイルは Exchange 2013 サーバーから別の Exchange 2013 サーバーにコピーできます。構成ファイルをコピーする際には、事前にコピーする構成ファイルを必ず更新してください。



2.  組織内のすべての Exchange 2013 サーバーで名前変更した構成ファイルに独自のスクリプトを追加します。

3.  `Scripting agent` コマンドレット拡張エージェントを有効にします。コマンドレット拡張エージェントの有効化の詳細については、「[コマンドレット拡張エージェントの管理](manage-cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

## Scripting agent の優先度

既定では、`Scripting agent` コマンドレット実行エージェントは、`Scripting agent` エージェントを除く他のすべてのエージェントの後に実行されます。独自に作成したスクリプトを既存のエージェントに置き換えるには、他のエージェントを無効にするか、`Scripting agent` コマンドレット拡張エージェントが最初に実行されるようにどちらか一方のエージェントの優先度を変更する必要があります。無効にする方法またはエージェントの優先度を変更する方法の詳細については、「[コマンドレット拡張エージェントの管理](manage-cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

