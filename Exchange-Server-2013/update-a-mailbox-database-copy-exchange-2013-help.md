---
title: 'メールボックス データベース コピーの更新: Exchange 2013 Help'
TOCTitle: メールボックス データベース コピーの更新
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 48269992
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス データベース コピーの更新

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-02_

更新処理 (*シード処理*と呼ばれることもあります) は、メールボックス データベース コピーを、データベース可用性グループ (DAG) 内の別のメールボックス サーバーに追加する処理です。新たに追加されたコピーは、アクティブ コピーからコピーされたログ ファイルが再生されるパッシブ コピーのベースライン データベースになります。以下の条件が発生した場合はシードを行う必要があります。

  - データベースの新しいパッシブ コピーが作成された場合。新しいメールボックス データベース コピーでシードが延期されますが、各パッシブ データベース コピーは最終的には冗長データベース コピーとして機能するためにシードされる必要があります。

  - パッシブ データベース コピーに相違があり回復不能であるためにデータが失われてフェールオーバーが発生した後。

  - データベースのパッシブ コピーに対して再生できない破損したログ ファイルがシステムで検出されたとき。

  - いずれかのデータベース コピーに対するオフラインでのディスクの最適化が発生した後。

  - データベースのログ生成シーケンスがリセットされ、1 に戻った後。

以下の方法を使用して、シードを実行できます。

  - <strong>自動シード</strong>   自動シードは、ターゲット メールボックス サーバー上でアクティブ データベースのパッシブ コピーを生成します。自動シードはデータベースの作成中にのみ発生します。

  - **Update-MailboxDatabaseCopy コマンドレットを使用したシード**   シェルで [Update-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335201\(v=exchg.150\)) コマンドレットを使用して、データベース コピーをいつでもシードできます。

  - <strong>データベース コピーの更新\] ウィザードを使用したシード**   EAC の \[データベース コピーの更新\] ウィザードを使用して、データベース コピーをいつでもシードできます。

  - **オフライン データベースの手動によるコピー**   データベースのアクティブ コピーのマウントを解除し、同じ DAG 内で、他のメールボックス サーバー上の同じ場所にデータベース ファイルをコピーできます。この方法を使用すると、データベースを解除するプロセスが必要になるため、サービスが中断します。

データベース コピーの更新処理には、長い時間がかかる可能性があります。コピーするデータベースが大きい場合、ネットワークの遅延が大きい場合、ネットワークの帯域幅が狭い場合は、特に長い時間がかかります。シード処理が開始されたら、処理が完了するまで EAC やシェルを閉じないでください。閉じてしまうと、シード処理が終了します。

アクティブ コピーまたは最新のパッシブ コピーをシードのソースとして使用して、データベース コピーをシードできます。パッシブ コピーからのシードの場合、次の環境ではネットワーク通信エラーが発生しシード操作が終了しますので注意してください。

  - シード ソースのコピーの状態が "Failed" または "FailedAndSuspended" に変わった場合。

  - データベースが他のコピーにフェールオーバーした場合。

複数のデータベース コピーを同時にシードできます。ただし、複数のコピーを同時にシードする場合は、データベース ファイルのみをシードし、コンテンツ インデックス カタログを省略する必要があります。[Update-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd335201\(v=exchg.150\)) コマンドレットで *DatabaseOnly* パラメーターを使用してこの操作を行うことができます。


> [!NOTE]
> 同一のソースから複数のターゲットをシードする際に <EM>DatabaseOnly</EM> パラメーターを使用しない場合は、SeedInProgressException エラー FE1C6491 が発生してタスクが失敗します。



メールボックス データベース コピーに関連する他の管理タスクについては、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:2 分 + データベースのコピーにかかる時間 (データベースの規模、速度、利用可能な帯域幅、ネットワークの待機時間、ストレージの速度など、さまざまな要因による)。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - メールボックス データベースのコピーが中断されている。詳細な手順については、「[メールボックス データベース コピーを中断または再開する](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md)」を参照してください。

  - 更新しているパッシブ データベース コピーをホストしているサーバーで、リモート レジストリ サービスを実行している。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス データベース コピーを更新する

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  更新するパッシブ コピーがあるメールボックス データベースを選択します。

3.  詳細ウィンドウの <strong>データベース コピー</strong> タブで、シードするパッシブ データベース コピーの下にある <strong>中断</strong> をクリックします。オプションのコメントを記入し、<strong>保存</strong> をクリックします。

4.  詳細ウィンドウの <strong>データベース コピー</strong> タブで、シードするパッシブ データベース コピーの下にある <strong>更新</strong> をクリックします。

5.    
    既定では、データベースのアクティブ コピーがシードのソース データベースとして使用されます。シードにデータベースのパッシブ コピーを使用する場合は、<strong>参照</strong> をクリックして、シード元として使用するパッシブ データベースのコピーを含むサーバーを選択します。

6.  <strong>保存</strong> をクリックして、パッシブ データベース コピーを更新します。

## シェルを使用してメールボックス データベース コピーを更新する

この例では、MBX1 上のデータベース DB1 のコピーをシードする方法を示します。

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1
```

この例は、シード用のソース メールボックス サーバーとして MBX2 を使用して、MBX1 上のデータベース DB1 のコピーをシードする方法を示します。

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2
```

この例では、コンテンツ インデックス カタログをシードせずに、MBX1 上のデータベース DB1 のコピーをシードする方法を示します。

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly
```

この例では、データベース ファイルをシードせずに、MBX1 上のデータベース DB1 のコピーのコンテンツ インデックス カタログをシードする方法を示します。

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly
```

## オフライン データベースを手動でコピーする

1.  データベースに対して循環ログが有効になっている場合、処理の前に無効にする必要があります。メールボックス データベースの循環ログを無効にするには、次の例のように [Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\)) コマンドレットを使用します。
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $false
    ```

2.  データベースのマウントを解除する。この例のように、[Dismount-Database](https://technet.microsoft.com/ja-jp/library/bb124936\(v=exchg.150\)) コマンドレットを使用できます。
    
    ```powershell
    Dismount-Database DB1 -Confirm $false
    ```

3.  手動で、データベース ファイル (データベース ファイルとすべてのログ ファイル) を外部のディスク ドライブやネットワーク共有などの別の場所にコピーします。

4.  データベースをマウントします。この例のように、[Mount-Database](https://technet.microsoft.com/ja-jp/library/aa998871\(v=exchg.150\)) コマンドレットを使用できます。
    
    ```powershell
    Mount-Database DB1
    ```

5.  コピーをホストするサーバー上で、外部のドライブまたはネットワーク共有からアクティブなデータベース コピーと同じパスにデータベース ファイルをコピーします。たとえば、アクティブ コピーのデータベースのパスが D:\\DB1\\DB1.edb で、ログ ファイルのパスが D:\\DB1 である場合、そのコピーをホストするサーバー上の D:\\DB1 にデータベース ファイルをコピーします。

6.  この例のように、*SeedingPostponed* パラメーターを指定して [Add-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd298105\(v=exchg.150\)) コマンドレットを使用し、メールボックス データベースのコピーを追加します。
    
    ```powershell
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed
    ```

7.  データベースに循環ログが有効になっている場合、この例のように、[Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\)) コマンドレットを使用して、循環ログを再度有効にします。
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $true
    ```

## 正常な動作を確認する方法

メールボックス データベース コピーが正常にシードされたことを確認するには、次のいずれかを実行します。

  - EAC で <strong>サーバー</strong> \> <strong>データベース</strong> に移動します。シードされたデータベースを選択します。詳細ペインに、データベースのコピーの状況とそのコンテンツ インデックスが、現在のコピー キューの長さと共に表示されます。

  - シェルで次のコマンドを実行して、メールボックス データベースのコピーが正常にシードされ、かつ正常な状態にあることを確認します。
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    ```
    
    ステータスとコンテンツ インデックス ステータスの両方が正常である必要があります。

