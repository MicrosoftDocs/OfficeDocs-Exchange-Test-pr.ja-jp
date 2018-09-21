---
title: 'メールボックス データベース コピーを追加する: Exchange 2013 Help'
TOCTitle: メールボックス データベース コピーを追加する
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 48269680
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックス データベース コピーを追加する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-30_

メールボックス データベースのコピーを追加すると、既存のデータベースとデータベースのコピー間での連続レプリケーションが自動的に有効になります。データベースのコピーには、\<*DatabaseName*\>\\\<*HostMailboxServerName*\> という形式の識別子が自動的に割り当てられます。たとえば、サーバー MBX3 にホストされているデータベース DB1 のコピーは、DB1\\MBX3 になります。

メールボックス データベース コピーに関連する他の管理タスクについては、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:2 分 + データベースのコピーにかかる時間 (データベースの規模、速度、利用可能な帯域幅、ネットワークの待機時間、ストレージの速度など、さまざまな要因による)。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - データベースのアクティブ コピーがマウントされている必要があります。

  - 指定されたメールボックス サーバーが、データベースのコピーをすでにホストしていてはいけません。

  - データベース コピーのパスとそのログ ファイルが、選択されたメールボックス サーバー上に存在する必要があります。

  - アクティブ コピーをホストするサーバー、およびパッシブ コピーをホストすることになるサーバーは、同一のデータベース可用性グループ (DAG) に存在する必要があります。DAG にはクォーラムが存在し、正常である必要もあります。

  - データベースの 2 番目のコピーを追加する場合 (データベースの最初のパッシブ コピーを作成する場合など)、循環ログをその指定されたメールボックス データベースで有効にしないでください。循環ログが有効である場合、先に無効にする必要があります。メールボックス データベースのコピーが追加されたら、循環ログを有効にできます。レプリケートされたメールボックス データベースで循環ログを有効にすると、JET 循環ログの代わりに連続レプリケーション循環ログ (CRCL) が使用されます。データベースの 3 番目以降のコピーを追加する場合は、CRCL を有効なままにできます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス データベース コピーを追加する

1.  
    
    EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  コピーするデータベースを選択し、![データベース コピーの追加](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "データベース コピーの追加") をクリックします。

3.  
    
    <strong>メールボックス データベース コピーの追加</strong> ページで、<strong>参照...</strong> をクリックし、データベースのコピーをホストするメールボックス サーバーを選択して、<strong>OK</strong> をクリックします。

4.  必要に応じて、データベース コピーの <strong>アクティブ化の優先順位</strong> を構成します。

5.  <strong>その他のオプション…</strong> をクリックして、再生の時間差を構成することによりデータベース コピーを時間差データベース コピーとして指定するか、データベース コピーの自動シードを延期します。

6.  <strong>保存</strong> をクリックして構成変更を保存し、メールボックス データベース コピーを追加します。

7.  <strong>OK</strong> をクリックして、表示されるメッセージを確認します。

## シェルを使用したメールボックス データベース コピーの追加

この例では、メールボックス データベース DB1 のコピーをメールボックス サーバー MBX3 に追加します。再生ラグ タイムと切り詰めラグ タイムは、既定値 0 のままであり、ライセンス認証の設定は値 2 で構成されます。

```powershell
Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2
```

この例では、メールボックス データベース DB2 のコピーをメールボックス サーバー MBX4 に追加します。再生ラグ タイムと切り詰めラグ タイムは、既定値 0 のままであり、ライセンス認証の設定は値 `5` で構成されます。さらに、現在のアクティブなデータベース コピーの代わりに、MBX4 とは地理的に離れた場所にあるローカルのシード元サーバーを使用してシードできるように、このコピーのシード処理は延期されます。

```powershell
Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed
```

この例では、メールボックス データベース DB3 のコピーをメールボックス サーバー MBX5 に追加します。再生ラグ タイムは 3 日に設定され、切り詰めラグ タイムは既定値 0 のままであり、ライセンス認証の設定は値 `4` で構成されます。

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4

## 正常な動作を確認する方法

メールボックス データベース コピーが正常に作成されたことを確認するには、次のいずれかを実行します。

  - EAC で <strong>サーバー</strong> \> <strong>データベース</strong> に移動します。コピーされたデータベースを選択します。\[詳細\] ウィンドウに、データベースのコピーの状況とそのコンテンツ インデックスが、現在のコピー キューの長さと共に表示されます。

  - シェルで次のコマンドを実行して、メールボックス データベースのコピーが作成され、かつ正常な状態にあることを確認します。
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
```
    
    ステータスとコンテンツ インデックス ステータスの両方が正常である必要があります。

## 詳細情報

[メールボックス データベース コピー](mailbox-database-copies-exchange-2013-help.md)

[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)

