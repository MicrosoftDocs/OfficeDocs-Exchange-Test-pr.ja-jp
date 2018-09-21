---
title: 'キュー データベースの場所を変更する: Exchange 2013 Help'
TOCTitle: キュー データベースの場所を変更する
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51407595
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# キュー データベースの場所を変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-03-09_

*キュー*は、次の処理段階に移るのを待っているメッセージが一時的に保持されている場所です。各キューは、トランスポート サーバーが特定の順序で処理するメッセージの論理的なセットを表します。

旧バージョンの Exchange と同様に、Microsoft Exchange Server 2013 はキュー メッセージ ストレージ用に Extensible Storage Engine (ESE) データベースを使用します。さまざまなキューはすべて 1 つの ESE データベースに格納されます。キューは、メールボックス サーバーまたはエッジ トランスポート サーバー上にのみ存在します。

キュー データベースとキュー データベース トランザクション ログの場所は、`%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML アプリケーション構成ファイル内のキーによって制御されます。このファイルは、Microsoft Exchange Transport サービスに関連付けられています。次の表で、それぞれのキーを詳しく説明します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>キー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>このキーには、キュー データベース ファイルの場所を指定します。以下のファイルがあります。</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>既定の場所は <code>%ExchangeInstallPath%TransportRoles\data\Queue</code> です。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>このキーには、キュー データベース トランザクション ログ ファイルの場所を指定します。以下のファイルがあります。</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>なお、Temp.edb は、Microsoft Exchange Transport サービスの開始時に、キュー データベース スキーマを確認するのに使用されます。Temp.edb はトランザクション ログ ファイルではありませんが、トランザクション ログ ファイルと同じ場所に格納されます。</p>
<p>既定の場所は <code>%ExchangeInstallPath%TransportRoles\data\Queue</code> です。</p></td>
</tr>
</tbody>
</table>


## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分。

  - Exchange のアクセス許可は、このトピックの手順には適用されません。これらの手順は、Exchange Server のオペレーティング システムで実行されます。

  - Microsoft Exchange Transport サービスを停止または再起動すると、サーバー上のメール フローが中断されます。

  - キュー データベースまたはトランザクション ログの場所を変更した場合、既存のキュー データベースとトランザクション ログ ファイルは移動されません。新しいキュー データベースと新しいトランザクション ログが新しい場所に作成されます。既存のファイルは古い場所に残ります。ただし、それらは今後使用されません。既存のキュー データベースまたはトランザクション ログ ファイルを新しい場所で再利用する場合は、Microsoft Exchange Transport サービスを停止した後、サービスを起動する前に、既存のファイルを新しい場所に移動する必要があります。

  - キュー データベースまたはトランザクション ログの変更先フォルダーが存在しない場合、親フォルダーに以下のアクセス許可が適用されていれば、そのフォルダーは自動的に作成されます。
    
      - ネットワーク サービス :フル コントロール
    
      - システム :フル コントロール
    
      - 管理者 :フル コントロール

  - Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## コマンド プロンプトを使用して新しいキュー データベースとトランザクション ログを新しい場所に作成する

1.  キュー データベースとトランザクション ログを保持するフォルダーを作成します。そのフォルダーに適切なアクセス許可が適用されていることを確認します。

2.  コマンド プロンプト ウィンドウで、次のコマンドを実行して、EdgeTransport.exe.config ファイルをメモ帳で開きます。
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  `<appSettings>` セクションで以下のキーを変更します。
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    たとえば、D:\\Queue\\QueueDB で新しいキュー データベースを作成し、D:\\Queue\\QueueLogs で新しいトランザクション ログを作成するには、次の値を使用します。
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  完了したら、EdgeTransport.exe.config ファイルを保存して閉じます。

5.  次のコマンドを実行して、Microsoft Exchange Transport サービスを再起動します。
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 正常な動作を確認する方法

新しいキュー データベースと新しいトランザクション ログが新しい場所に正常に作成されたことを確認するには、以下を実行します。

1.  新しいデータベース ファイル Mail.que および Trn.chk が新しい場所に存在することを確認します。

2.  新しいトランザクション ログ ファイル Trn.log、Trntmp.log、Trnres00001.jrs、Trnres00002.jrs、および Temp.edb ファイルが新しい場所に存在することを確認します。

3.  Microsoft Exchange Transport サービスの起動後に古いキュー データベースとトランザクション ログ ファイルを古い場所から削除可能な場合、それらのファイルはそれ以降使用されません。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

必要な作業

## コマンド プロンプトを使用して既存のキュー データベースとトランザクション ログを新しい場所に移動する

Microsoft Exchange Transport サービスが適切にシャットダウンしなかった場合や、ハード ディスク ドライブが故障した場合などの障害回復シナリオでのみ、既存のキュー データベースおよびその既存のトランザクション ログを復元し、再配置する必要があります。

通常の環境では、既存のトランザクション ログを再利用する必要はありません。通常、Microsoft Exchange Transport サービスをシャットダウンすると、コミットされていないすべてのトランザクション ログ エントリがキュー データベースに書き込まれます。さらに、循環ログが使用されるため、以前にコミットされたデータベースの変更を含むトランザクション ログは保存されません。

既存のキュー データベースとトランザクション ログを新しい場所に移動するには、次の手順を使用します。

1.  キュー データベースとトランザクション ログを保持するフォルダーを作成します。そのフォルダーに適切なアクセス許可が適用されていることを確認します。

2.  コマンド プロンプト ウィンドウで、次のコマンドを実行して、EdgeTransport.exe.config ファイルをメモ帳で開きます。
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  `<appSettings>` セクションで以下のキーを変更します。
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    たとえば、キュー データベースの場所を D:\\Queue\\QueueDB に変更し、トランザクション ログの場所を D:\\Queue\\QueueLogs に変更するには、次の値を使用します。
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  完了したら、EdgeTransport.exe.config ファイルを保存して閉じます。

5.  次のコマンドを実行して、Microsoft Exchange Transport サービスを停止します。
    
    ```powershell
net stop MSExchangeTransport
```

6.  既存のデータベース ファイル Mail.que および Trn.chk を元の場所から新しい場所に移動します。

7.  既存のトランザクション ログ ファイル Trn.log、Trntmp.log、Trn*nnnnn*.log、Trnres00001.jrs、Trnres00002.jrs、および Temp.edb を古い場所から新しい場所に移動します。

8.  次のコマンドを実行して、Microsoft Exchange Transport サービスを起動します。
    
    ```powershell
net start MSExchangeTransport
```

## 正常な動作を確認する方法

既存のキュー データベースとトランザクション ログが新しい場所に正常に移動されたことを確認するには、以下を実行します。

1.  キュー データベース ファイル Mail.que および Trn.chk が新しい場所に存在することを確認します。

2.  トランザクション ログ ファイル Trn.log、Trntmp.log、Trnres00001.jrs、Trnres00002.jrs、および Temp.edb ファイルが新しい場所に存在することを確認します。

3.  キュー データベースまたはトランザクション ログ ファイルが元の場所にないことを確認します。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

必要な作業

