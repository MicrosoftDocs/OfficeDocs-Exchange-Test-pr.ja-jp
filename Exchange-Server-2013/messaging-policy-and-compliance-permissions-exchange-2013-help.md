---
title: 'メッセージング ポリシーとコンプライアンスのアクセス許可: Exchange 2013 Help'
TOCTitle: メッセージング ポリシーとコンプライアンスのアクセス許可
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 48270208
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージング ポリシーとコンプライアンスのアクセス許可

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

メッセージングのポリシーと準拠を構成するのに必要なアクセス許可は、実行する手順、または実行するコマンドレットによって異なります。メッセージング ポリシーと準拠の詳細については、「[メッセージングのポリシーと準拠](messaging-policy-and-compliance-exchange-2013-help.md)」 を参照してください。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]  
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。


> [!NOTE]  
> 管理する機能の一部がエッジ トランスポート サーバー上にある場合があります。エッジ トランスポート サーバー上で機能を管理するには、管理するエッジ トランスポート サーバー上でローカルの Administrators グループのメンバーになる必要があります。エッジ トランスポート サーバーは、役割ベースのアクセス制御 (RBAC) を使用しません。エッジ トランスポート サーバー上で管理できる機能については、以下の表の [必要なアクセス許可] 列にエッジ トランスポートのローカル管理者と記載されています。



## メッセージング ポリシーとコンプライアンスのアクセス許可

次の表の機能を使用すると、メッセージング ポリシーと準拠の機能を構成できます。各機能を構成するために必要な役割グループの一覧が表示されています。

"View-Only Management/管理 (参照のみ可)" 役割グループが割り当てられているユーザーは、次の表の機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>必要なアクセス許可</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>データ損失防止 (DLP)</p></td>
<td><p>Office 365 を使用する場合:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 グローバル管理者</a>。この場合、Exchange の<a href="organization-management-exchange-2013-help.md">組織の管理</a>が自動的に含まれます。</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 サービス管理者</a>と、Exchange の<a href="organization-management-exchange-2013-help.md">組織の管理</a> 管理役割グループ。</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 パスワード管理者</a></p></li>
</ul>
<p>Exchange Server 2013 または Exchange Online のみを使用する場合:</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">コンプライアンス管理</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>メールボックス内容の削除 (<em>DeleteContent</em> スイッチを指定して <a href="https://technet.microsoft.com/ja-jp/library/dd298173(v=exchg.150)">Search-Mailbox</a> コマンドレットを使用)</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">検出の管理</a> <strong>および</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">&quot;Mailbox Import Export/メールボックスのインポートとエクスポート&quot; 役割</a></p>

> [!NOTE]  
> 既定では、"Mailbox Import Export/メールボックスのインポートとエクスポート" 役割は、どの役割グループにも割り当てられていません。管理の役割は、組み込みまたはカスタムの役割グループ、ユーザー、またはユニバーサル セキュリティ グループに割り当てることができます。役割を役割グループに割り当てることをお勧めします。詳細については、「<A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">ユーザーまたは USG に役割を追加する</A>」を参照してください。


</td>
</tr>
<tr class="odd">
<td><p>探索メールボックス - 作成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>ジャーナル</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メールボックス監査ログ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="even">
<td><p>メッセージ分類</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メッセージング レコード管理</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">コンプライアンス管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="even">
<td><p>インプレース電子情報開示 (eDiscovery)</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">検出の管理</a></p>

> [!NOTE]  
> 既定では、"Discovery Management/検出の管理" 役割グループにはメンバーが存在しません。管理者を含むユーザーには、メールボックスを検索するのに必要なアクセス許可がありません。詳細については、「<A href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Exchange の電子情報開示のアクセス許可を割り当てる</A>」を参照してください。


</td>
</tr>
<tr class="odd">
<td><p>インプレース保持</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">検出の管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>

> [!IMPORTANT]  
> クエリベースのインプレース保持を作成するには、ユーザーにメールボックス検索役割および訴訟ホールド役割が直接割り当てられているか、または両方の役割が割り当てられている役割グループのメンバーシップを通じて割り当てられている必要があります。すべてのメールボックス アイテムを保持するインプレース保持をクエリを使用しないで作成するには、ユーザーに訴訟ホールド役割が割り当てられている必要があります。探索管理役割グループには、両方の役割が割り当てられます。<BR>Organization Management 役割グループには、訴訟ホールド役割が割り当てられます。Organization Management 役割グループのメンバーは、メールボックス内のすべてのアイテムにインプレース保持を配置できますが、クエリベースのインプレース保持は作成できません。


</td>
</tr>
<tr class="even">
<td><p>インプレース アーカイブ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>インプレース アーカイブ - テスト接続</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>Information Rights Management (IRM) 構成</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">コンプライアンス管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>保持ポリシー – 適用</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="even">
<td><p>保持ポリシー - 作成</p></td>
<td><p>メッセージング レコード管理のエントリを表示する</p></td>
</tr>
<tr class="odd">
<td><p>トランスポート ルール</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
</tbody>
</table>

