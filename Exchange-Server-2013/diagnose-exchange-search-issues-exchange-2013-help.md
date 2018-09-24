---
title: 'Exchange Search の問題の診断: Exchange 2013 Help'
TOCTitle: Exchange Search の問題の診断
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52057830
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Search の問題の診断

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange Search は、メールボックスおよび Exchange メールボックス内のサポートされている添付ファイルのインデックスを作成します。電子メールの容量が増え、メールボックスのサイズとストレージ クォータが増え、ユーザーにアーカイブ メールボックスをプロビジョニングし、探索検索の実行用にインプレースの電子情報開示を導入するようになるにつれて、Exchange Search は Microsoft Exchange Server 2013 組織のメールボックス サーバーの重要なコンポーネントとなっています。Exchange Search の問題は、ユーザーの生産性を低下させ、インプレースの電子情報開示の機能に影響します。

Exchange Search の詳細については、「[Exchange Search](exchange-search-exchange-2013-help.md)」を参照してください。

Exchange Search の管理に関連する管理タスクについては、「[Exchange Search の手順](exchange-search-procedures-exchange-2013-help.md)」を参照してください。

## Test-ExchangeSearch コマンドレットの使用方法

このトピックのステップ 5 の手順で、**Test-ExchangeSearch** コマンドレットを使用して Exchange Search 問題の診断に役立てる方法が示されています。メールボックス サーバー、メールボックス データベース、または特定のメールボックスに対する Exchange Search 機能をテストするには、**Test-ExchangeSearch** コマンドレットを使用することができます。コマンドレットは指定されたメールボックス (メールボックスが指定されない場合は、データベースのシステム メールボックス) にテスト メッセージを送信し、メッセージのインデックスが作成されるかどうかを判別し、インデックス処理に要した時間を算定する検索を実行します。通常の条件では、Exchange Search は作成されてメールボックスに送信されるメッセージに約 10 秒以内でインデックス処理を行います。テスト後、テスト メッセージは自動的に削除されます。

構文およびパラメーターの詳細については、「[Test-ExchangeSearch](https://technet.microsoft.com/ja-jp/library/bb124733\(v=exchg.150\))」を参照してください。

## 検索不能アイテムの取得

[Get-FailedContentIndexDocuments](https://technet.microsoft.com/ja-jp/library/dd351154\(v=exchg.150\)) コマンドレットを使用して、Exchange Search で正常にインデックス処理できなかった検索不能なメールボックス アイテムの一覧を取得できます。このコマンドレットは、メールボックス サーバー、メールボックス データベース、または特定のメールボックスに対して実行できます。このコマンドレットを実行すると、検索できなかった各アイテムの詳細が返されます。メールボックス アイテムを検索できない場合、いくつかの理由があります。たとえば、電子メール メッセージに含まれている添付ファイルの種類が検索インデックス処理できない場合や、検索フィルターがインストールされていないか無効になっていることがあります。そのファイル タイプ用の検索フィルターが利用可能であるなら、それを exExchangeNoVersionExchange サーバーにインストールすることができます。


> [!IMPORTANT]
> マイクロソフトが提供している検索フィルターは、マイクロソフトがテストし、サポートしています。サードパーティ製の検索フィルターは、運用環境の exExchangeNoVersionExchange サーバーにインストールする前に、テスト環境でテストすることをお勧めします。



検索不能アイテムの詳細については、以下を参照してください。

  - [Exchange Search によってインデックス処理されるファイル形式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Exchange 電子情報開示の検索不能アイテム](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## Exchange Search の問題の診断

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「Exchange Search」。

1.  **サービス状態の確認**   メールボックス サーバー上で Microsoft Exchange Search (MSExchangeFastSearch) サービスが開始しているかどうかを確認します。開始している場合は手順 2 に進み、開始していない場合はサービス MMC スナップインを使用して、MSExchangeFastSearch サービスが実行されていることを確認します。
    
    1.  <strong>スタート</strong> ボタンをクリックし、<strong>管理ツール</strong> をポイントします。次に、<strong>サービス</strong> をクリックします。
    
    2.  <strong>サービス</strong> で、<strong>Microsoft Exchange 検索</strong> サービスの <strong>状態</strong> が <strong>開始</strong> になっていることを確認します。

2.  **メールボックス データベース構成をチェックする**   ユーザーのメールボックス データベースに対して *IndexEnabled* パラメーターが true に設定されていることを確認します。True に設定されている場合は手順 3. に進み、設定されていない場合はシェルで次のコマンドを実行して、*IndexEnabled* フラグが True に設定されていることを確認します。
    
    ```powershell
    Get-MailboxDatabase | Format-Table Name,IndexEnabled
    ```
    
    構文およびパラメーターの詳細については、「[Get-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb124924\(v=exchg.150\))」を参照してください。

3.  **メールボックス データベース クロール状態の確認**   Exchange データベースがクロールを完了しているかどうかを確認します。完了している場合は手順 4 に進みます。完了していない場合は、信頼性およびパフォーマンス モニターを使用して、<strong>MSExchange 検索インデックス</strong> パフォーマンス オブジェクトの  <strong>クローラー: 残りのメールボックス</strong> カウンターを確認します。次の手順を実行します。
    
    1.  <strong>パフォーマンス モニター</strong> (perfmon.exe) を開きます。
    
    2.  コンソール ツリーで、<strong>管理ツール</strong> の下の <strong>パフォーマンス モニター</strong> をクリックします。
    
    3.  パフォーマンス モニター ウィンドウで、<strong>追加</strong> (緑色のプラス記号) をクリックします。
    
    4.  <strong>カウンターの追加</strong> の <strong>次のコンピューターからカウンターを選ぶ</strong> ボックスの一覧から、監視するメールボックス データベースが置かれているサーバーを選択します。
    
    5.  <strong>次のコンピューターからカウンターを選ぶ</strong> リストの下のボックス (ラベルなし) で、<strong>MSExchange 検索インデックス</strong> パフォーマンス オブジェクトを選択します。
    
    6.  <strong>選択したオブジェクトのインスタンス</strong> ボックスで、ユーザーのメールボックス データベースのインスタンスを選択します。
    
    7.  <strong>追加</strong> をクリックし、<strong>OK</strong> をクリックします。
        
        \[パフォーマンス モニター\] ウィンドウで、<strong>MSExchange 検索インデックス</strong> パフォーマンス オブジェクトは <strong>オブジェクト</strong> 列にリストされ、その各種カウンターは <strong>カウンター</strong> 列にリストされます。
    
    8.  <strong>クローラー: 残りのメールボックス</strong> カウンターを確認します。1 以上の値は、データベースのメールボックスが現在もクロール中であることを示します。クロールが完了すると、値は **0** になります。
    
    パフォーマンス モニターの使用の詳細については、「[ステップ バイ ステップ ガイド - Windows Server 2008 のパフォーマンスと信頼性の監視](https://go.microsoft.com/fwlink/p/?linkid=178005)」を参照してください。

4.  **データベース コピーのインデックス処理の正常性をチェックする**   コンテンツ インデックスが正常であることを確認します。データベース コピーのコンテンツのインデックス処理の正常性をチェックするには、**Get-MailboxDatabaseCopyStatus** コマンドレットを使用します。
    
    ```powershell
    Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    ```
    
    構文およびパラメーターの詳細については、「[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ja-jp/library/dd298044\(v=exchg.150\))」を参照してください。

5.  **Test-ExchangeSearch コマンドレットを実行する**   メールボックス データベースのクロールが既に完了している場合、**Test-ExchangeSearch** コマンドレットは、特定のメールボックスのメールボックス データベースに対して実行できます。
    
    ```powershell
    Test-ExchangeSearch -Identity AlanBrewer@contoso.com
    ```
    
    構文およびパラメーターの詳細については、「[Test-ExchangeSearch](https://technet.microsoft.com/ja-jp/library/bb124733\(v=exchg.150\))」を参照してください。

6.  **アプリケーション イベント ログをチェックする**   イベント ビューアーまたはシェルを使用して、アプリケーション イベント ログ内の検索関連エラー メッセージを確認します。以下のイベント ソースを確認します。
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    詳細については、イベント ログのエントリのリンクを参照してください。

7.  **Microsoft Exchange Search サービスの再起動**    MicrosoftExchange Search (MSExchangeFastSearch) サービスを停止してから再起動するには、サービス MMC スナップインまたはシェルを使用します。
    
    1.  <strong>スタート</strong> ボタンをクリックし、<strong>管理ツール</strong> をポイントします。次に、<strong>サービス</strong> をクリックします。
    
    2.  <strong>サービス</strong> で、<strong>Microsoft Exchange Search</strong> を右クリックし、<strong>停止</strong> をクリックします。サービスが停止したら、サービスを再度右クリックして <strong>開始</strong> をクリックします。

8.  **検索カタログを再シードする**   検索カタログが壊れている場合など、カタログの再シードが必要になる場合があります。検索カタログを再シードする必要がある場合、Exchange Search によってアプリケーション イベント ログにログのエントリが記録されて通知されます。検索カタログの再作成の詳細については、「[検索カタログを再シードする](reseed-the-search-catalog-exchange-2013-help.md)」を参照してください。

