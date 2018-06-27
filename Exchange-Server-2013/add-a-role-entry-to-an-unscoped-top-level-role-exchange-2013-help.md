---
title: 'スコープ外の最上位の役割に役割エントリを追加する: Exchange 2013 Help'
TOCTitle: スコープ外の最上位の役割に役割エントリを追加する
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 49896254
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# スコープ外の最上位の役割に役割エントリを追加する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-03_

新しいスクリプトまたは Exchange 以外のコマンドレットを既存の対象範囲外の役割で使用できるようにする場合は、対象範囲外の最上位の役割にスクリプトと Exchange 以外のコマンドレットを追加します。 これらのスクリプトと Exchange 以外のコマンドレットは、管理役割エントリとして対象範囲外の最上位の管理役割に追加されます。 それらは、対象範囲外の最上位の役割エントリまたは最上位の役割から派生した対象範囲外の役割が使用できます。 スコープ外の役割のエントリの詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> Exchange コマンドレットを含む管理の役割の役割エントリを変更する場合、「<A href="change-a-role-entry-exchange-2013-help.md">役割エントリを変更する</A>」を参照してください。



役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - 役割エントリを対象範囲外の最上位の役割に追加する機能は、既定では管理役割グループに含まれません。 対象範囲外の最上位の役割エントリをユーザーが追加できるようにするには、最初に "Unscoped Role Management/スコープ外役割管理" 管理役割をユーザーか、もしくはユーザーが所属するユニバーサル セキュリティ グループ (USG) または役割グループに割り当てる必要があります。 役割を役割グループ、ユーザー、または USG に追加する方法の詳細については、以下のトピックを参照してください。
    
      - [役割グループの管理](manage-role-groups-exchange-2013-help.md)
    
      - [ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## スクリプト役割エントリを対象範囲外の最上位の役割に追加する

既存の対象範囲外の役割にスクリプトを追加する場合、この手順を使用します。既存の対象範囲外の役割に Exchange 以外のコマンドレットを追加する場合は、このトピックで後述する「Exchange 以外のコマンドレット役割エントリを対象範囲外の最上位の役割に追加する」を参照してください。

Windows PowerShell スクリプトを対象範囲外の最上位の役割に追加するには、管理役割エントリをその役割に追加する必要があります。 役割エントリには、スクリプトの名前と、その役割で使用可能にするスクリプトのパラメーターが含まれます。

スクリプトは、ユーザーがスクリプトを実行するために接続する可能性がある Exchange Server 2013 が実行されているすべてのサーバーの、Microsoft Exchange 2013 インストール パスの Scripts ディレクトリに置く必要があります。ユーザーにスクリプトを実行するためのアクセス許可があっても、ユーザーの接続先の Exchange 2013 サーバーにスクリプトが置かれていない場合は、エラーが発生します。既定では、Scripts ディレクトリのパスは、C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts です。

スクリプトを適切な Exchange 2013 サーバーにコピーし、どのスクリプト パラメーターを使用するか決定したら、次の構文を使用して役割エントリを作成します。

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

この例では、BulkProvisionUsers.ps1 スクリプトを、*Name* および *Location* パラメーターを持つ IT Scripts 役割に追加します。

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> コマンドレットは、スクリプトに存在するパラメーターだけを追加したことを確認するために基本的な検証を実行します。 ただし、役割エントリが追加された後にこれ以上の検証は実行されません。 パラメーターが後から追加または削除された場合は、このスクリプトを含む役割エントリを手動で更新する必要があります。



## Exchange 以外のコマンドレットの役割エントリを対象範囲外の最上位の役割に追加する

既存の対象範囲外の役割に Exchange 以外のコマンドレットを追加する場合、この手順を使用します。 既存の対象範囲外の役割にスクリプトを追加する場合は、このトピックの前述の「スクリプト役割エントリを対象範囲外の最上位の役割に追加する」を参照してください。

Exchange 以外のコマンドレットを対象範囲外の最上位の役割に追加するには、管理役割エントリをその役割に追加する必要があります。 役割エントリには、コマンドレット スナップイン、コマンドレット名、およびその役割で使用可能にするコマンドレットのパラメーターが含まれます。

Exchange 以外のコマンドレットを新しい役割に追加する場合は、コマンドレットを実行するためにユーザーが接続する可能性があるすべての Exchange 2013 サーバーに、コマンドレットをインストールする必要があります。 使用するコマンドレットを含む Windows PowerShell スナップインを正しくインストールおよび登録する方法については、製品のドキュメントを参照してください。

Windows サーバー上でコマンドレットを含む Exchange 2013 PowerShell スナップインをインストールして、使用すべきコマンドレット パラメーターを決定した後で、次の構文で役割エントリを作成します。

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

この例では、Contoso.Admin.Cmdlets スナップインの **Set-WidgetConfiguration** コマンドレットを、*Database* および *Size* パラメーターを持つ Widget Cmdlets 役割に追加します。

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> コマンドレットは、コマンドレットに存在するパラメーターだけを追加したことを確認するために基本的な検証を実行します。ただし、役割エントリが追加された後にこれ以上の検証は実行されません。 コマンドレットが後から変更され、パラメーターが追加または削除された場合は、このコマンドレットを含む役割エントリを手動で更新する必要があります。



## その他のタスク

役割エントリまたは対象範囲外の最上位の役割を追加した後で、次の操作も実行できます。

[役割エントリを役割に追加する](add-a-role-entry-to-a-role-exchange-2013-help.md)

[役割グループの管理](manage-role-groups-exchange-2013-help.md)

[役割グループのメンバーの管理](manage-role-group-members-exchange-2013-help.md)

[ユーザーまたは USG に役割を追加する](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[ユーザーまたは USG から役割を削除する](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

