---
title: 'インプレース電子情報開示検索用のカスタム管理スコープを作成する: Exchange Online Help'
TOCTitle: インプレース電子情報開示検索用のカスタム管理スコープを作成する
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219746
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# インプレース電子情報開示検索用のカスタム管理スコープを作成する

 

_**適用先:** Exchange Online, Exchange Server 2013_

カスタム管理スコープを使用すれば、特定の人物またはグループに、インプレース電子情報開示を使用した Exchange 2013 組織または Exchange Online 組織内のメールボックスのサブセットの検索を許可することができます。たとえば、探索マネージャーが特定の場所または部門のユーザーのメールボックスしか検索できないようにする場合を考えます。これは、カスタム管理スコープを作成することによって実現できます。このカスタム管理スコープでは、検索可能なメールボックスを制御するための受信者フィルターが使用されます。受信者フィルター スコープでは、受信者の種類またはその他の受信者プロパティに基づいて特定の受信者を絞り込むためのフィルターが使用されます。

インプレース電子情報開示では、カスタム スコープ用の受信者フィルターを作成するために使用可能なユーザー メールボックスの唯一のプロパティが配布グループ メンバーシップです (実際のプロパティ名は *MemberOfGroup* です)。*CustomAttributeN*、*Department*、*PostalCode* などの他のプロパティを使用した場合は、カスタム スコープが割り当てられた役割グループのメンバーによって実行された検索が失敗します。

管理スコープの詳細については、以下を参照してください。

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

  - [管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - 前述したように、電子情報開示に使用する目的でカスタム受信者フィルター スコープを作成する場合は、受信者フィルターとしてグループ メンバーシップしか使用することができません。その他の受信者プロパティを電子情報開示検索のカスタム スコープの作成に使用することはできません。動的配布グループのメンバーシップも使用できないことに注意してください。

  - 手順 1 ～ 3 を実行して、探索マネージャーがカスタム管理スコープを使用した電子情報開示検索の検索結果をエクスポートできるようにします。

  - 探索マネージャーが検索結果をプレビューする必要がない場合は、手順 4 を省略できます。

  - 探索マネージャーが検索結果をコピーする必要がない場合は、手順 5 を省略できます。

## 手順 1: ユーザーを電子情報開示用の配布グループに整理する

組織内のメールボックスのサブセットを検索する、または、探索マネージャーが検索可能なソース メールボックスのスコープを絞り込むには、メールボックスのサブセットを 1 つ以上の配布グループにまとめる必要があります。手順 2 でカスタム管理スコープを作成するときに、これらの配布グループを受信者フィルターとして使用します。これにより、探索マネージャーは、指定されたグループのメンバーであるユーザーのメールボックスしか検索できません。

電子情報開示のために既存の配布グループを使用することも、新しい配布グループを作成することもできます。電子情報開示検索の範囲指定に使用可能な配布グループの作成方法に関するヒントについては、このトピックの最後にある「詳細情報」を参照してください。

## 手順 2: カスタム管理スコープを作成する

ここでは、配布グループのメンバーシップによって定義されたカスタム管理スコープを作成します (*MemberOfGroup* 受信者フィルターを使用)。このスコープが電子情報開示に使用される役割グループに適用された場合は、その役割グループのメンバーが、カスタム管理スコープの作成に使用された配布グループのメンバーであるユーザーのメールボックスを検索できます。

この手順では、Exchange 管理シェル コマンドを使用して Ottawa Users eDiscovery Scope という名前のカスタム スコープを作成します。また、カスタム スコープの受信者フィルターとして Ottawa Users という名前の配布グループを指定します。

1.  このコマンドを実行して、Ottawa Users グループのプロパティを取得し、次のコマンドで使用する変数に保存します。
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  このコマンドを実行して、Ottawa Users 配布グループのメンバーシップに基づいてカスタム管理スコープを作成します。
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    変数 **$DG** に格納された配布グループの識別名が新しい管理スコープの受信者フィルターの作成に使用されます。

## 手順 3: 管理役割グループを作成する

この手順では、新しい管理役割グループを作成し、手順 2 で作成したカスタム スコープを割り当てます。役割グループのメンバーがインプレース電子情報開示検索を実行し、メールボックスをインプレース保持または訴訟ホールドの対象にできるように、法的情報保留の役割とメールボックス検索の役割を追加します。この役割グループにメンバーを追加して、手順 2 でカスタム スコープを作成するために使用された配布グループのメンバーのメールボックスを検索できるようにすることもできます。

次の例では、Ottawa Users eDiscovery Managers セキュリティ グループがこの役割グループのメンバーとして追加されます。この手順には、シェルと EAC のどちらも使用できます。

## シェルを使用して管理役割グループを作成する

手順 2 で作成したカスタムのスコープを使用する新しい役割グループを作成するには、このコマンドを実行します。このコマンドはまた、法的情報保留の役割とメールボックス検索の役割を追加し、新しい役割グループのメンバーとして Ottawa Users eDiscovery Managers のセキュリティ グループを追加します。

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## EAC を使用して管理役割グループを作成する

1.  EAC で、**\[アクセス許可\]** \> **\[管理者の役割\]** に移動してから、**\[新規作成\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  **\[役割グループの新規作成\]** で、次の情報を入力します。
    
      - **\[名前\]**   新しい役割グループの記述名を入力します。この例では、**Ottawa Discovery Management** を使用します。
    
      - **書き込みスコープ**   手順 2 で作成したカスタム管理スコープを選択します。このスコープは、新しい役割のグループに適用されます。
    
      - **\[役割\]** **\[追加\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、新しい役割グループに **Legal Hold** 役割と **Mailbox Search** 役割を追加します。
    
      - **\[メンバー\]** **\[追加\]** ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、新しい役割グループのメンバーとして追加するユーザー、セキュリティ グループ、または役割グループを選択します。この例では、**Ottawa Users eDiscovery Managers** セキュリティ グループのメンバーが、**Ottawa Users** 配布グループのメンバーであるユーザーのメールボックスしか検索できません。

3.  **\[保存\]** をクリックして役割グループを作成します。
    
    ここで、操作が完了したときの **\[役割グループの新規作成\]** ウィンドウの表示例を示します。
    
    ![カスタム スコープ用の役割グループの新規作成](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "カスタム スコープ用の役割グループの新規作成")  

## (オプション) 手順 4: カスタム管理スコープの作成に使用される配布グループのメンバーとして探索マネージャーを追加する

この手順は、探索マネージャーが電子情報開示検索結果をプレビューできるようにする場合にのみ実行する必要があります。

このコマンドを実行して、Ottawa Users 配布グループのメンバーとして Ottawa Users eDiscovery Managers セキュリティ グループを追加します。

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

EAC を使用して、配布グループにメンバーを追加することもできます。詳細については、「[配布グループの作成と管理](create-and-manage-distribution-groups-exchange-2013-help.md)」を参照してください。

## (オプション) 手順 5: カスタム管理スコープの作成に使用される配布グループのメンバーとして探索メールボックスを追加する

この手順は、探索マネージャーが電子情報開示検索結果をコピーできるようにする場合にのみ実行する必要があります。

このコマンドを実行して、Ottawa Users 配布グループのメンバーとして Ottawa Discovery Mailbox という名前の探索メールボックスを追加します。

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"


> [!NOTE]
> 探索メールボックスを開いて、検索結果を表示するには、探索マネージャーに、探索メールボックスに対するフル アクセスのアクセス許可を割り当てる必要があります。詳細については、「<A href="create-a-discovery-mailbox-exchange-2013-help.md">探索メールボックスの作成</A>」を参照してください。



## 正常な動作を確認する方法

ここでは、電子情報開示用のカスタム管理スコープの実装が正常に行われたかどうかを確認する方法を示します。確認する場合は、必ず、電子情報開示検索を実行するユーザーが、カスタム管理スコープを使用する役割グループのメンバーになっている必要があります。

  - 電子情報開示検索を作成して、カスタム管理スコープの作成時に検索対象メールボックスのソースとして使用した配布グループを選択します。すべてのメールボックスが正常に検索されるはずです。

  - 電子情報開示検索を作成して、カスタム管理スコープの作成に使用された配布グループのメンバーではないユーザーのメールボックスを検索します。探索マネージャーはカスタム管理スコープの作成に使用された配布グループのメンバーであるユーザーのメールボックスしか検索できないため、この検索は失敗するはずです。この場合は、「現在のユーザーにはメールボックスにアクセスするためのアクセス許可が付与されていないため、メールボックス \<*name of mailbox*\> を検索できません」のようなエラーが返されます。

  - 電子情報開示検索を作成して、カスタム管理スコープの作成に使用された配布グループのメンバーであるユーザーのメールボックスを検索します。同じ検索に、メンバーではないユーザーのメールボックスも含めます。この検索は部分的に成功するはずです。カスタム管理スコープの作成に使用された配布グループのメンバーのメールボックスが正常に検索されるはずです。グループのメンバーではないユーザーのメールボックスの検索は失敗するはずです。

## 詳細情報

  - このシナリオでは、配布グループがメッセージの配信ではなく、電子情報開示検索の範囲指定に使用されるため、電子情報開示用の配布グループを作成して構成するときに以下を考慮してください。
    
      - グループ所有者だけがグループに対してメンバーを追加または削除できるように、クローズド メンバーシップを使用して配布グループを作成します。シェルでグループを作成する場合は、`MemberJoinRestriction closed` 構文と `MemberDepartRestriction closed` 構文を使用します。
    
      - グループに送信されるメッセージが、メッセージを承認または拒否可能なグループ モデレーターに最初に送信されるようにグループ モデレートを有効にします。シェルでグループを作成する場合は、`ModerationEnabled $true` 構文を使用します。EAC を使用する場合は、グループの作成後にモデレートを有効にできます。
    
      - 組織の共有アドレス帳で配布グループを非表示にします。グループの作成後に、EAC または **Set-DistributionGroup** コマンドレットを使用します。シェルを使用する場合は、`HiddenFromAddressListsEnabled $true` 構文を使用します。
    
    次の例では、最初のコマンドがクローズド メンバーシップとモデレートが有効になっている配布グループを作成します。2 番目のコマンドが共有アドレス帳でグループを非表示にします。
    
        New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    
        Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    
    配布グループの作成と管理の詳細については、「[配布グループの作成と管理](create-and-manage-distribution-groups-exchange-2013-help.md)」を参照してください。

  - 電子情報開示に使用されるカスタム管理スコープ用の受信者フィルターとして使用できるのは配布グループ メンバーシップのみですが、他の受信者プロパティを使用してその配布グループにユーザーを追加することができます。ここで、**Get-Mailbox** コマンドレットと **Get-Recipient** コマンドレットを使用して、共通のユーザー属性またはメールボックス属性に基づいて特定のユーザー グループを返す例を示します。
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"

  - 前述の例を使用して、配布グループにユーザー グループを追加するための **Add-DistributionGroupMember** コマンドレットに使用可能な変数を作成することができます。次の例では、最初のコマンドが、ユーザー アカウント内の *Department* プロパティに **Vancouver** の値が設定されたすべてのユーザー メールボックスを含む変数を作成します。2 番目のコマンドがこれらのユーザーを Vancouver Users 配布グループに追加します。
    
        $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    
        $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}

  - **Add-RoleGroupMember** コマンドレットを使用して、電子情報開示検索の範囲指定に使用される既存の役割グループにメンバーを追加できます。たとえば、次のコマンドは、Ottawa Discovery Management 役割グループにユーザー admin@ottawa.contoso.com を追加します。
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    EAC を使用して役割グループにメンバーを追加することもできます。詳細については、[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md) の「役割グループにメンバーを追加する」セクションを参照してください。

  - Exchange Online では、電子情報開示用のカスタム管理スコープは非アクティブなメールボックスの検索には使用できません。これは、非アクティブなメールボックスは配布グループのメンバーになれないためです。たとえば、ユーザーが電子情報開示のカスタム管理スコープの作成に使用された配布グループのメンバーであるとします。そのユーザーが退職したため、(メールボックスを訴訟ホールドまたはインプレース保持の対象としてから、対応する Office 365 ユーザー アカウントを削除して) メールボックスを非アクティブにしたとします。結果として、そのユーザーは、電子情報開示用のカスタム管理スコープの作成に使用されたグループを含む、すべての配布グループからメンバーとして削除されます。証拠開示管理者 (カスタム管理スコープが割り当てられている役割グループのメンバー) が非アクティブなメールボックスを検索しようとすると、検索は失敗します。非アクティブなメールボックスを検索するには、証拠開示管理者は、証拠開示管理の役割グループまたは組織全体を検索するアクセス許可を持つ任意の役割グループのメンバーである必要があります。
    
    非アクティブなメールボックスの詳細については、「[Exchange Online の非アクティブなメールボックス](https://technet.microsoft.com/ja-jp/library/dn798632\(v=exchg.150\))」を参照してください。

