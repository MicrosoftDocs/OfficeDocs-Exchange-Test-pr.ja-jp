---
title: '役割スコープを表示する: Exchange 2013 Help'
TOCTitle: 役割スコープを表示する
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 49895229
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割スコープを表示する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-03_

管理役割スコープによって、ユーザーに対して使用可能にするオブジェクトを指定します。指定されたオブジェクトは、ユーザーに割り当てられたコマンドレットとパラメーターを使用して変更できるようになります。スコープを表示して、組織に追加されたスコープ、特定のスコープの構成、または孤立したスコープを確認できます。

Microsoft Exchange Server 2013 での管理役割スコープの詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

役割スコープに関連する他の管理タスクについては、「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理スコープ」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - このトピックでは、パイプライン処理および **Format-List** コマンドレットを利用します。これらの概念の詳細については、以下のトピックを参照してください。
    
      - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))
    
      - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 特定のスコープを表示する

**Get-ManagementScope** コマンドレットの出力を **Format-List** コマンドレットにパイプ処理することで、役割の詳細を表示できます。

特定のスコープの詳細を表示するには、次の構文を使用します。

    Get-ManagementScope <scope name> | Format-List

この例では、シアトル サーバー スコープの詳細を取得します。

    Get-ManagementScope "Seattle Servers" | Format-List

構文およびパラメーターの詳細については、「[Get-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd298180\(v=exchg.150\))」を参照してください。

## すべてのスコープを一覧表示する

この例では、組織内のスコープの一覧を取得します。

    Get-ManagementScope

このコマンドレットは排他的スコープと正規スコープの両方を取得します。排他的スコープまたは正規スコープのいずれか一方を取得したい場合は、後述の「排他的スコープまたは正規のスコープのいずれかすべてを一覧表示する」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd298180\(v=exchg.150\))」を参照してください。

## 孤立したすべてのスコープを一覧表示する

*孤立したスコープ*とは、管理役割割り当てに関連付けられていないスコープです。

この例では、孤立したスコープの一覧を取得します。

    Get-ManagementScope -Orphan

構文およびパラメーターの詳細については、「[Get-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd298180\(v=exchg.150\))」を参照してください。

## 排他的スコープまたは正規のスコープのいずれかすべてを一覧表示する

既定では、**Get-ManagementScope** コマンドレットは、排他的スコープと正規スコープの両方を含むスコープの一覧を返します。排他的スコープまたは正規スコープのいずれか一方のみを取得したい場合は、次の構文を使用してください。

    Get-ManagementScope -Exclusive < $true | $false >

この例では、排他的スコープのみ返します。

    Get-ManagementScope -Exclusive $true

この例では、正規のスコープの一覧のみ返します。

    Get-ManagementScope -Exclusive $false

構文およびパラメーターの詳細については、「[Get-ManagementScope](https://technet.microsoft.com/ja-jp/library/dd298180\(v=exchg.150\))」を参照してください。

