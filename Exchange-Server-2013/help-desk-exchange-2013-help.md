---
title: 'Help Desk (ヘルプ デスク): Exchange 2013 Help'
TOCTitle: Help Desk (ヘルプ デスク)
ms:assetid: e7958752-22e4-4155-a2fc-948099dec6f7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876949(v=EXCHG.150)
ms:contentKeyID: 49896532
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Help Desk (ヘルプ デスク)

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

ヘルプ デスク管理役割グループは、Microsoft Exchange Server 2013 の役割ベースのアクセス制御 (RBAC) というアクセス許可モデルを構成するいくつかの組み込みの役割グループの 1 つです。役割グループには、指定された一連のタスクの実行に必要なアクセス許可を含む 1 つ以上の管理役割が割り当てられます。役割グループのメンバーには、役割グループに割り当てられた管理役割に対するアクセス権が付与されます。役割グループの詳細については、「[管理役割グループについて](understanding-management-role-groups-exchange-2013-help.md)」を参照してください。

"Help Desk/ヘルプ デスク" 役割グループのメンバーであるユーザーは、Exchange 2013 受信者の制限された受信者管理を実行できます。

既定では、ヘルプ デスク役割グループによって、メンバーは組織内のすべてのユーザーの Outlook Web App オプションを表示および変更できます。これらのオプションにはユーザーの表示名、電話番号などの変更も含まれます。これらのオプションには、メールボックスのサイズ変更や、メールボックスのあるメールボックス データベースの構成などのような、Outlook Web App オプションで使用できないオプションは含まれていません。

この役割グループのメンバーは、ユーザーが変更できる Outlook Web App オプションを変更できるだけです。これはつまりユーザーが自分の表示名を変更できる場合、ヘルプ デスク役割グループのメンバーもまた、そのユーザーの表示名を変更できるということです。ただし、ユーザーが自分の表示名の変更を許可されていない場合、ヘルプ デスク役割グループのメンバーもまた、そのユーザーの表示名を変更できません。


> [!NOTE]
> ヘルプ デスク役割グループのメンバーが変更できる Outlook Web App オプションの制限事項は、Exchange 管理センター (EAC) によって強制されます。ヘルプ デスク役割グループのメンバーが Exchange 管理シェルにアクセスできる場合、そのメンバーはすべてのユーザーの Outlook Web App オプションを変更できます。ヘルプ デスク役割グループのメンバーを誰にするか、またそのメンバーにシェルへのアクセスも許可するかどうかについて、慎重に検討する必要があります。



非常に多くの種類の異なる組織があるため、ヘルプ デスク役割グループが他のタスクを有効にすることはありません。代わりにこの役割グループに管理役割を追加することで、組織のニーズに合うヘルプ デスク役割グループを作成できます。たとえば、ヘルプ デスク役割グループのメンバーがメールボックス、メール連絡先、およびメールが有効なユーザーを管理できるようにするには、この役割グループにメール受信者の管理役割を割り当てます。この役割グループに管理役割を追加する方法の詳細については、このトピックで後に説明する「役割グループのカスタマイズ」のセクションを参照してください。

RBAC の詳細については、「[役割ベースのアクセス制御について](understanding-role-based-access-control-exchange-2013-help.md)」を参照してください。

## 役割グループ メンバーシップ

この役割グループに対してメンバーを追加または削除する場合は、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」を参照してください。

既定では、"Organization Management" 役割グループのメンバーのみ、この役割グループに対してメンバーを追加または削除できます。役割グループの委任をさらに追加する方法の詳細については、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループの委任の追加または削除」を参照してください。

次のコマンドを使用して、この役割グループのメンバーであるユーザーまたはユニバーサル セキュリティ グループ (USG) の一覧を表示できます。

```powershell
Get-RoleGroupMember "Help Desk"
```

役割グループのメンバーの詳細については、「[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)」の「[View the members of a role group](manage-role-group-members-exchange-2013-help.md)」を参照してください。

## 役割グループのカスタマイズ

この役割グループには、既定で管理役割が割り当てられます。含まれている役割の一覧については、「この役割グループに割り当てられている管理役割」をご覧ください。組織のニーズに合わせて、この役割グループに対して役割の割り当てを追加または削除できます。

Exchange 2013 で提供される役割グループは、よりきめ細かなタスクに合うように設計されています。役割を役割グループに割り当てることで、その役割グループのメンバーがその役割に関連付けられているタスクを実行できるようにできます。たとえば、"Journaling /ジャーナリング" 役割では、ジャーナリング エージェントとジャーナリング ルールを管理できます。役割グループに役割を割り当てる方法について詳しくは、「[管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)」をご覧ください。

この役割グループに割り当てられる役割には、既定の管理スコープが与えられます。管理スコープは、役割グループのメンバーが表示または変更できる Exchange オブジェクトを決定します。役割と役割グループ間の割り当てに関連付けられているスコープは、変更できます。たとえば、役割グループのメンバーのみが特定の組織単位または特定の場所の受信者を変更できるようにする場合に、この操作を行うことができます。管理のスコープについて詳しくは、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」をご覧ください。

この役割グループのカスタマイズ方法について詳しくは、次のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)

役割グループを作成し、この役割グループに割り当てられている役割の一部を新しい役割グループに割り当てる場合は、「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループの作成」を参照してください。

## この役割グループに割り当てられている管理役割

次の表は、この役割グループに割り当てられるすべての管理役割、および各役割の割り当ての次の属性の一覧です。

  - **正規割り当て**   役割グループのメンバーが、関連付けられている管理役割によって利用可能にされた管理役割エントリにアクセスできるようにします。

  - **委任割り当て**   役割グループのメンバーが、特定の役割を他の役割グループ、役割割り当てポリシー、ユーザー、または USG に割り当てられるようにします。

  - **受信者の読み取りスコープ**   Active Directory から読み取りできる役割グループの受信者オブジェクト メンバーを決定します。

  - **受信者の書き込みスコープ**   Active Directory で変更できる役割グループの受信者オブジェクト メンバーを決定します。

  - **構成の読み取りスコープ**   Active Directory から読み取りできる役割グループの構成オブジェクトとサーバー オブジェクトのメンバーを決定します。

  - **構成の書き込みスコープ**   Active Directory で変更できる役割グループの構成オブジェクトとサーバー オブジェクトのメンバーを決定します。

役割の割り当てと管理スコープについて詳しくは、次のトピックを参照してください。

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

### この役割グループに割り当てられている管理役割

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>管理役割</th>
<th>正規の割り当て</th>
<th>委任の割り当て</th>
<th>受信者の読み取り範囲</th>
<th>受信者の書き込み範囲</th>
<th>構成の読み取り範囲</th>
<th>構成の書き込み範囲</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="user-options-role-exchange-2013-help.md">&quot;User Options/ユーザー オプション&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">&quot;View-Only Recipients/表示専用受信者&quot; 役割</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>

