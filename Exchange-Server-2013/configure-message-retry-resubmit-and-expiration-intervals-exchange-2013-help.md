---
title: 'メッセージの再試行、再送信、および有効期限の間隔を構成する: Exchange 2013 Help'
TOCTitle: メッセージの再試行、再送信、および有効期限の間隔を構成する
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51407534
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージの再試行、再送信、および有効期限の間隔を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-12-16_

Microsoft Exchange Server 2013 では、メールボックス サーバーおよびエッジ トランスポート サーバーのトランスポート サービスで、メッセージの再試行、再送信、および有効期限の間隔を構成できます。これらの設定の詳細については、「[メッセージの再試行、再送信、および有効期限の間隔](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:10 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート サービス」および「エッジ トランスポート サーバー」。

  - Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## EdgeTransport.exe.config を使用して、キューの誤作動による再試行回数、キューの誤作動による再試行の間隔、メールボックス配信キューの再試行の間隔、および次の再送信までの最大アイドル時間を構成する

キューの誤作動による再試行回数、キューの誤作動による再試行の間隔、メールボックス配信キューの再試行の間隔、および次の再送信までの最大アイドル時間を構成するには、メールボックス サーバーまたはエッジ トランスポート サーバーの XML アプリケーション構成ファイル %ExchangeInstallPath%Bin\\EdgeTransport.exe.config のキーを変更します。このファイルに保存した変更は、Microsoft Exchange Transport サービスの再起動後に適用されます。このサービスを再起動すると、サーバー上のメール フローは一時的に中断されます。

1.  メールボックス サーバーまたはエッジ トランスポート サーバーのコマンド プロンプト ウィンドウで、次のコマンドを実行して EdgeTransport.exe.config をメモ帳で開きます。
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  `<appSettings>` セクションで以下のキーを検索します。
    
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    
    この例では、キューの誤作動による再試行回数を 6 に、キューの誤作動による再試行の間隔を 30 秒 に、メールボックス配信キューの再試行の間隔を 3 分 に、そして次の再送信までの最大アイドル時間を 6 時間に変更します。
    
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />

3.  完了したら、EdgeTransport.exe.config ファイルを保存して閉じます。

4.  次のコマンドを実行して、Microsoft Exchange Transport サービスを再起動します。
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 一時エラー発生時の再試行、一時エラー発生時の再試行間隔、および送信接続失敗時の再試行間隔を構成する

一時エラー発生時の再試行には、`QueueGlitchRetryCount` キーと `QueueGlitchRetryInterval` キーで制御される接続試行が失敗した後に行う、接続試行の回数を指定します。一時エラー発生時の再試行回数の既定値は 6 です。このパラメーターの有効な入力範囲は 0 ～ 15 です。一時エラー発生時の再試行回数を 0 に設定すると、次の接続試行は、*送信接続失敗時の再試行間隔*で制御されます。

一時エラー発生時の再試行間隔には、一時エラー発生時の再試行回数で指定した各接続を試行する間隔を指定します。メールボックス サーバーのトランスポート サービスでは、一時エラー発生時の再試行間隔は既定では 5 分になっています。エッジ トランスポート サーバーでは、一時エラー発生時の再試行間隔は既定では 10 分になっています。

送信接続失敗時の再試行間隔には、前回失敗した送信接続に対する再試行の間隔を指定します。前回失敗した接続の試行は、一時エラー発生時の再試行回数と一時エラー発生時の再試行間隔によって制御されます。メールボックス サーバー上のトランスポート サービスでは、送信接続失敗時の再試行間隔の既定値は 10 分です。エッジ トランスポート サーバーでの既定値は 30 分です。

## EAC を使用して一時エラー発生時の再試行、一時エラー発生時の再試行間隔、または送信接続失敗時の再試行間隔を構成する

1.  Exchange 管理センター (EAC) で、<strong>サーバー</strong> \> <strong>サーバー</strong> の順にクリックしてサーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")、<strong>トランスポート制限</strong> をクリックします。

2.  <strong>再試行</strong> セクションで、<strong>送信接続失敗時の再試行間隔 (秒)</strong>、<strong>一時エラー発生時の再試行間隔 (分)</strong>、または <strong>一時エラー発生時の再試行</strong> の値を入力します。

3.  完了したら、<strong>Save</strong> をクリックします。

## シェルを使用して一時エラー発生時の再試行、一時エラー発生時の再試行間隔、および送信接続失敗時の再試行間隔を構成する

次の構文を使用して、メールボックス サーバーまたはエッジ トランスポート サーバーのトランスポート サービスで、一時エラー発生時の再試行、一時エラー発生時の再試行間隔、および送信接続失敗時の再試行間隔を構成します。

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

この例では、エッジ トランスポート サーバー Exchange01 の Mailbox01 というメールボックス サーバーの次の値を変更します。

  - 一時エラー発生時の再試行回数を 8 回に設定します。

  - 一時エラー発生時の再試行間隔を 1 分に設定します。

  - 送信接続失敗時の再試行間隔を 45 分に設定します。

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> クライアント アクセス サーバーのフロント エンド トランスポート サービスの場合、<STRONG>Set-FrontEndTransportService</STRONG> コマンドレットでは <EM>TransientFailureRetryCount</EM> および <EM>TransientFailureRetryInterval</EM> パラメーターも使用できます。



## 一時エラー発生時の再試行、一時エラー発生時の再試行間隔、および送信接続失敗時の再試行間隔を構成する

## EAC を使用して一時エラー発生時の再試行、一時エラー発生時の再試行間隔、および送信接続失敗時の再試行間隔を構成する

1.  EAC で、<strong>サーバー</strong> \> <strong>サーバー</strong> の順にクリックしてサーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")、<strong>トランスポート制限</strong> をクリックします。

2.  <strong>再試行</strong> セクションで、<strong>送信接続失敗時の再試行間隔 (秒)</strong>、<strong>一時エラー発生時の再試行間隔 (分)</strong>、または <strong>一時エラー発生時の再試行</strong> の値を入力します。

3.  完了したら、<strong>Save</strong> をクリックします。

## シェルを使用して一時エラー発生時の再試行、一時エラー発生時の再試行間隔、および送信接続失敗時の再試行間隔を構成する

次の構文を使用して、メールボックス サーバーまたはエッジ トランスポート サーバーのトランスポート サービスで、一時エラー発生時の再試行、一時エラー発生時の再試行間隔、および送信接続失敗時の再試行間隔を構成します。

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

この例では、エッジ トランスポート サーバー Exchange01 の Mailbox01 というメールボックス サーバーの次の値を変更します。

  - 一時エラー発生時の再試行回数を 8 回に設定します。

  - 一時エラー発生時の再試行間隔を 1 分に設定します。

  - 送信接続失敗時の再試行間隔を 45 分に設定します。

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> クライアント アクセス サーバーのフロント エンド トランスポート サービスの場合、<STRONG>Set-FrontEndTransportService</STRONG> コマンドレットでは <EM>TransientFailureRetryCount</EM> および <EM>TransientFailureRetryInterval</EM> パラメーターも使用できます。



## シェルを使用してメッセージの再試行間隔を構成する

既定では、メッセージの再試行の間隔は `00:15:00` (15 分) です。マイクロソフト カスタマー サービスおよびサポートからの指示がない限り、この既定値を変更しないことをお勧めします。

メッセージの再試行間隔を設定するには、次の構文を使用します。

    Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>

この例では、Mailbox01 というメールボックス サーバーで、メッセージの再試行間隔を 20 分に変更します。

    Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00

## 遅延 DSN タイムアウト設定を構成する

EAC またはシェルを使用して、遅延 DSN 通知のタイムアウト間隔を構成できます。この設定は、ローカルのトランスポート サーバーのみに適用されます。内部および外部送信者への遅延 DSN メッセージの送信を有効または無効にするために使用できるのはシェルのみです。これらの設定は、組織内のすべてのトランスポート サーバーに適用されます。


> [!NOTE]
> Exchange&nbsp;2007 ハブ トランスポート サーバーでは、すべての <EM>ExternalDSN*</EM> パラメーターと <EM>InternalDSN*</EM> パラメーターを <STRONG>Set-TransportConfig</STRONG> コマンドレットではなく、<STRONG>Set-TransportServer</STRONG> コマンドレットで使用できます。Exchange&nbsp;2007 ハブ トランスポート サーバーが組織にある場合は、それぞれの Exchange&nbsp;2007 ハブ トランスポート サーバーで <STRONG>Set-TransportServer</STRONG> コマンドレットを使用してこの値を変更する必要があります。



## EAC を使用して遅延 DSN メッセージの通知のタイムアウト間隔を構成する

1.  EAC で、<strong>サーバー</strong> \> <strong>サーバー</strong> の順にクリックしてサーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")、<strong>トランスポート制限</strong> をクリックします。

2.  <strong>通知</strong> セクションの <strong>次の時間の後、メールの送信者に通知する (時間)</strong> の値を入力します。

3.  完了したら、<strong>Save</strong> をクリックします。

## シェルを使用して遅延 DSN メッセージの通知のタイムアウト間隔を構成する

メッセージの再試行間隔を設定するには、次の構文を使用します。

    Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>

この例では、Mailbox01 というメールボックス サーバーで、遅延 DSN メッセージ通知のタイムアウト間隔を 6 時間に変更します。

    Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00

## シェルを使用して、外部または内部のメッセージ送信者への遅延 DSN 通知の送信を有効または無効にする

遅延 DSN 通知の設定を構成するには、次の構文を使用します。

    Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>

この例では、外部の送信者に遅延 DSN 通知メッセージを送信しないようにします。

    Set-TransportConfig -ExternalDelayDSNEnabled $false

この例では、内部の送信者に遅延 DSN 通知メッセージを送信しないようにします。

    Set-TransportConfig -InternalDelayDSNEnabled $false

## メッセージの有効期限のタイムアウト間隔を構成する

## EAC を使用してメッセージの有効期限のタイムアウト間隔を構成する

1.  EAC で、<strong>サーバー</strong> \> <strong>サーバー</strong> の順にクリックしてサーバーを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン")、<strong>トランスポート制限</strong> をクリックします。

2.  <strong>メッセージの有効期限</strong> セクションで、<strong>送信後の有効期間 (日)</strong> の値を入力します。

3.  完了したら、<strong>Save</strong> をクリックします。

## シェルを使用してメッセージの有効期限のタイムアウト間隔を構成する

メッセージの有効期限のタイムアウト間隔を構成するには、次の構文を使用します。

    Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>

この例では、Mailbox01 という Exchange サーバーで、メッセージの有効期限のタイムアウト間隔を 4 日に変更します。

    Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00

