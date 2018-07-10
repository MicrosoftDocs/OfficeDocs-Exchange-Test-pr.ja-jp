---
title: 'パブリック フォルダー メールボックスを別のメールボックス データベースに移動する: Exchange 2013 Help'
TOCTitle: パブリック フォルダー メールボックスを別のメールボックス データベースに移動する
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51407538
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# パブリック フォルダー メールボックスを別のメールボックス データベースに移動する

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2015-07-21_

負荷分散を目的として、または地理的に近い場所にリソースを移動するために、パブリック フォルダー メールボックスを別のメールボックス データベースに移動しなければならない場合があります。通常のメールボックスの移動と同様に、パブリック フォルダー メールボックスを移動するには **MoveRequest** コマンドレットを使用します。メールボックスの移動の詳細については、「[Exchange 2013 でのメールボックスの移動](mailbox-moves-in-exchange-2013-exchange-2013-help.md)」を参照してください。

パブリック フォルダーに関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 完了までの時間は、パブリック フォルダー メールボックスのサイズによって変わります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックスの移動および移行のアクセス許可」。

  - EAC でこのプロシージャは実行できません。このプロシージャを実行できるのはシェルのみです。

  - パブリック フォルダー メールボックスのサイズによっては、移動に数時間かかる場合があります。その間、ユーザーはパブリック フォルダーにアクセスすることができません。また、"完了処理が進行中" の間も、ユーザーは短時間ですがパブリック フォルダーにアクセスできなくなります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 移動要求を作成する

**New-MoveRequest** コマンドレットは、パブリック フォルダー メールボックスを Microsoft Exchange メールボックス レプリケーション サービス キューに格納します。Microsoft Exchange メールボックス レプリケーション サービスを使用できる場合は、サービスが移動要求を取得してパブリック フォルダー メールボックスの移動を開始します。サービスは要求全体を最初から最後まで実行します。

この例では、パブリック フォルダー PF\_SanFrancisco からメールボックス MBX\_DB01 への移動要求を開始します。

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01

構文およびパラメーターの詳細については、「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

## 移動要求を作成して後から実行する

移動要求の最終段階では、`CompletionInProgress` フェーズにおいて、ユーザーがパブリック フォルダー メールボックスからロックアウトされます。必要であれば、移動要求がそのフェーズに到達する前に要求を中断し、ユーザーに影響がない時間に再開できます。

この例では、パブリック フォルダー メールボックス PF\_SanFrancisco からメールボックス データベース MBX\_DB01 への移動要求を開始して、移動要求を実行する準備が整ったときに中断します。

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete

構文およびパラメーターの詳細については、「[New-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd351123\(v=exchg.150\))」を参照してください。

この例では、パブリック フォルダー メールボックス PF\_SanFrancisco に対する、進行中のメールボックス移動の状態を取得します。

    Get-MoveRequest -Identity "PF_SanFrancisco"

構文およびパラメーターの詳細については、「[Get-MoveRequest](https://technet.microsoft.com/ja-jp/library/dd335227\(v=exchg.150\))」を参照してください。

移動要求が "中断" 状態に達したら、要求を再開できます。この例では、パブリック フォルダー メールボックス PF\_SanFrancisco に対する移動要求を再開します。

    Resume-MoveRequest -Identity "PF_SanFrancisco"

構文およびパラメーターの詳細については、「[Resume-MoveRequest](https://technet.microsoft.com/ja-jp/library/ee332320\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

移動要求が正常に作成されたことを確認するには、次のコマンドを実行します。

    Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status

状態が `Completed` であれば、移動要求は成功しています。

移動に失敗すると、パブリック フォルダーの復元が必要になる場合があります。詳細については、「[失敗した移動からパブリック フォルダーとパブリック フォルダー メールボックスを復元する](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)」を参照してください。

