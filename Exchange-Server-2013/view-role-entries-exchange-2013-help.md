---
title: '役割エントリを表示する: Exchange 2013 Help'
TOCTitle: 役割エントリを表示する
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 49896506
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割エントリを表示する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-03_

各管理役割のエントリは、1 つのコマンドレットまたはスクリプトを表します。 役割エントリに指定されているパラメーターにより、ユーザーがアクセスできるコマンドレットまたはスクリプト上のパラメーターが決定されます。

役割エントリの ID は、役割エントリが関連付けられた管理役割の名前、役割エントリが参照するコマンドレットまたはスクリプトで構成されます。Microsoft Exchange Server 2013 での役割エントリの詳細については、「[管理の役割について](understanding-management-roles-exchange-2013-help.md)」を参照してください。

役割エントリに関連する他の管理タスクについては、 「[高度な権限](advanced-permissions-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理役割」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - ここでは、パイプライン処理、**Format-List** コマンドレット、オブジェクト、およびプロパティを利用します。 これらの概念の詳細については、以下のトピックを参照してください。
    
      - [パイプライン処理](https://technet.microsoft.com/ja-jp/library/aa998260\(v=exchg.150\))
    
      - [コマンド出力の操作](working-with-command-output-exchange-2013-help.md)
    
      - [構造化データ](https://technet.microsoft.com/ja-jp/library/aa996386\(v=exchg.150\))

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 役割エントリの一覧を表示する

**Get-ManagementRoleEntry** コマンドレットを使用して、役割エントリの一覧を取得することができます。 **Get-ManagementRoleEntry** コマンドレットを使用する場合は、一覧にする役割エントリを含んだ役割の名前、および一覧にする役割エントリのコマンドレットの名前の両方を含む値を指定する必要があります。 役割名とコマンドレット名をワイルドカード文字 (\*) と組み合わせることで、特定の役割エントリまたは広範な役割エントリの一覧を返すことができます。

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」を参照してください。

## 役割のすべての役割エントリの一覧を表示する

特定の役割の役割エントリの一覧を表示するには、次の構文を使用します。

    Get-ManagementRoleEntry <role name>\*

この例では、`Recipient Administrators` 役割のすべての役割エントリを取得します。

    Get-ManagementRole "Recipient Administrators\*"

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」を参照してください。

## 特定の役割エントリを含んだ役割の一覧を表示する

特定の役割エントリを含んだすべての役割の一覧を表示するには、次の構文を使用します。

    Get-ManagementRoleEntry *\<cmdlet name>

この例では、**Set-Mailbox** 役割エントリを含んだすべての役割を取得します。

    Get-ManagementRoleEntry *\Set-Mailbox

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」を参照してください。

## 類似の役割エントリを含んだ、対象となる役割の一覧を表示する

類似の名前を持つコマンドレットを含んだ、対象となる役割の一覧を表示するには、次の構文を使用します。

    Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*

この例では、名前の中に文字列 `Tier 1` を含んだ役割にある、文字列 `Mailbox` を含んだ役割エントリの一覧を返します。

    Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」を参照してください。

## 1 つの役割エントリを表示する

1 つの役割エントリの詳細を表示するには、次の構文を使用します。

    Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List

この例では、`Recipient Administrators` 役割にある **Set-Mailbox** 役割エントリの詳細を取得します。

    Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List

**Format-List** コマンドレットを使用して表示する役割エントリに、非常に多くのパラメーターが含まれている場合は、このトピックの後で紹介する「1 つの役割エントリのパラメーターを表示する」を参照してください。

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」を参照してください。

## 1 つの役割エントリのパラメーターを表示する

**Get-ManagementRoleEntry** コマンドレットの結果を **Format-List** コマンドレットにパイプ処理すると、役割エントリによっては、パラメーターの数が多すぎて表示しきれないことがあります。 役割エントリのすべてのパラメーターを表示する必要がある場合は、その役割エントリ オブジェクトの **Parameters** プロパティに直接アクセスする必要があります。

役割エントリ オブジェクトの **Parameters** プロパティに保存されたパラメーターを表示するには、次の構文を使用します。

    (Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters

この例では、"Mail Recipients/メール受信者" 役割にある **Set-Mailbox** 役割エントリのパラメーターを取得します。

    (Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters

構文およびパラメーターの詳細については、「[Get-ManagementRoleEntry](https://technet.microsoft.com/ja-jp/library/dd335210\(v=exchg.150\))」を参照してください。

