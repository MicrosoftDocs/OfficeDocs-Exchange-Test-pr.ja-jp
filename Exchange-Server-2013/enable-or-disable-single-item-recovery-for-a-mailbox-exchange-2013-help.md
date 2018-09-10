---
title: 'メールボックスの単一アイテムの回復を有効または無効にする: Exchange Online Help'
TOCTitle: メールボックスの単一アイテムの回復を有効または無効にする
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54651677
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの単一アイテムの回復を有効または無効にする

 

_**適用先:** Exchange Online, Exchange Server 2013_

メールボックスの単一アイテムの回復は、シェルを使用して有効または無効にすることができます。Exchange Online では、新しいメールボックスの作成時に単一アイテムの回復が既定で有効になります。Exchange 2013 では、メールボックスの作成時には単一アイテムの回復は無効になっています。単一アイテムの回復が有効になっている場合、ユーザーによって完全に削除されたメッセージは、削除済みアイテムの保持期間が過ぎるまでメールボックスの \[回復可能なアイテム\] フォルダーに保存されます。これにより、管理者は、削除済みアイテムの保持期間が過ぎる前に、ユーザーによって削除されたメッセージを回復できます。また、単一アイテムの回復が有効になっていれば、ユーザーまたはプロセスによってメッセージが変更されたときに、元のアイテムのコピーの保存も行われます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「保存期間および法的情報保留」。

  - Exchange 管理センター (EAC) を使用して単一アイテムの回復を有効または無効にすることはできません。

  - Exchange Online では、既定で、削除済みアイテム保存期間が 14 日に設定されます。この設定は最大 30 日にまで変更できます。詳細については、「[Exchange Online メールボックスの完全に削除したアイテムの保持期間を変更する](https://technet.microsoft.com/ja-jp/library/dn163584\(v=exchg.150\))」を参照してください。

  - Exchange 2013 では、メールボックスは既定でメールボックス データベースの削除済みアイテムの保存期間の設定を使用します。メールボックス データベースの削除済みアイテム保存期間は 14 日に設定されていますが、この設定をメールボックス単位で構成して既定値を書き換えることができます。詳細については、「[削除済みアイテムの保存期間と回復可能なアイテムのクォータを構成する](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## シェルを使用して単一アイテムの回復を有効にする

この例では、April Summers のメールボックスの単一アイテムの回復を有効にします。

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

この例では、Pilar Pinilla のメールボックスの単一アイテムの回復を有効にして、削除済みアイテムの保存日数を 30 日に設定します。

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

この例では、組織内のすべてのユーザー メールボックスの単一アイテムの回復を有効にします。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

この例では、組織内のすべてのユーザー メールボックスに対して単一アイテムの回復が有効にされ、削除済みアイテムを保持する日数が 30 日間に設定されます。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## シェルを使用して単一アイテムの回復を無効にする

ユーザーのメールボックスの単一アイテムの回復を無効にする必要がある場合があります。たとえば、**Search-Mailbox – DeleteContent** を使用してメールボックスからコンテンツを完全に削除できるようにするには、単一アイテムの回復を無効にする必要があります。詳細については、「[メッセージを検索して削除する - 管理者向けヘルプ](search-for-and-delete-messages-admin-help-exchange-2013-help.md)」を参照してください。

この例では、Ayla Kol のメールボックスの単一アイテムの回復を無効にします。

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## 正常な動作を確認する方法

メールボックスの単一アイテムの回復が有効になっていることを確認し、削除済みアイテムの保存期間に関する値 (日単位) を表示するには、次のコマンドを実行します。

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

この同じコマンドを使用して、メールボックスに対して単一アイテムの回復が無効にされていることを確認できます。

## 詳細情報

  - 単一アイテムの回復の詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」を参照してください。ユーザーによって削除されたメッセージを削除済みアイテム保持期間が過ぎる前に回復するには、「[ユーザーのメールボックス内の削除済みメッセージを復元する](https://docs.microsoft.com/ja-jp/exchange/recipients-in-exchange-online/manage-user-mailboxes/recover-deleted-messages)」を参照してください。

  - メールボックスがインプレース ホールドまたは訴訟ホールドになっている場合、保持期間が経過するまで、\[回復可能なアイテム\] フォルダー内のメッセージは保持されます。保持期間が無期限である場合は、ホールドが解除されるか、または保持期間が変更されるまで、アイテムは保持されます。

