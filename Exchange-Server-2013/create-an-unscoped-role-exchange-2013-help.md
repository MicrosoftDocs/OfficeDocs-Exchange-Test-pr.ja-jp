---
title: '対象範囲外の役割を作成する: Exchange 2013 Help'
TOCTitle: 対象範囲外の役割を作成する
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 49896263
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 対象範囲外の役割を作成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-09_

対象範囲外の管理役割を使用すると、管理者と専門家ユーザーが Windows PowerShell スクリプトと Exchange 以外のコマンドレットにアクセスできるようになります。対象範囲外の最上位の役割を作成してその役割にスクリプトまたは Exchange 以外のコマンドレットを追加することも、既存の対象範囲外の最上位の役割に基づく役割を作成することも可能です。対象範囲外の役割を作成してカスタマイズした後は、役割を管理役割グループ、ユーザー、およびユニバーサル セキュリティ グループ (USG) に割り当てることができます。対象範囲外の役割は、管理役割割り当てポリシーを割り当てることができません。対象範囲外の役割の詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> 対象範囲外の役割は、それらの名前が示すように、管理スコープが適用されないので効果的に使用できます。つまり、それらに含まれるスクリプトと Exchange 以外のコマンドレットを Exchange 組織内のオブジェクトに対して実行できます。これを検討するのは、スクリプトまたは Exchange 以外のコマンドレットを対象範囲外の役割に追加する場合と、対象範囲外の役割を割り当てる場合です。




> [!NOTE]
> Exchange コマンドレットを含む役割を作成する場合は、既存の管理役割に基づいて役割を作成する必要があります。Exchange コマンドレットで役割を作成する詳細については、「<A href="create-a-role-exchange-2013-help.md">役割を作成する</A>」を参照してください。



役割に関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - 対象範囲外の役割を作成する機能は、既定で管理役割グループに含まれていません。ユーザーが役割グループを追加できるようにするには、最初に "Unscoped Role Management/スコープ外役割管理" 役割をユーザーか、もしくはユーザーが所属する USG または役割グループに割り当てる必要があります。役割をユーザー、USG、または役割グループに追加する方法の詳細については、以下のトピックを参照してください。
    
      - [役割グループの管理](manage-role-groups-exchange-2013-help.md)
    
      - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 対象範囲外の最上位の管理役割を作成する

スクリプトまたは Exchange 以外のコマンドレットを組織内の管理者または専門家が使用できるようにする場合は、対象範囲外の最上位の役割を作成する必要があります。スクリプトと Exchange 以外のコマンドレットは、最上位の役割として作成された対象範囲外の役割にのみ追加できます。 理由は、最初の対象範囲外の役割はその他の役割から継承しないからです。新しい対象範囲外の最上位の役割は、追加されたスクリプトと Exchange 以外のコマンドレットも使用できるその他の対象範囲外の役割の親にすることができます。

ここでは、対象範囲外の最上位の役割を作成する手順を示します。

## 手順 1:対象範囲外の最上位の役割を作成する

対象範囲外の最上位の役割には親の役割がありません。親なしで役割を作成するには、*UnscopedTopLevel* スイッチを指定する必要があります。新しい役割を作成するには、次の構文を使用します。

    New-ManagementRole <name of new role> -UnscopedTopLevel

この例では、IT スクリプトの対象範囲外の最上位役割を作成します。

    New-ManagementRole "IT Scripts" -UnscopedTopLevel

作成した後、役割はスクリプトまたは Exchange 以外のコマンドレットを追加するまで空です。

構文とパラメーターの詳細については、「[New-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd298073\(v=exchg.150\))」を参照してください。

## 手順 2a:スクリプト管理役割のエントリを追加する

新しい対象範囲外の役割にスクリプトを追加する場合、この手順を使用します。新しい対象範囲外の役割に Exchange 以外のコマンドレットを追加する場合、「手順 2b:Exchange 以外のコマンドレット役割のエントリを追加する」を使用します。

Windows PowerShell スクリプトを対象範囲外の最上位の役割に追加するには、管理役割エントリをその役割に追加する必要があります。役割エントリには、スクリプトの名前と、その役割で使用可能にするスクリプトのパラメーターが含まれます。

スクリプトは、ユーザーがスクリプトを実行するために接続する可能性がある、Exchange 2013 を実行している全サーバー上の Microsoft Exchange Server 2013 インストール パスの `RemoteScripts` ディレクトリに置く必要があります。ユーザーにスクリプトを実行するためのアクセス許可があっても、ユーザーの接続先の Exchange 2013 サーバーにスクリプトが置かれていない場合は、エラーが発生します。既定では、`RemoteScripts` ディレクトリのパスは、C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts です。

スクリプトを適切な Exchange 2013 サーバーにコピーし、どのスクリプト パラメーターを使用するか決定したら、次の構文を使用して役割エントリを作成します。

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

この例では、BulkProvisionUsers.ps1 スクリプトを、*Name* および *Location* パラメーターを持つ IT Scripts 役割に追加します。

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> コマンドレットは、スクリプトに存在するパラメーターだけを追加したことを確認するために基本的な検証を実行します。ただし、役割エントリが追加された後にこれ以上の検証は実行されません。パラメーターが後から追加または削除された場合は、このスクリプトを含む役割エントリを手動で更新する必要があります。



## 手順 2b:Exchange 以外のコマンドレット役割のエントリを追加する

新しい対象範囲外の役割に Exchange 以外のコマンドレットを追加する場合、この手順を使用します。新しい対象範囲外の役割にスクリプトを追加する場合、「手順 2a:スクリプト管理役割のエントリを追加する」を使用します。

Exchange 以外のコマンドレットを対象範囲外の最上位の役割に追加するには、管理役割エントリをその役割に追加する必要があります。役割エントリには、コマンドレット スナップイン、コマンドレット名、およびその役割で使用可能にするコマンドレットのパラメーターが含まれます。

Exchange 以外のコマンドレットを新しい役割に追加する場合は、コマンドレットを実行するためにユーザーが接続する可能性があるすべての Exchange 2013 サーバーに、コマンドレットをインストールする必要があります。使用するコマンドレットを含む Windows PowerShell スナップインを正しくインストールおよび登録する方法については、製品のドキュメントを参照してください。

Windows サーバー上でコマンドレットを含む Exchange 2013 PowerShell スナップインをインストールして、使用すべきコマンドレット パラメーターを決定した後で、次の構文で役割エントリを作成します。

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

この例では、Contoso.Admin.Cmdlets スナップインの **Set-WidgetConfiguration** コマンドレットを、*Database* および *Size* パラメーターを持つ Widget Cmdlets 役割に追加します。

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> コマンドレットは、コマンドレットに存在するパラメーターだけを追加したことを確認するために基本的な検証を実行します。ただし、役割エントリが追加された後にこれ以上の検証は実行されません。コマンドレットが後から変更され、パラメーターが追加または削除された場合は、このコマンドレットを含む役割エントリを手動で更新する必要があります。



## 手順 3:管理役割を割り当てる

役割を作成および構成したときの最後の手順は、役割を役割の被割り当て者に割り当てることです。


> [!IMPORTANT]
> 対象範囲外の役割を割り当てる役割の割り当てでは、管理スコープを構成することはできません。役割グループ、ユーザー、USG のいずれに対して役割の割り当てを作成する場合でも、管理スコープなしの役割の割り当てを作成するためのオプションを選択する必要があります。



新しい役割を役割グループ、ユーザー、または USG に割り当てることができます。詳細については、以下のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## 対象範囲外の役割を別の対象範囲外の役割に基づいて作成する

既存の対象範囲外の最上位役割または新しい対象範囲外の役割が基礎を置くその他の対象範囲外の役割がある場合、子の対象範囲外の役割を作成できます。子の対象範囲外の役割には、親の対象範囲外の役割に存在するスクリプトおよびコマンドレットのサブセットを含むことができます。これは、たとえば、親の対象範囲外の役割で使用可能なスクリプトまたはコマンドレットのサブセットのみを経験豊富でない管理者に付与する場合、役に立ちます。

ここでは、対象範囲外の子の役割を作成する手順を示します。

## 手順 1:対象範囲外の子の役割を作成する

新しい対象範囲外の子の役割は、既存の対象範囲外の役割をベースにすることができます。役割を作成する場合は、既存の役割とその管理役割エントリが新しい役割にコピーされます。既存の役割が、新しい子の役割に対する親になります。別の対象範囲外の役割に基づく対象範囲外の役割を作成する場合、使用が必要なすべてのコマンドレットおよびパラメーターを含む役割を選択してから、不要なものを削除する必要があります。子の対象範囲外の役割は、親の役割に存在しない管理役割エントリを持つことができません。


> [!NOTE]
> その他の対象範囲外の役割に存在しないスクリプトまたは Exchange 以外のコマンドレットが含まれる対象範囲外の役割を作成する必要がある場合は、対象範囲外の最上位の役割を作成します。詳細については、このトピックに前述した「対象範囲外の最上位の管理役割を作成する」を参照してください。



新しい役割を作成するには、次の構文を使用します。

    New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>

この例では、"IT Global Scripts/IT グローバル スクリプト" 役割とその管理役割エントリを "Diagnostic IT Scripts/診断 IT スクリプト" 役割にコピーします。

    New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"

構文およびパラメーターの詳細については、「[New-ManagementRole](https://technet.microsoft.com/ja-jp/library/dd298073\(v=exchg.150\))」を参照してください。

## 手順 2:役割の管理役割エントリを変更します。

役割を作成した後に役割のエントリを変更する必要があります。役割エントリ全体を削除して、関連付けられたスクリプトまたは Exchange 以外のコマンドレットへのアクセスも完全に削除することができます。または、役割エントリからパラメーターを削除して、関連付けられたスクリプトまたは Exchange 以外のコマンドレットの特定パラメーターへのアクセスを削除することもできます。

親の役割に存在しない限り、役割エントリまたは役割エントリのパラメーターを追加することはできません。手順 1 で親の役割から役割を作成したばかりなので、追加の役割エントリまたは役割エントリのパラメーターは、親の役割に存在しないため追加できません。

役割の役割エントリを変更する場合、以下のいずれかを実行できます。

  - 単一の役割エントリ全体を削除する。

  - 複数の役割エントリ全体を削除する。

  - 役割エントリからパラメーターを削除する。

新しい役割から役割エントリを削除するには、「[役割から役割エントリを削除する](remove-a-role-entry-from-a-role-exchange-2013-help.md)」を参照してください。

## 手順 3:管理役割を割り当てる

役割を作成および構成したときの最後の手順は、役割を役割の被割り当て者に割り当てることです。


> [!IMPORTANT]
> 対象範囲外の役割を割り当てる役割の割り当てでは、管理スコープを構成することはできません。役割グループ、ユーザー、USG のいずれに対して役割の割り当てを作成する場合でも、管理スコープなしの役割の割り当てを作成するためのオプションを選択する必要があります。



新しい役割を役割グループ、ユーザー、または USG に割り当てることができます。詳細については、以下のトピックを参照してください。

  - [役割グループの管理](manage-role-groups-exchange-2013-help.md)

  - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

