---
title: 'ルーティング テーブル ログ出力を構成する: Exchange 2013 Help'
TOCTitle: ルーティング テーブル ログ出力を構成する
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 49896309
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ルーティング テーブル ログ出力を構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

ルーティング テーブルのログ記録は、Microsoft Exchange Server 2013 が使用するルーティング テーブルのスナップショットを定期的に記録し、メッセージを宛先にルーティングします。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート サービス」および「エッジ トランスポート サーバー」。

  - この手順を実行するには、シェルを使用する必要があります。

  - ルーティング テーブルの自動再計算の間隔を構成するには、EdgeTransport.exe.config XML アプリケーション構成ファイルを変更します。このファイルに保存した変更は、Microsoft Exchange Transport サービスの再起動後に適用されます。このサービスを再起動すると、サーバー上のメール フローは一時的に中断されます。

  - Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してルーティング テーブルのログ記録を構成する

次のコマンドを実行します。

    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>

この例では、Mailbox01 というメールボックス サーバーで次のようなルーティング テーブルのログ設定を行います。

  - ルーティング テーブルのログ ファイルの場所を D:\\Routing Table Log に設定します。フォルダーが存在しない場合は、新たに作成されます。

  - ルーティング テーブルのログ フォルダーの最大サイズを 70 MB に設定します。

  - ルーティング テーブルのログ ファイルの最大保存期間を 45 日に設定します。

<!-- end list -->

    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00


> [!NOTE]
> <EM>RoutingTableLogMaxAge</EM> パラメーターの値を <CODE>00:00:00</CODE> に設定すると、ルーティング テーブルのログ ファイルが保存期間によって自動的に削除されなくなります。



## 正常な動作を確認する方法

ルーティング テーブルのログ記録が正常に構成されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*

2.  表示された値が構成した値であることを確認します。

## コマンド プロンプトを使用して EdgeTransport.exe.config ファイル内のルーティング テーブルの自動再計算の間隔を構成する

1.  コマンド プロンプト ウィンドウで、次のコマンドを実行して、EdgeTransport.exe.config アプリケーション構成ファイルをメモ帳で開きます。
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  `<appSettings>` セクションで以下のキーを変更します。
    
        <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    
    たとえば、ルーティング テーブルの自動再計算の間隔を 10 時間に変更するには、次の値を使用します。
    
        <add key="RoutingConfigReloadInterval" value="10:00:00" />

3.  完了したら、EdgeTransport.exe.config ファイルを保存して閉じます。

4.  次のコマンドを実行して、Microsoft Exchange Transport サービスを再起動します。
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 正常な動作を確認する方法

ルーティング テーブルの自動再計算の間隔が正常に構成されたことを確認するには、ルーティング テーブルのログが指定した間隔中に更新されることを確認します。

以下のいずれかの状況が生じた場合は、*RoutingConfigReloadInterval* キーで指定されている値より早く、ルーティング テーブルが再計算され、ログ記録されます。

  - ルーティング構成の変更が検出された場合。たとえば、送信コネクタまたは受信コネクタが追加、削除、または変更されたか、6 時間ごとの Kerberos トークンの更新が発生した場合です。

  - Microsoft Exchange Transport サービスが開始された場合。

