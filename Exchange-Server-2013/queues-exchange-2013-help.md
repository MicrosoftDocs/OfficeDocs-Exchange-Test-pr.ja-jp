---
title: 'キュー: Exchange 2013 Help'
TOCTitle: キュー
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51407599
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# キュー

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

*キュー*は、次の処理段階への移行または送信先への配信を待っているメッセージが一時的に保持されている場所です。各キューは、Exchange サーバーが特定の順序で処理するメッセージの論理的なセットを表します。Microsoft Exchange Server 2013 では、キューで配信前、配信中、および配信後のメッセージを保持します。キューは、メールボックス サーバーとエッジ トランスポート サーバーに存在します。このトピック全体を通じて、メールボックス サーバーとエッジ トランスポート サーバーを*トランスポート サーバー*と呼びます。

旧バージョンの Exchange と同様に、Exchange 2013 はキュー ストレージ用に単一の Extensible Storage Engine (ESE) データベースを使用します。

Exchange ツールボックスの Exchange 管理シェルとキュー ビューアを使用してキューとキュー内のメッセージを管理できます。これらのインターフェイスを使用すると、キューの状態と内容、および詳細なメッセージ プロパティを表示できます。また、キューまたはキューのメッセージを変更する操作を実行することもできます。

**目次**

  - キューの種類

  - キュー データベース ファイル

  - キューのプロパティ
    
      - NextHopSolutionKey
    
      - IncomingRate、OutgoingRate、および Velocity
    
      - キューの状態
    
      - その他のキューのプロパティ

  - メッセージのプロパティ
    
      - メッセージの状態
    
      - その他のメッセージのプロパティ

  - キューおよびキュー内のメッセージを管理する

## キューの種類

Exchange 2013 で使用されるキューの種類は次のとおりです。

  - **永続キュー** *永続キュー*は、各 Exchange 組織内の各トランスポート サーバーに存在するキューです。旧バージョンの Exchange と同様に、Exchange 2013 には 3 つの永続キューがあります。
    
      - **発信キュー**   発信キューは、トランスポート サーバー上のトランスポート エージェントが解決し、ルーティングして、処理する必要のあるすべてのメッセージを収集するためにカテゴライザーによって使用されます。トランスポート サーバーによって受信されたすべてのメッセージは、送信キューでの処理に入ります。メールボックス サーバーで、メッセージは受信コネクタ、ピックアップまたは再生ディレクトリ、またはメールボックス トランスポート発信サービスを経由して送信されます。エッジ トランスポート サーバーでは、通常メッセージは受信コネクタ経由で送信されますが、ピックアップおよび再生ディレクトリも利用可能です。
        
        このキューからメッセージを取得したカテゴライザーが行う処理の中には、受信者の場所の特定と、その場所へのルーティングがあります。分類の後、メッセージは配信キューまたは到達不能キューに移されます。各トランスポート サーバーが備える送信キューは 1 つだけです。送信キューに入れられたメッセージは、同時に他のキューに存在することはできません。カテゴライザーとトランスポート パイプラインの詳細については、「[メール フロー](mail-flow-exchange-2013-help.md)」を参照してください。
    
      - **到達不能キュー**   到達不能キューには、送信先にルーティングできないメッセージが格納されます。通常、到達不能の送信先が発生する原因は、構成の変更により、配信用のルーティング パスが変更されるためです。送信先に関係なく、受信者に到達できないメッセージはすべてこのキューに格納されます。各トランスポート サーバーが備える到達不能キューは 1 つだけです。
        
        到達不能キューのメッセージは、ルーティングの変更が検出されたときに自動的に再送信されます。そのため、メッセージが到達不能キューに格納される原因となった条件または構成エラーが修復された後に、到達不能キューのメッセージを配信のために移動する追加の操作は不要です。
        
        通常、到達不能キューは空です。到達不能キューは、メッセージが含まれていない場合、キュー ビューアまたは **Get-Queue** の結果には表示されません。
    
      - **有害メッセージ キュー**   有害メッセージ キューは、トランスポート サーバーまたはサービスのエラーの後で Exchange 2013 システムに対して有害であることが検出されたメッセージを分離するために使用される特別なキューです。このメッセージには、純粋に有害な内容および形式が含まれている可能性があります。または、エージェントが適切に作成されていないため、有害と見なされたメッセージを処理している間に、Exchange サーバーでエラーが発生した可能性もあります。
        
        通常、有害メッセージ キューは空です。有害メッセージ キューは、メッセージが含まれていない場合、キュー ビューアまたは **Get-Queue** の結果には表示されません。有害メッセージ キューにあるメッセージは、自動で再開されたり期限切れになったりすることはありません。有害メッセージ キューにあるメッセージは、管理者によって手動で再開または削除されるまでキュー内に残ります。

  - **配信キュー**   配信キューは、SMTP を使用してローカルまたはリモートの送信先に配信されるメッセージを保持します。すべてのメッセージは SMTP を使用して Exchange サーバー間で送信されます。SMTP 以外の送信先も、配信エージェント コネクタが送信先に対応している場合は、配信キューを使用します。. 各配信キューには、同じ送信先にルーティングされるメッセージが含まれます。トランスポート サーバーには、ほぼ確実に複数の配信キューが存在することになります。配信キューは必要な場合に動的に作成され、キューが空になるか、有効期限が過ぎると自動的に削除されます。キューの有効期限は、**Set-TransportService** コマンドレットの *QueueMaxIdleTime* パラメーターによって制御されます。既定値は 3 分です。

  - **シャドウ キュー**   シャドウ キューは、メッセージの送信中にメッセージの冗長コピーを保持します。詳細については、「[シャドウ冗長](shadow-redundancy-exchange-2013-help.md)」を参照してください。

  - **セーフティ ネット**   セーフティ ネットは、トランスポート サーバーによって正常に配信されたメッセージのコピーを保持します。セーフティ ネットは、キュー管理ツールからアクセスできませんが、キュー データベース内に存在するキューの 1 つです。詳細については、「[セーフティ ネット](safety-net-exchange-2013-help.md)」を参照してください。

ページのトップへ

## キュー データベース ファイル

さまざまなキューはすべて 1 つの ESE データベースに格納されます。既定では、キュー データベースは `%ExchangeInstallPath%TransportRoles\data\Queue` のトランスポート サーバーにあります。

ESE データベースと同様に、キュー データベースはログ ファイルを使用して、データの受け付け、追跡、および維持を行います。パフォーマンスを強化するために、メッセージ トランザクションはすべて、最初にログ ファイルとメモリに書き込まれ、次にデータベース ファイルに書き込まれます。チェックポイント ファイルは、データベースにコミットされたトランザクション ログ エントリを追跡します。Microsoft Exchange Transport サービスの通常のシャットダウン中は、トランザクション ログにあるコミットされていないデータベースの変更は、常にデータベースにコミットされます。

キュー データベースには循環ログが使用されます。これは、トランザクション ログにあるコミットされたトランザクションの履歴が保持されていないことを意味します。現在のチェックポイントより古いトランザクション ログは、すべて即座に自動削除されます。このため、キュー データベースを回復するために、バックアップからトランザクション ログを再生することはできません。

Exchange 2013 は、キュー データベース内でのメッセージの保存とクリーンアップに*生成テーブル*を使用します。1 つの大きなテーブルから個々のメッセージ レコードを処理および削除する代わりに、キュー データベースは時間ベースのテーブルにメッセージを格納し、テーブル内のメッセージがすべて正常に処理された後にのみテーブル全体を削除します。たとえば、午後 1:00 ～ 2:00 の間にキューに入ったメッセージはすべて、キューまたは送信先に関係なく `1p-2p_msgs` テーブルに格納されます。午後 2:00 には、新しいメッセージは `2p-3p_msgs` テーブルに格納されます。午後 4:00 には、`4p-5p_msgs` という新しいテーブルが作成され、`1p-2p_msgs` テーブルは、テーブル内のすべてのメッセージが正常に処理された場合のみ、全体が削除されます。個々のメッセージではなくメッセージ テーブル全体を削除するこのアプローチは、キュー データベースを保持するドライブの I/O パフォーマンスの改善に役立ちます。

次の表に、キュー データベースを構成するファイルの一覧を示します。

### キュー データベースを構成するファイル

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ファイル</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>このキュー データベース ファイルは、キューに入れられたメッセージをすべて格納します。</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>この一時データベース ファイルは、起動時にキュー データベース スキーマを確認するために使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>このトランザクション ログは、キュー データベースに対するすべての変更を記録します。データベースへの変更は、最初にトランザクション ログに書き込まれ、次にデータベースにコミットされます。Trn.log は、現在アクティブなトランザクション ログ ファイルです。Trntmp.log は、前もって作成され、準備されている次のトランザクション ログ ファイルです。既存の Trn.log トランザクション ログ ファイルが最大サイズに達すると、Trn.log の名前は Trn<em>nnnn</em>.log に変更されます。ここで、<em>nnnn</em> はシーケンス番号です。次に、Trntmp.log の名前が Trn.log に変更され、現在アクティブなトランザクション ログ ファイルになります。</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>このチェックポイント ファイルは、データベースにコミットされたトランザクション ログ エントリを追跡します。このファイルは、常に mail.que ファイルと同じ場所にあります。</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>これらの予約トランザクション ログ ファイルはプレースホルダーとして動作します。これらのファイルが使用されるのは、トランザクション ログを格納しているハード ディスクで、キュー データベースを正常に停止するための領域が不足している場合のみです。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## キュー データベースを構成するためのオプション

キュー データベースは、`%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML アプリケーション構成ファイルにキーを追加するか、またはそのキーを変更することで構成します。このファイルは、Microsoft Exchange Transport サービスに関連付けられています。EdgeTransport.exe.config ファイルに加えた変更は、Microsoft Exchange Transport サービスを再起動した後に反映されます。

EdgeTransport.exe.config ファイルの `<appSettings>` セクションでは、新しいキーを追加するか、または既存のキーを変更することができます。特定のキーが存在しない場合は、手動でキーを追加し、その値を変更できます。

EdgeTransport.exe.config ファイルで使用できるキュー データベースのキーについて、次の表で説明します。

### EdgeTransport.exe.config ファイルで使用できるメッセージ キュー データベースのキー

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>キー</th>
<th>既定値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>このキーには、実行する前にグループ化できるデータベース I/O 操作の数を指定します。既定では、このキーは、EdgeTransport.exe.config ファイルに存在しません。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>このキーには、実行前に複数のデータベース I/O 操作がグループ化されるまでデータベースが待機する最大時間を指定します (ミリ秒単位)。データベース I/O 操作は、以下の条件が満たされると、それ以上の操作を待たずに実行されます。</p>
<ul>
<li><p><em>QueueDatabaseBatchSize</em> キーで指定されたデータベース I/O 操作の数に到達しなかった。</p></li>
<li><p><em>QueueDatabaseBatchTimeout</em> キーで指定された時間が経過した。</p></li>
</ul>
<p>既定では、このキーは、EdgeTransport.exe.config ファイルに存在しません。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>このキーには、開くことができる ESE データベース接続の数を指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>このキーには、トランザクション ログ ファイルに書き込まれる前のトランザクション レコードをキャッシュするために使用されるメモリを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>このキーには、トランザクション ログ ファイルの最大サイズを指定します。ログ ファイルの最大サイズに達すると、新しいログ ファイルが開かれます。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>このキーには、キュー データベース ログ ファイルの既定のディレクトリを指定します。キュー データベースの場所を変更する方法については、「<a href="change-the-location-of-the-queue-database-exchange-2013-help.md">キュー データベースの場所を変更する</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>このキーには、データベース エンジンのスレッド プールに対するキューに任意の時点で置くことができる、バックグラウンドでのクリーンアップ作業の最大アイテム数を指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>このキーを使用すると、メール キュー データベースの、スケジュールが設定されたオンラインでの最適化を有効または無効にできます。既定では、このキーは、EdgeTransport.exe.config ファイルに存在しません。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> または午前 1:00</p></td>
<td><p>このキーには、メール キュー データベースのオンラインでの最適化を開始する時刻を、24 時間形式で指定します。値を指定するには、<em>hh:mm:ss</em> の形式で期間として入力します。<em>h</em> = 時間、<em>m</em> = 分、<em>s</em> = 秒です。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> または 3 時間</p></td>
<td><p>このキーには、オンラインでの最適化タスクの実行を許可する時間の長さを指定します。指定した時間で最適化タスクが終了しない場合でも、キュー データベースは整合状態で残されます。値を指定するには、<em>hh:mm:ss</em> の形式で期間として入力します。<em>h</em> = 時間、<em>m</em> = 分、<em>s</em> = 秒です。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>このキーには、キュー データベース ファイルの既定のディレクトリを指定します。キュー データベースの場所を変更する方法については、「<a href="change-the-location-of-the-queue-database-exchange-2013-help.md">キュー データベースの場所を変更する</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。



ページのトップへ

## キューのプロパティ

キューには、キューの目的と状態を示す多くのプロパティがあります。キューの一部のプロパティは、キューが作成されたときにキューに適用され、変更されません。その他のプロパティは、状態、サイズ、時間、またはその他のインジケーターを含み、頻繁に更新されます。

ページのトップへ

## NextHopSolutionKey

Microsoft Exchange Transport サービス内のカテゴライザーのルーティング コンポーネントがメッセージの送信先を選択し、この送信先が配信キューの作成に使用されます。送信先は、**NextHopSolutionKey** 属性として各受信者にスタンプされます。**NextHopSolutionKey** 属性の一意の値はそれぞれ、個別の配信キューに対応します。

**NextHopSolutionKey** 属性には、次のフィールドが含まれます。

  - **DeliveryType**   このフィールドの値は、メッセージの分類結果、Microsoft Exchange Transport サービスが意図するメッセージの次ホップへの送信方法、メッセージの最終的な送信先、またはその経路の中間ホップを表します。Microsoft Exchange Transport サービスは、対象のルーティング先または配信グループに基づいて事前定義された **DeliveryType** の値一覧を使用します。

  - **NextHopDomain**   このフィールドでは、**DeliveryType** フィールドの値に基づく特定の値を使用します。配信キューの場合、このフィールドの値は事実上キューの名前になります。**NextHopDomain** の値は、常にドメイン名であるとは限りません。たとえば、値は、対象の Active Directory サイトまたはデータベース可用性グループ (DAG) の名前の場合もあります。このフィールドは、値がルーティング先または対象の配信グループの名前である次ホップ名と考えてください。

  - **NextHopConnector**   このフィールドでは、**DeliveryType** フィールドの値に基づく特定の値を使用します。値は常に GUID として表されます。このフィールドが使用されていない場合、値はすべて 0 の GUID となります。**NextHopConnector** の値は、常にコネクタの GUID であるとは限りません。たとえば、値は、対象の Active Directory サイトまたは DAG の GUID の場合もあります。このフィールドは、値がルーティング先または対象の配信グループの GUID である次ホップ名と考えてください。

Exchange 2013 は、**DeliveryType** の値に基づいて、**NextHopCategory** プロパティもキューに追加します。**NextHopCategory** の値は、`External` または `Internal` です。値 `External` は、キューの次ホップが Exchange 組織の外部にあることを示しています。値 `Internal` は、キューの次ホップが Exchange 組織の内部にあることを示しています。外部受信者宛てのメッセージには、メッセージを外部に配信する前に 1 つ以上の内部ホップが必要となることがある点に注意してください。

**DeliveryType**、**NextHopCategory**、**NextHopDomain**、および **NextHopConnector** の値について、次の表で説明しています。


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>キュー ビューアでの配信の種類</th>
<th>シェルの DeliveryType</th>
<th>説明</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>配信エージェント</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>キューは、SMTP アドレス スペース以外の受信者に配信するためのメッセージを保持します。メッセージは、ローカル サーバーに構成された配信エージェント コネクタを使用して配信されます。</p></td>
<td><p>External</p></td>
<td><p>この値は、配信エージェント コネクタに構成された送信先アドレス スペースを示しています。</p></td>
<td><p>この値は、配信エージェント コネクタの GUID です。たとえば、<code>4520e633-d83d-411a-bbe4-6a84648674ee</code> などです。</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>キューは、SMTP アドレス スペース内の受信者に配信するためのメッセージを保持します。メッセージは、ローカル サーバーに構成された送信コネクタを使用して配信されます。送信コネクタは、DNS ルーティングを使用するように構成されます。</p></td>
<td><p>External</p></td>
<td><p>この値は、送信コネクタに構成された送信先アドレス スペースを示しています。たとえば、<code>contoso.com</code> などです。</p></td>
<td><p>この値は、送信コネクタの GUID です。たとえば、<code>4520e633-d83d-411a-bbe4-6a84648674ee</code> などです。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>キューは、SMTP アドレス スペース以外の受信者に配信するためのメッセージを保持します。メッセージは、ローカル サーバーに構成された外部コネクタを使用して配信されます。</p></td>
<td><p>External</p></td>
<td><p>この値は、外部コネクタに構成された送信先アドレス スペースを示しています。</p></td>
<td><p>この値は、外部コネクタの GUID です。たとえば、<code>4520e633-d83d-411a-bbe4-6a84648674ee</code> などです。</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>キューは、SMTP アドレス スペース内の受信者に配信するためのメッセージを保持します。メッセージは、ローカル サーバーに構成された送信コネクタを使用して配信されます。送信コネクタは、スマート ホスト ルーティングを使用するように構成されます。</p></td>
<td><p>External</p></td>
<td><p>この値は、送信コネクタに構成されたスマート ホストの一覧です。スマート ホストは FQDN、IP アドレス、またはその両方として構成することができます。値は次のいずれかになります。</p>
<ul>
<li><p><strong>FQDN</strong>   構文は <code>&lt;FQDN1,FQDN2,...&gt;</code> です。たとえば、<code>smarthost01.contoso.com</code> または <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code> のように指定します。</p></li>
<li><p><strong>IP アドレス</strong>   構文は <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code> です。たとえば、<code>[10.10.10.100]</code> または <code>[10.10.10.100],[10.10.10.101]</code> のように指定します。</p></li>
<li><p><strong>FQDN および IP アドレス</strong>   構文は <code>&lt;[IPAddress1],FQDN1,...&gt;</code> で、スマート ホストが送信コネクタで一覧表示される方法に依存します。たとえば、<code>[172.17.17.7],relay.tailspintoys.com</code> または <code>mail.contoso.com,[192.168.1.50]</code> のように指定します。</p></li>
</ul></td>
<td><p>この値は、送信コネクタの GUID です。たとえば、<code>4520e633-d83d-411a-bbe4-6a84648674ee</code> などです。</p></td>
</tr>
<tr class="odd">
<td><p><strong>メールボックスへの SMTP 配信</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>キューは、Exchange 2013 メールボックス受信者に配信するためのメッセージを保持します。送信先メールボックス データベースは、次の場所のいずれかにあります。</p>
<ul>
<li><p>ローカルの Exchange 2013 メールボックス サーバー。</p></li>
<li><p>同じ DAG 内の Exchange 2013 メールボックス サーバー。</p></li>
<li><p>DAG 以外の環境の同じ Active Directory サイト内の Exchange 2013 メールボックス サーバー。</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>この値は、送信先メールボックス データベースの名前です。たとえば、<code>Mailbox Database 0471695037</code> などです。</p></td>
<td><p>この値は、対象のメールボックス データベースの GUID です。たとえば、<code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code> などです。</p></td>
</tr>
<tr class="even">
<td><p><strong>送信コネクタの送信元サーバーへの SMTP リレー</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>キューは、SMTP または SMTP 以外の受信者に配信するためのメッセージを保持します。メッセージは、リモート トランスポート サーバーに構成された送信コネクタ、配信エージェント コネクタ、または外部コネクタを使用して配信されます。リモート トランスポート サーバーとしては、Exchange 2013 メールボックス サーバー、または旧バージョンの Exchange の Exchange 2007 または Exchange 2010 ハブ トランスポート サーバーを使用できます。リモート サーバーは、ローカル Active Directory サイトまたはリモート Active Directory サイトに配置されます。</p></td>
<td><p>Internal</p></td>
<td><p>この値は、送信先の送信コネクタ、配信エージェント コネクタ、または外部コネクタの名前です。たとえば、<code>Contoso.com Send Connector</code> などです。</p></td>
<td><p>この値は、送信先の送信コネクタ、配信エージェント コネクタ、または外部コネクタの GUID です。たとえば、<code>4520e633-d83d-411a-bbe4-6a84648674ee</code> などです。</p></td>
</tr>
<tr class="odd">
<td><p><strong>データベース可用性グループへの SMTP リレー</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>キューは、送信先メールボックス データベースがリモート DAG 内にある Exchange 2013 メールボックス受信者に送信するためのメッセージを保持します。リモート DAG は、ローカル Active Directory サイトまたはリモート Active Directory サイトに配置されます。</p></td>
<td><p>Internal</p></td>
<td><p>この値は、送信先 DAG の名前です。たとえば、<code>DAG1</code> などです。</p></td>
<td><p>この値は、送信先 DAG の GUID です。たとえば、<code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code> のように指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>メールボックス配信グループへの SMTP リレー</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>キューは、送信先メールボックスが Exchange 2007 または Exchange 2010 メールボックス サーバー上にある従来のメールボックス受信者に送信するためのメッセージを保持します。メッセージは、送信先メールボックスとして同じバージョンの Exchange を実行しているハブ トランスポート サーバーに関連しています。送信先ハブ トランスポート サーバーは、ローカル Active Directory サイトまたはリモート Active Directory サイトに配置されます。</p></td>
<td><p>Internal</p></td>
<td><p>キュー名は、次の構文を使用します。<code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>。ここで、<em>&lt;ADSiteName&gt;</em> は送信先 Active Directory サイトの名前、<em>&lt;ExchangeVersion&gt;</em> はメールボックス サーバー上の Exchange のバージョンです。</p></td>
<td><p>この値は空白です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>リモート Active Directory サイトへの SMTP リレー</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>キューはリモート送信先に配信するためのメッセージを保持し、ルーティング トポロジではメッセージを特定の Active Directory サイトを経由してルーティングする必要があります。このサイトは、最終送信先への経路上の中間ホップとなります。これは、次の状況で発生します。</p>
<ul>
<li><p>メッセージを、ハブ サイト経由でルーティングする必要がある。</p></li>
<li><p>メッセージを、リモート Active Directory サイトにサブスクライブしているエッジ トランスポート サーバーに構成された送信コネクタ経由で配信する必要がある。</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>この値は、対象の Active Directory サイトの名前です。たとえば、<code>NorthAmericanSite</code> などです。</p></td>
<td><p>この値は、対象の Active Directory サイトの GUID です。たとえば、<code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code> などです。</p></td>
</tr>
<tr class="even">
<td><p><strong>指定された Exchange サーバーへの SMTP リレー</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>キューは、特定の展開サーバーに構成された送信先グループに配信するためのメッセージを保持します。展開サーバーとしては、Exchange 2013 メールボックス サーバー、または Exchange 2007 あるいは Exchange 2010 ハブ トランスポート サーバーを使用できます。サーバーは、ローカル Active Directory サイトまたはリモート Active Directory サイトに配置されます。</p></td>
<td><p>Internal</p></td>
<td><p>この値は、対象の展開サーバーの FQDN です。たとえば、<code>mailbox01.contoso.com</code> などです。</p></td>
<td><p>この値は <code>00000000-0000-0000-0000-000000000000</code> です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Active Directory サイト内でのエッジ トランスポート サーバーへの SMTP リレー</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>キューは、SMTP アドレス スペースに配信するためのメッセージを保持します。メッセージは、ローカル Active Directory サイトにサブスクライブしているエッジ トランスポート サーバーに構成された送信コネクタを使用して配信されます。</p></td>
<td><p>Internal</p></td>
<td><p>この値は、組織からインターネットに送信インターネット メールを送信する送信コネクタの名前です。この送信コネクタは、エッジ サブスクリプションによって自動的に作成され、<code>EdgeSync - &lt;ADSiteName&gt; to Internet</code> という名前が付けられます。<em>&lt;ADSiteName&gt;</em> は、エッジ トランスポート サーバーをサブスクライブしているローカル Active Directory サイトの名前です。</p></td>
<td><p>この値は、送信コネクタの GUID です。たとえば、<code>4520e633-d83d-411a-bbe4-6a84648674ee</code> などです。</p></td>
</tr>
<tr class="even">
<td><p><strong>Heartbeat</strong></p></td>
<td><p><strong>Heartbeat</strong></p></td>
<td><p>この値は、Microsoft の内部使用目的に予約されています。ハートビートの詳細については、「<a href="shadow-redundancy-exchange-2013-help.md">シャドウ冗長</a>」を参照してください。</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p><strong>シャドウ冗長</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>キューは、シャドウ キュー内にメッセージを保持します。シャドウ キューは、プライマリ メッセージが正常に配信されなかった場合に、送信中のメッセージの冗長コピーを保持します。詳細については、「<a href="shadow-redundancy-exchange-2013-help.md">シャドウ冗長</a>」を参照してください。</p></td>
<td><p>Internal</p></td>
<td><p>この値は、シャドウ キューがプライマリ メッセージの冗長コピーを保持しているプライマリ サーバーの FQDN です。たとえば、<code>mailbox01.contoso.com</code> などです。</p></td>
<td><p>この値は <code>00000000-0000-0000-0000-000000000000</code> です。</p></td>
</tr>
<tr class="even">
<td><p><strong>Undefined</strong></p></td>
<td><p><strong>Undefined</strong></p></td>
<td><p>この値は、送信キューおよび有害メッセージ キューでのみ使用されます。</p></td>
<td><p>Internal</p></td>
<td><p>送信キューの場合、この値は <code>Submisssion</code> です。有害メッセージ キューの場合、この値は <code>Poison Message</code> です。</p></td>
<td><p>この値は <code>00000000-0000-0000-0000-000000000000</code> です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>到達不能</strong></p></td>
<td><p><strong>Unreachable</strong></p></td>
<td><p>この値は、到達不能キューでのみ使用されます。</p></td>
<td><p>Internal</p></td>
<td><p>この値は <code>Unreachable Domain</code> です。</p></td>
<td><p>この値は <code>00000000-0000-0000-0000-000000000000</code> です。</p></td>
</tr>
</tbody>
</table>


Exchange 2013 は、旧バージョンの Exchange との下位互換性のために **DeliveryType** の従来の値をサポートしている点に注意してください。これらの値は、キュー ビューアとシェルで使用可能ですが、Exchange 2013 では使用されません。従来の **DeliveryType** の値は、次のとおりです。

  - **MapiDelivery**   キューは、Exchange 2007 または Exchange 2010 ハブ トランスポート サーバーによって、ローカル Active Directory サイトの Exchange 2007 または Exchange 2010 メールボックス サーバー上のメールボックスに配信されるメッセージを保持します。

  - **SmtpRelayWithinAdSite**   キューは、Exchange 2007 または Exchange 2010 ハブ トランスポート サーバーによって、同じ Active Directory サイト内の別のハブ トランスポート サーバーに配信されるメッセージを保持します。送信先ハブ トランスポート サーバーは、コネクタの送信元サーバーの場合もあれば、送信先グループ展開サーバーの場合もあります。

  - **SmtpRelaytoTiRg**   キューは、Exchange 2007 または Exchange 2010 ハブ トランスポート サーバーによって、Exchange Server 2003 ルーティング グループに配信されるメッセージを保持します。送信先サーバーは、コネクタの送信元サーバーの場合もあれば、送信先グループ展開サーバー、または Exchange 2003 ブリッジヘッド サーバーの場合もあります。

ページのトップへ

## IncomingRate、OutgoingRate、および Velocity

Exchange 2013 は、メッセージがキューに出入りする速度を測定し、これらの値をキュー プロパティに格納します。これらの速度は、キューとトランスポート サーバーの状態のインジケーターとして使用できます。以下のプロパティがあります。

  - **IncomingRate**   このプロパティはメッセージがキューに入る速度です。
    
    この値は、直近の 60 秒間において、5 秒ごとにキューに入ったメッセージ数を平均して算出されます。数式は、`(i1+i2+i3+i4+i5+i6)/6` として表されます。ここで、i*n* は、5 秒間の受信メッセージ数です。

  - **OutgoingRate**   このプロパティはメッセージがキューから出る速度です。
    
    この値は、直近の 60 秒間において、5 秒ごとにキューから出たメッセージ数を平均して算出されます。数式は、`(o1+o2+o3+o4+o5+o6)/6` として表されます。ここで、o*n* は、5 秒間の送信メッセージ数です。

  - **Velocity**   このプロパティは、キューのドレイン速度で、**OutgoingRate** の値から **IncomingRate** の値を引いて算出されます。
    
    **Velocity** の値が 0 より大きい場合、メッセージはキューに入るより早い速度でキューから出ています。
    
    **Velocity** の値が 0 に等しい場合、メッセージはキューに入るのと同じ速度でキューから出ています。これは、キューがアクティブでないときにも表示される値です。
    
    **Velocity** の値が 0 より小さい場合、メッセージはキューから出るより早い速度でキューに入って出ています。

基本レベルでは、**Velocity** の正の値は効率的にドレインされている正常なキューを示し、**Velocity** の負の値は効率的にドレインされていないキューを示しています。ただし、キューの **Velocity** 値の大きさと同様に、**IncomingRate**、**OutgoingRate**、および **MessageCount** プロパティの値も考慮する必要があります。たとえば、**Velocity** が大きな負の値で、**MessageCount** 値が大きく、**OutgoingRate** 値が小さく、さらに **IncominRate** 値が大きいキューは、キューが適切にドレインされていないことを明確に示しています。ただし、**Velocity** がかなり 0 に近い負の値で、**IncomingRate**、**OutgoingRate**、および **MessageCount** の値も非常に小さいキューは、キューに問題があるこをを示しているわけではありません。

ページのトップへ

## キューの状態

キューの現在の状態は、キューの **Status** プロパティに格納されます。キューの状態値は、次のいずれかです。

  - **アクティブ**   キューはアクティブにメッセージを送信中です。

  - **接続中**   キューは次ホップへの接続の処理中です。

  - **準備完了**   キューは最近メッセージを送信しましたが、現在は空です。

  - **再試行**   前回の自動または手動の接続試行が失敗し、キューは接続の再試行を待機中です。

  - **中断**   メッセージを配信しないようにするため、キューは管理者によって手動で中断されました。新しいメッセージはキューに入ることができ、次ホップに送信するように処理されたメッセージは配信されキューから出ていきます。それ以外の場合は、キューが管理者によって手動で再開されるまで、メッセージはキューに留まります。キューが中断されても、キュー内の個々のメッセージの状態は変更されない点に注意してください。
    
    状態が "アクティブ" または "再試行" であるキューを中断できます。また、到達不能キューや送信キューも中断できます。
    
    到達不能キューを中断した場合、構成の更新が検出されても、メッセージはカテゴライザーに自動的に再送信されません。これらのメッセージを自動的に再送信するには、到達不能キューを手動で再開する必要があります。送信キューを中断した場合は、そのキューが再開されるまで、メッセージはカテゴライザーによって取得されません。

ページのトップへ

## その他のキューのプロパティ

上記の他に、説明の必要がないキューがいくつかあります。ほとんどのキューのプロパティは、フィルター オプションとして使用します。フィルター条件を指定することにより、すばやくキューを見つけ出し、それに対する処理を実行することができます。フィルター処理可能なキューのプロパティの詳細については、「[キューのフィルター](queue-filters-exchange-2013-help.md)」を参照してください

ここで説明しておいた方がよい重要なキューのプロパティとしては、キュー内のメッセージ数を示す **MessageCount** プロパティがあります。このプロパティは、キューの状態の重要なインジケーターです。たとえば、増加し続け、減少することのない多数のメッセージを含む配信キューは、注意を必要とするルーティングまたはトランスポート パイプラインの問題を示している可能性があります。

ページのトップへ

## メッセージのプロパティ

キュー内のメッセージには多くのプロパティがあります。プロパティの多くは、メッセージを作成するために使用された情報を反映しています。メッセージの状態および情報プロパティの一部は、キューの対応するプロパティに大きく影響されます。ただし、個々のメッセージが、キューの対応するプロパティと異なる値を持つ場合もあります。その他のプロパティには、状態、時刻、または頻繁に更新されるその他のインジケーターが含まれています。

ページのトップへ

## メッセージの状態

メッセージの現在の状態は、メッセージの **Status** プロパティに格納されます。メッセージの状態は、以下のいずれかの値になります。

  - **アクティブ**   このメッセージが配信キューにある場合、メッセージは送信先に配信されています。このメッセージが送信キューにある場合、メッセージはカテゴライザーによって処理されています。

  - **ロック済み**   この値は、Microsoft の内部使用目的に予約されており、社内 Exchange 組織では使用されません。

  - **削除保留**   メッセージは管理者によって削除されましたが、既に次ホップに送信するように処理されています。この配信がエラーになり、メッセージがキューに再度置かれた場合、そのメッセージは削除されます。それ以外の場合、配信は続行されます。

  - **中断保留**   メッセージは管理者によって中断されましたが、既に次ホップに送信するように処理されています。この配信がエラーになり、メッセージがキューに再度置かれた場合、そのメッセージは中断されます。それ以外の場合、配信は続行されます。

  - **準備完了**   このメッセージはキューで待機中で、処理の準備ができています。

  - **再試行**   このメッセージが置かれているキューに対する前回の自動または手動の接続試行は失敗しました。メッセージは、キューの次回の自動再試行を待機しています。

  - **中断**   このメッセージは管理者によって手動で中断されました。有害メッセージ キューにあるすべてのメッセージは、恒久的に中断された状態にあります。

ページのトップへ

## その他のメッセージのプロパティ

上記の他に、説明の必要がないメッセージのプロパティがいくつかあります。ほとんどのメッセージのプロパティは、フィルター オプションとして使用できます。フィルター条件を指定すると、メッセージをすばやく見つけて、操作を行うことができます。フィルター処理可能なメッセージのプロパティの詳細については、「[メッセージ フィルター](message-filters-exchange-2013-help.md)」を参照してください。

ページのトップへ

## キューおよびキュー内のメッセージを管理する

キュー ビューアと、ほぼすべてのキューおよびメッセージ管理コマンドレットは、単一の Exchange サーバーに制限されています。個々のキューやメッセージ、または複数のキューやメッセージを表示あるいは操作できますが、それらは特定のサーバー上にあるものだけに限定されています。

Exchange 2013 では、たとえば、DAG、Active Directory サイト、サーバー一覧、Active Directory フォレスト全体などの特定のスコープ内のすべてのサーバー上のキューについて高レベルの集計ビューを提供する **Get-QueueDigest** コマンドレットが導入されています。境界ネットワーク内のサブスクライブ済みエッジ トランスポート サーバー上のキューは、結果に含まれないことに注意してください。また、**Get-QueueDigest** はエッジ トランスポート サーバーでは使用できますが、その場合、結果は エッジ トランスポート サーバー上のキューに制限されます。


> [!NOTE]
> 既定では、<STRONG>Get-QueueDigest</STRONG> コマンドレットは、10 以上のメッセージを含む配信キューを表示します。この結果は 1 ～ 2 分間前のものです。これらの既定値の変更方法の説明については、「<A href="configure-get-queuedigest-exchange-2013-help.md">Configure Get-QueueDigest</A>」を参照してください。



次の表では、キューまたはキュー内のメッセージに対して実行できる管理タスクを説明しています。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>タスク</th>
<th>説明</th>
<th>使用するツール</th>
<th>手順</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>サーバー上のキューを表示およびフィルター処理する</p></td>
<td><p>この操作では、トランスポート サーバー上の 1 つまたは複数のキューが表示されます。その結果を使用して、キューを操作できます。</p></td>
<td><p>キュー ビューアまたは<strong>Get-Queue</strong> コマンドレット。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">キューを管理する</a></p></td>
</tr>
<tr class="even">
<td><p>特定の DAG、特定の Active Directory サイト、または Active Directory フォレスト全体の中の特定のサーバー上のキューを表示およびフィルター処理する。</p></td>
<td><p>この操作では、定義されたスコープ (サーバー、DAG、Active Directory サイト、または Active Directory フォレスト全体) 内のキューの概要ビューが表示されます。</p></td>
<td><p><strong>Get-QueueDigest</strong> コマンドレットのみ。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">キューを管理する</a></p></td>
</tr>
<tr class="odd">
<td><p>キューを中断する</p></td>
<td><p>この操作では、キューに現在入っているメッセージの配信を一時的に停止します。キューは引き続き新しいメッセージを受け付けますが、キューからメッセージが出ていくことはありません。</p></td>
<td><p>キュー ビューアまたは <strong>Suspend-Queue</strong> コマンドレット。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">キューを管理する</a></p></td>
</tr>
<tr class="even">
<td><p>キューを再開する</p></td>
<td><p>この操作では、キュー中断操作の逆で、キューに入っているメッセージの配信を再開できるようにします。</p></td>
<td><p>キュー ビューアまたは <strong>Resume-Queue</strong> コマンドレット。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">キューを管理する</a></p></td>
</tr>
<tr class="odd">
<td><p>キューを再試行する</p></td>
<td><p>この操作では、すぐに次ホップに接続しようとします。手動で操作を行うことなく、次ホップへの接続が失敗すると、試行後一定の間隔が経過した後に、一定の回数分、接続が再試行されます。</p>
<p>手動か自動かに関係なく、接続試行は次の再試行時にリセットされます。詳細については、「<a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">メッセージの再試行、再送信、および有効期限の間隔</a>」を参照してください。</p></td>
<td><p>キュー ビューアまたは <strong>Retry-Queue</strong> コマンドレット。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">キューを管理する</a></p></td>
</tr>
<tr class="even">
<td><p>キュー内のメッセージを再送信する</p></td>
<td><p>この操作では、キュー内のメッセージを送信キューに再送信し、分類プロセスを再実行します。</p></td>
<td><p><strong>Retry-Queue</strong> と <em>Resubmit</em> パラメーター</p>
<p>キュー ビューアを使用してメッセージを再送信できるのは、有害メッセージ キューのみである点に注意してください。有害メッセージ キュー内のメッセージを再送信するには、キュー ビューア内、または <strong>Resume-Message</strong> コマンドレットを使用して、メッセージを再開します。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">キューを管理する</a></p></td>
</tr>
<tr class="odd">
<td><p>キュー内のメッセージを中断する</p></td>
<td><p>この操作では、メッセージの配信を一時的に停止します。メッセージ中断操作を使用すると、特定のキューにおけるすべての受信者に対するメッセージの配信、またはすべてのキューにおけるすべての受信者に対するメッセージの配信を、停止することができます。</p></td>
<td><p>キュー ビューアまたは <strong>Suspend-Message</strong> コマンドレット。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">キュー内のメッセージを管理する</a></p></td>
</tr>
<tr class="even">
<td><p>キュー内のメッセージを再開する</p></td>
<td><p>この操作では、メッセージ中断操作の逆で、キューに入っているメッセージの配信を再開できるようにします。メッセージ再開操作を使用すると、特定のキューにおけるすべての受信者に対するメッセージの配信、またはすべてのキューにおけるすべての受信者に対するメッセージの配信を、再開することができます。</p></td>
<td><p>キュー ビューアまたは <strong>Resume-Message</strong> コマンドレット。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">キュー内のメッセージを管理する</a></p></td>
</tr>
<tr class="odd">
<td><p>キューからメッセージを削除する</p></td>
<td><p>この操作では、メッセージの配信を永続的に停止します。メッセージ削除操作を使用すると、指定したキューにおける任意の受信者に対するメッセージの配信、またはすべてのキューにおけるすべての受信者に対するメッセージの配信を、停止することができます。また、メッセージが削除されたら送信者に配信不能レポート (NDR) が送信されるように、メッセージ削除操作を構成することもできます。</p></td>
<td><p>キュー ビューアまたは <strong>Remove-Message</strong> コマンドレット。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">キュー内のメッセージを管理する</a></p></td>
</tr>
<tr class="even">
<td><p>キューからメッセージをエクスポートする</p></td>
<td><p>この操作では、メッセージを指定したファイル パスにコピーします。キューからメッセージは削除されず、メッセージのコピーがファイルの場所に保存されます。これにより、組織の管理者や担当者は後でメッセージを調べることができます。メッセージをエクスポートする前に、キューのメッセージを中断し、エクスポート プロセスの間に通常の配信が継続されないようにする必要があります。</p></td>
<td><p><strong>Export-Message</strong> コマンドレットのみ。</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">キューからメッセージをエクスポートする</a></p></td>
</tr>
</tbody>
</table>


ページのトップへ

