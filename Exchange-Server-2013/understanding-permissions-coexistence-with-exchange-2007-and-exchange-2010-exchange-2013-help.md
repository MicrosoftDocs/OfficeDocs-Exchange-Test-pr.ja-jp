---
title: 'Exchange 2007 と Exchange 2010 のアクセス許可の共存について: Exchange 2013 Help'
TOCTitle: Exchange 2007 と Exchange 2010 のアクセス許可の共存について
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54915166
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2007 と Exchange 2010 のアクセス許可の共存について

 

_**適用先:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

Microsoft Exchange Server 2013 を既存の Microsoft Exchange Server 2010 組織または Microsoft Exchange Server 2007 組織にインストールする場合は、新しい組織でアクセス許可がどのように機能するかを理解しておく必要があります。自分の組織に該当するセクションをお読みください。

  - 既存の Exchange 2010 組織への Exchange 2013 のインストール

  - 既存の Exchange 2010 組織への Exchange 2007 のインストール

## 既存の Exchange 2010 組織への Exchange 2013 のインストール

Exchange 2013 では、Exchange 2010 で使用されているものと同じ役割ベースのアクセス制御 (RBAC) のアクセス許可モデルが使用されます。Exchange 2013 を既存の Exchange 2010 組織にインストールすると、同じ管理役割グループ、管理役割、および管理スコープが Exchange 2013 と Exchange 2010 の両方のサーバーと受信者に適用されます。役割グループのメンバーまたは役割に割り当てられたユーザーは、その役割グループまたは役割のスコープに含まれるすべての Exchange 2013 または Exchange 2013 のサーバーまたは受信者を管理できます。組織内でスコープを使用せず、既存の役割グループのメンバーが Exchange 2010 と Exchange 2013 のサーバーと受信者を管理できるようにする場合は、他に何もする必要がありません。このような管理者は、組織に追加された Exchange 2013 のサーバーと受信者を管理できます。Exchange 2010 と Exchange 2013 におけるアクセス許可の機能を確認するには、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

新しい組織で、Exchange 2010 と Exchange 2013 のサーバーと受信者の管理を別々に行います。Exchange 2010 のサーバーと受信者の管理を担当する管理者のグループは Exchange 2013 のサーバーと受信者を管理することができず、その逆も同じです。この場合は、管理スコープを使用して、管理者のグループごとに管理を許可するサーバーと受信者を定義できます。必要なスコープを作成したら、既存の役割グループをコピーして、それぞれのメンバーである管理者を追加し、それらの役割グループにスコープを追加できます。そうすれば、各役割グループのメンバーはそれぞれのスコープと一致するサーバーと受信者しか管理できなくなります。

役割グループ、スコープ、役割グループのコピー、および役割グループへのスコープの追加に関する詳細については、次のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

## 既存の Exchange 2010 組織への Exchange 2007 のインストール

Exchange 2013 には、Microsoft Exchange Server 2007 で使用されていた Active Directory アクセス制御エントリ (ACE) ベースの承認モデルに代わる役割ベースのアクセス制御 (RBAC) アクセス許可が含まれています。RBAC は、Exchange 2013 の管理のほとんどで使用される承認機構です。この機構には、以下の管理領域が含まれます。

  - Exchange 管理シェル

  - Exchange 管理センター (EAC)

  - Exchange Web サービス

Exchange 2013 と Exchange 2007 の共存を計画する方法については、「[Exchange 2007 から Exchange 2013 へのアップグレード](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)」を参照してください。

アクセス許可に関連する管理タスクについては、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## Exchange 2013 アクセス許可

Exchange 2013 RBAC アクセス許可モデルは、いくつかの管理役割の 1 つを割り当てられた管理役割グループから成ります。管理役割には、管理者が Exchange 組織内でタスクを実行できるアクセス許可が含まれています。管理者は役割グループのメンバーとして追加され、その役割が提供するすべてのアクセス許可が与えられます。次の表は、役割グループ、役割グループに割り当てられる役割の一部、および役割グループのメンバーとなる可能性のあるユーザーの種類についての説明の一例です。

### Exchange 2013 の役割グループと役割の例

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割グループ</th>
<th>管理役割</th>
<th>この役割グループのメンバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織の管理</p></td>
<td><p>この役割グループに割り当てられる役割は次のとおりです。</p>
<ul>
<li><p>&quot;Address Lists/アドレス一覧&quot;</p></li>
<li><p>Exchange Servers</p></li>
<li><p>&quot;Journaling/ジャーナリング&quot;</p></li>
<li><p>Mail Recipients</p></li>
<li><p>&quot;Public Folders/パブリック フォルダー&quot;</p></li>
</ul></td>
<td><p>Exchange 2013 組織全体を管理するユーザーは、この役割グループのメンバーとなる必要があります。一部の例外を除き、この役割グループのメンバーは Exchange 2013 組織のほぼ全部を管理することができます。</p>
<p>既定では、Active Directory の Exchange 2013 の準備に使用するユーザー アカウントは、この役割グループのメンバーです。</p>
<p>この役割グループの詳細と、この役割グループに割り当てられる役割の完全な一覧については、「<a href="organization-management-exchange-2013-help.md">組織の管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>組織の管理のみ表示</p></td>
<td><p>この役割グループに割り当てられる役割は次のとおりです。</p>
<ul>
<li><p>&quot;Monitoring/監視&quot;</p></li>
<li><p>&quot;View-Only Configuration/表示専用構成&quot;</p></li>
<li><p>&quot;View-Only Recipients/表示専用受信者&quot;</p></li>
</ul></td>
<td><p>Exchange 2013 組織全体の構成を表示するユーザーは、この役割グループのメンバーとなる必要があります。このようなユーザーは、組織や受信者の構成を変更せずに、サーバー構成と受信者情報を表示して監視機能を実行できる必要があります。</p>
<p>この役割グループの詳細については、「<a href="view-only-organization-management-exchange-2013-help.md">表示限定の組織管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>Recipient Management</p></td>
<td><p>この役割グループに割り当てられる役割は次のとおりです。</p>
<ul>
<li><p>&quot;Distribution Groups/配布グループ&quot;</p></li>
<li><p>&quot;Mail Enabled Public Folders/メールが有効なパブリック フォルダー&quot;</p></li>
<li><p>&quot;Mail Recipient Creation/メール受信者の作成&quot;</p></li>
<li><p>Mail Recipients</p></li>
<li><p>&quot;Message Tracking/メッセージ追跡&quot;</p></li>
<li><p>&quot;Migration/移行&quot;</p></li>
<li><p>&quot;Move Mailboxes/メールボックスの移動&quot;</p></li>
<li><p>&quot;Recipient Policies/受信者ポリシー&quot;</p></li>
</ul></td>
<td><p>Exchange 2013 組織でメールボックス、連絡先、配布グループなどの受信者を管理するユーザーは、この役割グループのメンバーである必要があります。これらのユーザーは、受信者の作成、既存の受信者の変更や削除、またはメールボックスの移動を行うことができます。</p>
<p>この役割グループの詳細と、この役割グループに割り当てられる役割の完全な一覧については、「<a href="recipient-management-exchange-2013-help.md">受信者の管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>&quot;Server Management/サーバー管理&quot;</p></td>
<td><p>この役割グループに割り当てられる役割は次のとおりです。</p>
<ul>
<li><p>&quot;Databases/データベース&quot;</p></li>
<li><p>&quot;Exchange Connectors/Exchange コネクタ&quot;</p></li>
<li><p>&quot;Exchange Servers/Exchange サーバー&quot;</p></li>
<li><p>&quot;Receive Connectors/受信コネクタ&quot;</p></li>
<li><p>&quot;Transport Queues/トランスポート キュー&quot;</p></li>
</ul></td>
<td><p>Exchange サーバーの構成 (受信コネクタ、証明書、データベース、仮想ディレクトリなど) を管理するユーザーは、この役割グループのメンバーである必要があります。これらのユーザーは、Exchange サーバーの構成の変更、データベースの作成や、トランスポート キューの再起動および操作を行うことができます。</p>
<p>この役割グループの詳細と、この役割グループに割り当てられる役割の完全な一覧については、「<a href="server-management-exchange-2013-help.md">サーバー管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>Discovery Management</p></td>
<td><p>この役割グループに割り当てられる役割は次のとおりです。</p>
<ul>
<li><p>&quot;Legal Hold/法的情報保留&quot;</p></li>
<li><p>&quot;Mailbox Search/メールボックス検索&quot;</p></li>
</ul></td>
<td><p>法的手続きのサポートまたは法的情報保留の構成のためにメールボックスの検索を実行するユーザーは、この役割グループのメンバーである必要があります。</p>
<p>これは、法務部門の担当者など、Exchange 管理者でない人が含まれる可能性のある役割グループの一例です。法務担当者は Exchange 管理者の介入なしにタスクを実行することができます。</p>
<p>この役割グループの詳細と、この役割グループに割り当てられる役割の完全な一覧については、「<a href="discovery-management-exchange-2013-help.md">検出の管理</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


この表は、Exchange 2013 により、管理者に付与するアクセス許可を詳細なレベルで制御できることを示しています。Exchange 2013 では、12 の役割グループから選択できます。役割グループおよびそのアクセス許可の完全な一覧については、「[組み込みの役割グループ](built-in-role-groups-exchange-2013-help.md)」を参照してください。

Exchange 2013 では多数の役割グループが提供され、異なる役割を組み合わせて役割グループを作成することによりカスタマイズが可能であるため、Active Directory オブジェクトに対するアクセス制御リスト (ACL) の操作は不要となり、効果がありません。Exchange 2013 では、ACL を使用して個々の管理者やグループにアクセス許可を適用することはなくなりました。メールボックスを作成する管理者やメールボックスにアクセスするユーザーなど、すべてのタスクは RBAC で管理します。RBAC によりタスクが承認され、許可されている場合は Exchange がユーザーに代わってタスクを実行します。Exchange は、Exchange Trusted Subsystem ユニバーサル セキュリティ グループ (USG) でこのタスクを実行します。一部の例外を除き、Active Directory がアクセスする必要のある Exchange 2010 内のオブジェクト上の ACL にはすべて Exchange Trusted Subsystem USG が付与されます。これが、Exchange 2007 のアクセス許可の処理方法から根本的に変更された点です。

Active Directory で与えられるアクセス許可は、Exchange 2013 管理ツールを使用する際に RBAC によって与えられるアクセス許可とは別のものです。

RBAC の詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

## Exchange 2007 アクセス許可

Exchange 2007 管理モデルでは、Active Directory フォレストを利用してセキュリティ境界を定義します。特定のフォレスト内でのセキュリティ アクセス許可の分離はありません。フォレストの所有者はおよびエンタープライズ管理者は、すべてのドメインのすべてのリソースに常にアクセスできます。Exchange 2007 では、一時的な目的のみで、エンタープライズ管理者の権限およびトップレベル ドメイン管理者の権限の付与が必要な場合があります。

Exchange 2007 では、次のような定義済みの管理者の役割があります。

  - **"Exchange Organization Administrator/Exchange 組織管理者" 役割**   この役割は、Exchange 2007 組織のすべての要素を制御するためのアクセス許可を付与します。また、この役割の管理者は、他の Exchange 管理者にアクセス許可を付与できます。この役割は、Exchange 2007 のインストールに使用するアカウントに付与されます。

  - **"Exchange View-Only Administrator/Exchange 表示専用管理者" 役割**   この役割は、Exchange 構成を表示するためのアクセス許可を付与します。ただし、この役割の管理者は、Exchange 2007 組織内のオブジェクトを変更することはできません。

  - **"Exchange Recipient Administrator/Exchange 受信者管理者" 役割**   この役割は、電子メール受信者を管理するためのアクセス許可を付与します。この役割の管理者は、ユーザー、グループ、連絡先、および配布グループの Exchange に関連するアイテムを変更できます。

  - **"Exchange Server Administrator/Exchange サーバー管理者" 役割**   この役割は、特定のサーバーを管理するためのアクセス許可を付与します。ただし、この役割は Exchange 2007 組織全体に影響を与える操作を実行するためのアクセス許可は付与しません。

  - **"Exchange Public Folder Administrator/Exchange パブリック フォルダー管理者" 役割**   この役割は、Exchange 2007 Service Pack 1 で追加されました**。**この役割は、Exchange 2007 組織内のパブリック フォルダーを管理するためのアクセス許可を付与します。

このアクセス許可モデルでは、Exchange サーバー管理者役割を除くすべての役割に対して USG が使用されます。Exchange 2007**Setup /PrepareAD** コマンドを実行すると、セットアップ プログラムによって、ルート ドメイン内に USG が作成され、フォレスト全体のスコープが USG に割り当てられます。USG は、Active Directory 全体の Exchange オブジェクトを管理するために ACL を割り当てられます。

Exchange 2007 では、さまざまな役割を割り当てることにより、管理者を分けることができます。アクセス許可は、ユーザーまたはユーザーがメンバーとなっている USG のいずれかに直接割り当てられます。ユーザーの操作はすべて、そのユーザーの Active Directory アカウントのコンテキスト内で実行されます。次の表は、Exchange 2007 管理者の役割、およびそれぞれの Exchange に関連するアクセス許可の一覧です。

### Exchange 2007 管理者の役割

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>管理者の役割</th>
<th>メンバー</th>
<th>所属するグループ</th>
<th>Exchange のアクセス許可</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;Exchange Organization Administrator/Exchange 組織管理者&quot;</p></td>
<td><p>Administrator アカウント、または最初の Exchange 2007 サーバーのインストールに使用したアカウント</p></td>
<td><p>&quot;Exchange Recipient Administrator/Exchange 受信者管理者&quot;</p>
<p><em>&lt;サーバー名&gt;</em> のローカルの Administrators グループ</p></td>
<td><p>Active Directory 内の Microsoft Exchange コンテナーのフル コントロール</p></td>
</tr>
<tr class="even">
<td><p>&quot;Exchange View-Only Administrator/Exchange 表示専用管理者&quot;</p></td>
<td><p>&quot;Exchange Recipient Administrators/Exchange 受信者管理者&quot;</p>
<p>&quot;Exchange Server Administrators/Exchange サーバー管理者&quot; (<em>&lt;サーバー名 &gt;</em>)</p></td>
<td><p>&quot;Exchange Recipient Administrators/Exchange 受信者管理者&quot;</p>
<p>&quot;Exchange Server Administrators/Exchange サーバー管理者&quot;</p></td>
<td><p>Active Directory 内の Exchange コンテナーに対する読み取りアクセス</p>
<p>Exchange 受信者を含むすべての Windows ドメインに対する読み取りアクセス</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Exchange Recipient Administrator/Exchange 受信者管理者&quot;</p></td>
<td><p>&quot;Exchange Organization Administrators/Exchange 組織管理者&quot;</p></td>
<td><p>&quot;Exchange View-Only Administrators/Exchange 表示専用管理者&quot;</p></td>
<td><p>Active Directory ユーザー オブジェクトの Exchange プロパティのフル コントロール</p></td>
</tr>
<tr class="even">
<td><p>&quot;Exchange Server Administrator/Exchange サーバー管理者&quot;</p></td>
<td><p>&quot;Exchange Organization Administrators/Exchange 組織管理者&quot;</p></td>
<td><p>&quot;Exchange View-Only Administrators/Exchange 表示専用管理者&quot;</p>
<p><em>&lt;サーバー名</em>&gt; のローカルの Administrators グループ</p></td>
<td><p>Exchange<em>&lt;サーバー名&gt;</em> のフル コントロール</p></td>
</tr>
<tr class="odd">
<td><p>Exchange サーバー</p></td>
<td><p>各 Exchange 2007 コンピューター アカウント</p></td>
<td><p>&quot;Exchange View-Only Administrators/Exchange 表示専用管理者&quot;</p></td>
<td><p>特殊</p></td>
</tr>
<tr class="even">
<td><p>&quot;Exchange Public Folder Administrator/Exchange パブリック フォルダー管理者&quot;</p></td>
<td><p>&quot;Exchange Organization Administrators/Exchange 組織管理者&quot;</p></td>
<td><p>&quot;Exchange View-Only Administrators/Exchange 表示専用管理者&quot;</p></td>
<td><p>すべてのパブリック フォルダーを管理するフル コントロール (最上位のパブリック フォルダーの作成の拡張された権利を付与)</p></td>
</tr>
</tbody>
</table>


さらに詳細なアクセス許可の割り当てを行う必要がある場合は、アドレス リストやデータベースなど、個別の Exchange 2007 オブジェクトの ACL を変更できます。ユーザーまたはユーザーがメンバーになっているセキュリティ グループを直接 ACL に追加する必要があります。そうすれば、特定のユーザーのコンテキスト内で操作が実行されます。

Exchange 2007 でアクセス許可を管理する方法の詳細については、「[Exchange Server 2007 でのアクセス許可の構成](http://go.microsoft.com/fwlink/p/?linkid=90671)」を参照してください。

## Exchange 2013 と Exchange 2007 の共存アクセス許可

Exchange 2013 と Exchange 2007 のアクセス許可モデルは異なるため、Exchange 2013 のアクセス許可の割り当ては、Exchange 2007 のアクセス許可の割り当てとは分けて行います。これは、両方のバージョンの Exchange が同じフォレスト内にインストールされている場合でも同じです。追加の構成を実施しなければ、Exchange 2013 管理者には Exchange 2007 ベースのサーバーの管理に必要なアクセス許可が付与されず、Exchange 2007 管理者には Exchange 2013 ベースのサーバーの管理に必要なアクセス許可が付与されません。以下の質問を検討する必要があります。

  - Exchange 2013 の管理者が Exchange 2007 サーバーにアクセスして管理できるようにするか。

  - Exchange 2007 の管理者が Exchange 2013 サーバーにアクセスして管理できるようにするか。

  - Exchange 2013 のアクセス許可をカスタマイズして、Exchange 2007 の ACL に行ったカスタマイズと一致させるかどうか。

## Exchange 2007 管理者に対する Exchange 2013 アクセス許可の付与

Exchange 2007 管理者が Exchange 2013 サーバーを管理できるようにするには、Exchange 2007 管理者を 1 つまたは複数の Exchange 2013 役割グループのメンバーとして追加する必要があります。役割グループには、ユーザーまたは USG のいずれかを追加できます。役割グループに与えられるアクセス許可は、メンバーとして追加するユーザーまたは USG に適用されます。


> [!IMPORTANT]
> ドメインのローカルまたはグローバルの Active Directory セキュリティ グループを使用する場合、これらのセキュリティ グループを Exchange 2013 役割グループのメンバーとして追加するには、USG に変更する必要があります。Exchange 2013 では USG のみがサポートされています。



次の表は、Exchange 2007 管理者役割と Exchange 2013 役割グループとの間のマッピングを示しています。

### Exchange 2007 の管理役割および Exchange 2010 の役割グループ

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007 の管理役割</th>
<th>Exchange 2013 の役割グループ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;Exchange Organization Administrator/Exchange 組織管理者&quot;</p></td>
<td><p>組織の管理</p></td>
</tr>
<tr class="even">
<td><p>&quot;Exchange Recipient Administrator/Exchange 受信者管理者&quot;</p></td>
<td><p>Recipient Management</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Exchange Server Administrator/Exchange サーバー管理者&quot;</p></td>
<td><p>&quot;Server Management/サーバー管理&quot;</p></td>
</tr>
<tr class="even">
<td><p>&quot;Exchange View-Only Administrator/Exchange 表示専用管理者&quot;</p></td>
<td><p>組織の管理のみ表示</p></td>
</tr>
<tr class="odd">
<td><p>&quot;Exchange Server/Exchange サーバー&quot;</p></td>
<td><p>Exchange 2013 には対応する役割グループはありません</p>
<p>(カスタム役割グループを作成する方法の詳細については、「<a href="manage-role-groups-exchange-2013-help.md">役割グループの管理</a>」を参照してください)。</p></td>
</tr>
<tr class="even">
<td><p>&quot;Exchange Public Folder Administrator/Exchange パブリック フォルダー管理者&quot;</p></td>
<td><p>&quot;Public Folder Management/パブリック フォルダーの管理&quot;</p></td>
</tr>
</tbody>
</table>


すべての Exchange 2007 管理者が Exchange 2007 の管理役割のいずれかのメンバーである場合は、各管理グループのメンバーを Exchange 2013 の同等の役割グループに追加することができます。たとえば、すべての Exchange 2007 組織管理者に Exchange 2013 オブジェクトへのフル アクセスを付与する場合は、"Exchange Organization Administrators/Exchange 組織管理者" USG を 組織の管理 役割グループに追加します。

ユーザーおよび USG の役割グループへの追加方法の詳細については、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。

Exchange 2007 オブジェクトの ACL を変更して、より詳細なアクセス許可を Exchange 2007 管理者に与えたうえで、これらの管理者に Exchange 2013 サーバーと同様のアクセス許可を割り当てるには、次の手順に従います。

1.  Exchange 2007 オブジェクトに行った ACL のカスタマイズを確認し、各オブジェクトにアクセス許可を付与した管理者を見つけます。

2.  それぞれの Exchange 2007 オブジェクトを分類します。たとえば、オブジェクトがデータベースか、サーバーか、受信者オブジェクトかを判別します。

3.  対応する Exchange 2013 役割グループにオブジェクトをマッピングします。組み込みの役割グループの一覧については、「[組み込みの役割グループ](built-in-role-groups-exchange-2013-help.md)」を参照してください。

4.  各種オブジェクトの USG またはユーザーを、対応する Exchange 2013 役割グループに追加します。ユーザーおよび USG の役割グループへの追加方法の詳細については、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。

以上の手順を完了すると、Exchange 2007 管理者は適切な Exchange 2013 オブジェクトにマップされた特定の役割グループのメンバーになります。Exchange 2007 管理者は、Exchange 2013 管理ツールを使用して、Exchange 2013 サーバーおよび受信者を管理できるようになります。


> [!IMPORTANT]
> 一般的に、Exchange&nbsp;2007 サーバーと受信者は Exchange&nbsp;2007 管理ツールを使用して、Exchange 2013 サーバーと受信者は Exchange 2013 管理ツールを使用して管理する必要があります。



管理者に付与する必要のある特定のアクセス許可のセットが組み込みの役割グループで提供されていない場合は、カスタム役割グループを作成できます。カスタム役割グループの作成時に、追加する役割を選択できます。役割グループのメンバーが管理する特定の機能を定義できます。たとえば、管理者に配布グループのみを管理させる場合は、カスタム役割グループを作成し、"Distribution Groups/配布グループ" の役割だけを選択します。この操作を行った後、そのカスタム役割グループのメンバーは配布グループのみを管理できるようになります。カスタム役割グループを作成する方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」を参照してください。

特定の Exchange 2007 オブジェクトに選択的なアクセス許可を割り当てており (たとえば、管理者に特定のデータベースのみの管理を許可するなど)、これと同じ構成を Exchange 2013 サーバーに適用する場合は、このトピックに記載されている「Exchange 2007 で管理スコープを使用して Exchange 2013 の ACL カスタマイズを再作成する」を参照してください。

## Exchange 2013 の管理者に対する Exchange 2007 アクセス許可の付与

Exchange 2013 管理者が Exchange 2007 サーバーを管理できるようにするには、Exchange 2013 管理者を USG または特定の Exchange 2007 管理者役割に相当するセキュリティ グループに追加します。もしくは、カスタマイズした ACL 設定がある場合は、管理者を適切な ACL に追加します。役割グループは USG であるため、Exchange 2007 管理役割 USG に直接追加できます。

完了すると、Exchange 2013 管理者は 1 つまたは複数の適切な Exchange 2007 管理者役割のメンバーとなります。Exchange 2013 管理者は、Exchange 2007 管理ツールを使用して、Exchange 2007 サーバーおよび受信者を管理できるようになります。

## Exchange 2013 で管理スコープを使用して Exchange 2017 の ACL カスタマイズを再作成する

Exchange 2007 では、特定のメールボックス ストアやユーザーを管理したり、メールボックスの作成先のメールボックス ストアを制御したりすることができるユーザーを制限する場合は、制限しようとするオブジェクトの ACL を変更する必要があります。Exchange 2013 にも同じ機能がありますが、ACL を変更する必要はありません。管理スコープ (RBAC のコンポーネント) を使用してこれを行います。

管理スコープを使用すると、組み込みのスコープとカスタム スコープにより、管理者が管理できるオブジェクトを定義できます。管理スコープを適用すると、管理できる受信者、メールボックスを作成できるメールボックス データベースや、管理者の小規模グループのみで管理する必要がある受信者やサーバーを定義できます。

以下の種類の管理スコープを作成できます。

  - **定義済み相対**Exchange 2013 には、定義済み相対スコープが含まれます。ユーザーが参照して変更できる内容を制御できます。たとえば、定義済み相対スコープを使用すると、ユーザー自身に関する情報のみを参照するよう制御したり、組織全体に関する情報を参照するよう制御したりできます。

  - **受信者**   受信者スコープによって、管理者が作成、変更、または削除できる受信者を制御します。この選択は、組織単位 (OU)、受信者フィルター、またはその両方に基づきます。受信者フィルターによって、受信者がスコープに含まれるために一致する必要がある条件を指定します。たとえば、特定の場所や部署の全ユーザーが含まれる受信者フィルター スコープを作成する場合などがあります。OU と受信者フィルターを組み合わせて、特定の OU 内の特定のマネージャーにレポートするユーザーという条件に一致させることもできます。

  - **サーバー**   サーバー スコープによって、管理者が管理できるサーバーを制御します。サーバー リストまたはサーバー フィルターのいずれかを指定できます。サーバー リストでは、管理できるサーバーの静的一覧を定義します。サーバー フィルターは、一致する必要がある条件を指定できるという点で、受信者フィルターと同様に動作します。たとえば、特定の Active Directory サイト内の全サーバーという条件に一致するサーバー スコープを作成する場合があります。

  - **データベース**   データベース スコープによって、管理者が管理できるデータベースを制御します。データベース スコープにより、メールボックスの作成先や移動先にすることのできるデータベースも制御できます。データベース スコープは、サーバー スコープと同様に、リストまたはフィルターとして定義できます。たとえば、特定の支社が管理する特定のメールボックス データベースに対する管理者によるメールボックスの作成や移動を許可するリストやフィルターを作成する場合があります。

  - **排他的**   受信者、サーバー、およびデータベースのスコープは、排他的スコープとして作成することもできます。排他的スコープは、ACL の拒否アクセス ACE と同様に動作します。排他的スコープと一致するオブジェクトがあると、排他的スコープが割り当てられている管理者のみがそのオブジェクトを管理できます。これは、他の排他的でないスコープがそのオブジェクトと一致している場合でも当てはまります。これは、数人の十分に信用できる個人だけが上級管理者のメールボックスを管理できるようにしたい場合などに特に有用です。別の標準の受信者スコープがより広範囲で、そのスコープに上級管理者のメールボックスが含まれている場合でも、その広範囲な標準の受信者スコープが割り当てられている管理者に排他的スコープも割り当てられていない限り、その管理者は上級管理者のメールボックスを管理できません。

管理スコープは、管理役割、管理役割の割り当て、および管理役割グループで、オブジェクトの管理者と種類、およびそれらのオブジェクトを管理する方法を制御するために使用されます。詳細については、以下のトピックを参照してください。

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

  - [排他スコープについて](understanding-exclusive-scopes-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

  - [管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)

  - [管理の役割について](understanding-management-roles-exchange-2013-help.md)

カスタマイズした ACL を使用して定義した管理スコープを使用し、Exchange 2013 で同じアクセス許可モデルを作成するには、カスタマイズした ACL をインベントリし、その ACL と一致する管理スコープを作成する必要があります。受信者、サーバー、およびデータベース オブジェクトで使用できるフィルター可能なプロパティを使用して、各管理スコープでアクセスを制御するオブジェクトを含む管理スコープを作成できます。管理スコープ フィルターで使用できるプロパティの詳細については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

管理スコープを作成する方法の詳細については、「[通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)」を参照してください。

