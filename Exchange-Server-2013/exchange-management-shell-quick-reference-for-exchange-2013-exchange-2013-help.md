---
title: 'Exchange 2013 の Exchange 管理シェル クイック リファレンス: Exchange 2013 Help'
TOCTitle: Exchange 2013 の Exchange 管理シェル クイック リファレンス
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 49129392
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 の Exchange 管理シェル クイック リファレンス

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

このトピックでは、Microsoft Exchange Server 2013 の RTM (Release To Manufacturing) 版およびそれ以降のバージョンで最もよく使用されるコマンドレットについて説明し、使用法の例を示します。


> [!NOTE]
> Exchange 2013 に関するその他の多くのコンテンツが近く追加される予定です。



Exchange の Exchange 2013 管理シェルおよびすべての使用可能なコマンドレットの詳細については、以下のトピックを参照してください。

  - [Exchange 2013 で Powershell を使用する (Exchange 管理シェル)](https://technet.microsoft.com/ja-jp/library/bb123778\(v=exchg.150\))

  - [Exchange 2013 コマンドレット](https://technet.microsoft.com/ja-jp/library/bb124413\(v=exchg.150\))

## 参照する内容

## コマンドレットの共通アクション

以下の動詞は、ほとんどのコマンドレットでサポートされ、特定のアクションと関連付けられています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>New という動詞は、新しい構成設定、新しいデータベース、新しい SMTP コネクタなど、何らかのインスタンスを作成します。</p></td>
</tr>
<tr class="even">
<td><p>Remove</p></td>
<td><p>動詞 Remove は、メールボックスやトランスポート ルールなど、何らかのインスタンスを削除します。</p>
<p>すべての Remove コマンドレットは、<em>WhatIf</em> パラメーターと <em>Confirm</em> パラメーターをサポートします。これらのパラメーターの詳細については、「Important Parameters」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>Enable</p></td>
<td><p>動詞 Enable は、設定を有効にしたり、受信者のメールを有効にしたりします。</p></td>
</tr>
<tr class="even">
<td><p>Disable</p></td>
<td><p>動詞 Disable は、有効な設定を無効にしたり、受信者のメールを無効にしたりします。</p>
<p>すべての Disable タスクも、<em>WhatIf</em> パラメーターと <em>Confirm</em> パラメーターをサポートします。これらのパラメーターの詳細については、「Important Parameters」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>Set</p></td>
<td><p>動詞 Set は、連絡先のエイリアスや、メールボックス データベースの削除済みアイテムの保存期間など、オブジェクトの特定の設定を変更します。</p></td>
</tr>
<tr class="even">
<td><p>Get</p></td>
<td><p>動詞 Get は、特定のメールボックス、すべてのメールボックス ユーザー、あるドメインのメールボックス ユーザーなど、特定のオブジェクトやある種類のオブジェクトのサブセットを照会します。</p></td>
</tr>
</tbody>
</table>


## 重要なパラメーター

以下のパラメーターは、コマンドの実行方法を制御したり、コマンドがデータに影響を与える前にコマンドの動作を正確に指定したりするために使用します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Identity</p></td>
<td><p><em>Identity</em> パラメーターによって、タスクの一意のオブジェクトが識別されます。通常は、Enable、Disable、Remove、Set、および Get の各コマンドレットと共に使用します。<em>Identity</em> は位置パラメーターでもあります。つまり、コマンド ラインでパラメーターの値を指定する際に、<em>Identity</em> を指定する必要はありません。</p>
<p>たとえば、<em>Get-Mailbox -Identity user1</em> では、<em>user1</em> のメールボックスが照会されます。<em>Get-Mailbox user1</em> は、<em>Get-Mailbox -Identity user1</em> と同じです。</p></td>
</tr>
<tr class="even">
<td><p>WhatIf</p></td>
<td><p><em>WhatIf</em> パラメーターには、オブジェクトに対して行われる操作をシミュレートすることを指定します。<em>WhatIf</em> パラメーターを使用すると、変更を実際に適用することなく、どのような変化が発生するのかを確認できます。既定値は <em>$true</em> です。</p></td>
</tr>
<tr class="odd">
<td><p>Confirm</p></td>
<td><p><em>Confirm</em> パラメーターを指定すると、コマンドレットは、処理を継続する前にいったん停止し、これから実行することを確認するよう管理者に要求します。既定値は <em>$true</em> です。</p></td>
</tr>
<tr class="even">
<td><p>Validate</p></td>
<td><p><em>Validate</em> パラメーターを指定すると、コマンドレットは、操作を実行するためのすべての前提条件が満たされていて、操作が正常に完了することを確認します。</p></td>
</tr>
</tbody>
</table>


## ヒント

次のコマンドは、Exchange 2013 を管理する際に使用できるさまざまなタスクに関連付けられています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-Command</p></td>
<td><p>このコマンドレットは、Exchange 2013 で実行できるすべてのタスクを取得します。</p></td>
</tr>
<tr class="even">
<td><p>Get-Command *<em>keyword</em>*</p></td>
<td><p>このコマンドレットは、コマンドレット内で <em>keyword</em> を含むタスクを取得します。</p></td>
</tr>
<tr class="odd">
<td><p>Get-<em>task</em> | Get-Member</p></td>
<td><p>このコマンドレットは、<em>task</em> のすべてのプロパティとメソッドを取得します。</p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List</p></td>
<td><p>このコマンドレットは、クエリの出力を書式設定された一覧で表示します。Get コマンドレットの出力を Format-List にパイプ処理し、そのコマンドによって返されるオブジェクトに存在するプロパティのセット全体を表示できます。または、次の例で示すように、個々のプロパティをコンマで区切って指定して表示することもできます。<em>Get-Mailbox *john* | Format-List alias,*quota</em></p></td>
</tr>
<tr class="odd">
<td><p>Help <em>task</em></p></td>
<td><p>このコマンドレットは、次の例のように、Exchange の任意のタスクに対する Exchange 2013 管理シェルのヘルプ情報を取得します。<em>Help Get-Mailbox</em></p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List &gt; <em>file.txt</em></p></td>
<td><p>このコマンドレットは、<em>task</em> の出力を次のテキスト ファイルにエクスポートします。<em>file.txt</em></p></td>
</tr>
</tbody>
</table>


## アクセス許可


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-RoleGroupMember &quot;<em>Organization Management/組織の管理</em>&quot;</p></td>
<td><p>このコマンドは、&quot;<em>Organization Management/組織の管理</em>&quot; 管理役割グループのメンバーを取得します。</p></td>
</tr>
<tr class="even">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation/メール受信者の作成</em>&quot; -GetEffectiveUsers</p></td>
<td><p>このコマンドは、&quot;<em>Mail Recipient Creation/メール受信者の作成</em>&quot; 管理役割により指定されたアクセス許可を与えられたすべてのユーザーの一覧を取得します。これには、&quot;Mail Recipient Creation/メール受信者の作成&quot; 役割に割り当てられた役割グループまたはユニバーサル セキュリティ グループ (USG) のメンバーであるユーザーも含まれます。これには別のフォレストのリンクされた役割グループのメンバーであるユーザーは含まれません。</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -RoleAssignee <em>Administrator</em> | Get-ManagementRole | Get-ManagementRoleEntry</p></td>
<td><p>このコマンドは、ユーザー <em>Administrator</em> が実行できるコマンドレットの一覧を取得します。</p></td>
</tr>
<tr class="even">
<td><p>ForEach ($RoleEntry in Get-ManagementRoleEntry *\<em>Remove-Mailbox</em> -parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne &quot;All Group Members&quot;} | FL Role, EffectiveUserName, AssignmentChain}</p></td>
<td><p>このコマンドは、<em>Remove-Mailbox</em> コマンドレットを実行できるすべてのユーザーの一覧を取得します。</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -WritableRecipient <em>kima</em> -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain</p></td>
<td><p>このコマンドは、<em>kima</em> のメールボックスを変更できるすべてのユーザーの一覧を取得します。</p></td>
</tr>
<tr class="even">
<td><p>New-ManagementScope &quot;<em>Seattle Users</em>&quot; -RecipientRestrictionFilter { <em>City</em> -Eq &quot;<em>Seattle</em>&quot; }</p>
<p>New-RoleGroup &quot;<em>Seattle Admins</em>&quot; -Roles &quot;<em>Mail Recipients</em>&quot;, &quot;<em>Mail Recipient Creation</em>&quot;, &quot;<em>Mailbox Import Export</em>&quot;, -CustomRecipientWriteScope &quot;<em>Seattle Users</em>&quot;</p></td>
<td><p>このコマンドは、新しい管理スコープと管理役割グループを作成し、役割グループのメンバーが Seattle の受信者を管理できるようにします。</p>
<p>最初に、<em>Seattle Users</em> 管理スコープを作成します。これはユーザー オブジェクトの <em>City</em> 属性が <em>Seattle</em> である受信者だけに一致します。</p>
<p>次に、&quot;<em>Seattle Admins/シアトル管理者</em>&quot; という新しい役割グループを作成し、&quot;<em>Mail Recipients/メール受信者</em>&quot;、&quot;<em>Mail Recipient Creation/メール受信者の作成</em>&quot;、および &quot; <em>Mailbox Import Export/メールボックスのインポート/エクスポート</em>&quot; 役割を割り当てます。役割グループには、そのメンバーが<em>Seattle Users</em> 受信者フィルター スコープに一致するユーザーだけを管理できるようなスコープが設定されます。</p></td>
</tr>
<tr class="odd">
<td><p>New-ManagementScope &quot;<em>Vancouver Servers</em>&quot; -ServerRestrictionFilter { <em>ServerSite</em> -Eq &quot;<em>Vancouver</em>&quot; }</p>
<p>$RoleGroup = Get-RoleGroup &quot;<em>Server Management</em>&quot;</p>
<p>New-RoleGroup &quot;<em>Vancouver Server Management</em>&quot; -Roles $RoleGroup.Roles -CustomConfigWriteScope &quot;<em>Vancouver Servers</em>&quot;</p></td>
<td><p>このコマンドは、新しい管理スコープを作成し、既存の役割グループをコピーして、新しい役割グループのメンバーが Vancouver Active Directory サイトのサーバーのみを管理できるようにします。</p>
<p>最初に、<em>Vancouver Servers</em> 管理スコープを作成します。これは <em>Vancouver</em> Active Directory サイトにあるサーバーのみに一致します。その Active Directory サイトは、サーバー オブジェクトの <em>ServerSite</em> 属性に格納さています。</p>
<p>次に、&quot;<em>Vancouver Server Management/バンクーバー サーバー管理</em>&quot; という新しい役割グループを作成します。これは &quot;<em>Server Management/サーバー管理</em>&quot; 役割グループのコピーです。ただしこの新しい役割グループには、そのメンバーが <em>Vancouver Servers</em> 構成フィルター スコープに一致するサーバーのみを管理できるようにするスコープが設定されています。</p></td>
</tr>
<tr class="even">
<td><p>Add-RoleGroupMember &quot;<em>Organization Management</em>&quot; -Member <em>davids</em></p></td>
<td><p>このコマンドは、ユーザー <em>davids</em> を &quot;<em>Organization Management/組織の管理</em>&quot; 役割グループに追加します。</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -RoleAssignee &quot;<em>Seattle Admins</em>&quot; | Remove-ManagementRoleAssignment</p></td>
<td><p>このコマンドは、&quot;<em>Mail Recipient Creation/メール受信者の作成</em>&quot; 役割を &quot;<em>Seattle Admins/シアトル管理者</em>&quot; 役割グループから削除します。このコマンドは、役割を役割グループに割り当てる管理役割割り当ての名前を知る必要がないので便利です。</p></td>
</tr>
</tbody>
</table>


## リモート シェル


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos</p>
<p>Import-PSSession $Session</p></td>
<td><p>これらのコマンドは、ローカル ドメインに参加しているコンピューターと、FQDN が <em>ExServer.contoso.com</em> であるリモート Exchange 2013 サーバーの間に新しいリモート シェル セッションを開きます。Windows PowerShell コマンドライン インターフェイスを持つ Windows Management Framework のみがインストールされているローカル コンピューターで、リモート Exchange 2013 サーバーを管理したい場合は、このコマンドを使用します。このコマンドは、リモート Exchange 2013 サーバーに対する認証に、現在のログオン資格情報を使用します。</p></td>
</tr>
<tr class="even">
<td><p>$UserCredential = Get-Credential</p>
<p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos -Credential $UserCredential</p>
<p>Import-PSSession $Session</p></td>
<td><p>これらのコマンドは、ローカル ドメインに参加しているコンピューターと、FQDN が <em>ExServer.contoso.com</em> であるリモート Exchange 2013 サーバーの間に新しいリモート シェル セッションを開きます。Windows PowerShell を持つ Windows Management Framework のみがインストールされているローカル コンピューターで、リモート Exchange 2013 サーバーを管理したい場合は、このコマンドを使用します。このコマンドは、リモート Exchange 2013 サーバーに対する認証に、明示的に指定された資格情報を使用します。</p></td>
</tr>
<tr class="odd">
<td><p>Remove-PSSession $Session</p></td>
<td><p>このコマンドは、ローカル コンピューターとリモート Exchange 2013 サーバーの間のリモート シェル セッションを閉じます。</p></td>
</tr>
<tr class="even">
<td><p>Import-RecipientDataProperty -Identity &quot;Tony Smith&quot; -SpokenName -FileData <em>([Byte[]]$(Get-Content -Path &quot;M:\AudioFiles\TonySmith.wma&quot; -Encoding Byte -ReadCount 0))</em></p></td>
<td><p>このコマンドは、コマンドレット上で FileData パラメーターを使用してリモート Exchange 2013 サーバーにファイルをインポートする際に必要な構文例 (イタリック表示) を表示します。この構文によって、<em>M:\AudioFiles\TonySmith.wma</em> ファイルに含まれるデータがカプセル化され、そのデータが Import-RecipientDataProperty コマンドレットの FileData プロパティに流されます。</p>
<p>FileData パラメーターは、ほとんどのコマンドレットでこの構文を使用して、ローカル コンピューター上のファイルからのデータを受け付けます。</p></td>
</tr>
<tr class="odd">
<td><p>Export-RecipientDataProperty -Identity tony@contoso.com -SpokenName <em>| ForEach { $_.FileData | Add-Content C:\tonysmith.wma -Encoding Byte}</em></p></td>
<td><p>このコマンドは、リモート Exchange 2013 サーバーからファイルをエクスポートする際に必要な構文例 (イタリック表示) を表示します。この構文によって、コマンドレットによって返されるオブジェクト上の FileData プロパティに格納されているデータがカプセル化され、そのデータがローカル コンピューターに流されます。続いてそのデータが、<em>C:\tonysmith.wma</em> ファイルに格納されます。</p>
<p>FileData プロパティを持つオブジェクトを出力するほとんどのコマンドレットは、ローカル コンピューターへのデータのエクスポートにこの構文を使用します。</p></td>
</tr>
</tbody>
</table>

