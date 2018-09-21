---
title: 'メールボックスの監査ログの出力: Exchange 2013 Help'
TOCTitle: メールボックスの監査ログの出力
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 49895308
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの監査ログの出力

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

メールボックスには機密情報、ビジネスへの影響が大きい (HBI) 情報、および個人情報 (PII) が含まれていることがあるため、組織内のメールボックスに誰がログオンしたか、およびどんな操作を行ったかを追跡することが重要です。メールボックスの所有者以外のユーザーによるメールボックスへのアクセスを追跡することが特に重要です。これらのユーザーは、*代理ユーザー*と呼ばれます。

*メールボックス監査ログ* を使用すると、メールボックスの所有者、代理人 (メールボックスへのフル アクセス許可を持つ管理者を含む)、および管理者によるメールボックスへのアクセスをログに記録できます。

メールボックスの監査ログを有効にする場合は、ログオンの種類 (管理者、代理ユーザー、または所有者) に応じてログに記録するユーザー操作 (メッセージへのアクセス、移動、削除など) を指定できます。監査ログ エントリには、メールボックスへのアクセスに使用されたクライアント IP アドレス、ホスト名、プロセスやクライアントなどの重要な情報も含まれています。移動されるアイテムの場合、エントリには移動先フォルダーの名前が含まれます。

## メールボックス監査ログ

メールボックス監査ログは、メールボックス監査ログが有効になっている各メールボックスに対して生成されます。ログ エントリは、監査対象メールボックスの \[回復可能なアイテム\] フォルダーの \[監査\] サブフォルダーに保存されます。これにより、メールボックスへのアクセスに使用されたクライアント アクセス方法、あるいは管理者がメールボックス監査ログへのアクセスに使用したサーバーまたはワークステーションとは無関係に、すべての監査ログ エントリが 1 つの場所から利用可能になります。メールボックスを別のメールボックス サーバーに移動した場合、そのメールボックスのメールボックス監査ログも移動されます。これは、監査ログがメールボックス内に配置されているためです。

既定では、メールボックス監査ログ エントリはメールボックスに 90 日間保存されてから、削除されます。この保存期間を変更するには、[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットで *AuditLogAgeLimit* パラメーターを使用します。メールボックスがインプレース保持または訴訟ホールドになっている場合、メールボックスの監査ログの保存期間が終わる時点までに限って、監査ログ エントリは保持されます。監査ログ エントリをさらに長く保存するには、*AuditLogAgeLimit* パラメーターの値を変更することで保存期間を長くする必要があります。また、保存期限に達する前に監査ログのエントリをエクスポートすることもできます。詳細については、次のトピックを参照してください。

  - [メールボックス監査ログをエクスポートする](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/export-mailbox-audit-logs)

  - [メールボックス監査ログの検索を作成する](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## メールボックス監査ログの有効化

メールボックス監査ログは、メールボックスごとに有効にします。メールボックス監査ログを有効または無効にするには、**Set-Mailbox** コマンドレットを使用します。詳細については、「[メールボックスのメールボックス監査ログを有効または無効にする](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)」を参照してください。

メールボックスのメールボックス監査ログを有効にすると、メールボックスへのアクセス、および特定の管理者と代理人の操作が既定で記録されます。メールボックスの所有者が実行した操作をログに記録するには、監査対象にする所有者の操作を指定する必要があります。

## メールボックス監査ログによって記録されるメールボックスの操作

次の表に、操作を記録できるログオンの種類を含め、メールボックス監査ログによって記録される操作を示します。


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
<th>操作</th>
<th>説明</th>
<th>管理者</th>
<th>代理人</th>
<th>所有者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>コピーする</p></td>
<td><p>アイテムが別のフォルダーにコピーされます。</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Create</p></td>
<td><p>アイテムが、メールボックスの予定表、連絡先、メモ、またはタスク フォルダーに作成されます。たとえば、新しい会議出席依頼が作成されます。なお、メッセージまたはフォルダーの作成は監査されません。</p></td>
<td><p>はい*</p></td>
<td><p>はい*</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>FolderBind</p></td>
<td><p>メールボックス フォルダーにアクセスされます。</p></td>
<td><p>はい*</p></td>
<td><p>はい**</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>HardDelete</p></td>
<td><p>アイテムが [回復可能なアイテム] フォルダーから完全に削除されます。</p></td>
<td><p>はい*</p></td>
<td><p>はい*</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>MessageBind</p></td>
<td><p>アイテムが閲覧ウィンドウでアクセスされるか、開かれます。</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>移動する</p></td>
<td><p>アイテムが別のフォルダーに移動されます。</p></td>
<td><p>はい*</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>MoveToDeletedItems</p></td>
<td><p>アイテムが [削除済みアイテム] フォルダーに移動されます。</p></td>
<td><p>はい*</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>SendAs</p></td>
<td><p>メッセージが &quot;送信者&quot; アクセス許可を使用して送信されます。</p></td>
<td><p>はい*</p></td>
<td><p>はい*</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>SendOnBehalf</p></td>
<td><p>メッセージが &quot;代理送信&quot; アクセス許可を使用して送信されます。</p></td>
<td><p>はい*</p></td>
<td><p>はい</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="even">
<td><p>SoftDelete</p></td>
<td><p>アイテムが [削除済みアイテム] フォルダーから削除されます。</p></td>
<td><p>はい*</p></td>
<td><p>はい*</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>更新する</p></td>
<td><p>アイテムのプロパティが更新されます。</p></td>
<td><p>はい*</p></td>
<td><p>はい*</p></td>
<td><p>はい</p></td>
</tr>
</tbody>
</table>


\* メールボックスの監査が有効になっている場合、既定で監査されます。

\*\* 代理人により実行されたフォルダー バインド操作のエントリは統合されます。24 時間の時間内の個々のフォルダー アクセスに対して 1 つのログ エントリが生成されます。

特定の種類のメールボックス操作を監査する必要がなくなった場合、これらの操作を無効にするように、メールボックスの監査ログ構成を変更する必要があります。既存のログ エントリは、監査ログ エントリの有効期限に達するまで削除されません。

## メールボックス監査ログ エントリの検索

次の方法を使用すると、メールボックス監査ログ エントリを検索できます。

  - **単一のメールボックスの同期的検索**   [Search-MailboxAuditLog](https://technet.microsoft.com/ja-jp/library/ff522360\(v=exchg.150\)) コマンドレットを使用すると、単一のメールボックスのメールボックス監査ログ エントリを同期的に検索できます。検索結果は、コマンドレットによって Exchange 管理シェル ウィンドウに表示されます。詳細については、「[メールボックスのメールボックス監査ログを検索する](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md)」を参照してください。

  - **1 つ以上のメールボックスの非同期的検索**   メールボックス監査ログ検索を作成して 1 つ以上のメールボックスのメールボックス監査ログを非同期に検索し、検索結果を指定された電子メール アドレスに送信できます。検索結果は、XML 添付ファイルとして送信されます。検索を作成するには、[New-MailboxAuditLogSearch](https://technet.microsoft.com/ja-jp/library/ff522362\(v=exchg.150\)) コマンドレットを使用します。詳細については、「[メールボックス監査ログの検索を作成する](create-a-mailbox-audit-log-search-exchange-2013-help.md)」を参照してください。

  - **Exchange 管理センター (EAC) の監査レポートを使用**   EAC の <strong>監査</strong> タブを使用して、所有者以外のメールボックス アクセスのレポートを実行したり、メールボックス監査ログからエントリをエクスポートしたりできます。詳細については、以下を参照してください。
    
      - [所有者以外のメールボックス アクセスのレポートの実行](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/non-owner-mailbox-access-report)
    
      - [メールボックス監査ログをエクスポートする](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/exchange-auditing-reports/export-mailbox-audit-logs)

## メールボックス監査ログ エントリ

次の表に、メールボックス監査ログ エントリに記録されるフィールドを示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド</th>
<th>入力内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>次のいずれかの操作。</p>
<ul>
<li><p>Copy</p></li>
<li><p>Create</p></li>
<li><p>FolderBind</p></li>
<li><p>HardDelete</p></li>
<li><p>MessageBind</p></li>
<li><p>Move</p></li>
<li><p>MoveToDeletedItems</p></li>
<li><p>SendAs</p></li>
<li><p>SendOnBehalf</p></li>
<li><p>SoftDelete</p></li>
<li><p>Update</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>次のいずれかの結果。</p>
<ul>
<li><p>Failed</p></li>
<li><p>PartiallySucceeded</p></li>
<li><p>Succeeded</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>操作を実行したユーザーのログオンの種類。ログオンの種類には次のものが含まれます。</p>
<ul>
<li><p>所有者</p></li>
<li><p>代理人</p></li>
<li><p>管理者</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>移動操作の宛先フォルダーの GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>移動操作の宛先フォルダーのパス。</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>フォルダーの GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>フォルダーのパス。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>操作を実行したクライアントまたは Exchange コンポーネントを識別する詳細情報。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>クライアント コンピューターの IP アドレス。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>クライアント コンピューター名。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>クライアント アプリケーションのプロセス名。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>クライアント アプリケーションのバージョン。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>操作を実行したユーザーのログオンの種類。ログオンの種類には次のものが含まれます。</p>
<ul>
<li><p>所有者</p></li>
<li><p>代理人</p></li>
<li><p>管理者</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>メールボックス所有者のユーザー プリンシパル名 (UPN)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>メールボックス所有者のセキュリティ識別子 (SID)。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>メールボックス間操作用に記録された宛先メールボックス所有者の UPN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>メールボックス間操作用に記録された宛先メールボックス所有者の SID。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>宛先メールボックス所有者の GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>記録される操作がメールボックス間操作 (メールボックス間でのメッセージのコピーや移動など) であるかどうかに関する情報。</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>ログオンしたユーザーの表示名。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>代理ユーザーの表示名。</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>ログオンしたユーザーの SID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>記録対象操作 (移動や削除など) が実行されるメールボックス アイテムの ItemID。多数のアイテム上で実行される操作の場合、このフィールドはアイテムの集合として返されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>ソース フォルダーの GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>アイテム ID。</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>アイテムの件名。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>メールボックスの GUID。</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p>メールボックス ユーザーの解決された名前 (形式は、<em>ドメイン</em>\<em>SamAccountName</em>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>操作が実行された時刻。</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>監査ログ エントリの ID。</p></td>
</tr>
</tbody>
</table>


## 詳細情報

  - **メールボックスに対する管理者アクセス**   以下のシナリオでは、管理者だけがメールボックスにアクセスすると見なしています。
    
      - [インプレース電子情報開示 (eDiscovery)](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery) をメールボックスの検索に使用する。
    
      - [New-MailboxExportRequest](https://technet.microsoft.com/ja-jp/library/ff607299\(v=exchg.150\)) コマンドレットを使用してメールボックスをエクスポートする。
    
      - [Microsoft Exchange Server MAPI エディター](https://go.microsoft.com/fwlink/p/?linkid=204086)を使用してメールボックスにアクセスする。

  - **メールボックス監査ログのバイパス**   サード パーティのツールで使用されるアカウントや、法令に基づく監視に使用されるアカウントなどの承認された自動プロセスによるメールボックスのアクセスは、大量のメールボックス監査ログ エントリを作成する可能性がある上、組織にとって意味がないものである可能性があります。このようなアカウントを構成して、メールボックス監査ログをバイパスするようにできます。詳細については、「[メールボックス監査ログからユーザー アカウントをバイパスする](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md)」を参照してください。

  - **メールボックス所有者による操作の記録**   より機密性の高い情報が含まれる可能性がある探索検索メールボックスなどのメールボックスでは、メッセージの削除などのメールボックス所有者の操作に対してメールボックス監査ログを有効にすることを検討してください。

メールボックス監査ログ

