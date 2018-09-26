---
title: 'メールボックス データベース コピーをアクティブにする: Exchange 2013 Help'
TOCTitle: メールボックス データベース コピーをアクティブにする
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 48270126
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックス データベース コピーをアクティブにする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-01_

メールボックス データベース コピーのアクティブ化は、特定のパッシブ コピーをメールボックス データベースの新しいアクティブ コピーとして指定するプロセスです。このプロセスは、*データベースの切り替え*と呼ばれます。データベースの切り替えでは、現在アクティブなデータベースのマウントを解除し、指定のサーバーに新しいアクティブ メールボックス データベース コピーとしてデータベース コピーをマウントします。アクティブ メールボックス データベースになるデータベース コピーは、正常で、最新の状態になっている必要があります。

メールボックス データベース コピーに関連する他の管理タスクについては、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間: 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してアクティブ メールボックス データベースを移動する

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  コピーをアクティブにするデータベースを選択します。

3.  \[詳細\] ウィンドウの <strong>データベース コピー</strong> で、アクティブにするデータベース コピーの下にある <strong>アクティブにする</strong> をクリックします。

4.  <strong>はい</strong> をクリックして、データベース コピーをアクティブします。

## シェルを使用してアクティブ メールボックス データベースを移動する

この例では、MBX3 上でホストされているデータベース DB4 のコピーをアクティブ化して、マウントします。このコマンドにより、DB4 が新しいアクティブ メールボックス データベースになり、MBX3 のデータベース マウント ダイヤル設定は上書きされません。

```powershell
Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None
```

この例では、データベース DB2 とメールボックス サーバー MBX1 との間の切り替えを実行します。コマンドが完了すると、MBX1 は DB2 のアクティブ コピーをホストします。*MountDialOverride* パラメーターは `None` に設定されているため、MBX1 は独自に定義済みのデータベースの自動マウント ダイヤル設定を使用してデータベースをマウントします。

```powershell
Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None
```

この例では、データベース DB1 とメールボックス サーバー MBX3 との間の切り替えを実行します。コマンドが完了すると、MBX3 は DB1 のアクティブ コピーをホストします。*MountDialOverride* パラメーターには `Good Availability` の値が指定されているため、MBX3 は、*GoodAvailability* のデータベース自動マウント ダイヤル設定を使用してデータベースをマウントします。

```powershell
Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability
```

この例では、データベース DB3 とメールボックス サーバー MBX4 との間の切り替えを実行します。コマンドが完了すると、MBX4 は DB3 のアクティブ コピーをホストします。*MountDialOverride* パラメーターは指定されていないため、MBX4 は、*Lossless* のデータベース自動マウント ダイヤル設定を使用してデータベースをマウントします。

```powershell
Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4
```

この例では、メールボックス サーバー MBX1 のサーバー切り替えを実行します。MBX1 上のすべてのアクティブ メールボックス データベース コピーは、MBX1 上のアクティブ データベースの正常なコピーを使用して 1 つまたは複数のその他のメールボックス サーバー上でアクティブ化されます。

```powershell
Move-ActiveMailboxDatabase -Server MBX1
```

この例では、データベース DB4 とメールボックス サーバー MBX5 との間の切り替えを実行します。この例では、MBX5 上のデータベース コピーに、長さが 6 を超える再生キューがあります。そのため、*SkipLagChecks* パラメーターを指定して、MBX5 上のデータベース コピーをアクティブ化する必要があります。

```powershell
Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks
```

この例では、データベース DB5 とメールボックス サーバー MBX6 との間の切り替えを実行します。この例では、MBX6 上のデータベース コピーが失敗の *ContentIndexState* になっています。そのため、*SkipClientExperienceChecks* パラメーターを指定して、MBX6 上のデータベース コピーをアクティブ化する必要があります。

```powershell
Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks
```

## 正常な動作を確認する方法

メールボックス データベース コピーが正常にアクティブ化されたことを確認するには、次のいずれかを実行します。

  - EAC で <strong>サーバー</strong> \> <strong>データベース</strong> に移動します。適切なデータベースを選択し、\[詳細\] ウィンドウで <strong>詳細の表示</strong> をクリックして、データベース コピーのプロパティを表示します。

  - シェルで次のコマンドを実行して、データベース コピーの状態情報を表示します。
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
    ```

## 詳細情報

[メールボックス データベース コピー](mailbox-database-copies-exchange-2013-help.md)

[メールボックス データベースのコピーのプロパティを構成する](configure-mailbox-database-copy-properties-exchange-2013-help.md)

