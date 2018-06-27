---
title: 'メールボックスの完全削除: Exchange 2013 Help'
TOCTitle: メールボックスの完全削除
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50555887
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの完全削除

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2012-11-16_

アクティブ メールボックスや切断されたメールボックスを完全に削除すると、メールボックスのすべてのコンテンツが Exchange メールボックス データベースから削除されれデータを復旧できなくなります。アクティブ メールボックスを完全に削除すると、関連付けられている Active Directory ユーザー アカウントも削除されます。

メールボックスの完全削除の代わりに選択できる方法が、メールボックスの切断です。メールボックスを切断した場合、既定では、そのメールボックスはメールボックス データベースに 30 日間保存されます。このため、切断したメールボックスについては、データベースから削除されるまでに再接続や復元の機会があります。

切断されたメールボックスおよびその他の関連する管理タスクの実行方法の詳細については、次のトピックを参照してください。

  - [未接続のメールボックス](disconnected-mailboxes-exchange-2013-help.md)

  - [メールボックスの無効化または削除](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [無効にされたメールボックスを接続する](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [削除されたメールボックスの接続または復元](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)


> [!NOTE]
> EAC を使用して、アクティブ メールボックスや切断されたメールボックスを完全に削除することはできません。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## アクティブ メールボックスを完全に削除する

## シェルを使用してアクティブ メールボックスを完全に削除する

次のコマンドを実行して、アクティブ メールボックスと関連付けられている Active Directory ユーザー アカウントを完全に削除します。

    Remove-Mailbox -Identity <identity> -Permanent $true


> [!NOTE]
> <EM>Permanent</EM> パラメーターを含めなければ、既定で、削除されたメールボックスはメールボックス データベースに 30 日間保存され、その後完全に削除されます。



構文およびパラメーターの詳細については、「[Remove-Mailbox](https://technet.microsoft.com/ja-jp/library/aa995948\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

アクティブ メールボックスを完全に削除したことを確認するには、次の手順を実行します。

1.  メールボックスが EAC に表示されなくなったことを確認します。

2.  関連付けられているユーザー アカウントが Active Directory ユーザーとコンピューターに表示されなくなったことを確認します。

3.  次のコマンドを実行して、Exchange メールボックス データベースからメールボックスが正常に削除されたことを確認します。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }
    
    メールボックスが正常に削除されていれば、コマンドは結果を返しません。メールボックスが削除されていない場合、コマンドはメールボックスに関する情報を返します。

## 切断されたメールボックスを完全に削除する

## シェルを使用して切断されたメールボックスを完全に削除する

切断されたメールボックスには、無効化されたメールボックス、および回復可能な削除によって削除されたメールボックスの 2 種類があります。コマンドレットを実行してメールボックスを完全に削除する場合、どちらかの種類を指定する必要があります。指定した種類が切断されたメールボックスの実際の種類と一致しない場合、コマンドは失敗します。

切断されたメールボックスが無効化されているかそれとも回復可能な削除によって削除されているかを確認するには、次のコマンドを実行します。

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason

切断されたメールボックスの *DisconnectReason* プロパティの値は、`Disabled` または `SoftDeleted` です。

組織内のすべての切断されたメールボックスの種類を表示するために、次のコマンドを実行できます。

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason


> [!WARNING]
> <STRONG>Remove-StoreMailbox</STRONG> コマンドレットを使用して切断されたメールボックスを完全に削除すると、そのすべてのコンテンツがメールボックス データベースから削除され、データは完全に失われます。



この例では、メールボックス データベース MBD01 から、GUID が 2ab32ce3-fae1-4402-9489-c67e3ae173d3 の無効化されたメールボックスを完全に削除します。

    Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled

この例では、メールボックス データベース MBD01 から、回復可能な削除によって削除された Dan Jump のメールボックスを完全に削除します。

    Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted

この例では、メールボックス データベース MBD01 から、回復可能な削除によって削除されたメールボックスをすべて完全に削除します。

    Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}

構文およびパラメーターの詳細については、「[Remove-StoreMailbox](https://technet.microsoft.com/ja-jp/library/ff829913\(v=exchg.150\))」と「[Get-MailboxStatistics](https://technet.microsoft.com/ja-jp/library/bb124612\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

切断されたメールボックスを完全に削除したことと、Exchange メールボックス データベースからそのメールボックスが正常に削除されたことを確認するには、次のコマンドを実行します。

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }

メールボックスが正常に削除されていれば、コマンドは結果を返しません。メールボックスが削除されていない場合、コマンドはメールボックスに関する情報を返します。

