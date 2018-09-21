---
title: 'メールボックス データベースのコピーのライセンス認証ポリシーを構成する: Exchange 2013 Help'
TOCTitle: メールボックス データベースのコピーのライセンス認証ポリシーを構成する
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 48269616
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス データベースのコピーのライセンス認証ポリシーを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-02_

*アクティブ化*は、メールボックス データベースのコピーをパッシブ コピーからアクティブ コピーに変更する処理です。アクティブ化は、データベースまたはサーバーのフェールオーバー操作の一部としてシステムにより自動的に行われますが、データベースまたはサーバーの切り替え操作の一部として管理者が手動で実行することもできます。データベースまたはサーバーのフェールオーバー中にデータベースのアクティブ化がブロックされると、データベースのコピーはアクティブ コピーに変更されません。

メールボックス データベース コピーに関連する他の管理タスクについては、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス データベースのコピーのアクティブ化ポリシーを構成する

1.  
    
    EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  構成するデータベースを選択します。

3.  
    
    \[詳細\] ウィンドウの <strong>データベース コピー</strong> で、構成するデータベース コピーを指定して <strong>中断</strong> をクリックします。

4.  必要に応じてコメントを追加し、<strong>このコピーは手動操作によってのみアクティブにできます</strong> というチェック ボックスをオンにします。

5.  <strong>保存</strong> をクリックしてメールボックス データベース コピーの構成変更を保存します。

## シェルを使用してデータベース コピーのアクティブ化を中断または再開する

この例では、サーバー MBX2 上にあるデータベース DB1 のコピーのアクティブ化をブロックします。

```powershell
Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly
```

この例では、サーバー MBX2 上にあるデータベース DB1 のコピーのアクティブ化を再開します。

```powershell
Resume-MailboxDatabaseCopy -Identity DB1\MBX2
```

構文およびパラメーターの詳細については、「[Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd351074\(v=exchg.150\))」または「[Resume-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335220\(v=exchg.150\))」を参照してください。

## シェルを使用してサーバーのアクティブ化ポリシーを構成する

この例では、サーバー MBX2 上のデータベース コピーについて、アクティブ化をブロックするように構成します。

```powershell
Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked
```

この例では、サーバー MBX3 上のデータベース コピーについて、サイト外のアクティブ化をブロックするように構成します。

```powershell
Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly
```

この例では、サーバー MBX4 上のデータベース コピーについて、アクティブ化のブロックを解除するように構成します。

```powershell
Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted
```

構文およびパラメーターの詳細については、「[Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd351074\(v=exchg.150\))」、「[Resume-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335220\(v=exchg.150\))」または「[Set-MailboxServer](https://technet.microsoft.com/ja-jp/library/aa998651\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

アクティブ化ポリシーが正常に構成されたことを確認するには、次のいずれかの手順を実行します。

  - シェルで次のコマンドを実行して、データベース コピーのアクティブ化設定を確認します。
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended
```

  - シェルで次のコマンドを実行して、DAG メンバーのアクティブ化設定を確認します。
    
    ```powershell
Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy
```

