---
title: '管理者監査ログ: Exchange 2013 Help'
TOCTitle: 管理者監査ログ
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50555747
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理者監査ログ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2018-03-05_

Microsoft Exchange Server 2013 では、管理者監査ログを使用して、ユーザーまたは管理者が組織において変更を行った際にログを記録することができます。変更のログを記録することによって、変更を行った担当者に対する変更の追跡、変更の詳細レコードによる変更ログの拡張、規制要件や証拠開示要求の遵守などが可能となります。

既定では、Exchange 2013 を新規にインストールすると、監査ログが有効になります。

**目次**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## 監査対象

Exchange 管理シェルで直接実行されるコマンドレットが監査されます。さらに、Exchange 管理センター (EAC) を使用して実行する操作もバックグラウンドでコマンドレットを実行するため、ログに記録されます。

コマンドレットでは、場所を実行している、監査コマンドレットは、コマンドレットの一覧と 1 つの監査では、またはパラメーターの監査リストには、そのコマンドレットの多くのパラメーター。Exchange組織内のオブジェクトを変更するのにはどのようなアクションが作成されたを表示する監査ログは、どのようなオブジェクトが表示されているのではなく。


> [!IMPORTANT]
> コマンドレットが管理監査ログ コマンドレット拡張エージェントを呼び出す前にエラーが発生した場合、コマンドレットはログ記録されない可能性があります。管理監査ログ エージェントが呼び出された後にエラーが発生した場合、コマンドレットは関連するエラーとともにログ記録されます。詳細については、後述する「Admin Audit Log Agent」を参照してください。<BR>Microsoft Exchange Server 2010 管理ツールを使用して行われた変更はログ記録されますが、Microsoft Exchange Server 2007 管理ツールを使用して行われた変更はログ記録されません。<BR>監査ログ構成への変更は、構成変更の実行時にシェルを開いたコンピューター上で 60 分ごとに更新されます。変更を直ちに適用するには、各コンピューター上でシェルを閉じてから再度開きます。<BR>コマンドは、実行してから監査ログの検索結果に表示されるまで、最大 15 分かかることがあります。そのため、監査ログのエントリをインデックス処理してから検索してください。管理者監査ログにコマンドが表示されない場合は、数分待機してから検索を再実行してください。



## 監査ログの構成

既定では、監査ログが有効な場合、ログ エントリが作成、コマンドレットが実行されるたびにします。実行されるすべてのコマンドレットを監査しない場合は、コマンドレットと興味のパラメーターのみを監査する監査のログを構成できます。**Set-AdminAuditLogConfig**コマンドレットでは、監査ログを構成します。次のセクションで参照されているパラメーターは、このコマンドレットで使用されます。


> [!IMPORTANT]
> 管理者監査ログの構成に対する変更は、<STRONG>Set-AdministratorAuditLog</STRONG> コマンドレットが監査対象のコマンドレット一覧に含まれているかどうか、および監査ログが有効か無効かにかかわらず、常にログ記録されます。



コマンドを実行すると、Exchange は使用されたコマンドレットを検査します。実行されたコマンドレットが、*AdminAuditLogConfigCmdlets* パラメーターが入力されているコマンドレットのいずれかと一致すると、Exchange は *AdminAuditLogConfigParameters* パラメーターに指定されているパラメーターを確認します。パラメーター一覧のパラメーターが 1 つ以上一致した場合は、*AdminAuditLogMailbox* パラメーターを使用して指定されたメールボックスで実行されたコマンドレットが Exchange により記録されます。以降のセクションでは、監査ログ構成に関する各側面の詳細を説明します。

監査ログ構成の管理の詳細については、「[管理者監査ログの管理](manage-administrator-audit-logging-exchange-2013-help.md)」を参照してください。

ページのトップへ

## コマンドレット

ログ対象とするコマンドレットとそのパラメーターの一覧を入力することにより、監査対象となるコマンドレットを制御できます。監査ログを構成するとき、すべてのコマンドレットを監査するように指定したり、*AdminAuditLogConfigCmdlets* パラメーターを使用して監査するコマンドレットを指定できます。**New-Mailbox** のような完全なコマンドレット名を入力できます。また、部分的なコマンドレット名を指定して、アスタリスク (`*`) などのワイルドカード文字でその名前を囲むことができます。たとえば、文字列 `Transport` を含むあらゆるコマンドレットをログ記録する場合、`*Transport*` の値を指定できます。同時に完全コマンドレット名と部分コマンドレット名との混合を使用することで、監査ログ構成をニーズに合わせることができます。

## パラメーター

ログ対象のコマンドレットを指定することに加え、それらのコマンドレットで特定パラメーターが使用された場合にのみ、コマンドレットをログ記録するように指定することもできます。*AdminAuditLogConfigParameters* パラメーターを使用して、ログの対象とするパラメーターを指定します。コマンドレットと同様、`Database` のような完全なパラメーター名、およびワイルドカード文字 (`*`) で囲んだ部分的なパラメーター名 (`*Address*` など)、またはそれらの組み合わせを指定できます。

## 監査ログ有効期限

既定では、監査ログはログ エントリを 90 日間保存するように構成されています。監査ログ エントリは 90 日後に削除されます。*AdminAuditLogAgeLimit*パラメーターを使用して、監査ログの有効期限を変更できます。監査ログ エントリを保存しておく日数、時間数、分数、秒数を指定できます。値を指定するには、`dd.hh:mm:ss` (各項の意味は以下を参照) の形式を使用します。

  - **dd**   監査ログ エントリを保持する日数

  - **hh**   監査ログ エントリを保持する時間数

  - **mm**   監査ログ エントリを保持する分数

  - **ss**   監査ログ エントリを保持する秒数

複数年を指定するには `dd` フィールドを使用する必要があります。たとえば、365 日は 1 年、730 日は 2 年であるため、913 日は 2 年 6 か月になります。監査ログの有効期限を 2 年 6 か月に設定するには、`913.00:00:00` という構文を使用します。


> [!NOTE]
> 監査ログの有効期限は、現在の有効期限よりも小さく指定できます。この場合、新たに指定した有効期限を超えている監査ログ エントリは削除されます。<BR>有効期限を 0 に設定すると、Exchange により監査ログのエントリがすべて削除されます。<BR>監査ログの有効期限を構成するためのアクセス許可は、十分に信頼できるユーザーのみに付与することをお勧めします。



## 詳細ログ

既定では、管理者監査ログには、コマンドレット名、コマンドレット パラメーター (と指定した値)、変更されたオブジェクト、コマンドレットを実行したユーザー、コマンドレットが実行された時間、およびコマンドレットが実行されたサーバーのみが記録されます。管理者監査ログでは、オブジェクトで変更されたプロパティは記録されません。監査ログに変更されたオブジェクトのプロパティを含める場合は、*LogLevel* パラメーターを `Verbose` に設定して詳細ログを有効にします。詳細ログを有効にすると、既定で記録される情報に加えて、オブジェクトで変更されたプロパティ (元の値と変更後の値を含む) が監査ログに追加されます。

## Test コマンドレット

動詞 **Test** で始まるコマンドレットは、既定ではログ記録されません。*TestCmdletLoggingEnabled* パラメーターを `$true` に設定することにより、**Test** コマンドレットをログ記録するように指定できます。Test コマンドレットのログ記録を有効にすることは可能ですが、短時間のみにとどめることをお勧めします。これは、Test コマンドレットにより大量の情報が生成されることがあるためです。

## 監査ログ

コマンドレットがログ記録されるたびに、監査ログ エントリが作成されます。監査ログは、非表示の専用の調停メールボックスに格納されます。このメールボックスにアクセスするには、EAC あるいは **Search-AdminAuditLog** コマンドレットまたは **New-AdminAuditLogSearch** コマンドレットを使用する必要があります。Microsoft Outlook Web App または Microsoft Outlook を使用して開くことはできません。以降のセクションでは、次の情報を提供します。

  - ログに含まれる内容

  - EAC の <strong>監査</strong> ページで使用可能なレポート

  - 監査ログ検索のコマンドレット

## 監査ログの内容

それぞれの監査ログ エントリには、次の表に記載されている情報が含まれます。監査ログには、1 つまたは複数の監査ログ エントリが含まれています。監査ログ エントリの数は、**Set-AdminAuditLogConfig** コマンドレットを使用して指定された監査ログ有効期限によって制御されます。有効期限を過ぎた監査ログ エントリは削除されます。

### 監査ログ エントリのフィールド

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>このフィールドは、Exchange によって内部で使用されます。</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>このフィールドには、<code>CmdletName</code> フィールドで指定されたコマンドレットにより変更されたオブジェクトが含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>このフィールドには、<code>Caller</code> フィールドのユーザーによって実行されたコマンドレットの名前が含まれます。</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>このフィールドには、<code>CmdletName</code> フィールドのコマンドレットが実行されたときに指定されたパラメーターが含まれます。パラメーターで指定された値があれば、それもこのフィールドに格納されます (既定の出力では表示されません)。このフィールドの追加情報にアクセスする方法の詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes">役割グループの変更または管理者監査ログを検索する</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>このフィールドには、<code>ObjectModified</code> フィールドのオブジェクトで変更されたプロパティが含まれます。プロパティの以前の値と格納された新しい値も、このフィールドに格納されます (既定の出力では表示されません)。このフィールドの追加情報にアクセスする方法の詳細については、「<a href="https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes">役割グループの変更または管理者監査ログを検索する</a>」を参照してください。</p>

> [!IMPORTANT]
> このフィールドは、<STRONG>Set-AdminAuditLogConfig</STRONG> コマンドレットで <EM>LogLevel</EM> パラメーターが <CODE>Verbose</CODE> に設定される場合にのみ読み込まれます。


</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>このフィールドには、<code>CmdletName</code> フィールドのコマンドレットを実行したユーザーのユーザー アカウントが含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>このフィールドは、<code>CmdletName</code>フィールドのコマンドレットが正常に実行されたかどうかを示します。値は、<code>True</code> または <code>False</code> のどちらかです。</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>このフィールドには、<code>CmdletName</code> フィールドのコマンドレットが正常に完了しなかった場合に生成されるエラー メッセージが含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>このフィールドには、<code>CmdletName</code> フィールドのコマンドレットが実行された日時が含まれます。日時は、世界協定時刻 (UTC) 形式で格納されます。</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>このフィールドは、<code>CmdletName</code> フィールドで指定されたコマンドレットが実行されたサーバーを示します。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>このフィールドは、Exchange によって内部で使用されます。</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>このフィールドは、Exchange によって内部で使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>このフィールドは、Exchange によって内部で使用されます。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## EAC 監査レポート

EAC の <strong>監査</strong> ページには、さまざまな種類の規制準拠および管理構成の変更についての情報を提供する、いくつかのレポートがあります。以下のレポートは、組織における構成の変更についての情報を提供します。

  - **管理者の役割グループ レポート**   このレポートでは、指定された期間内の指定した管理役割グループに対する変更を検索できます。返される結果には、変更された役割グループ、変更を行った担当者、日時、および変更の内容が含まれます。最大で 3,000 エントリまで返すことができます。検索の結果として 3,000 を超えるエントリが返される場合は、<strong>管理者監査ログ</strong> レポートまたは **Search-AdminAuditLog** コマンドレットを使用します。

  - **管理者監査ログ**   このレポートでは、指定された期間内に記録された監査ログ エントリを XML ファイルにエクスポートし、ファイルを指定した受信者に電子メールで送信できます。XML ファイルの内容の詳細については、「[管理者監査ログの構造](administrator-audit-log-structure-exchange-2013-help.md)」を参照してください。

これらのレポートを使用する方法については、「[役割グループの変更または管理者監査ログを検索する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes)」を参照してください。

<strong>監査</strong> ページに含まれるその他のレポートについては、「[Exchange 監査レポート](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports)」を参照してください。

## Search-AdminAuditLog コマンドレット

**Search-AdminAuditLog** コマンドレットを実行すると、指定した検索条件に一致する監査ログ エントリがすべて返されます。以下の検索条件を指定できます。

  - **コマンドレット**   管理者監査ログで検索するコマンドレットを指定します。

  - **パラメーター**   管理者監査ログで検索するパラメーターをコンマで区切って指定します。検索するコマンドレットを指定した場合のみ、パラメーターを検索できます。

  - **終了日**   管理者監査ログの結果の範囲を、指定の日付以前に発生したログ エントリに限定します。

  - **開始日**   管理者監査ログの結果の範囲を、指定の日付以後に発生したログ エントリに限定します。

  - **オブジェクト ID**   指定された変更済みオブジェクトを含む管理者監査ログ エントリのみを返すように指定します。

  - **ユーザー ID**   コマンドレットを実行したユーザーの指定された ID を含む管理者監査ログ エントリのみを返すように指定します。

  - **正常完了**   成功または失敗を示した管理者監査ログ エントリのみを返すかどうかを指定します。

それぞれの監査ログ エントリには、「Audit Log Contents」の表に記載されている情報が含まれます。既定では、指定した条件に一致するログ エントリのうち、最初の 1,000 エントリのみが返されます。しかし、*ResultSize* パラメーターを使用してこの既定値を変更し、より多くのエントリまたはより少ないエントリを返すようにすることも可能です。`Unlimited` の値を *ResultSize* パラメーターと共に指定し、指定した条件に一致するログ エントリをすべて返すことができます。

**Search-AdminAuditLog** コマンドレットを使用する方法については、「[役割グループの変更または管理者監査ログを検索する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes)」を参照してください。

## New-AdminAuditLogSearch コマンドレット

**New-AdminAuditLogSearch** コマンドレットは、**Search-AdminAuditLog** コマンドレットと同様に、監査ログを検索します。しかし、監査ログの検索結果をシェルに表示する代わりに、**New-AdminAuditLogSearch** コマンドレットでは、検索を実行してその結果を指定した受信者に電子メール メッセージで送信します。結果は、電子メール メッセージに XML 添付ファイルとして含まれます。

**Search-AdminAuditLog** コマンドレットで使用した検索条件と同じ条件を **New-AdminAuditLogSearch** コマンドレットで使用できます。検索条件の一覧については、「Search-AdminAuditLog Cmdlet」を参照してください。

**New-AdminAuditLogSearch** コマンドレットの実行後に、Exchange から指定された送信者にレポートが配信されるまで、最大で 15 分かかる場合があります。XML ファイルとして添付されたレポートは、最大で 10 MB になることがあります。この XML ファイルには、「Audit Log Contents」の表に記載された情報と同じものが含まれます。XML ファイルの構造の詳細については、「[管理者監査ログの構造](administrator-audit-log-structure-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Outlook Web App では、既定では XML の添付ファイルを開くことができません。Outlook Web App を使用して XML 添付ファイルを表示できるように Exchange を構成するか、Microsoft Outlook など別のメール クライアントを使用して添付ファイルを表示することができます。XML 添付ファイルを表示できるように Outlook Web App を構成する方法については、「<A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Outlook Web App 仮想ディレクトリの表示や構成</A>」をご覧ください。



**New-AdminAuditLogSearch** コマンドレットを使用する方法については、「[役割グループの変更または管理者監査ログを検索する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes)」を参照してください。

ページのトップへ

## 手動による監査ログ エントリ

Exchange コマンドレットの実行時のログ記録に加えて、Exchange 2013 では、手動で監査ログにログ エントリを書き込むことができます。Exchange 2013 では **Write-AdminAuditLog** コマンドレットを使用してこれを実行できます。手動でログ エントリを追加する必要が生じる状況は以下のとおりです。

  - カスタム スクリプトの開始と終了

  - 制御情報の変更

  - メンテナンスの開始時刻および終了時刻

**Write-AdminAuditLog** コマンドレットでは、*Comment* パラメーターを使用して、監査ログに含めるテキスト文字列を指定します。*Comment* パラメーターは、最大 500 文字までの英数字を指定できます。手動による監査ログ エントリとコメント文字列には、Exchange コマンドレットのログ記録時にキャプチャされた情報と同じ情報がすべて含まれています。監査ログに含まれる各フィールドの説明については、「Audit Log Contents」のテーブルを参照してください。

手動による監査ログ エントリは、EAC の <strong>監査</strong> ページ、**Search-AdminAuditLog** コマンドレットまたは **New-AdminAuditLogSearch** コマンドレットを使用して、他のログ エントリと同様の方法で取得できます。

手動による監査ログエントリで、**Write-AdminAuditLog** コマンドレットの *Comment* パラメーターの内容を確認するには、「[役割グループの変更または管理者監査ログを検索する](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/search-role-group-changes)」を参照してください。

## Active Directory のレプリケーション

管理者の監査ログは、Active Directory レプリケーションに依存して、組織内のドメイン コントローラーに指定する構成設定をレプリケートします。レプリケーション設定によっては、加えた変更が組織内の Exchange 2013 または Exchange 2010 を実行するすべてのサーバーに直ちに適用されない場合もあります。

## 管理監査ログ エージェント

管理監査ログ ビルトイン拡張エージェントは、Exchange 2013 内でコマンドレット操作の管理者監査ログを実行します。このエージェントは監査ログ構成を読み取り、組織内で実行される各コマンドレットの評価を実行します。監査ログ構成で指定した条件が実行中のコマンドレットと一致する場合は、エージェントにより監査ログが生成されます。

管理監査ログ エージェントは既定で有効 (監査ログが機能するのに必要な状態) となっています。これを無効にすることはできません。また、その優先度は変更できません。コマンドレット拡張エージェントの詳細については、「[コマンドレット拡張エージェント](cmdlet-extension-agents-exchange-2013-help.md)」を参照してください。

