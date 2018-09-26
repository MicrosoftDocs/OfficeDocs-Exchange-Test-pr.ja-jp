---
title: 'メールボックス データベースのコピーのプロパティを構成する: Exchange 2013 Help'
TOCTitle: メールボックス データベースのコピーのプロパティを構成する
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 48270065
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# メールボックス データベースのコピーのプロパティを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-01_

各メールボックス データベース コピーは、それぞれが構成可能なプロパティを持っています。これには、再生ラグ タイム、切り詰めラグ タイム、アクティブ化優先順位番号が含まれることがあります。再生ラグ、切り詰めラグ、アクティブ化優先順位番号の詳細については、「[メールボックス データベースのコピーの管理](managing-mailbox-database-copies-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間: 1 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用してメールボックス データベース コピーのプロパティを構成する

1.  EAC で、<strong>サーバー</strong> \> <strong>データベース</strong> に移動します。

2.  構成するデータベースを選択します。

3.  \[詳細\] ウィンドウの <strong>データベース コピー</strong> で、必要なデータベース コピーの <strong>詳細の表示</strong> をクリックし、次の項目を表示または構成します。
    
      - <strong>データベース</strong>   選択したデータベースの名前を表示します。
    
      - <strong>メールボックス サーバー</strong>   選択したデータベース コピーをホストするメールボックス サーバーの名前を表示します。
    
      - <strong>コンテンツ インデックスの状態</strong> 選択したデータベース コピーのコンテンツ インデックスの現在の状態を表示します。
    
      - <strong>状態</strong>   選択したデータベース コピーの現在の状態を表示します。
    
      - <strong>コピー キューの長さ</strong>   選択したデータベース コピーへのコピーを待っているログ ファイルの数を示します。このフィールドは、パッシブ データベース コピーのみに関連しています。
    
      - <strong>再生キューの長さ</strong>   選択したデータベース コピーへの再生を待っているログ ファイルの数を示します。このフィールドは、パッシブ データベース コピーのみに関連しています。
    
      - <strong>エラー メッセージ</strong>   状態が「`Failed`」または「`Failed and Suspended`」であるデータベース コピーのエラー メッセージを表示します。
    
      - <strong>最新の空きログ時間</strong>   データベースのアクティブなコピー上で生成された最新のログ ファイルの日付とタイム スタンプを表示します。このフィールドは、パッシブ データベース コピーのみに関連しています。(レプリケートされたスタンドアロンの) アクティブなデータベース コピーでは、このフィールドは**無効**と表示されます。
    
      - <strong>最後に検査されたログの時刻</strong>   選択したデータベース コピーで LogInspector によって検査された最後のログ ファイルの日付とタイム スタンプを表示します。このフィールドは、パッシブ データベース コピーのみに関連しています。(レプリケートされたスタンドアロンの) アクティブなデータベース コピーでは、このフィールドは**無効**と表示されます。
    
      - <strong>直前のコピーのログ時間</strong>   選択したデータベース コピーで LogCopier によってコピーされた最後のログ ファイルの日付とタイム スタンプを表示します。このフィールドは、パッシブ データベース コピーのみに関連しています。(レプリケートされたスタンドアロンの) アクティブなデータベース コピーでは、このフィールドは**無効**と表示されます。
    
      - <strong>直前の再生のログ時間</strong>   選択したデータベース コピーで LogReplayer によって再生された最後のログ ファイルの日付とタイム スタンプを表示します。このフィールドは、パッシブ データベース コピーのみに関連しています。(レプリケートされたスタンドアロンの) アクティブなデータベース コピーでは、このフィールドは**無効**と表示されます。
    
      - <strong>アクティブ化の優先順位</strong>   アクティブ化の優先順位番号を表示します。これは、アクティブ マネージャーの最適なコピー選択プロセスの一環として、RedistributeActiveDatabases.ps1 スクリプトを使用して DAG 全体のアクティブ メールボックス データベースを再配布することにより、DAG のバランスを保つために使用されます。アクティブ化優先順位の値は 1 以上の数字です。ここで、1 は最も優先順位が高いことを表します。この数字は、メールボックス データベースのコピーの数よりも大きくすることはできません。
    
      - <strong>再生ラグ タイム (日)</strong>   Microsoft Exchange Replication サービスによりパッシブ データベース コピーの場所にコピーされたログ ファイルを再生する前に、Microsoft Exchange Information Store サービスが待機する時間を表示します。このパラメーターを 0 よりも大きい値に設定すると、遅延データベース コピーが作成されます。この値の既定の設定は 0 日です。この設定の最大許容値は 14 日です。最小許容値は 0 日であり、この値を 0 に設定すると再生ラグは無効になります。

## シェルを使用してメールボックス データベース コピーのプロパティを構成する

この例では、アクティブ化優先順位番号の値を 3 にして、メールボックス データベース コピーを構成します。

```powershell
Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3
```

この例では、再生ラグ タイム、切り詰めラグ タイムが1日、アクティブ化優先順位番号が 2 の設定で Server1 上にホストされる、データベース DB1 のコピーを構成します。

```powershell
    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2
```

## 正常な動作を確認する方法

メールボックス データベース コピーが正常に構成されたことを確認するには、次のいずれかを実行します。

  - EAC で <strong>サーバー</strong> \> <strong>データベース</strong> に移動します。適切なデータベースを選択し、\[詳細\] ウィンドウで <strong>詳細の表示</strong> をクリックして、データベース コピーのプロパティを表示します。

  - シェルで次のコマンドを実行して、データベース コピーの構成情報を表示します。
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
    ```

## 詳細情報

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/ja-jp/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ja-jp/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb124924\(v=exchg.150\))

