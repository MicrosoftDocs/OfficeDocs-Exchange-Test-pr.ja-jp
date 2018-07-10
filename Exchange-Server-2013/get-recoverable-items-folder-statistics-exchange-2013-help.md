---
title: " フォルダーの統計を取得する: Exchange 2013 Help"
TOCTitle: " フォルダーの統計を取得する"
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52057867
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# [回復可能なアイテム] フォルダーの統計を取得する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-01-22_

\[回復可能なアイテム\] フォルダーには、Microsoft Outlook および Microsoft OfficeOutlook Web App のユーザーまたは Mailbox Assistant によって削除されたアイテムが格納されます。削除済みアイテムがこのフォルダーに残される期間は、メールボックス データベースまたはメールボックスに対して構成された削除済みアイテムの保存期間の設定に基づきます。既定では、メールボックス データベースは削除済みアイテムを 14 日間保存するように構成され、回復可能なアイテムの警告クォータおよび回復可能なアイテムのクォータはそれぞれ 20 GB (ギガバイト) と 30 GB に設定されます。ただし、メールボックスに対しインプレース保持または訴訟ホールドが有効になっている場合、\[回復可能なアイテム\] フォルダーは指定した保存期間を超えて削除済みアイテムを蓄積することができ、変更されたメールボックス アイテムの異なるバージョンを保持することもできます。

\[回復可能なアイテム\] フォルダーが回復可能なアイテムの警告クォータに到達すると、警告イベントがアプリケーション イベント ログに記録されます。メールボックスが訴訟ホールドの対象となっていない場合、アイテムは先入れ先出し法 (FIFO) で削除されます。しかし、メールボックスが訴訟ホールドの対象となっている場合は、メールボックスが空にされることはなく、回復可能なアイテムのクォータに達すると、メールボックスの機能は影響を受けます。

そのため、メールボックスが回復可能なアイテムのクォータに達するときに生成される警告についてイベントログを監視することが重要です。この手順を使用して、特に訴訟ホールドの対象となっているメールボックスに対し、\[回復可能なアイテム\] フォルダーの統計情報を報告することもできます。

詳細については、次のトピックを参照してください。

  - [\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)

  - [インプレース保持と訴訟ホールド](in-place-hold-and-litigation-hold-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス フォルダー」。

  - Exchange 管理センター (EAC) を使用して、メールボックスの \[回復可能なアイテム\] フォルダーの統計情報を取得することはできません。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 必要な作業

## 回復可能なアイテム フォルダーの統計情報を取得する

この例では、Soumya Singhi の \[回復可能なアイテム\] フォルダーの統計情報を取得し、リスト形式でその出力を表示します。

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List

この例では、Soumya Singhi の \[回復可能なアイテム\] フォルダーの統計情報を取得し、フォルダー名、フォルダー パス、フォルダー内のアイテム数、およびフォルダー サイズを表形式で表示します。

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize

構文およびパラメーターの詳細については、「[Get-MailboxFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa996762\(v=exchg.150\))」を参照してください。

## 訴訟ホールドの対象となっているすべてのメールボックスの回復可能なアイテム フォルダーの統計情報を取得する

この例では、訴訟ホールドの対象となっているすべてのメールボックスのリストを取得し、各メールボックスの \[回復可能なアイテム\] フォルダーとそのサブフォルダーの統計情報を取得します。**Identity** (メールボックス フォルダー ID) および **FolderAndSubfolderSize** プロパティは表形式で表示されます。

    Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize

構文およびパラメーターの詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」と「[Get-MailboxFolderStatistics](https://technet.microsoft.com/ja-jp/library/aa996762\(v=exchg.150\))」を参照してください。

## メールボックスの回復可能なアイテムのクォータを取得する

次の例は、ユーザー メールボックスの \[回復可能なアイテム\] フォルダーのクォータと警告クォータを表示しています。例では、メールボックスが訴訟ホールドまたはインプレース保持の対象になっているかどうかに関する情報も取得します。

    Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

次の例は、組織内のユーザー メールボックスすべての \[回復可能なアイテム\] フォルダーのクォータと警告クォータを表示しています。例では、保留情報も取得します。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

