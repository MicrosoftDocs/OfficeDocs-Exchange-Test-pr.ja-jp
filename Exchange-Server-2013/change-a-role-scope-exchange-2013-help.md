---
title: '役割のスコープを変更する: Exchange 2013 Help'
TOCTitle: 役割のスコープを変更する
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 49896369
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割のスコープを変更する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-03_

管理役割スコープでユーザーが使用できるオブジェクトを決定すると、割り当てられたコマンドレットとパラメーターを使用してオブジェクトを変更できます。 スコープを変更することで、作成、変更、または削除するのにユーザーが使用できるオブジェクトを変更できます。

カスタム管理スコープを変更できます。 排他的または通常のスコープを変更できます。 排他的なスコープを変更すると、新しいスコープが直ちに有効になります。 あらかじめ定義された管理スコープ、または組織単位 (OU) 管理スコープを使用して管理役割割り当てを変更する場合は、「[役割の割り当てを変更する](change-a-role-assignment-exchange-2013-help.md)」を参照してください。

Microsoft Exchange Server 2013 での管理役割スコープおよび割り当ての詳細については、以下のトピックを参照してください。

  - [管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)

  - [管理役割の割り当てについて](understanding-management-role-assignments-exchange-2013-help.md)

役割スコープに関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理スコープ」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## スコープの名前を変更する

スコープの名前を変更するには、以下の構文を使用します。

    Set-ManagementScope <current scope name> -Name <new scope name>

この例では、シアトルの Exchange サーバーに対するシアトルのサーバーのスコープを変更します。

    Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"

構文およびパラメーターの詳細については、「[Set-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd297996\(v=exchg.150\))」を参照してください。

## スコープの受信者フィルターを変更する

スコープの受信者フィルターを変更するには、以下の構文を使用します。

    Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }

この例では、**Company** プロパティが contoso に設定されているすべての受信者オブジェクトに一致させるように受信者フィルターを変更します。

    Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }

構文およびパラメーターの詳細については、「[Set-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd297996\(v=exchg.150\))」を参照してください。

受信者フィルター、およびフィルター処理可能な受信者プロパティの一覧を表示する方法の詳細については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

## スコープの組織単位ルートを変更する

スコープの OU ルートを変更するには、以下の構文を使用します。

    Set-ManagementScope <scope name> -RecipientRoot <OU>

この例では、OU ルートを、contoso.com ドメインの下の North America/Sales Sales Users OU に変更します。

    Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"

構文およびパラメーターの詳細については、「[Set-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd297996\(v=exchg.150\))」を参照してください。

## スコープのサーバー フィルターを変更する

スコープのサーバー フィルターを変更するには、以下の構文を使用します。

    Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }

この例では、サーバー フィルターを、**ServerSite** プロパティが 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' に設定されているすべてのサーバー オブジェクトに一致するように変更します。

    Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

構文およびパラメーターの詳細については、「[Set-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd297996\(v=exchg.150\))」を参照してください。

サーバー フィルター、およびフィルター処理可能なサーバー プロパティの一覧を表示する方法の詳細については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

## スコープのサーバーの一覧を変更する

スコープのサーバーの一覧を変更することはできません。 サーバーの一覧を変更する場合は、以下の操作を実行する必要があります。

1.  必要に応じて、「[役割スコープを表示する](view-role-scopes-exchange-2013-help.md)」の「特定のスコープを表示する」手順に従って、置き換えるスコープ内の現在のサーバーの一覧を取得します。

2.  「[通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)」の「手順 1: カスタムのスコープを作成する」手順に従って、新しいサーバーの一覧を使用してスコープを作成します。

3.  「[役割の割り当てを変更する](change-a-role-assignment-exchange-2013-help.md)」の「シェルを使用して、役割割り当てのサーバー フィルターまたはサーバーの一覧を使用したスコープを変更する」手順に従って、古いスコープを使用するすべての管理役割割り当てを変更して、新しいスコープを使用するようにします。

4.  「[役割のスコープを削除する](remove-a-role-scope-exchange-2013-help.md)」の手順に従って、古いスコープを削除します。

## スコープのデータベース フィルターを変更する

スコープのデータベース フィルターを変更するには、以下の構文を使用します。

    Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }

この例では、**Name** プロパティに文字列 "Executive" が含まれているすべてのデータベース オブジェクトに一致させるようにデータベース フィルターを変更します。

    Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }

構文およびパラメーターの詳細については、「[Set-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd297996\(v=exchg.150\))」を参照してください。

データベース フィルター、およびフィルター処理可能なデータベース プロパティの一覧を表示する方法の詳細については、「[管理ロールのスコープ フィルターについて](understanding-management-role-scope-filters-exchange-2013-help.md)」を参照してください。

## スコープのデータベースの一覧を変更する

スコープのデータベースの一覧を変更することはできません。 データベースの一覧を変更する場合は、以下の操作を実行する必要があります。

1.  必要に応じて、「[役割スコープを表示する](view-role-scopes-exchange-2013-help.md)」の「特定のスコープを表示する」手順に従って、置き換えるスコープ内の現在のデータベースの一覧を取得します。

2.  「[通常または排他スコープを作成する](create-a-regular-or-exclusive-scope-exchange-2013-help.md)」の「手順 1: カスタムのスコープを作成する」手順に従って、新しいデータベースの一覧を使用してスコープを作成します。

3.  「[役割の割り当てを変更する](change-a-role-assignment-exchange-2013-help.md)」の「シェルを使用して、役割割り当てのデータベース フィルターまたはデータベースの一覧を使用したスコープを変更する」手順に従って、古いスコープを使用するすべての管理役割割り当てを変更して、新しいスコープを使用するようにします。

4.  「[役割のスコープを削除する](remove-a-role-scope-exchange-2013-help.md)」の手順に従って、古いスコープを削除します。

