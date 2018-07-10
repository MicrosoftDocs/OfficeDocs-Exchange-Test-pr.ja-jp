---
title: 'Configure Get-QueueDigest: Exchange 2013 Help'
TOCTitle: Configure Get-QueueDigest
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59634987
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configure Get-QueueDigest

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-12-16_

**Get-QueueDigest** コマンドレットでは、単一のコマンドにより、Exchange 組織内の一部またはすべてのキューの情報を表示できます。

既定では、**Get-QueueDigest** コマンドレットが返す結果は、1 ～ 2 分経過しています。これらの値は、次の設定によって制御されます。

  - **QueueLoggingInterval key in EdgeTransport.exe.config**   このキーでは、キュー データが記録される頻度とデータが **Get-QueueDigest** で入手できることを指定します。既定値は `00:01:00`、つまり 1 分間です。値を指定するには、*hh:mm:ss* の形式で期間として入力します。*h* = 時間、*m* = 分、*s* = 秒です。既定では、このキーは、EdgeTransport.exe.config ファイルに存在しません。

  - **QueueDiagnosticsAggregationInterval parameter on Set-TransportConfig**   このパラメーターは、キュー データがどのくらいの頻度でメールボックス サーバー間で共有されるかを指定します。既定値は `00:01:00`、つまり 1 分間です。値を指定するには、*hh:mm:ss* の形式で期間として入力します。*h* = 時間、*m* = 分、*s* = 秒です。

**QueueLoggingInterval** キーと *QueueDiagnosticsAggregationInterval* パラメーターの合計値は、**Get-QueueDigest** で返される結果の最大待機時間を決定します。

また、**Get-QueueDigest** は、キューの種類と状態に基づいて異なる結果を返します。たとえば、少なくとも 1 つのメッセージが含まれている場合には、次のキューが結果に表示されます。

  - 発信キュー、到達不能キュー、および有害なメッセージ キュー (永続的なキュー)。

  - 保留状態の配信キュー (管理者によって手動で中断されたキュー)。

既定では、配信キューがアクティブ、接続中、準備完了、再試行の状態の場合には、キューに 10 以上のメッセージがある場合のみ結果を返します。この値は、EdgeTransport.exe.config ファイルの **QueueLoggingThreshold** キーで制御されます。整数値の大きさを指定できます。既定では、このキーは、EdgeTransport.exe.config ファイルに存在しません。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - Exchange のアクセス許可を確認するには、**Set-TransportConfig** を Exchange 管理シェルで実行する必要があります。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「トランスポート構成」を参照してください。

  - Exchange のアクセス許可は、EdgeTransport.exe.config ファイルの修正および Microsoft Exchange トランスポート サービスの再起動には適用されません。これらの手順は、Exchange Server のオペレーティング システムで実行されます。

  - EdgeTransport.exe.config ファイルに保存した変更は、Microsoft Exchange トランスポート サービスを再起動した後に適用されます。このサービスを再起動すると、サーバー上のメール フローは一時的に中断されます。

  - Exchange XML アプリケーション構成ファイルで行うカスタマイズ済みのサーバーごとの設定 (クライアント アクセス サーバーの web.config ファイルまたはメールボックス サーバーの EdgeTransport.exe.config ファイルなど) は、Exchange 累積更新プログラム (CU) のインストール時に上書きされます。インストール後にサーバーを簡単に再構成できるよう、必ずこの情報を保存しておいてください。これらの設定は、Exchange 累積更新プログラムのインストール後に構成し直す必要があります。

  - **Set-TransportConfig** を使用した変更は、組織のすべてのメールボックス サーバーに影響します。EdgeTransport.exe.config ファイルで行った変更は、ローカルのメールボックス サーバーのみに影響します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Configure Get-QueueDigest

1.  コマンド プロンプト ウィンドウで、次のコマンドを実行して、EdgeTransport.exe.config ファイルをメモ帳で開きます。
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  `<appSettings>` セクションに、一方または両方の以下のキーを追加します。
    
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    
    たとえば、**QueueLoggingThreshold** の値を 1 とし、**QueueLoggingInterval** の値を 30 秒とするには、次の値を使用します。
    
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />

3.  完了したら、EdgeTransport.exe.config ファイルを保存して閉じます。

4.  次のコマンドを実行して、Microsoft Exchange トランスポート サービスを再起動します。
    
        net stop MSExchangeTransport && net start MSExchangeTransport

5.  *QueueDiagnosticsAggregationInterval* の値を変更する場合、Exchange 管理シェルのパラメーターには次の構文を使用します。
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
    
    たとえば、値を 30 秒に変更するには、次のコマンドを実行します。
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30

## 正常な動作を確認する方法

**Get-QueueDigest** が正しく設定されたことを確認するには、次の操作を実行します。

1.  EdgeTransport.exe.config ファイルの **QueueLoggingThreshold** および **QueueLoggingInterval** キーの値を確認します。キーがない場合は既定値が使用されます。

2.  次のコマンドを実行して *QueueDiagnosticsAggregationInterval* パラメーターの値を確認します。
    
        Get-TransportConfig | Format-List *queue*

