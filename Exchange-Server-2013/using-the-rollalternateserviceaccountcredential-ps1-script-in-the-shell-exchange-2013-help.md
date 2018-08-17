---
title: 'シェルでの RollAlternateserviceAccountCredential.ps1 スクリプトの使用: Exchange 2013 Help'
TOCTitle: シェルでの RollAlternateserviceAccountCredential.ps1 スクリプトの使用
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63918670
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# シェルでの RollAlternateserviceAccountCredential.ps1 スクリプトの使用

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Exchange Server 2013 に含まれている RollAlternateServiceAccountPassword.ps1 スクリプトを使用すると、代替サービス アカウントの資格情報 (ASA 資格情報) を更新して、その更新を指定したクライアント アクセス サーバーに配布できます。


> [!NOTE]  
> Exchange 管理シェルでは、スクリプトは自動的に読み込まれません。すべてのスクリプトの先頭には ".\" を付ける必要があります。たとえば、RollAlternateServiceAccountPassword.ps1 スクリプトを実行するには、「<code>.\RollAlternateServiceAccountPassword.ps1</code>」と入力します。




> [!NOTE]  
> このスクリプトは英語版のみが提供されます。



スクリプトの使用方法および記述方法の詳細については、「[Exchange 管理シェルを使用したスクリプトの作成](https://technet.microsoft.com/ja-jp/library/bb123798\(v=exchg.150\))」を参照してください。

## 構文

    RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -

## 解説

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「クライアント アクセス許可」の「クライアント アクセスのセキュリティ」

## 代替サービス アカウントの資格情報スクリプトの技術的詳細

このスクリプトを使用すると、ASA 資格情報の設定と管理が容易になります。ASA 資格情報を作成し、適切なサービス プリンシパル名を設定したら、スクリプトを使用して、資格情報を対象となるすべてのクライアント アクセス サーバーに配布できます。

スクリプトを使用するには、配布対象となるサーバーと、ASA 資格情報として使用する資格情報を特定する必要があります。

## サーバー スコープ

スクリプトの実行対象として、フォレスト内のすべてのクライアント アクセス サーバー、特定のクライアント アクセス サーバー アレイのすべてのメンバー、特定のサーバーのいずれかを選択してください。利用可能なパラメーターは、*ToEntireForest*、*ToArraryMembers*、および *ToSpecificServers* です。スクリプトの実行対象として、特定のサーバーまたは特定のサーバー アレイのメンバーのいずれかを指定する場合は、*Identity* パラメーターに、対象のサーバー名またはサーバー アレイ名を指定する必要があります。

## 資格情報ソース

このスクリプトは、代替サービス アカウント パスワードを既存のサーバーからコピーできます。または、使用する代替サービス アカウントを指定して、スクリプトを使用してこのアカウントの新しいパスワードを生成できます。利用可能なパラメーターは、*GenerateNewPasswordFor* および *CopyFrom* です。*GenerateNewPasswordFor* パラメーターを使用する場合は、アカウント文字列を「ドメイン\\アカウント名」という形式で指定する必要があります。コンピューター アカウントを使用する場合は、CONTOSO\\ClientServerAcct$ のように、アカウント名の最後に "$" を指定する必要があります。*CopyFrom* パラメーターには、資格情報ソースとして既存のクライアント アクセス サーバー名を指定します。

## 資格情報の新しいパスワードの生成

新しいパスワードは、スクリプトによって作成されます。ユーザーによる入力は必要ありません。スクリプトによって、パスワードがすべての対象コンピューターに配布され、新しく生成されたパスワードで Active Directory アカウントの資格情報が更新されます。

新しく生成されたパスワードは最大 73 文字で、強力なパスワードの標準的な要件を満たします。パスワードの要件が異なる場合は、パスワードを手動で設定し、そのパスワードを対象サーバーにコピーする必要がある場合があります。

サービスの中断を防止するために、スクリプトによって各クライアント アクセス サーバーが調査され、新しいパスワードが追加される以外に、現在のパスワードも保持されます。スクリプトを実行すると、共有される ASA 資格情報は次の 2 つのパスワードのいずれかを使用できるようになります。Active Directory に保存されている現在のパスワード、または Active Directory に設定されていない新しいパスワード。

期限が切れたパスワードなどの有効でなくなったパスワードはすべて、配布先サーバーから削除されます。おそらくパスワードの有効期限が切れたために Active Directory のパスワードが変更できない場合は、スクリプトによってパスワードのリセットが試みられます。これを行うには、代替サービス アカウントがコンピューター アカウントであるかユーザー アカウントであるかによって、Active Directory のコンピューター アカウント パスワードまたはユーザー アカウント パスワードをリセットするアクセス許可が、スクリプトを実行しているアカウントに必要になります。

対象のクライアント アクセス サーバーすべてに対してパスワードが正常に変更されない場合、Active Directory パスワードの更新によって、認証エラーが発生することがあります。スクリプトを無人モードで実行すると、対象のクライアント アクセス サーバーすべてが正常に更新されなければ、Active Directory パスワードは新しいパスワードで更新されません。スクリプトを有人モードで実行すると、Active Directory のパスワードを更新するかを確認するメッセージが表示されます。

## パスワードの管理を自動化するためのスケジュールされたタスクの作成

継続的にパスワードを管理するためにスケジュールされたタスクを作成するためにスクリプトを使用する場合、*CreateScheduledTask* パラメーターを使用します。このパラメーターには、作成するタスク名の文字列が必要です。


> [!NOTE]  
> スケジュールされた無人タスクを作成する場合、事前にスクリプトを実行して、有人モードでスクリプトが正常に動作することを確認してください。



スクリプトによって、スクリプトが保存されているフォルダー内に .cmd ファイルが作成されます。次に、作成された .cmd ファイルを 3 週間おきに実行するタスクがスクリプトによって作成されます。Windows タスク スケジューラを使用して、スケジュールされたタスクを変更できます。たとえば、タスクの実行頻度を変更できます。既定では、タスクは現在ログインしているユーザーとして実行されます。さらに、スクリプトはユーザーがコンピューターにログインしているときにのみ実行されます。ユーザーがログインしているかどうかに関係なくスケジュールされたタスクを実行するように変更することをお勧めします。パスワードをリセットするための Active Directory アクセス許可および Exchange Enterprise 管理者の役割が別のアカウントにある場合、スクリプトをそのアカウントで実行するように設定することも可能です。スケジュールされたタスクを作成すると、スクリプトは自動的に無人モードで実行されます。

## スクリプトのスコープ外のタスク

スクリプトによって ASA 資格情報の SPN は管理されません。また、スクリプトを使用しても、代替サービス アカウントをサーバーから削除することはできません。代替サービス アカウントをサーバーから削除するには、「[負荷分散されたクライアント アクセス サーバーの Kerberos 認証の構成](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)」の「[Turn Kerberos authentication off](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)」セクションを参照してください。

## スクリプトのトラブルシューティング

スケジュールされた無人タスクを作成する場合、事前にスクリプトを実行して、有人モードでスクリプトが正常に動作するのを確認することをお勧めします。トラブルシューティング情報については、「[RollAlternateServiceAccountCredential.ps1 スクリプトのトラブルシューティング](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md)」を参照してください。

## スクリプトの検証

\-verbose フラグを使用してスクリプトを対話的に実行する場合、スクリプトの出力によって正常に終了したスクリプトの処理が示される必要があります。クライアント アクセス サーバーが更新されたことを確認するには、ASA 資格情報上の最終変更時刻のタイム スタンプを確認してください。次の例では、クライアント アクセス サーバーの一覧と、代替サービス アカウントの最終更新時刻を生成します。

    Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration

スクリプトを実行しているコンピューターでイベント ログを調べることもできます。スクリプトのイベント ログ エントリは、ソースの *MSExchange Management Application* から収集され、アプリケーション イベント ログに記録されます。次の表に、記録されるイベントと、その意味を一覧します。

### スクリプトのイベント ID と説明

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベント</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>開始</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>成功 (情報)</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>成功しましたが、警告が生成されました。</p>
<p>スクリプトでいくつかの問題が発生しましたが、それらを解決できたか、またはユーザー入力によって問題を解決する必要がないことが確認されました。スクリプトを対話モードで実行している場合、警告の詳細については、スクリプトの出力を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>失敗</p></td>
</tr>
</tbody>
</table>


スクリプトをスケジュールされたタスクとして実行する場合、タスクの実行結果は、Exchange サーバーの <strong>Logging</strong> フォルダー内の、\[**RollAlternateServiceAccountPassword**\] という名前のサブフォルダーにログ記録されます。

ログを使用して、タスクが正常に実行されたことを確認できます。

## パラメーター


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ToEntireForest</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>ToEntireForest</em> パラメーターは、スクリプトの実行対象として、フォレスト内のすべてのクライアント アクセス サーバーを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>ToArrayMembers</em> パラメーターは、スクリプトの実行対象として、特定のクライアント アクセス サーバー アレイのすべてのメンバーを指定します。</p>

> [!NOTE]  
> <EM>ToArrayMembers</EM> パラメーターまたは <EM>ToSpecificServers</EM> パラメーターを使用する場合は、<EM>Identity</EM> パラメーターを使用してサーバー名またはサーバー アレイ名を指定する必要があります。


</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>ToSpecificServers</em> パラメーターは、スクリプトの実行対象として、特定のサーバーを指定します。</p>

> [!NOTE]  
> <EM>ToArrayMembers</EM> パラメーターまたは <EM>ToSpecificServers</EM> パラメーターを使用する場合は、<EM>Identity</EM> パラメーターを使用してサーバー名またはサーバー アレイ名を指定する必要があります。


</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p><em>Identity</em> パラメーターには、対象とするクライアント アクセス サーバー アレイの名前または特定のサーバー名を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>GenerateNewPasswordFor</em> パラメーターを指定すると、スクリプトによって ASA の新しいパスワードが生成されます。文字列値は、ASA アカウントであり、「ドメイン\アカウント名」という形式で指定する必要があります。コンピューター アカウントを使用する場合は、アカウント名の最後に &quot;$&quot; を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>CopyFrom</em> パラメーターを指定すると、別のクライアント アクセス サーバーから資格情報がコピーされます。文字列値には、クライアント アクセス サーバー名を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>Mode</em> スイッチは、スクリプトを有人モードまたは無人モードのいずれで実行するのかを指定します。無人モードを指定すると、ユーザーの入力に対してプロンプト メッセージが表示されず、必要に応じたより安全なオプションが自動的に選択されます。</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>CreateScheduledTask</em> パラメーターは、スクリプトに対して、スケジュールされたタスクを作成して ASA 資格情報の更新を実行することを指示します。文字列値は、作成されるスケジュールされたタスクの名前です。</p>

> [!NOTE]  
> このスクリプトが保存されるフォルダー内にスクリプトによって .cmd ファイルが作成されます。スケジュールされたタスクは, .cmd ファイルを 3 週間おきに実行します。Windows タスク スケジューラ内で直接タスクを編集し、タスクの実行頻度を変更できます。


</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>WhatIf</em> スイッチは、オブジェクトに対して行われる操作をシミュレートすることを指定します。<em>WhatIf</em> スイッチを使用することで、実際には変更を加えずに、発生する変更内容を確認できます。<em>WhatIf</em> スイッチに値を指定する必要はありません。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>Confirm</em> スイッチを指定すると、コマンドの処理が一時停止します。処理を続行するには、コマンドの処理内容を確認する必要があります。<em>Confirm</em> スイッチに値を指定する必要はありません。</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>Verbose</em> パラメーターは、スクリプトに対して、詳細なログ出力を実行することを指示し、これにより、スクリプトの処理についての追加情報がログ ファイルに書き込まれます。</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>省略可能</p></td>
<td><p><em>Debug</em> パラメーターは、スクリプトに対して、デバッグ モードで実行することを指示します。スクリプトの失敗理由を特定する場合、このパラメーターを使用してください。</p></td>
</tr>
</tbody>
</table>


## 例

## 例 1

この例では、スクリプトを使用して、最初のセットアップを行うためにフォレスト内のすべてのクライアント アクセス サーバーに資格情報をプッシュ転送します。

    .\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose

## 例 2

この例では、ユーザー アカウントの ASA 資格情報の新しいパスワードを生成し、名前が \*mailbox\* に一致するクライアント アクセス サーバー アレイのすべてのメンバーにパスワードを配布します。

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose

## 例 3

この例は、月に 1 回自動的にパスワードをロールする、"Exchange-RollAsa" という名前のスケジュールされたタスクを設定します。フォレスト全体のすべてのクライアント アクセス サーバーの ASA 資格情報を、スクリプトによって生成された新しいパスワードで更新します。スケジュールされたタスクは作成されますが、スクリプトは実行されません。スケジュールされたタスクが実行されても、スクリプトは無人モードで実行されます。

    .\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'

## 例 4

この例では、"CAS01" という名前のクライアント アクセス サーバー アレイ内のすべてのクライアント アクセス サーバーの ASA 資格情報を更新します。ドメイン Contoso の Active Directory コンピューター アカウント ServiceAc1 から資格情報を入手します。

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 

## 例 5

この例では、サーバー アレイのサイズが増加しているか、保守後にアレイのメンバーを再導入するためのいずれかにより、新しいコンピューターまたはサービスに戻すコンピューターに ASA を配布するためにスクリプトを使用する方法を示します。

クライアント アクセス サーバーがトラフィックを受け取る前に、ASA 資格情報を更新する必要があります。共有 ASA 資格情報を、既に適切に構成されているクライアント アクセス サーバーからコピーします。たとえば、現時点でサーバー A に有効な ASA 資格情報が存在し、そのアレイにたった今サーバー B を追加した場合、スクリプトを使用してサーバー A からサーバー B に資格情報 (パスワードを含む) をコピーすることができます。これは、サーバー B が停止している場合や、パスワードを最後に登録したときにサーバー B がまだアレイのメンバーでなかった場合に便利です。

    .\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose

