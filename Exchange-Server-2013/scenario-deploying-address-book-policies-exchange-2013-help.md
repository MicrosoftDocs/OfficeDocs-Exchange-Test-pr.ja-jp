---
title: 'シナリオ: アドレス帳ポリシーの展開: Exchange 2013 Help'
TOCTitle: 'シナリオ: アドレス帳ポリシーの展開'
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 49896294
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# シナリオ: アドレス帳ポリシーの展開

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

## 展開シナリオ

次の 3 つのシナリオは、3 つのタイプの組織で可能な展開ソリューションについて説明しています。この他にも多くのシナリオがありますが、ここでは最もよく使用されているシナリオについて取り上げます。これらのシナリオのアドレス一覧とグローバル アドレス一覧 (GAL) は、カスタム属性など、オブジェクトを理論的にグループ化するフィルターに基づいて作成されました。

## シナリオ 1: 2 つの個別の企業 - 1 つの Exchange 組織

このシナリオは、インフラストラクチャを共有するが、指揮系統は共有せず、共通の従業員がいない政府機関、事業部、部署に適用できます。また、事業部には、セキュリティやプライバシーに関する特殊な懸念事項はありません。このシナリオでは、2 つのアドレス帳ポリシー (ABP) が作成され、従業員が GAL または他の配布グループのメンバーシップを閲覧する場合、同じ組織のメンバーのみを閲覧できます。また、組織全体にまたがる配布グループのメンバーとなるユーザーはいません。

![2 つの別々の会社に対応するアドレス帳ポリシー](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "2 つの別々の会社に対応するアドレス帳ポリシー")

Contoso および Humungous Insurance の ABP は、カスタム属性などのフィルターでオブジェクトをグループ化する受信者フィルターを使用して作成された、次のアドレス一覧、グローバル アドレス一覧、会議室一覧、OAB を使用して作成されました。この 2 つの企業は交流のない個別の企業であるため、共通のアドレス一覧はありません。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humungous Insurance</p></td>
</tr>
<tr class="even">
<td><p>&quot;Address Lists/アドレス一覧&quot;</p></td>
<td><p>AL_CON_Groups</p>
<p>AL_CON_Users</p>
<p>AL_CON_Contacts</p></td>
<td><p>AL_HI_Groups</p>
<p>AL_HI_Users</p>
<p>AL_HI_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>グローバル アドレス一覧</p></td>
<td><p>GAL_CON</p></td>
<td><p>GAL_HI</p></td>
</tr>
<tr class="even">
<td><p>会議室アドレス一覧</p></td>
<td><p>AL_CON_Rooms</p></td>
<td><p>AL_HI_Rooms</p></td>
</tr>
<tr class="odd">
<td><p>オフライン アドレス帳 (OAB)</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## シナリオ 2: CEO が共通の 2 つの企業

このシナリオでは、Fabrikam と Tailspin Toys が、同じ Exchange 組織と同じ CEO を共有します。CEO は、2 つの企業間で唯一の共通のユーザーです。このシナリオでは、次の特性を持つ 3 つの ABP が必要になります。

  - Tailspin Toys のユーザーは、GAL の閲覧時にのみ Tailspin Toys ユーザーを閲覧できる。

  - Fabrikam のユーザーは、GAL の閲覧時にのみ Fabrikam ユーザーを閲覧できる。

  - 各企業に、各企業の幹部と CEO が含まれている SeniorLeaders 配布グループがある。

  - CEO のグループ メンバーを閲覧するユーザーは、ユーザーの会社に属するグループのみを閲覧できる。自社以外のグループは閲覧できません。

  - 3 つの ABP、**Fab**、**Tail**、および **CEO** が作成されます。

![2 つの企業に一人の CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "2 つの企業に一人の CEO")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>CEO</p></td>
</tr>
<tr class="even">
<td><p>アドレス一覧</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p></td>
<td><p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p>
<p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>グローバル アドレス一覧</p></td>
<td><p>GAL_FAB</p></td>
<td><p>GAL_TAIL</p></td>
<td><p>既定の GAL</p></td>
</tr>
<tr class="even">
<td><p>会議室アドレス一覧</p></td>
<td><p>AL_FAB_Rooms</p></td>
<td><p>AL_TAIL_Rooms</p></td>
<td><p>既定のすべての会議室</p></td>
</tr>
<tr class="odd">
<td><p>オフライン アドレス帳 (OAB)</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>既定の OAB</p></td>
</tr>
</tbody>
</table>


CEO が各組織の配布グループに追加され、各企業の ABP の範囲内にある場合、CEO が各企業から閲覧可能になります。CEO は、両社にまたがる配布グループを作成でき、各社の GAL に表示されます。ただし、配布グループのメンバーが閲覧できるのは、自分の組織内のグループのメンバーのみです。

## シナリオ 3: 教育

このシナリオは、クラス単位で生徒のプライバシーを確保する必要のある学校や大学に当てはまります。この教育シナリオには、次の特性があります。

  - 各クラスの生徒は、自分のクラスの他の生徒と教師、校長のみを閲覧できる。

  - 教師は、自分のクラスの生徒のみを閲覧できる。

  - 教師は、他のすべての教師と校長を閲覧できる。

  - 各クラスの父兄および教職員用の配布グループが作成される。

![アドレス帳ポリシーの教育シナリオ](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "アドレス帳ポリシーの教育シナリオ")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Students_ClassA</p></td>
<td><p>Teachers_ClassA</p></td>
<td><p>校長</p></td>
</tr>
<tr class="even">
<td><p>&quot;Address Lists/アドレス一覧&quot;</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>AL_ClassA</p>
<p>AL_ClassB</p>
<p>AL_AllTeachers</p>
<p>AL_AllStudents</p>
<p>AL_AllGroups</p></td>
</tr>
<tr class="odd">
<td><p>グローバル アドレス一覧</p></td>
<td><p>GAL_StudentsClassA</p></td>
<td><p>GAL_TeachersClassA</p></td>
<td><p>GAL_Everyone</p></td>
</tr>
<tr class="even">
<td><p>会議室アドレス一覧</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>既定のすべての会議室</p></td>
</tr>
<tr class="odd">
<td><p>オフライン アドレス帳 (OAB)</p></td>
<td><p>OAB_StudentsClassA</p></td>
<td><p>OAB_TeachersClassA</p></td>
<td><p>既定の OAB</p></td>
</tr>
</tbody>
</table>


## 考慮事項とベスト プラクティス

組織内で ABP を使用する際は、以下のことを考慮してください。

  - ABP を正しく動作させるには、ABP を割り当てるユーザー メールボックスが Exchange 2010 SP3 サーバー上または Exchange 2013 サーバー上にある必要があります。

  - Exchange 2010 クライアント アクセス サーバーの役割をグローバル カタログ サーバー上で実行しないでください。実行すると、Microsoft Exchange アドレス帳サービスではなく、Active Directory が NSPI (Name Service Provider Interface) に使用されます。Exchange 2013 サーバーの役割をグローバル カタログ サーバー上で実行し、ABP を正しく動作させることは可能ですが、ドメイン コントローラーに Exchange をインストールすることはお勧めしません。

  - 階層型アドレス帳 (HAB) と ABP を同時に使用することはできません。詳細については、「[階層型アドレス帳](https://docs.microsoft.com/ja-jp/exchange/address-books/hierarchical-address-books/hierarchical-address-books)」を参照してください。

  - ABP を割り当てられているどのユーザーも、各自の GAL に含まれている必要があります。

  - LDAP によってクライアント アプリケーションが Active Directory に直接アクセスできるようにすると、クライアント アプリケーションは ABP に組み込まれたロジックをバイパスするようになります。Outlook for Mac 2011 と Entourage 2008 はダイレクト LDAP クエリを使用して Active Directory にアクセスするため、ドメイン コントローラーまたはグローバル カタログ サーバーが設定されているか、または自動検出サービスによって提供される場合、Outlook for Mac 2011 と Entourage 2008 のクライアント アプリケーションで ABP は正しく動作しません。Outlook for Mac 2011 は、EWS またはローカルの OAB を使用してディレクトリ情報にアクセスします。ただし、Outlook for Mac 2011 が LDAP サービスに直接アクセス可能な場合は、LDAP サービスに直接アクセスします。

  - ABP で使用される GAL には、少なくとも、会議室アドレス一覧など、ABP で定義され、設定されたアドレス一覧がすべて含まれています。同じ ABP 内のどのアドレス一覧よりも含まれているオブジェクト数が少ない GAL は作成しないでください。

  - 仮想組織の境界をまたがずに配布グループを作成することをお勧めします。複数の仮想組織のメンバーを含めた配布グループを作成すると、次のような問題が発生します。
    
      - グループ メンバーが配布グループにメールを送信する際に配信済みメッセージまたは開封確認メッセージをリクエストすると、他の仮想組織のグループ メンバーの電子メール アドレスを閲覧できるようになります。
    
      - 暗号化されたメッセージが配布グループに送信される際に、一部のグループ メンバーが有効なデジタル ID を持っていないと、送信者は、有効な ID を持っていないメンバーの合計人数とその電子メール アドレスの一覧が記載された警告メッセージを受け取ります。ただし、有効なデジタル ID を持っていないこうしたメンバーの一部が送信者と別の組織に属している場合は、警告メッセージには、正確な人数が記載されますが、別の組織のメンバーの電子メール アドレスは記載されません。そのため、合計人数とメンバーのアドレスの一覧は一致しません。
        
        たとえば、配布グループに機関 A と機関 B の 2 つの組織から合計 5 人のメンバーが含まれているとします。3 人のグループ メンバーは機関 A に属し、そのうち 1 人は無効なデジタル ID を持っています。残りの 2 人は機関 B に属し、2 人とも無効な ID を持っています。機関 A のメンバーが暗号化されたメッセージを配布グループに送信すると、そのメンバーは、有効なデジタル ID を持っていない受信者の合計人数が 3 人と記載された警告メッセージを受け取ります。しかし、その警告メッセージに記載される電子メール アドレスは、機関 A の受信者の電子メール アドレスのみです。
    
      - ABP は、**Get-Group** コマンドレットには適用されません。そのため、**Get-Group** を実行できるユーザーまたはプロセスは、アクセスできるグループのメンバー全員を閲覧できます。
        
        ユーザーが Outlook Web App を使用してグループを管理できないように、OWA オプションのグループ管理設定を変更することをお勧めします。ユーザーが OWA オプションを使用してグループを管理できないようにするには、ユーザーを MyDistributionGroupMembership RBAC の役割から除外します。詳細については、「[MyDistributionGroupMembership 役割](mydistributiongroupmembership-role-exchange-2013-help.md)」を参照してください。
    
      - ユーザーが Outlook または Outlook Web App を使用してグループを管理できるようにする場合は、グループ オーナーにグループ メンバーシップ一覧に対する完全な可視性が必要です。

  - すべての ABP に、会議室アドレス一覧が含まれている必要があります。ただし、その組織が会議室アドレス一覧を使用しない場合は、既定の空の会議室アドレス一覧を作成できます。

  - ABP の展開によって、仮想組織のユーザーが他の仮想組織のユーザーに電子メールを送信できないようにすることはできません。ユーザーが組織外に電子メールを送信しないようにする場合は、トランスポート ルールを作成することをお勧めします。たとえば、Contoso のユーザーが Fabrikam のユーザーからメッセージを受信できず、Fabrikam の幹部が Contoso のユーザーにメッセージを送信できるようにトランスポート ルールを作成するには、次のシェル コマンドを実行します。
    
        New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com

  - Lync クライアントに ABP と同様の機能を適用するには、特定のユーザー オブジェクトに `msRTCSIP-GroupingID` 属性を設定します。詳細については、「[PartitionByOU から msRTCSIP-GroupingID への置き換え](https://go.microsoft.com/fwlink/p/?linkid=232306)」を参照してください。

## 一般的な展開手順

## アドレス一覧セグメンテーションから ABP への移行

現在、(ホワイト ペーパー「[Exchange 2007 での仮想組織とアドレス一覧セグメンテーションの構成](https://go.microsoft.com/fwlink/p/?linkid=109601)」の手順に従って) Exchange 2007 アドレス一覧セグメンテーションを構成している場合は、「[Exchange Server 2007 アドレス一覧セグメンテーションから Exchange Server 2010 アドレス帳ポリシーへの移行](https://go.microsoft.com/fwlink/p/?linkid=235967)」で説明されている手順に従って、最初に Exchange Server 2010 に移行する必要があります。この手順には、一部組織のダウンタイムが伴うため、適宜計画を立てる必要があります。

## ABP の新規展開

組織で Exchange 2013 ABP を展開していて、Exchange 2007 アドレス一覧セグメンテーションを使用していない場合、次の手順に従って組織内に ABP を展開できます。

このセクションの手順で、「シナリオ 2: シナリオ 2: CEO が共通の 2 つの企業」について順を追って説明します。シナリオ 2: CEO が共通の 2 つの企業。このシナリオでは、2 つの会社 (Fabrikam と Tailspin Toys) は、CEO と幹部が共通の別個の企業です。

## 手順 1:アドレス帳ポリシー ルーティング エージェントをインストールおよび構成する

ABP を使用しており、個別の仮想組織内のユーザーにお互いの個人情報の可能性がある内容を表示したくない場合は、アドレス帳ポリシー ルーティング エージェントをオンにします。アドレス帳ポリシー ルーティング エージェントは、メールボックス サーバー上で動作するトランスポート エージェントで、受信者が組織内でどのように解決されるかを制御します。アドレス帳ポリシー ルーティング エージェントがインストールおよび構成されると、異なる GAL を割り当てられたユーザーは外部受信者として表示されるようになり、この場合、外部受信者の連絡先カードは表示できません。

詳細な手順については、「[アドレス帳ポリシー ルーティング エージェントをインストールおよび構成する](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)」を参照してください。

## 手順 2:仮想組織の分割

組織を分割する方法を策定する必要があります。仮想組織を分割する際に、次のような理由から、メールボックス、連絡先、グループに、既定の条件属性 (\[会社名\]、\[部署\]、\[都道府県\] など) ではなく、CustomAttribute1-15 プロパティを使用することをお勧めします。

  - オブジェクトのすべてのタイプの受信者が、Active Directory 内に既定の条件属性を持つわけではありません。たとえば、配布グループと動的配布グループは、会社、部署、都道府県といった属性をサポートしていません。

  - 一部の受信者のコマンドレットでは、すべての既定の条件属性は表示されません。たとえば、メール ユーザー、連絡先、配布グループ、メールが有効なパブリック フォルダーのコマンドレットでは、*Company*、*department*、および *StateOrProvince* パラメーターは表示されません。

  - 既定の条件属性を使用して受信者を分割するには、複数のコマンドレットが必要です。たとえば、ユーザー メールボックスに *Company*、*Department*、*StateOrProvince* のタグを設定するには、**New-Mailbox** または **Set-Mailbox** コマンドレットを実行した後に、Set-User を実行する必要があります。

  - 各受信者タイプの Set-\* コマンドレットでは、*CustomAttributeX* パラメーターがすべて表示されるため、このタイプについては、1 つの Set- コマンドレットですべてのセグメンテーションを完了できます。

  - CustomAttributeX 属性は、組織をカスタマイズするために明示的に予約され、組織の管理者によって完全に制御されます。

組織を分割する際に実装を考慮すべきもう 1 つのベスト プラクティスとして、配布グループと動的配布グループの名前に企業識別子を使用する例があります。Exchange には、配布グループ名にサフィックスまたはプレフィックスを自動的に追加するグループの名前付けポリシーがあります。このポリシーは、配布グループを作成しているユーザーの多くの属性 (配布グループの作成者の \[会社名\]、\[都道府県\]、\[役職\]、CustomAttribute1 から CustomAttribute15 など) に基づいてサフィックスまたはプレフィックスを追加します。グループの名前付けポリシーは、ユーザーが独自の配布グループを作成できるようにする場合に、特に重要です。詳細については、「[配布グループ名前付けポリシーを作成する](https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy)」を参照してください。

グループ名前付けポリシーは動的配布グループに適用されないため、これらのグループを手動で分割し、名前付けポリシーを手動で適用する必要があります。

## 手順 3:アドレス一覧、GAL、および OAB の作成

アドレス一覧とグローバル アドレス一覧を作成する際に、ConditionalCompany や ConditionalCustomAttribute5 など、"IncludedRecipient" と "ConditionalX" は使用しないでください。代わりに、受信者フィルターを使用してください。受信者フィルターの作成には、シェルを使用する必要があります。受信者フィルターの詳細については、「[エッジ トランスポート サーバー上での受信者フィルター処理](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)」を参照してください。

ABP を作成する際に、ユーザーが Outlook または Outlook Web App でどのようにアドレス一覧を閲覧できるようにするかに基づいて、複数のアドレス一覧を作成します。この組織には、次の 4 つのアドレス一覧があります。

  - AL\_FAB\_Users\_DGs

  - AL\_FAB\_Contacts

  - AL\_TAIL\_Users\_DGs

  - AL\_TAIL\_Contacts

この例では、アドレス一覧 list AL\_TAIL\_Users\_DGs を作成します。このアドレス一覧には、CustomAttribute15 が TAIL となっているすべてのユーザーと配布グループが含まれています。

    New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}

受信者フィルターを使用したアドレス一覧の作成の詳細については、「[受信者フィルターを使用したアドレス一覧の作成](https://docs.microsoft.com/ja-jp/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list)」を参照してください。

ABP を作成するには、会議室アドレス一覧を指定する必要があります。組織に会議室や備品用メールボックスなどのリソース メールボックスがない場合、空の会議室アドレス一覧を作成することをお勧めします。次の例では、組織に会議室メールボックスがないため、空の会議室アドレス一覧を作成します。

    New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}

ただし、このシナリオでは、Fabrikam と Contoso 両社に会議室メールボックスがあります。この例では、CustomAttribute15 が FAB の受信者フィルターを使用して Fabrikam の会議室一覧を作成します。

    New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}

ABP で使用されるグローバル アドレス一覧は、アドレス一覧のスーパーセットである必要があります。ABP 内のどのアドレス一覧よりも含まれているオブジェクトが少ない GAL は作成しないでください。この例では、Tailspin Toys のグローバル アドレス一覧を作成します。これには、アドレス一覧と会議室アドレス一覧内に存在するすべての受信者が含まれています。

    New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}

詳細については、「[グローバル アドレス一覧の作成](https://docs.microsoft.com/ja-jp/exchange/address-books/address-lists/create-global-address-list)」を参照してください。

OAB を作成する場合、New-OfflineAddressBook または Set-OfflineAddressBook の *AddressLists* パラメーターの入力時に適切な GAL を含めて、意図せずエントリが漏れないようにします。基本的に、New/Set-OfflineAddressBook の AddressLists パラメーターにアドレス一覧を指定することで、ユーザーが閲覧するエントリのセットをカスタマイズしたり、OAB のダウンロード サイズを削減したりできます。ただし、ユーザーが OAB の GAL エントリのフル セットを閲覧できるようにする場合は、必ず AddressLists パラメーターに GAL を含めてください。

この例では、OAB\_FAB という名前の Fabrikam の OAB を作成します。

    New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"

詳細については、「[オフライン アドレス帳の作成](https://docs.microsoft.com/ja-jp/exchange/address-books/offline-address-books/create-offline-address-book)」を参照してください。

## 手順 4:ABP の作成

必要なオブジェクトをすべて作成した後に、ABP を作成できます。この例では、ABP\_TAIL という名前の ABP を作成します。

    New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"

詳細については、「[アドレス帳ポリシーの作成](https://docs.microsoft.com/ja-jp/exchange/address-books/address-book-policies/create-an-address-book-policy)」を参照してください。

## 手順 5:メールボックスに ABP を割り当てる

このプロセスの最終ステップが、ABP のユーザーへの割り当てです。ユーザーのアプリケーションがクライアント アクセス サーバーの Microsoft Exchange アドレス帳サービスに接続すると、ABP が有効になります。ABP をユーザー アカウントに適用する際に、ユーザーがすでに Outlook または Outlook Web App に接続している場合は、新しいアドレス一覧と GAL を閲覧する前に、クライアント アプリケーションを再起動する必要があります。

この例では、ABP\_FAB を、CustomAttribute15 が "FAB" となっているすべてのメールボックスに割り当てます。

    Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"

詳細については、「[メール ユーザーへのアドレス帳ポリシーの割り当て](https://docs.microsoft.com/ja-jp/exchange/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users)」を参照してください。

