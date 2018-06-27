---
title: 'クライアントおよびモバイル デバイスのアクセス許可: Exchange 2013 Help'
TOCTitle: クライアントおよびモバイル デバイスのアクセス許可
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 48269524
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアントおよびモバイル デバイスのアクセス許可

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-11-10_

クライアントとモバイル デバイスのタスクの実行に必要なアクセス許可は、実行する手順、またはユーザーが実行するコマンドレットによって異なります。クライアントとモバイル デバイスの機能の詳細については、「[クライアントとモバイル](clients-and-mobile-exchange-2013-help.md)」を参照してください。

手順の実行またはコマンドレットの実行に必要なアクセス許可を確認するには、次の手順を実行します。

1.  以下の表で、実行する手順またはコマンドレットに最も関係する機能を見つけます。

2.  次に、その機能に必要なアクセス許可を確認します。それらの役割グループのいずれか、同等のカスタム役割グループ、または同等の管理役割が割り当てられている必要があります。役割グループをクリックして、その管理役割を確認することもできます。機能が複数の役割グループを示している場合、その機能を使用する役割グループを 1 つだけが割り当てる必要があります。役割グループと管理役割について詳しくは、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」をご覧ください。

3.  ここで、**Get-ManagementRoleAssignment** コマンドレットを実行して、ユーザーに割り当てられている役割グループまたは管理役割を調べ、その機能の管理に必要なアクセス許可があるかどうかを確認します。
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するには、"Role Management/役割管理" 管理役割が割り当てられている必要があります。<STRONG>Get-ManagementRoleAssignment</STRONG> コマンドレットを実行するアクセス許可がない場合は、Exchange 管理者に連絡して、自分に割り当てられている役割グループまたは管理役割を取得してください。



機能の管理能力を別のユーザーに委任する場合は、「[役割割り当てを委任する](delegate-role-assignments-exchange-2013-help.md)」をご覧ください。


> [!NOTE]
> 一部の機能では、管理するサーバーのローカル管理者アクセス許可を持っている必要がある場合があります。これらの機能を管理するには、このサーバーでローカルの Administrators グループのメンバーである必要があります。



## クライアント アクセス サーバーのアクセス許可

クライアント アクセス サーバーには次の機能のいずれかを構成できます。

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
<td><p>クライアント アクセス サーバーのアレイ設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>クライアント アクセス サーバーの設定</p></td>
<td><p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>クライアント アクセス サービスの電子メール チャネル設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>クライアント アクセス ユーザー設定</p></td>
<td><p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>クライアント アクセス仮想ディレクトリの設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>RPC クライアント アクセス設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>プッシュ通知プロキシ設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>OAuth 認証のリダイレクトの設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange ActiveSync のアクセス許可

Exchange ActiveSync には次のいずれかを構成できます。

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
<td><p>Exchange ActiveSync Autoblock の設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync のメールボックス ポリシー設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync のサーバー設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync の設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync のユーザー設定</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync の仮想ディレクトリ設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>モバイル デバイスのメールボックス ポリシーの設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>モバイル デバイスのユーザー設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
</tbody>
</table>


## 自動検出のアクセス許可

自動検出サービスには次を構成できます。

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
<td><p>自動検出サービスの構成設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委任されたセットアップ</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>自動検出の仮想ディレクトリ設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
</tbody>
</table>


## 空き時間情報サービスのアクセス許可

空き時間情報サービスには次を構成できます。

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
<td><p>空き時間情報サービスのアドレス スペース設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>空き時間情報サービスの構成設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
</tbody>
</table>


## クライアント調整のアクセス許可

クライアント調整には次を構成できます。

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
<td><p>クライアント調整の設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
</tbody>
</table>


## Exchange Web サービスのアクセス許可

Web サービスの仮想ディレクトリには次を構成できます。

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
<td><p>Exchange Web サービスの仮想ディレクトリ設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange Web サービスのテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web サービスのテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


## Outlook Anywhere のアクセス許可

Outlook Anywhere の次の設定を構成および管理できます。

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
<td><p>Outlook Anywhere の構成 (有効化、無効化、変更、表示)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委任されたセットアップ</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
<tr class="even">
<td><p>RPC over HTTP プロキシ コンポーネント</p></td>
<td><p>ローカル サーバー管理者</p></td>
</tr>
<tr class="odd">
<td><p>Outlook Anywhere の接続テスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
</tbody>
</table>


## Outlook Web App のアクセス許可

Outlook Web App の設定の表示、セキュリティおよび Outlook Web App へのユーザー アクセスの制御、Outlook Web App の接続テストには、次の機能を使用できます。

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
<td><p>グラフィックス エディター</p></td>
<td><p>ローカル サーバー管理者</p></td>
</tr>
<tr class="even">
<td><p>IIS マネージャー</p></td>
<td><p>ローカル サーバー管理者</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>ISA Server エンタープライズ管理者</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App メールボックス ポリシー</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App の仮想ディレクトリ</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p></td>
</tr>
<tr class="even">
<td><p>レジストリ エディター</p></td>
<td><p>ローカル サーバー管理者</p></td>
</tr>
<tr class="odd">
<td><p>S/MIME の構成</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>テキスト エディター</p></td>
<td><p>ローカル サーバー管理者</p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App のメールボックス ポリシーの表示</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">委任されたセットアップ</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">検疫管理</a></p></td>
</tr>
</tbody>
</table>


## POP3 および IMAP4 のアクセス許可

POP3 と IMAP4 には次を構成できます。

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
<td><p>IMAP4 の設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>POP3 の設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="odd">
<td><p>IMAP4 設定のテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
<tr class="even">
<td><p>POP3 設定のテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="server-management-exchange-2013-help.md">サーバー管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a></p></td>
</tr>
</tbody>
</table>


## Windows PowerShell 仮想ディレクトリのアクセス許可

Windows PowerShell には次を構成できます。

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
<td><p>Windows PowerShell のテスト</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
<tr class="even">
<td><p>Windows PowerShell の設定</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


## テキスト メッセージの送受信のアクセス許可

テキスト メッセージの送受信には次を構成できます。

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
<td><p>テキスト メッセージの送受信の通知設定</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p>テキスト メッセージの送受信の設定</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="odd">
<td><p>テキスト メッセージの送受信のユーザー設定</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 役割</a></p>
<p>ユーザーは、ユーザー自身のメールボックスのテキスト メッセージング設定を構成することができます。管理者は、別のユーザーのメールボックスのテキスト メッセージング設定を構成することができません。</p></td>
</tr>
</tbody>
</table>

