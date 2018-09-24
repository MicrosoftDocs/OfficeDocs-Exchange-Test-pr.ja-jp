---
title: 'パブリック フォルダーを別のパブリック フォルダー メールボックスに移動する: Exchange 2013 Help'
TOCTitle: パブリック フォルダーを別のパブリック フォルダー メールボックスに移動する
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51407563
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダーを別のパブリック フォルダー メールボックスに移動する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2016-11-16_

パブリック フォルダー メールボックスの容量がメールボックス クォータを超えると、パブリック フォルダーを別のパブリック フォルダー メールボックスに移さなければならない場合があります。これを実行する方法は、いくつかあります。サブフォルダーがない 1 つ以上のパブリック フォルダーを移動するには、**PublicFolderMoveRequest** コマンドレットを使用できます。(親パブリック フォルダーとすべてのサブフォルダーを含む) パブリック フォルダーのブランチ全体を移動する必要がある場合は、Exchange 2013 をインストールする際に利用できる `Move-PublicFolderBranch.ps1` スクリプトを使用できます。

パブリック フォルダーに関連する追加の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 移動に要する時間はパブリック フォルダーのサイズによって変わります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パブリック フォルダー」。

  - EAC を使用してこれらの手順を実行することはできません。シェルを使用する必要があります。

  - 移動するフォルダーにサブフォルダーがある場合、既定ではサブフォルダーは移動されません。パブリック フォルダーとすべてのサブフォルダーを移動する場合は、**Move-PublicFolderBranch.ps1** スクリプトを使用します。

  - パブリック フォルダーの移動では、パブリック フォルダーの物理的な内容のみを移動し、論理階層は変更されません。

  - パブリック フォルダーのサイズとコンテンツ量によっては、移動が完了するまでに数時間かかる場合があります。その間もユーザーはパブリック フォルダーにアクセスすることができます。ただし、フォルダーの状態が "完了処理が進行中" の短時間だけはパブリック フォルダーにアクセスできません。

  - パブリック フォルダーの移動要求は一度に 1 回しかできません。移動が完了したら、**Remove-PublicFolderMoveRequest** コマンドレットを使用して要求を削除する必要があります。

  - 進行中のパブリック フォルダーの移動要求の状態を確認するには、[Get-PublicFolderMoveRequest](https://technet.microsoft.com/ja-jp/library/jj878076\(v=exchg.150\)) コマンドレットを実行します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 1 つのパブリック フォルダーを移動する

この例では、パブリック フォルダー \\CustomerEnagagements を、パブリック フォルダー メールボックス DeveloperReports から DeveloperReports01 に移動する移動要求を開始します

```powershell
    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01
```


> [!NOTE]
> 移動要求がアクティブになっている間は、移動先パブリック フォルダー メールボックスはロックされます。



構文およびパラメーターの詳細については、「[New-PublicFolderMoveRequest](https://technet.microsoft.com/ja-jp/library/jj878081\(v=exchg.150\))」を参照してください。

## 複数のパブリック フォルダーを移動する

この例では、\\Dev パブリック フォルダーのブランチの下にあるパブリック フォルダーの、移動先パブリック フォルダー メールボックス DeveloperReports01 への移動要求を開始します。この例ではパブリック フォルダー \\Dev は移動されません。

```powershell
    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01
```


> [!NOTE]
> 移動要求がアクティブになっている間は、移動先パブリック フォルダー メールボックスはロックされます。



構文およびパラメーターの詳細については、「[New-PublicFolderMoveRequest](https://technet.microsoft.com/ja-jp/library/jj878081\(v=exchg.150\))」を参照してください。

## パブリック フォルダーのブランチを移動する

この例では、`Move-PublicFolderBranch.ps1` スクリプトを使用してパブリック フォルダーのブランチを移動します。パブリック フォルダー \\Dev とすべてのサブフォルダーの、パブリック フォルダー メールボックス DeveloperReports01 への移動要求を開始します。このスクリプトはスクリプト フォルダーにあり、そこから実行する必要があります。

```powershell
    CD $env:ExchangeInstallPath\scripts
```
```powershell
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01
```
## 正常な動作を確認する方法

パブリック フォルダーの移動要求が成功したことを確認するには、次のコマンドを実行します。

```powershell
Get-PublicFolderMoveRequest | Format-List Status
```

状態が `Completed` であれば、移動要求は成功しています。

移動要求が失敗した場合は、パブリック フォルダーやその内容を復元する必要があります。詳細については、「[失敗した移動からパブリック フォルダーとパブリック フォルダー メールボックスを復元する](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)」をご覧ください。

