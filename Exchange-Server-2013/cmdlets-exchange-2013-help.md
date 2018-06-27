---
title: 'コマンドレット: Exchange 2013 Help'
TOCTitle: コマンドレット
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 49115960
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# コマンドレット

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

*コマンドレット*とは、Exchange 管理シェル内の機能の最小単位です。コマンドレットは、他のシェル内の組み込みコマンド (たとえば `cmd.exe` の `dir` コマンド) に似ています。これらの一般的なコマンドと同様に、コマンドレットはシェル内のコマンド ラインから直接呼び出すことができ、個別のプロセスとしてではなく、シェルのコンテキストで実行されます。


> [!NOTE]
> Microsoft Exchange Server 2007 以降、Exchange 2013&nbsp;PowerShell&nbsp;のリモート機能の使用により Windows がコマンドレッドを内部的に使用する方法が変更されました。これらの変更によりコマンドレットの使用の必要性が高まり、さらに Exchange サーバーを柔軟に管理できるようになりました。



コマンドレットは通常、繰り返し行われる管理タスクを中心にして設計されています。シェルでは、Exchange 固有の管理タスク用に何百ものコマンドレットが提供されています。Exchange PowerShell の基本的なシェル設計に含まれている Windows 以外のシステム コマンドレットに加え、これらのコマンドレットが使用できます。Exchange 管理シェルを開く方法の詳細については、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。

シェルのすべてのコマンドは、動詞と名詞の組み合わせで示されます。動詞と名詞の組み合わせは常にハイフン (-) で区切られ (スペースはありません)、コマンドレットの名詞は常に単数形です。動詞は、コマンドレットが行う処理を表します。名詞は、コマンドレットが処理を行うオブジェクトを表します。たとえば、**Get-SystemMessage** コマンドレットでは、動詞が **Get** で、名詞が **SystemMessage** です。特定の機能を管理するすべてのシェル コマンドレットには、同じ名詞が使用されます。次の表に、シェルで使用できる動詞の例を示します。


> [!NOTE]
> 既定では、動詞が省略されている場合、シェルは <STRONG>Get</STRONG> 動詞であると見なします。たとえば、<STRONG>Mailbox</STRONG> を呼び出した場合、<STRONG>Get-Mailbox</STRONG> を呼び出した場合と同じ結果になります。



### Exchange 管理シェルでの動詞の例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>動詞</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Disable</strong></p></td>
<td><p><strong>Disable</strong> コマンドレットは、指定したExchange オブジェクトの <code>Enabled</code> 状態を <code>$False</code> に設定します。これにより、オブジェクトが存在している場合でも、オブジェクトがデータを処理しないようになります。</p></td>
</tr>
<tr class="even">
<td><p><strong>Enable</strong></p></td>
<td><p><strong>Enable</strong> コマンドレットは、指定した Exchange オブジェクトの &quot;有効&quot; 状態を <code>$True</code> に設定します。これにより、オブジェクトがデータを処理できるようになります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get</strong></p></td>
<td><p><strong>Get</strong> コマンドレットは、特定の Exchange オブジェクトに関する情報を取得します。</p>

> [!NOTE]
> ほとんどの <STRONG>Get</STRONG> コマンドレットは、実行時に概要情報のみを返します。コマンド実行時に詳細情報を返すよう <STRONG>Get</STRONG> コマンドレットに伝えるには、コマンドを <STRONG>Format-List</STRONG> コマンドレットにパイプ処理します。<STRONG>Format-List</STRONG> コマンドの詳細については、「<A href="working-with-command-output-exchange-2013-help.md">コマンド出力の操作</A>」を参照してください。パイプライン処理の詳細については、「<A href="https://technet.microsoft.com/ja-jp/library/aa998260(v=exchg.150)">パイプライン処理</A>」を参照してください。


</td>
</tr>
<tr class="even">
<td><p><strong>Install</strong></p></td>
<td><p><strong>Install</strong> コマンドレットは、新しいオブジェクトまたは機能を Exchange サーバーにインストールします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move</strong></p></td>
<td><p><strong>Move</strong> コマンドレットは、指定した Exchange オブジェクトを、1 つのコンテナーまたはサーバーから別のコンテナーまたはサーバーに移します。</p></td>
</tr>
<tr class="even">
<td><p><strong>New</strong></p></td>
<td><p><strong>New</strong> コマンドレットは、新しい Exchange オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remove</strong></p></td>
<td><p><strong>Remove</strong> コマンドレットは、指定した Exchange オブジェクトを削除します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set</strong></p></td>
<td><p><strong>Set</strong> コマンドレットは、既存の Exchange オブジェクトのプロパティを変更します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Test</strong></p></td>
<td><p><strong>Test</strong> コマンドレットは、指定した Exchange コンポーネントをテストし、参照用のログ ファイルを生成します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Uninstall</strong></p></td>
<td><p><strong>Uninstall</strong> コマンドレットは、Exchange サーバーからオブジェクトまたは機能を削除します。</p></td>
</tr>
</tbody>
</table>


以下のコマンドレットの一覧は、完全なコマンドレット セットの例です。このコマンドレット セットは、Exchange 2013 の配信状態通知 (DSN) メッセージおよびメールボックス クォータ メッセージ機能を管理するために使用されます。

  - **Get-SystemMessage**

  - **New-SystemMessage**

  - **Remove-SystemMessage**

  - **Set-SystemMessage**

