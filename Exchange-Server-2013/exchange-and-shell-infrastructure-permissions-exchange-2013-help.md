---
title: 'Exchange およびシェル インフラストラクチャのアクセス許可: Exchange 2013 Help'
TOCTitle: Exchange およびシェル インフラストラクチャのアクセス許可
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 48269361
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange およびシェル インフラストラクチャのアクセス許可

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

Microsoft Exchange Server 2013 の各種コンポーネントの構成作業を実行するために必要なアクセス許可は、実行している処理または実行するコマンドレットによって異なります。各機能の詳細については、このトピックの各セクションを参照してください。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]  
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。


> [!NOTE]  
> 一部の機能では、管理するサーバーのローカル管理者アクセス許可を持っている必要がある場合があります。これらの機能を管理するには、このサーバーでローカルの Administrators グループのメンバーである必要があります。



## Exchange インフラストラクチャのアクセス許可

次の表は、一般的な Exchange 2013 設定を構成する作業の実行に必要なアクセス許可を示します。

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
<td><p>管理者監査ログ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange管理センターの構成設定</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 管理センターの接続</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange サーバーの構成設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ヘルプ設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>メッセージのカテゴリ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">Help Desk (ヘルプ デスク)</a></p></td>
</tr>
<tr class="odd">
<td><p>プロダクト キー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>システム状態のテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>表示専用の管理者監査ログ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p>

> [!NOTE]  
> "View-Only Audit Logs/表示専用監査ログ" 管理役割を手動で管理役割グループに割り当てることもできます。詳細については、「<A href="view-only-audit-logs-role-exchange-2013-help.md">"View-Only Audit Logs/表示専用監査ログ" 役割</A>」を参照してください。


</td>
</tr>
<tr class="even">
<td><p>監査ログへの書き込み</p></td>
<td><p>任意の役割グループのメンバーであるユーザーまたは任意の管理役割が割り当てられているユーザーは、管理者監査ログに書き込むことができます。</p></td>
</tr>
</tbody>
</table>


## シェル インフラストラクチャのアクセス許可

次の表は、Exchange シェルの実行方法を制御する機能を構成する作業の実行に必要なアクセス許可を示します。

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
<td><p>Active Directory ドメイン サービス サーバーの設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>コマンドレット拡張エージェント</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>PowerShell 仮想ディレクトリ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>PowerShell および WinRM のインストール</p></td>
<td><p>ローカル サーバー管理者</p></td>
</tr>
<tr class="odd">
<td><p>リモート シェル</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


## フェデレーションと証明書のアクセス許可

次の表は、フェデレーションの信頼、OAuth 構成、証明書管理、ハイブリッド展開構成に関連するタスクの実行に必要なアクセス許可を示します。

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
<td><p>証明書管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>フェデレーションの信頼、OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>フェデレーションの信頼のテスト、OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>ハイブリッド展開構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>組織内のコネクタ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="records-management-exchange-2013-help.md">レコードの管理</a></p></td>
</tr>
</tbody>
</table>

