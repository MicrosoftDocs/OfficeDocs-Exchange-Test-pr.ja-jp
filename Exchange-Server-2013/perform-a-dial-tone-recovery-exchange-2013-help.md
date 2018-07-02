---
title: 'ダイヤル トーン回復を実行する: Exchange 2013 Help'
TOCTitle: ダイヤル トーン回復を実行する
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51407504
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ダイヤル トーン回復を実行する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-06-27_

ダイヤル トーン ポータビリティを使用することで、ユーザーは、自分のメールボックスが復元中または修復中の場合に、電子メールの送受信用に一時メールボックスを持つことができます。一時メールボックスは、同じ Exchange 2013 メールボックス サーバー上、または組織内の他のExchange 2013 メールボックス サーバー上に持つことができます。ダイヤル トーン ポータビリティを使用する処理のことをダイヤル トーン復旧と呼びます。この処理では、メールボックス サーバー上に、障害が発生したデータベースを代替する空のデータベースが作成されます。詳細については、「[ダイヤル トーンの移植性](dial-tone-portability-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分にデータの復元と移動にかかる時間を合計した時間。

  - ダイヤル トーン データベースを作成するには、展開されているデータベース数が最大数よりも少ない必要があります。Exchange 2013 Standard Edition は、1 サーバーあたり最大 5 つのデータベースをサポートします。Exchange 2013 Enterprise Edition は、RTM と CU1 ではサーバーごとに最大 50 のデータベースを、CU2 以降ではサーバーごとに最大 100 のデータベースをサポートします。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス回復」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## シェルを使用して、単一サーバー上でダイヤル トーン復旧を実行する


> [!NOTE]
> EAC を使用して、単一サーバー上でダイヤル トーン復旧を実行することはできません。



1.  その後の復旧操作に必要となる場合、復旧対象データベースの任意の既存ファイルが保持されるようにしてください。

2.  この例の方法で [New-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/aa997976\(v=exchg.150\)) コマンドレットを使用して、ダイヤル トーン データベースを作成します。
    
        New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB

3.  この例の方法で [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\)) コマンドレットを使用して、復旧対象データベース上にホストされるユーザー メールボックスを移動します。
    
        Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1

4.  この例の方法で [Mount-Database](https://technet.microsoft.com/ja-jp/library/aa998871\(v=exchg.150\)) コマンドレットを使用して、データベースをマウントして、クライアント コンピューターがデータベースにアクセスして、メッセージを送受信できるようにします。
    
        Mount-Database -Identity DTDB1

5.  回復データベース (RDB) を作成して、回復するデータを含むデータベースとログ ファイルを RDB に回復、またはコピーします。詳細な手順については、「[回復用データベースを作成する](create-a-recovery-database-exchange-2013-help.md)」を参照してください。

6.  データを RDB にコピーした後、回復したデータベースをマウントする前に、障害が発生したデータベースから回復データベースのログ フォルダーにすべてのログ ファイルをコピーして、回復されたデータベースに対してログ ファイルを再生できるようにします。

7.  この例の方法で RDB をマウントしてから、[Dismount-Database](https://technet.microsoft.com/ja-jp/library/bb124936\(v=exchg.150\)) コマンドレットを使用してマウント解除します。
    
        Mount-Database -Identity RDB1
        Dismount-Database -Identity RDB1

8.  RDB のマウント解除後、RDB フォルダー内の現在のデータベースとログ ファイルを安全な場所に移動します。これは、回復したデータベースとダイヤル トーン データベースとを交換する準備段階で行われます。

9.  この例の方法でダイヤル トーン データベースをマウント解除します。このデータベースをマウント解除すると、エンド ユーザーに対するサービスの中断が発生します。
    
        Dismount-Database -Identity DTDB1

10. ダイヤル トーン データベース フォルダーから RDB フォルダーにデータベースとログ ファイルを移動します。

11. この例の方法で、回復したデータベースを含む安全な場所からダイヤル トーン データベース フォルダーにデータベースとログ ファイルを移動し、データベースをマウントします。
    
        Mount-Database -Identity DTDB1
    
    これにより、エンド ユーザーに対するサービスが再開します。エンド ユーザーは、本来の運用データベースにアクセスして、メッセージを送受信できるようになります。

12. この例の方法で RDB をマウントします。
    
        Mount-Database -Identity RDB1

13. この例の方法で、[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\)) および [New-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829875\(v=exchg.150\)) コマンドレットを使用して、RDB からデータをエクスポートし、それを復旧したデータベースにインポートします。これにおり、ダイヤル トーン データベースを使用して送受信されたすべてのメッセージが運用データベースにインポートされます。
    
        $mailboxes = Get-Mailbox -Database DTDB1
    
        $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }

14. 復旧操作が完了したら、この例の方法で RDB をマウント解除して削除します。
    
        Dismount-Database -Identity RDB1
        Remove-MailboxDatabase -Identity RDB1

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [New-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/ja-jp/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/ja-jp/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/aa997931\(v=exchg.150\))

## 正常な動作を確認する方法

メールボックスが正常に移動されたことを確認するには、次の手順を実行します。

  - Microsoft Office Outlook Web App を使用してメールボックスを開きます。

  - Microsoft Outlook を使用してメールボックスを開きます。

