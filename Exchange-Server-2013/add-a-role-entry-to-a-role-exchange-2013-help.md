---
title: '役割エントリを役割に追加する: Exchange 2013 Help'
TOCTitle: 役割エントリを役割に追加する
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 49896183
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割エントリを役割に追加する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-04_

コマンドレットへのアクセスを許可する場合、関連付けられた管理役割エントリを管理役割に追加する必要があります。 役割エントリを役割に追加すると、その役割に割り当てられたユーザーがコマンドレットにアクセスできるようになります。Microsoft Exchange Server 2013 での管理役割エントリの詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

組み込みの役割に役割エントリを追加することはできません。 役割をカスタマイズする場合は、新しい役割を作成する必要があります。 新しい役割を作成する方法の詳細については、「[役割を作成する](create-a-role-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> ここでは対象範囲外の管理役割エントリを対象範囲外の管理役割に追加する方法については説明しません。 対象範囲外の役割エントリを追加する方法の詳細については、「<A href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">スコープ外の最上位の役割に役割エントリを追加する</A>」を参照してください。



役割に関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - 管理役割に追加する役割エントリは、その役割のすぐ上の親管理役割に存在する必要があります。

  - ここではパイプライン処理を利用します。 パイプライン処理の詳細については、「[パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 親役割から 1 つの役割エントリを追加する

次の構文を使用して親役割に表示されるとおりに役割エントリを役割に追加できます。

    Add-ManagementRoleEntry <child role name>\<cmdlet>

この例では、**Set-Mailbox** コマンドレットを "Recipient Administrators/受信者管理者" 役割に追加します。

    Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"

このコマンドは、親の役割を確認し、役割エントリが存在する場合、それを子の役割に追加します。 役割エントリが子の役割に既に存在する場合は、既存の役割エントリを上書きするために *Overwrite* パラメーターを指定できます。

構文およびパラメーターの詳細については、「[Add-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351236\(v=exchg.150\))」を参照してください。

## 親の役割から 1 つの役割エントリを追加し、特定のパラメーターのみを含める

親の役割から役割エントリを追加するときに、子の役割の役割エントリに特定のパラメーターのみを含める場合は、次の構文を使用します。

    Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

この例では、**Set-Mailbox** コマンドレットを "Help Desk/ヘルプ デスク" 役割に追加しますが、子の役割のエントリに *DisplayName* パラメーターと *EmailAddresses* パラメーターのみを含めます。

    Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses

このコマンドは、親の役割を確認し、役割エントリが存在する場合、それを子の役割に追加します。役割エントリが子の役割に既に存在する場合は、既存の役割エントリを上書きするために *Overwrite* パラメーターを指定できます。

構文およびパラメーターの詳細については、「[Add-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351236\(v=exchg.150\))」を参照してください。

## 親の役割から複数の役割エントリを追加する

役割に複数の役割エントリを追加する場合は、子の役割に追加する、親の役割に存在する役割エントリの一覧を取得する必要があります。 それには、**Get-ManagementRoleEntry** コマンドレットを使用して親の役割の役割エントリの一覧を取得します。 次に、**Get-ManagementRoleEntry** コマンドレットの出力を **Add-ManagementRoleEntry** コマンドレットにパイプ設定します。 複数の役割エントリを取得するには、ワイルドカード文字 (\*) を使用する必要があります。

親の役割から子の役割に複数のエントリを追加するには、次の構文を使用します。

    Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>

この例では、"Mail Recipient/メール受信者" 親役割のコマンドレット名に文字列 `Mailbox` を含むすべての役割エントリを、"Seattle Mail Recipients/Seattle のメール受信者" 子役割に追加します。

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"

役割エントリが子の役割に既に存在する場合は、既存の役割エントリを上書きするために *Overwrite* パラメーターを含めることができます。

管理役割エントリの一覧を取得する方法の詳細については、「[役割エントリを表示する](view-role-entries-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」と「[Add-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd351236\(v=exchg.150\))」を参照してください。

