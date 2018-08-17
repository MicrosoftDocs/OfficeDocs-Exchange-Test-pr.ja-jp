---
title: '受信者のアクセス許可: Exchange 2013 Help'
TOCTitle: 受信者のアクセス許可
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 48269543
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信者のアクセス許可

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

受信者を管理するタスクの実行に必要なアクセス許可は、実行する手順、または実行するコマンドレットによって異なります。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]  
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。

## メールボックス サーバーのアクセス許可

"View-Only Management (閲覧限定の管理)" 役割グループが割り当てられているユーザーは、次の表にある機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


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
<td><p>予定表の修復、サーバーの構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックス サーバーの委任</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>電子メール アドレス ポリシー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange Search</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Search – 診断</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p>&quot;Support Diagnostics/サポート診断&quot; 役割</p>

> [!NOTE]  
> "Support Diagnostics/サポート診断" 役割は、役割グループに割り当てられていません。詳細については、「<A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">ユーザーまたは USG に役割を追加する</A>」を参照してください。


</td>
</tr>
<tr class="even">
<td><p>グループ測定値</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>インポート エクスポート</p></td>
<td><p>&quot;Mailbox Import Export/メールボックスのインポートとエクスポート&quot; 役割</p>

> [!NOTE]  
> "Mailbox Import Export/メールボックスのインポートとエクスポート" 役割は、役割グループに割り当てられていません。詳細については、「<A href="mailbox-import-export-role-exchange-2013-help.md">"Mailbox Import Export/メールボックスのインポートとエクスポート" 役割</A>」を参照してください。


</td>
</tr>
<tr class="even">
<td><p>メールボックス アシスタント</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メールボックスの移動</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックスの回復</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メールボックスの修復要求</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックスの復元要求</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メールボックス サーバーの構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックス サーバーの Exchange Search Indexer サービスの管理</p></td>
<td><p>メールボックス サーバーのローカル管理者</p></td>
</tr>
<tr class="odd">
<td><p>MAPI 接続</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>OAB 仮想ディレクトリ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>ストアのメールボックスの削除</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
</tbody>
</table>


## 予定表と共有のアクセス許可

"View-Only Management (閲覧限定の管理)" 役割グループが割り当てられているユーザーは、次の表にある機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


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
<td><p>予定表の構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="even">
<td><p>予定表の診断</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p>
<p><a href="compliance-management-exchange-2013-help.md">コンプライアンス管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="odd">
<td><p>予定表の処理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="even">
<td><p>通知</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>組織の関係</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>共有ポリシー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


## リソース メールボックス構成のアクセス許可

"View-Only Management (閲覧限定の管理)" 役割グループが割り当てられているユーザーは、次の表にある機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


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
<td><p>予約ポリシー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="even">
<td><p>委任</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>リソース メールボックスのスキーマの構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


## メールボックス データベースのアクセス許可

"View-Only Management (閲覧限定の管理)" 役割グループが割り当てられているユーザーは、次の表にある機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


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
<td><p>メールボックス データベース</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
</tbody>
</table>


## 受信者プロビジョニングのアクセス許可

この表には、受信者を管理するために必要なさまざまなアクセス許可が含まれています。

"View-Only Management (閲覧限定の管理)" 役割グループが割り当てられているユーザーは、次の表にある機能の構成を表示できます。詳細については、「[表示限定の組織管理](view-only-organization-management-exchange-2013-help.md)」を参照してください。


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
<td><p>アドレス一覧、GAL</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>スパム対策</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook 用アプリ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="even">
<td><p>共有ポリシーの適用</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>調停</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>アーカイブ接続</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>オフライン アドレス帳の割り当て</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>自動応答</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="odd">
<td><p>予定表の構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>予定表の修復</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>連絡先集計の設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>未接続のメールボックス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="odd">
<td><p>配布グループ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>動的配布グループ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>電子メール アドレス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>受信トレイ ルール</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="odd">
<td><p>メール連絡先</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールのヒント</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>メール ユーザー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックス フォルダーのアクセス許可</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="odd">
<td><p>メールボックス フォルダー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>MAPI 接続</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>メッセージの構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="even">
<td><p>メッセージのクォータ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>モデレート</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>アクセス許可と委任</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>アーカイブ メールボックス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>受信者データのプロパティ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>リモート メールボックス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>保存期間および法的情報保留</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="odd">
<td><p>送信者</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>スペル チェックの構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="odd">
<td><p>ユニファイド メッセージング</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>ユーザー メールボックス</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>ユーザーの写真</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
</tbody>
</table>


## メールボックスの移動と移行のアクセス許可

この表には、社内メールボックスを別のドメインまたはフォレストに移動したり、クラウドベース組織との間で社内メールボックスを移行したりするために必要なアクセス許可を記載しています。


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
<td><p>メールボックスの移動 (ローカルまたはフォレスト間)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>メールボックスの移動 (ハイブリッド展開)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>移行 (クラウドからのオンボードとオフボード)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
</tbody>
</table>

