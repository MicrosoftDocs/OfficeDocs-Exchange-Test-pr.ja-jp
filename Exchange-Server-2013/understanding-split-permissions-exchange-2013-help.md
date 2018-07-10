---
title: '分割型アクセス許可について: Exchange 2013 Help'
TOCTitle: 分割型アクセス許可について
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 49895313
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 分割型アクセス許可について

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-07_

Microsoft Exchange Server 2013 オブジェクトおよび Active Directory オブジェクトの管理を分割している組織は、*分割型アクセス許可*と呼ばれるモデルを使用します。組織

### セキュリティ プリンシパルの管理役割

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割</th>
<th>役割グループ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">&quot;メール受信者の作成&quot; 役割</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">&quot;Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ&quot; 役割</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


は分割型アクセス許可を使用すると、特定のアクセス許可と関連作業を組織内の特定のグループに割り当てることができます。このような作業の分割によって基準とワークフローを管理しやすくなり、組織内の変更を容易に制御できるようになります。

最上位レベルの分割型アクセス許可では、Exchange 管理と Active Directory 管理が分割されます。多くの組織には、サーバーや受信者などの組織の Exchange インフラストラクチャを管理する管理者と、Active Directory インフラストラクチャを管理する管理者の 2 つのグループがあります。Active Directory インフラストラクチャは、多くの場合、多くの場所、ドメインやサービス、アプリケーション、さらには Active Directory フォレストに及ぶため、多くの組織にとってこのような分割は重要になります。Active Directory 管理者は Active Directory に対して行われた変更が他のサービスに悪影響を及ぼすことがないようにしなければなりません。このため通常は、より小規模な管理者グループのみに、該当するインフラストラクチャの管理を許可するようにします。

と同時に、サーバーや受信者などの Exchange のインフラストラクチャも複雑になりがちで、専門知識を必要とします。さらに、Exchange は、組織のビジネス上の極めて機密性の高い情報を格納します。Exchange 管理者は、このような情報にアクセスする可能性が高くなりますExchange 管理者数を制限すると、組織は Exchange の構成を変更できる人間、および機密情報にアクセスできる人間を制限できます。

分割型アクセス許可は、通常、Active Directory 内のユーザーやセキュリティ グループなどのセキュリティ プリンシパルの作成と、後で行われるこれらのオブジェクトの構成を区別します。このように区別すると、ネットワークにアクセスする権限を付与するオブジェクトを作成できる人間を制御することで、ネットワークへの不正アクセスを削減できます。ほとんどの場合、Active Directory 管理者のみがセキュリティ プリンシパルを作成可能で、一方 Exchange 管理者などのその他の管理者は、既存の Active Directory オブジェクトの特定の属性を管理できます。

Exchange と Active Directory 管理を分割するためのさまざまなニーズに対応するため、Exchange 2013 では共有アクセス許可モデルと分割型アクセス許可モデルのどちらかを選択できます。Exchange 2013 では 2 種類の分割アクセス許可モデルを用意しています。RBAC と Active Directory. Exchange 2013 の既定は、共有アクセス許可モデルです。

**目次**

役割ベースのアクセス制御と Active Directory の説明

共有アクセス許可

分割型アクセス許可

RBAC 分割型アクセス許可

Active Directory の分割型アクセス許可

## 役割ベースのアクセス制御と Active Directory の説明


分割型アクセス許可を理解するには、Exchange 2013 の役割ベースのアクセス制御 (RBAC) アクセス許可モデルが、Active Directory でどのように動作するかを理解する必要があります。RBAC モデルは、誰がどのアクションを実行可能であるか、またどのオブジェクトがこれらのアクションを実行可能であるかを制御します。このトピックで説明する RBAC の各種コンポーネントの詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

Exchange 2013 では、Exchange オブジェクトに対して実行されるすべてのタスクは、Exchange 管理シェルまたは Exchange 管理インターフェイス (EAC) を介して実行する必要があります。どちらの管理ツールも、実行されるすべてのタスクを認証するために RBAC を使用します。

RBAC は、Exchange 2013 を実行しているすべてのサーバーに存在するコンポーネントです。アクションを実行するユーザーがこのアクションを実行することを許可されているかどうかを、RBAC が以下のようにチェックします。

  - ユーザーがこのアクションの実行を許可されていない場合、RBAC はこのアクションの続行を許可しません。

  - ユーザーがこのアクションの実行を許可されている場合、RBAC はユーザーが要求している特定のオブジェクトに対するアクションの実行を許可するかどうかをチェックします。
    
      - ユーザーが許可される場合、RBAC はこのアクションの続行を許可します。
    
      - ユーザーが許可されない場合、RBAC はこのアクションの続行を許可しません。

RBAC がアクションの続行を許可する場合、そのアクションは、Exchange Trusted Subsystem のコンテキストで実行され、ユーザーのコンテキストでは実行されません。Exchange Trusted Subsystem は高い特権を持つユニバーサル セキュリティ グループ (USG) であり、Exchange 組織内のすべての Exchange 関連オブジェクトに対する読み取りおよび書き込みアクセスが可能です。また Exchange Trusted Subsystem は、Administrators ローカル セキュリティ グループと Windows アクセス許可 USG のメンバーでもあり、これらのメンバーであることにより、Exchange で Active Directoryオブジェクトを作成および管理できます。


> [!NOTE]
> Exchange Trusted Subsystem セキュリティ グループのメンバーシップには、手動によるいかなる変更も加えないでください。また、オブジェクトのアクセス制御リスト (ACL) への追加または削除はしないでください。Exchange Trusted Subsystem USG に自分自身で変更を加えると、Exchange 組織に回復困難な損傷が発生する可能性があります。



ユーザーが、Exchange 管理ツールを使用する際にどのような Active Directory アクセス許可を持っているかはそれほど問題ではないことを理解することが重要です。ユーザーが RBAC を介して Exchange 管理ツールでのアクションの実行を許可されると、付与されている Active Directory アクセス許可に関係なくそのアクションを実行できます。反対に、ユーザーが Active Directory の Enterprise Admin であっても、メールボックスの作成などのアクションの実行を許可されていない場合は、RBAC に基づく必要なアクセス許可がそのユーザーに付与されていないので、Exchange 管理ツールでのアクションは続行できません。


> [!IMPORTANT]
> RBAC アクセス許可モデルが Active Directory ユーザーとコンピューター管理ツールに適用されていなくても、Active Directory ユーザーとコンピューターは Exchange 構成を管理できません。したがって、ユーザーの表示名などの Active Directory オブジェクトの一部の属性を変更するためのアクセス許可がユーザーに付与されているとしても、Exchange 管理ツールを使用する必要があり、このため、Exchange 属性を管理するには RBAC によって許可されなくてはなりません。



ページのトップへ

## 共有アクセス許可

共有アクセス許可モデルは、Exchange 2013 の既定モデルです。このモデルが使用するアクセス許可モデルである場合は、何も変更する必要はありません。このモデルは、Exchange 管理ツールからの Exchange オブジェクトと Active Directory オブジェクトの管理を分割しません。このモデルを使用すると管理者は、Exchange 管理ツールを使用して Active Directory でセキュリティ プリンシパルを作成することができます。

次の表は、Exchange でのセキュリティ プリンシパルの作成を可能にする役割と、これらの役割を既定で割り当てられる管理役割グループを示しています。

### セキュリティ プリンシパルの管理役割

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割</th>
<th>役割グループ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">&quot;メール受信者の作成&quot; 役割</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">&quot;Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ&quot; 役割</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


"Mail Recipient Creation/メール受信者の作成" 役割が割り当てられた役割グループ、ユーザー、または USG のみが、Active Directory ユーザーなどのセキュリティ プリンシパルを作成できます。既定では、組織の管理 および Recipient Management 役割グループが、この役割に割り当てられます。したがって、これらの役割グループのメンバーはセキュリティ プリンシパルを作成できます。

"Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割が割り当てられた役割グループ、ユーザー、または USG のみが、セキュリティ グループを作成したり、セキュリティ グループのメンバーシップを管理したりできます。既定では、組織の管理 役割グループだけが、この役割に割り当てられます。したがって、組織の管理 役割グループのメンバーだけが、セキュリティ グループのメンバーシップを作成または管理できます。

他のユーザーがセキュリティ プリンシパルを作成できるようにするには、その他の役割グループ、ユーザー、または USG に "Mail Recipient Creation/メール受信者の作成" 役割と "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割を割り当てます。

Exchange 2013 で既存のセキュリティ プリンシパルを管理できるようにするために、組織の管理 と Recipient Management 役割グループには既定で "Mail Recipient/メール受信者" 役割が割り当てられています。"Mail Recipient/メール受信者" 役割が割り当てられた役割グループ、ユーザー、または USG のみが、既存のセキュリティ プリンシパルを管理できます。その他の役割グループ、ユーザー、または USG が既存のセキュリティ プリンシパルを管理できるようにするには、"Mail Recipient/メール受信者" 役割を割り当てる必要があります。

役割を役割グループ、ユーザー、または USG に追加する方法の詳細については、以下のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

分割型アクセス許可モデルに切り替えた後で、再度共有アクセス許可モデルに戻す方法については、[Exchange 2013 の共有アクセス許可を構成する](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)を参照してください。

ページのトップへ

## 分割型アクセス許可

組織で Exchange 管理と Active Directory 管理を分離する場合、分割型アクセス許可モデルをサポートするように Exchange を構成する必要があります。正しく構成すると、セキュリティ プリンシパルを作成させたいと考える管理者 (Active Directory 管理者など) のみがセキュリティ プリンシパルを作成できるようになり、Exchange 管理者のみが既存のセキュリティ プリンシパルの Exchange 属性を変更できるようになります。このアクセス許可の分割は、だいたい Active Directory のドメインと構成パーティションの線に沿ったかたちで収まります。パーティションは名前付けコンテキストとも呼ばれます。ドメイン パーティションには、特定のドメインのユーザー、グループ、およびその他のオブジェクトが格納されます。構成パーティションには、Exchange などの、Active Directory を使用したサービスのフォレスト全体の構成情報が格納されます。ドメイン パーティションに格納されたデータは、通常 Active Directory 管理者によって管理されますが、Exchange 固有の属性を含むオブジェクトは Exchange 管理者によって管理されます。構成パーティションに格納されるデータは、個のパーティションにデータを格納するそれぞれのサービスの管理者によって管理されます。Exchange では、これは通常 Exchange 管理者です。

Exchange 2013 は、次の 2 種類の分割アクセス許可をサポートしています。

  - **RBAC 分割型アクセス許可**   Active Directory ドメイン パーティションにセキュリティ プリンシパルを作成するアクセス許可を RBAC で制御します。Exchange サーバー、サービス、および適切な役割グループのメンバーだけが、セキュリティ プリンシパルを作成できます。

  - **Active Directory の分割型アクセス許可**   Active Directory ドメイン パーティション内にセキュリティ プリンシパルを作成するアクセス許可が、すべての Exchange ユーザー、サービス、またはサーバーから完全に削除されています。RBAC でセキュリティ プリンシパルを作成するオプションは用意されていません。Active Directory でセキュリティ プリンシパルを作成する場合は、Active Directory 管理ツールを使用する必要があります。
    

    > [!IMPORTANT]
    > Active Directory の分割型アクセス許可は、Exchange 2013 がインストールされたコンピューター上でセットアップ プログラムを実行して有効または無効にできますが、Active Directory 分割型アクセス許可の構成は Exchange 2013 サーバーと Exchange 2010 サーバーの両方に適用されます。ただし、Microsoft Exchange Server 2007 サーバーには影響しません。



組織が、共有アクセス許可ではなく分割型アクセス許可の使用を選択する場合は、RBAC 分割型アクセス許可モデルの使用をお勧めします。RBAC 分割型アクセス許可モデルにより、Active Directory 分割型アクセス許可とほぼ同じ管理の分離を提供しながら柔軟性が大幅に向上します。違いは、RBAC 分割型アクセス許可モデルでは Exchange サーバーおよびサービスがセキュリティ プリンシパルを作成できるという点です。

セットアップ プログラムの実行中に、Active Directory 分割型アクセス許可を有効にするかどうかをたずねられます。Active Directory 分割型アクセス許可を有効にすることを選択した場合、セットアップ プログラムを再実行して Active Directory 分割型アクセス許可を無効にすることで、共有アクセス許可または RBAC 分割型アクセス許可に変更することだけができます。この選択は、組織内のすべての Exchange 2010 サーバーと Exchange 2013 サーバーに適用されます。

以下では、RBAC および Active Directory 分割型アクセス許可をより詳細に説明します。

ページのトップへ

## RBAC 分割型アクセス許可

RBAC セキュリティ モデルは既定の管理役割の割り当てを変更し、Active Directory ドメイン パーティションにおいてセキュリティ プリンシパルを作成可能なユーザーを、Active Directory 構成パーティションにおいて Exchange 組織データを管理するユーザーから分離します。メールボックスや配布グループを持つユーザーのようなセキュリティ プリンシパルは、"Mail Recipient Creation/メール受信者の作成" 役割および "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割のメンバーである管理者が作成できます。これらのアクセス許可は、Exchange 管理ツール以外でセキュリティ プリンシパルを作成するのに必要なアクセス許可とは分離されます。"Mail Recipient Creation/メール受信者の作成" 役割または "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割が割り当てられていない Exchange 管理者は依然としてセキュリティ プリンシパルの Exchange に関連する属性を変更できます。Active Directory 管理者にも Active Directory セキュリティ プリンシパルを作成するための Exchange 管理ツールを使用するオプションがあります。

Exchange サーバーおよび Exchange Trusted Subsystem もまた、ユーザーおよび RBAC と統合するサードパーティ プログラムの代理として Active Directory でセキュリティ プリンシパルを作成するアクセス許可があります。

以下の条件にあてはまる場合は、RBAC 分割型アクセス許可は組織に適しています。

  - 組織は、Active Directory 管理ツールを使用する場合のみ、および特定の Active Directory アクセス許可が割り当てられたユーザーだけが、セキュリティ プリンシパルの作成を実行できる必要はない。

  - 組織は、Exchange サーバーなどの、サービスがセキュリティ プリンシパルを作成するのを許可する。

  - Exchange 管理ツール内から、メールボックスの作成、メールが有効なユーザー、配布グループ、および役割グループの作成をできるようにすることで、必要な処理を単純化したい。

  - Exchange 管理ツール内の配布グループおよび役割グループのメンバーシップを管理したい。

  - Exchange サーバーが代理でセキュリティ プリンシパルを作成できることが必要なサードパーティ製のプログラムがある。

Exchange 管理ツールの使用、または Exchange サービスによる Active Directory 管理の実行を許可しないような、Exchange と Active Directory 管理の完全な分離が組織に必要な場合は、後の「Active Directory の分割型アクセス許可」を参照してください。

共有アクセス許可から RBAC 分割型アクセス許可への切り換えは手動によるプロセスで、既定で付与される、セキュリティ プリンシパルを作成するのに必要なアクセス許可を役割グループから削除します。次の表は、Exchange でのセキュリティ プリンシパルの作成を可能にする役割と、これらの役割を既定で割り当てられる管理役割グループを示しています。

### セキュリティ プリンシパルの管理役割

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割</th>
<th>役割グループ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">&quot;メール受信者の作成&quot; 役割</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">受信者の管理</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">&quot;Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ&quot; 役割</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織の管理</a></p></td>
</tr>
</tbody>
</table>


既定では、組織の管理 と Recipient Management 役割グループのメンバーは、セキュリティ プリンシパルを作成できます。組み込みの役割グループから、セキュリティ プリンシパルを作成するための機能を作成した新しい役割グループに転送する必要があります。

RBAC 分割型アクセス許可モデルを構成するには、次の手順を実行します。

1.  Active Directory 分割型アクセス許可が有効の場合は無効にします。

2.  役割グループを作成し、セキュリティ プリンシパルを作成できる Active Directory 管理者を含めます。

3.  "Mail Recipient Creation/メール受信者の作成" 役割と新しい役割グループの間に、正規および委任の役割の割り当てを作成します。

4.  "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割と新しい役割グループの間に、正規および委任の役割の割り当てを作成します。

5.  "Mail Recipient Creation/メール受信者の作成" 役割と、組織の管理 および Recipient Management 役割グループの間の、正規および委任の役割の割り当てを削除します。

6.  "Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ" 役割と 組織の管理 役割グループの間の、正規および委任の役割の割り当てを削除します。

この操作を実行すると、作成した新しい役割グループのメンバーのみが、メールボックスなどのセキュリティ プリンシパルを作成できるようになります。新しいグループは、オブジェクトの作成のみができます。新しいオブジェクトに Exchange 属性を構成することはできません。新しいグループのメンバーである Active Directory 管理者はオブジェクトを作成する必要があり、Exchange 管理者はオブジェクトの Exchange 属性を構成する必要があります。Exchange 管理者は、以下のコマンドレットを使用できなくなります。

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

ただし、Exchange 管理者は、トランスポート ルールや配布グループなどの Exchange 固有のオブジェクトの作成、管理、およびすべてのオブジェクトの Exchange 関連の属性を管理することはできます。

また、メールボックスの新規作成ウィザードなど、EAC と Outlook Web App の関連機能は、利用できなくなるか、使用するとエラーが発生するようになります。

新しい役割グループが、新しいオブジェクトの Exchange 属性も管理できるようにするには、さらに新しい役割グループに "Mail Recipient/メール受信者" 役割を割り当てる必要があります。

分割型アクセス許可モデルの構成の詳細については、「[Exchange 2013 の分割型アクセス許可を構成する](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)」を参照してください。

ページのトップへ

## Active Directory の分割型アクセス許可

Active Directory 分割型アクセス許可では、メールボックスや配布グループの作成などの Active Directory ドメイン パーティションにおけるセキュリティ プリンシパルの作成は、Active Directory 管理ツールを使って実行する必要があります。Exchange Trusted Subsystem および Exchange サーバーに対して付与されたアクセス許可にいくつかの変更が加えられ、Exchange 管理者およびサーバーが実行できることに制限が加えられます。Active Directory 分割型アクセス許可を有効にすると、機能に以下の変更が発生します。

  - メールボックス、メールが有効なユーザー、配布グループ、およびその他のセキュリティ プリンシパルの作成は、Exchange 管理ツールから取り除かれます。

  - 配布グループ メンバーの追加と削除は、Exchange 管理コンソールからは実行できません。

  - セキュリティ プリンシパルを作成するために Exchange Trusted Subsystem および Exchange サーバーに与えられたすべてのアクセス許可は削除されます。

  - Exchange サーバーおよび Exchange 管理ツールは、Active Directory の既存のセキュリティ プリンシパルの Exchange 属性の変更だけを行えます。

たとえば、Active Directory 分割型アクセス許可が有効な状態でメールボックスを作成するには、必要な Active Directory アクセス許可を持つユーザーが Active Directory ツールを使用して、ユーザーを最初に作成する必要があります。次に、Exchange 管理ツールを使用してユーザーのメールボックスを有効にします。Exchange 管理ツールを使用する Exchange 管理者は、メールボックスの Exchange 関連の属性だけを変更できます。

以下の条件にあてはまる場合は、Active Directory 分割型アクセス許可は組織に適しています。

  - 組織は、Active Directory 管理ツールを使用する場合のみ、または Active Directory で特定のアクセス許可が与えられたユーザーのみが、セキュリティ プリンシパルの作成を実行できる必要がある。

  - セキュリティ プリンシパルを作成する機能を、Exchange 組織を管理するユーザーから完全に分離する。

  - Active Directory 管理ツールを使用して、配布グループの作成およびそれらのグループのメンバーの追加と削除を含む、すべての配布グループの管理を実行する。

  - Exchange サーバー、または Exchange を代理で使用するサードパーティ製のプログラムがセキュリティ プリンシパルを作成しないようにする。


> [!IMPORTANT]
> セットアップ ウィザードを使用して、または <EM>ActiveDirectorySplitPermissions</EM> パラメーターを指定してコマンド ラインから <CODE>setup.exe</CODE> を実行して Exchange 2013 をインストールするときに、Active Directory 分割型アクセス許可に切り換えることができます。Active Directory をインストールした後に、コマンド ラインから <CODE>setup.exe</CODE> を再実行して Exchange 2013 分割型アクセス許可を有効または無効にできます。Active Directory 分割型アクセス許可を有効にするには、<EM>ActiveDirectorySplitPermissions</EM> パラメーターを <CODE>true</CODE> に設定します。無効にするには、パラメーターを <CODE>false</CODE> に設定します。<EM>ActiveDirectorySplitPermissions</EM> パラメーターと共に <EM>PrepareAD</EM> スイッチも常に指定する必要があります。<BR>同じフォレスト内に複数のドメインがある場合は、Active Directory 分割型アクセス許可を適用するときに <EM>PrepareAllDomains</EM> スイッチを指定するか、またはそれぞれのドメインで <EM>PrepareDomain</EM> スイッチを指定してセットアップを実行するかのいずれかを行う必要があります。<EM>PrepareAllDomains</EM> スイッチを使用する代わりに、それぞれのドメインで <EM>PrepareDomain</EM> スイッチを使用してセットアップを実行することを選択する場合、Exchange サーバーによってアクセスされる可能性のある、Exchange サーバー、メールが有効なオブジェクト、またはグローバル カタログ サーバーを含むすべてのドメインについて準備する必要があります。




> [!IMPORTANT]
> Exchange 2010 か Exchange 2013 をドメイン コントローラーにインストールした場合、Active Directory 分割型アクセス許可は有効にすることができません。<BR>Active Directory 分割型アクセス許可を有効または無効にした後は、組織の Exchange 2010 サーバーと Exchange 2013 サーバーを再起動して、更新されたアクセス許可の新しい Active Directory アクセス トークンを強制的に取得することをお勧めします。



Exchange 2013 は、ExchangeWindows アクセス許可セキュリティ グループからアクセス許可とメンバーシップを削除して、Active Directory 分割型アクセス許可を設定します。共有アクセス許可および RBAC 分割型アクセス許可において、このセキュリティ グループは Active Directory 全体を通して数多くの Exchange 以外のオブジェクトおよび属性に対して与えられます。アクセス許可とメンバーシップを、このセキュリティ グループから削除することで、Exchange 管理者およびサービスが、これら ExchangeActive Directory 以外のオブジェクトを作成または変更するのを防止できます。

Active Directory 分割型アクセス許可を有効または無効にする場合の、ExchangeWindows アクセス許可のセキュリティ グループおよびその他の Exchange コンポーネントに対して発生する変更の一覧については、次の表を参照してください。


> [!NOTE]
> Exchange 管理者がセキュリティ プリンシパルを作成できるようにするための役割グループへの役割の割り当ては、Active Directory 分割型アクセス許可が有効になった時点で削除されます。これは、関連する Active Directory オブジェクトを作成するアクセス許可を持たないために、実行すればエラーが発生するコマンドレットへのアクセスを削除するために行われます。



### Active Directory の分割型アクセス許可の変更

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>Exchange による変更</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>最初の Exchange 2013 サーバーのインストール中に Active Directory 分割型アクセス許可を有効にする</p></td>
<td><p>セットアップ ウィザードを通して、または <code>setup.exe</code> を <code>/PrepareAD</code> および <code>/ActiveDirectorySplitPermissions:true</code> パラメーターで実行するかのいずれかにより Active Directory 分割型アクセス許可を有効にすると、以下の事が起こります。</p>
<ul>
<li><p><strong>[Microsoft Exchange Protected Groups]</strong> という名前の組織単位 (OU) が作成されます。</p></li>
<li><p><strong>[Exchange Windows Permissions]</strong> セキュリティ グループが <strong>[Microsoft Exchange Protected Groups]</strong> OU 内に作成されます。</p></li>
<li><p><strong>[Exchange Trusted Subsystem]</strong> セキュリティ グループは <strong>[Exchange Windows Permissions]</strong> セキュリティ グループには追加されません。</p></li>
<li><p>以下の管理役割の種類の管理役割に対する、委任管理役割以外の割り当ての作成はスキップされます。</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p><strong>[Exchange Windows Permissions]</strong> セキュリティ グループに割り当てられていたはずのアクセス制御エントリ (ACE) は、Active Directory ドメイン オブジェクトには追加されません。</p></li>
</ul>
<p><em>PrepareAllDomains</em> スイッチまたは <em>PrepareDomain</em> スイッチを指定してセットアップを実行する場合、準備されたそれぞれの子ドメインにおいて次のことが起こります。</p>
<ul>
<li><p><strong>[Exchange Windows Permissions]</strong> セキュリティ グループに割り当てられたすべての ACE は、ドメイン オブジェクトから削除されます。</p></li>
<li><p>ACE は、<strong>[Exchange Windows Permissions]</strong> セキュリティ グループに割り当てられたすべての ACE を除き、各ドメインで設定されます。</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>共有アクセス許可または RBAC 分割型アクセス許可から Active Directory 分割型アクセス許可に切り換える</p></td>
<td><p><code>setup.exe</code> コマンドを <code>/PrepareAD</code> および <code>/ActiveDirectorySplitPermissions:true</code> パラメーターで実行すると以下の事が起こります。</p>
<ul>
<li><p><strong>[Microsoft Exchange Protected Groups]</strong> という名前の OU が作成されます。</p></li>
<li><p><strong>[Exchange Windows Permissions]</strong> セキュリティ グループが <strong>[Microsoft Exchange Protected]</strong> グループ OU 内に移動されます。</p></li>
<li><p><strong>[Exchange Trusted Subsystem]</strong> セキュリティ グループは <strong>[Exchange Windows Permissions]</strong> セキュリティ グループから削除されます。</p></li>
<li><p>以下の役割の種類の管理役割に対する、すべての委任管理役割以外の割り当ては削除されます。</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p><strong>[Exchange Windows Permissions]</strong> セキュリティ グループに割り当てられたすべての ACE は、ドメイン オブジェクトから削除されます。</p></li>
</ul>
<p><em>PrepareAllDomains</em> スイッチまたは <em>PrepareDomain</em> スイッチのいずれかを指定してセットアップを実行する場合、準備されたそれぞれの子ドメインにおいて次のことが起こります。</p>
<ul>
<li><p><strong>[Exchange Windows Permissions]</strong> セキュリティ グループに割り当てられたすべての ACE は、ドメイン オブジェクトから削除されます。</p></li>
<li><p>ACE は、<strong>[Exchange Windows Permissions]</strong> セキュリティ グループに割り当てられたすべての ACE を除き、各ドメインで設定されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Active Directory 分割型アクセス許可から、共有アクセス許可または RBAC 分割型アクセス許可に切り換える</p></td>
<td><p><code>setup.exe</code> コマンドを <code>/PrepareAD</code> および <code>/ActiveDirectorySplitPermissions:false</code> パラメーターで実行すると以下の事が起こります。</p>
<ul>
<li><p><strong>[Exchange Windows Permissions]</strong> セキュリティ グループが <strong>[Microsoft Exchange Security Groups]</strong> OU 内に移動されます。</p></li>
<li><p><strong>[Microsoft Exchange Protected Groups]</strong> OU は削除されます。</p></li>
<li><p><strong>[Exchange Trusted Subsystems]</strong> セキュリティ グループが <strong>[Exchange Windows Permissions]</strong> セキュリティ グループに追加されます。</p></li>
<li><p>ACE が <strong>[Exchange Windows Permissions]</strong> セキュリティ グループのドメイン オブジェクトに追加されます。</p></li>
</ul>
<p><em>PrepareAllDomains</em> スイッチまたは <em>PrepareDomain</em> スイッチのいずれかを指定してセットアップを実行する場合、準備されたそれぞれの子ドメインにおいて次のことが起こります。</p>
<ul>
<li><p>ACE が <strong>[Exchange Windows Permissions]</strong> セキュリティ グループのドメイン オブジェクトに追加されます。</p></li>
<li><p>ACE は、<strong>[Exchange Windows Permissions]</strong> セキュリティ グループに割り当てられた ACE を含む各ドメインに設定されます。</p></li>
</ul>
<p>Active Directory 分割型アクセス許可から共有アクセス許可に切り換える場合、&quot;Mail Recipient Creation/メール受信者の作成&quot; 役割および &quot;Security Group Creation and Membership/セキュリティ グループの作成とメンバーシップ&quot; 役割に対する役割の割り当ては、自動的に作成されません。Active Directory 分割型アクセス許可を有効にする前に、委任する役割の割り当てがカスタマイズされた場合、それらのカスタマイズは保持されます。これらの役割と 組織の管理 役割グループの間の役割の割り当てを作成するには、「<a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">Exchange 2013 の共有アクセス許可を構成する</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>


Active Directory 分割型アクセス許可を有効化した後は、以下のコマンドレットは使用できなくなります。

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Active Directory 分割型アクセス許可を有効化した後は、以下のコマンドレットはアクセス可能ですが、それらを使用して配布グループを作成したり配布グループのメンバーシップを変更したりすることはできません。

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

コマンドレットのいくつかは依然として使用可能ですが、Active Directory 分割型アクセス許可で使用すると機能が制限される場合があります。これは、ドメイン Active Directory パーティションにある受信者オブジェクト、および構成 Active Directory パーティションにある Exchange 構成オブジェクトを構成できるようにするためです。それらによって、ドメイン パーティションに格納されたオブジェクトの Exchange 関連の属性を構成できるようにもなります。コマンドレットを使用してオブジェクトを作成しようとするか、オブジェクトの Exchange 関連以外の属性を変更しようとすると、ドメイン パーティションでエラーが発生します。たとえば、メールボックスにアクセス許可を追加しようとすると、**Add-ADPermission** コマンドレットはエラーを返します。ただし、受信コネクタ上でアクセス許可を構成すると、**Add-ADPermission** コマンドレットは成功します。これは、メールボックスはドメイン パーティションに格納されていますが、受信コネクタは構成パーティションに格納されていることによるものです。

また、メールボックスの新規作成ウィザードなど、Exchange 管理センターと Outlook Web App の関連機能は、利用できなくなるか、使用するとエラーが発生するようになります。

ただし、Exchange 管理者は、トランスポート ルールなどの Exchange 固有のオブジェクトの作成および管理を行うことはできます。

Active Directory 分割型アクセス許可モデルの構成の詳細については、「[Exchange 2013 の分割型アクセス許可を構成する](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)」を参照してください。

ページのトップへ

