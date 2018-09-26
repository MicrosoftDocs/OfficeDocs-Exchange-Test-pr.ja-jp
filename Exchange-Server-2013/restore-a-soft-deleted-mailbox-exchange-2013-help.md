---
title: '回復可能な削除によって削除されたメールボックスを復元する: Exchange 2013 Help'
TOCTitle: 回復可能な削除によって削除されたメールボックスを復元する
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50555776
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 回復可能な削除によって削除されたメールボックスを復元する

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-29_

シェルを使用して、回復可能な削除によって削除されたメールボックスを Active Directory ユーザー アカウントに接続する。メールボックスを別のメールボックス データベースに移動すると、そのメールボックスは移動元のメールボックス データベース内で*削除済み (回復可能)* の状態になります。Exchange は、移動が完了しても、移動元のメールボックス データベースからメールボックスを完全に削除しません。その代わり、ソース メールボックス データベースのメールボックスは、回復可能な削除によって削除された状態に移行します。これにより、移動中にエラーが発生したために移動先のデータベースのメールボックスで障害または破損が発生した場合に、移動元のメールボックスを復元できます。この問題が発生した場合、移動元のメールボックスを復元し、再度移動を試みることができます。

回復可能な削除によって削除されたメールボックスは、削除済みメールボックスの保持期間が経過するか **Remove-StoreMailbox** コマンドレットを使用して回復可能な削除によって削除されたメールボックスを削除するまでの間、移動元のデータベースに保持されます。回復可能な削除によって削除されたメールボックスが Exchange メールボックス データベースから完全に削除されるまで、シェルを使用して、回復可能な削除によって削除されたメールボックスのコンテンツを既存のメールボックスまたはアーカイブ メールボックスに復元できます。

回復可能な削除によって削除されたメールボックスの詳細、および関連する他の管理タスクの実行方法については、次のトピックを参照してください。

  - [未接続のメールボックス](disconnected-mailboxes-exchange-2013-help.md)

  - [削除されたメールボックスの接続または復元](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [メールボックス復元要求を管理する](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [メールボックスの完全削除](permanently-delete-a-mailbox-exchange-2013-help.md)

## 始める前に把握しておくべき情報

  - 予想所要時間: 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順は、シェルでのみ実行できます。EAC を使用して、回復可能な削除によって削除されたメールボックスを復元することはできません。

  - 次のコマンドを実行して、ユーザー アカウントを接続する回復可能な削除によって削除されたメールボックスがまだメールボックス データベース内に存在し、無効にされたメールボックスでないことを確認します。
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    ```
    
    回復可能な削除によって削除されたメールボックスは、メールボックス データベース内に存在する必要があり、*DisconnectReason* プロパティの値は `SoftDeleted` である必要があります。メールボックスがデータベースから削除されている場合、コマンドから結果は返されません。
    
    または、次のコマンドを実行して、組織内の回復可能な削除によって削除されたすべてのメールボックスを表示します。
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate
    ```

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

  - 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## シェルを使用して、回復可能な削除によって削除されたメールボックスを復元する

シェルを使用すると、回復可能な削除によって削除されたメールボックスを既存のメールボックスに復元できます。これには、**New-MailboxRestoreRequest** コマンドレットを使用します。回復可能な削除によって削除されたメールボックスを復元する場合、そのコンテンツは、*移動先メールボックス*と呼ばれる既存のメールボックスにコピーされます。メールボックスの復元要求が正常に完了すると、その要求は削除されるまで既定で 30 日間保持されます。**Remove-MailboxRestoreRequest** コマンドレットを使用すると、その要求をすぐに削除できます。

回復可能な削除によって削除されたメールボックスが復元された後、そのメールボックスは、管理者によって完全に削除されるか、削除済みメールボックスの保持期間が経過して削除されるまで、メールボックス データベースに保持されます。

メールボックスの復元要求を作成するには、回復可能な削除によって削除されたメールボックスの表示名、メールボックス GUID、または従来の識別名 (DN) を使用する必要があります。**Get-MailboxStatistics** コマンドレットを使用して、復元する回復可能な削除によって削除されたメールボックスの **DisplayName**、**MailboxGuid**、および **LegacyDN** プロパティの値を表示します。たとえば、次のコマンドを実行すると、組織内の無効にされたすべてのメールボックスと回復可能な削除によって削除されたすべてのメールボックスに関して、この情報が返されます。

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database
```

この例では、*SourceStoreMailbox* パラメーターの表示名で識別され、MBXDB01 メールボックス データベースにある回復可能な削除によって削除されたメールボックスを、Debra Garcia という名前の移動先メールボックスに復元します。*AllowLegacyDNMismatch* パラメーターを使用すると、移動元メールボックスを、回復可能な削除によって削除されたメールボックスと同じ従来の DN 値を持たないメールボックスに復元できます。

```powershell
New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch
```

この例では、メールボックス GUID で識別される Pilar Pinilla の回復可能な削除によって削除されたアーカイブ メールボックスを、彼女の現在のアーカイブ メールボックスに復元します。この場合、プライマリ メールボックスと対応するアーカイブ メールボックスの従来の DN が同じであるため、*AllowLegacyDNMismatch* パラメーターは不要です。

```powershell
New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive
```

構文およびパラメーターの詳細については、「[New-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829875\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

回復可能な削除によって削除されたメールボックスが移動先メールボックスに正常に復元されたことを確認するには、**Get-MailboxRestoreRequest** コマンドレットまたは **Get-MailboxRestoreRequestStatistics** コマンドレットを実行して、復元要求に関する情報を表示します。復元要求が正常に作成された場合、*Status* プロパティの値は、**Queued**、**InProgress**、または **Completed** になります。復元要求が完了すると、回復可能な削除によって削除されたメールボックスのコンテンツが移動先メールボックスに表示されます。

詳細については、次のトピックを参照してください。

  - [メールボックス復元要求を管理する](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ja-jp/library/ff829912\(v=exchg.150\))

