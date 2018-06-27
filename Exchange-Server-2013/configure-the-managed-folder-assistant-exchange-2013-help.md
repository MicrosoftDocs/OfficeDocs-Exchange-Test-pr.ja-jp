---
title: '管理フォルダー アシスタントの構成: Exchange 2013 Help'
TOCTitle: 管理フォルダー アシスタントの構成
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 49896390
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理フォルダー アシスタントの構成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2014-10-01_

*管理フォルダー アシスタント*は、アイテム保持ポリシーに構成されたメッセージ保持設定を適用する MicrosoftExchange メールボックス アシスタントです。

メッセージング レコード管理 (MRM) に関連する追加の管理タスクについては、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 所要時間:1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

  - Exchange 管理センター (EAC) を使用して管理フォルダー アシスタントを構成することはできません。シェルを使用する必要があります

  - Exchange 2013 では、管理フォルダー アシスタントは調整ベースのアシスタントです。調整ベースのアシスタントは常に実行中であるため、スケジュールする必要はありません。消費可能なシステム リソースは調整されます。管理フォルダー アシスタントを、特定の期間 (*ワーク サイクル*といいます) 内のメールボックス サーバー上のすべてのメールボックスについて処理するよう構成できます。作業サイクルは既定で 1 日に設定されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用した管理フォルダー アシスタントの構成

この例では、1 日以内にすべてのメールボックスを処理するよう管理フォルダー アシスタントを構成します。

    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

構文およびパラメーターの詳細については、「[Set-MailboxServer](https://technet.microsoft.com/ja-jp/library/aa998651\(v=exchg.150\))」を参照してください。

## 設定が適用されたことを確認する方法

管理フォルダー アシスタントを正常に構成したことを確認するには、[Get-MailboxServer](https://technet.microsoft.com/ja-jp/library/bb123539\(v=exchg.150\)) コマンドレットを使用して *ManagedFolderWorkCycle* パラメーターをチェックします。

このコマンドは、組織内のすべてのメールボックス サーバーを取得し、各サーバーの管理フォルダー アシスタントの作業サイクルのプロパティを表形式で出力します。*Auto* スイッチを使用すると、列の幅が自動的に調節されます。

    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto

## シェルを使用して管理フォルダー アシスタントを開始する

この例では、管理フォルダー アシスタントを開始して即座に Morris Cornejo のメールボックスを処理します。

    Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com

構文およびパラメーターの詳細については、「[Start-ManagedFolderAssistant](https://technet.microsoft.com/ja-jp/library/aa998864\(v=exchg.150\))」を参照してください。

