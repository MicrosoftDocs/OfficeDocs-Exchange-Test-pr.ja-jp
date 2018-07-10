---
title: 'メール フローのアクセス許可: Exchange 2013 Help'
TOCTitle: メール フローのアクセス許可
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 48270260
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール フローのアクセス許可

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

メール フローに関連するタスクの実行に必要なアクセス許可は、実行する手順、または実行するコマンドレットによって異なります。トランスポート機能の詳細については、「[メール フロー](mail-flow-exchange-2013-help.md)」 を参照してください。

このトピックでは、Microsoft Exchange Server 2013 のメール フロー機能を管理するために必要なアクセス許可を示します。Office 365 のアクセス許可と Exchange のアクセス許可の関連についての詳細は、「[Office 365 の権限](https://go.microsoft.com/fwlink/p/?linkid=335814)」を参照してください。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。


> [!NOTE]
> 管理する機能の一部がエッジ トランスポート サーバー上にある場合があります。エッジ トランスポート サーバー上で機能を管理するには、管理するエッジ トランスポート サーバー上でローカルの Administrators グループのメンバーになる必要があります。エッジ トランスポート サーバーは、役割ベースのアクセス制御 (RBAC) を使用しません。エッジ トランスポート サーバー上で管理できる機能については、以下の表の [必要なアクセス許可] 列にエッジ トランスポートのローカル管理者と記載されています。




> [!NOTE]
> 一部の機能では、管理するサーバーのローカル管理者アクセス許可を持っている必要がある場合があります。これらの機能を管理するには、このサーバーでローカルの Administrators グループのメンバーである必要があります。



## メール フローのアクセス許可

クライアント アクセスサーバーのフロント エンド トランスポート サービス、メールボックス サーバーのトランスポート サービス、メールボックス サーバーのメールボックス トランスポート サービス、およびエッジ トランスポート サーバーで、メール フロー設定を構成するために、次の表の機能を使用できます。各機能を構成するために必要なアクセス許可の一覧を示します。

"View-Only Management/管理 (参照のみ可)" 役割グループが割り当てられているユーザーは、次の表の機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。

**メールボックス サーバーおよびクライアント アクセス サーバー**


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
<td><p>承認済みドメイン</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>Active Directory サイトおよびサイト リンクの管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>スパム対策機能</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>スパム対策の更新</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>証明書管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>配信エージェント コネクタ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>DSN</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>外部コネクタ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>フロント エンド トランスポート サービス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>ジャーナル</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックス アクセス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メールボックスの迷惑メールの構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックス トランスポート サービス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メール ヒント</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>メッセージ分類</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メッセージ追跡</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>モデレート トランスポート</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>キュー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>受信コネクタ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="odd">
<td><p>リモート ドメイン</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>セーフ リスト集約機能</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="odd">
<td><p>送信コネクタ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>シャドウ冗長</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メール フローのテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>トランスポート ルール処理のテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>トランスポート エージェント</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="even">
<td><p>トランスポート構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>トランスポート ログ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>トランスポート ルール</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Transport サービス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>X.400 ドメイン</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


**エッジ トランスポート サーバー**


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
<td><p>承認済みドメイン - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="even">
<td><p>アドレスの書き換え - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="odd">
<td><p>エッジ トランスポート サーバー</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="odd">
<td><p>キュー - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="even">
<td><p>受信コネクタ - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="odd">
<td><p>送信コネクタ - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="even">
<td><p>トランスポート構成 - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="odd">
<td><p>トランスポート ログ - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
<tr class="even">
<td><p>トランスポート ルール - エッジ トランスポート</p></td>
<td><p>エッジ トランスポートのローカル管理者</p></td>
</tr>
</tbody>
</table>

