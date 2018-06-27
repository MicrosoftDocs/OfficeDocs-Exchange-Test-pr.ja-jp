---
title: '階層型アドレス帳を有効または無効にする: Exchange Online Help'
TOCTitle: 階層型アドレス帳を有効または無効にする
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 49896426
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 階層型アドレス帳を有効または無効にする

 

_**適用先:**Exchange Online, Exchange Server 2013_

Microsoft Outlook 2010 以降でエンド ユーザーが使用できる機能である階層型アドレス帳 (HAB) を構成できます。HAB では、ユーザーは上下関係や管理構造に基づく組織階層を使用して、Exchange 組織の受信者を検索できます。HAB の詳細については、「[階層型アドレス帳](hierarchical-address-books-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 時間。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「配布グループ」。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - 開始する前に、「[階層型アドレス帳](hierarchical-address-books-exchange-2013-help.md)」トピックを読んでください。自分の Exchange 組織に HAB が適しているかどうかを理解する必要があります。

  - 組織単位 (OU)、グループ、ユーザー、および連絡先が、現在 Exchange 組織内でどのように構成されているか理解している。

  - 次の表にある HAB の構成に必要なコマンドレットおよび関連するパラメーターについて理解している。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>コマンドレット</th>
    <th>パラメーター</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/ja-jp/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/ja-jp/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/ja-jp/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/ja-jp/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して HAB を有効にする


> [!NOTE]
> EAC を使用して HAB を有効にすることはできませんが、有効にした後で EAC を使用して組織階層内のグループのメンバーシップを管理できます。



この例では、HAB に "HAB" という OU が作成されます。組織のドメイン名は "Contoso-dom" で、階層内の最上位の組織 (ルート組織) の名前は "Contoso,Ltd" となります。"Contoso,Ltd" の下に、子組織として "Corporate Office"、"Product Support Organization"、および "Sales & Marketing Organization" という下位グループが作成されます。また、"Corporate Office" の下に、子組織として "Human Resources"、"Accounting Group"、および "Administration Group" というグループが作成されます。

配布グループの作成の詳細については、「[配布グループの作成と管理](create-and-manage-distribution-groups-exchange-2013-help.md)」を参照してください。

1.  "Contoso" 組織内に "HAB" という名前の OU を作成します。Active Directory ユーザーとコンピューターを使用するか、コマンド プロンプトで次のように入力します。
    

    > [!NOTE]
    > または、Exchange フォレスト内の既存の OU を使用できます。

    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    

    > [!NOTE]
    > 詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=198986">新しい組織単位を作成する</A>」を参照してください。



2.  HAB に "Contoso,Ltd" というルート配布グループを作成します。
    

    > [!NOTE]
    > このトピックの目的上、例ではシェルを使用しています。ただし、EAC を使用して配布グループを作成することもできます。詳細については、「<A href="create-and-manage-distribution-groups-exchange-2013-help.md">配布グループの作成と管理</A>」を参照してください。

    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  "Contoso,Ltd" を HAB のルート組織として指定します。
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  HAB の他の層に配布グループを作成します。この例では、以下のグループを作成します。"Corporate Office"、"Product Support Organization"、"Sales & Marketing Organization"、"Human Resources"、"Accounting Group"、および "Administration Group"。この例では、"Corporate Office" という配布グループを作成します。
    

    > [!NOTE]
    > このトピックの目的上、例ではシェルを使用しています。ただし、EAC を使用して配布グループを作成することもできます。詳細については、「<A href="create-and-manage-distribution-groups-exchange-2013-help.md">配布グループの作成と管理</A>」を参照してください。

    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  各グループを HAB のメンバーとして指定します。この例では、階層型グループとして次のグループを指定します。"Contoso, Ltd"、"Corporate Office"、"Product Support Organization"、"Sales & Marketing Organization"、"Human Resources"、"Accounting Group"、および "Administration Group"。この例では、"Contoso,Ltd" という配布グループを HAB のメンバーとして指定します。
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  各下位グループをルート組織のメンバーとして追加します。この例では、"Corporate Office"、"Product Support Organization"、および "Sales & Marketing Organization" という配布グループが、ルート組織 "Contoso,Ltd" のメンバーとして HAB に追加されます。この例では、"Corporate Office" という配布グループが "Contoso,Ltd" というルート配布グループのメンバーとして追加されます。
    

    > [!NOTE]
    > この例では、配布グループのエイリアスを使用します。

    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  "Corporate Office" という配布グループの各下位グループを、グループのメンバーとして追加します。この例では、"Human Resources"、"Accounting Group"、および "Administration Group" という配布グループが、"Corporate Office" という配布グループのメンバーとして追加されます。この例では、"Human Resources" という配布グループが "Corporate Office" という配布グループのメンバーとして追加されます。
    

    > [!NOTE]
    > この例では配布グループのエイリアスを使用しており、"Human Resources" という配布グループのエイリアスが "HumanResources" であると仮定しています。

    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  HAB 内のグループにユーザーを追加します。この例では、"David Hamilton" (SMTP アドレスは DHamilton@contoso.com) が "Contoso-dom.Contoso.com/Users" という OU の既存のユーザーであり、"Corporate Office" というグループに追加されます。この手順を繰り返して、HAB 内のグループに他のユーザーを追加します。
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  HAB 内のグループに *SeniorityIndex* パラメーターを設定します。この例では、"Corporate Office" グループに、"Human Resources"、"Accounting Group"、および "Administration Group" という 3 つの子グループが含まれます。グループをアルファベットの昇順 (既定) で一覧表示するのではなく、"Human Resources" (*SeniorityIndex* = 100)、"Accounting Group" (*SeniorityIndex* = 50)、および "Administration Group" (*SeniorityIndex* = 25) という、好ましい順序で並べ替えます。この例では、"Human Resources" グループの *SeniorityIndex* パラメーターを 100 に設定します。
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    

    > [!NOTE]
    > <EM>SeniorityIndex</EM> パラメーターは、HAB 内でグループやユーザーを数字の降順で並べ替えるために使用する数値です。<EM>SeniorityIndex</EM> パラメーターが設定されていない場合や、複数のユーザーに同じ値が設定されている場合は、HAB の並べ替え順序に <EM>PhoneticDisplayName</EM> パラメーター値が使用され、ユーザーがアルファベットの昇順で一覧表示されます。<EM>PhoneticDisplayName</EM> 値が設定されていない場合は、HAB の並べ替え順序は既定で <EM>DisplayName</EM> パラメーター値となり、ユーザーはアルファベットの昇順で一覧表示されます。



10. HAB グループ内のユーザーに *SeniorityIndex* パラメーターを設定します。この例では、"Corporate Office" グループに "Amy Alberts"、"David Hamilton"、および "Rajesh M. Patel" という 3 人のユーザーが含まれます。ユーザーをアルファベットの昇順 (既定) で表示するのではなく、"David Hamilton" (*SeniorityIndex* = 100)、"Rajesh M. Patel" (*SeniorityIndex* = 50)、および "Amy Alberts" (*SeniorityIndex* = 25) という、好ましい順序に並べ替えます。この例では、"David Hamilton" というユーザーの *SeniorityIndex* パラメーターを 100 に設定します。
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

上記の手順が完了すると、Outlook に HAB が表示されるようになります。HAB を表示するには、Outlook を開いて **\[アドレス帳\]** をクリックします。HAB は次の図のように **\[組織\]** タブに表示されます。

**Contoso,Ltd の HAB の例**

![\[階層型アドレス帳\] ダイアログ](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "[階層型アドレス帳] ダイアログ")

HAB を作成すると、EAC を使用して組織階層内のグループのメンバーシップを管理できます。ただし、新しいグループやユーザーの *SeniorityIndex* パラメーターを変更するには、シェルを使用する必要があります。

構文およびパラメーターの詳細については、以下を参照してください。

  - [New-DistributionGroup](https://technet.microsoft.com/ja-jp/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/ja-jp/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/ja-jp/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/ja-jp/library/aa998221\(v=exchg.150\))

## シェルを使用して階層型アドレス帳を無効にする

この例では、HAB で使用されているルート組織を無効にします。

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null


> [!NOTE]
> このコマンドを実行しても、HAB の構造で使用されているルート組織や子グループを削除したり、グループやユーザーの <EM>SeniorityIndex</EM> 値をリセットしたりすることはできません。Outlook で HAB が表示されないようにするだけです。同じ構成設定で HAB を再度有効にするには、ルート組織を再度有効にするだけで済みます。



構文およびパラメーターの詳細については、「[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))」を参照してください。

