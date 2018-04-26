---
title: トラブルシューティングに Exchange Server 2013 管理パックを使用する
TOCTitle: トラブルシューティングに Exchange Server 2013 管理パックを使用する
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53181897
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トラブルシューティングに Exchange Server 2013 管理パックを使用する

 

_**トピックの最終更新日:** 2013-04-09_

[Exchange Server 2013 管理パックをお使いになる前に](getting-started-with-exchange-server-2013-management-pack.md) は、管理パック ダッシュボードの概要を説明します。このトピックでは、問題のトラブルシューティング方法の手順を具体的に説明します。このプロセスを例を使ってわかりやすく説明します。次のシナリオについて考えます。

Rob Fielder は Contoso の Exchange 管理者です。彼は SCOM コンソールを開いて Exchange Server 2013 ダッシュボードの **\[サーバーの状態\]** をクリックして、自分の Exchange サーバーの状態をチェックします。彼は、1 台の CAS サーバーの **\[サービス コンポーネント\]** が重大な状態であることに気づきました。

![CAS サーバーの障害](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "CAS サーバーの障害")

Rob はそのサーバーをダブルクリックして、**\[正常性エクスプローラー\]** ウィンドウを開きました。このウィンドウでは、正常な状態にないサービス コンポーネントが OWA.Proxy 正常性セットであることが確認できます。このサービス コンポーネントをクリックすると、この正常性セットの関連情報が表示されます。

![CAS サーバーの障害における正常性セットの詳細](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "CAS サーバーの障害における正常性セットの詳細")

外部技術情報リソースの下に表示されているリンクをクリックすると、「[OWA.Proxy 正常性セットのトラブルシューティング](https://technet.microsoft.com/ja-jp/library/jj737712\(v=exchg.150\))」が表示されます。この記事から、最初にやるべきことは問題がまだ存在しているかを確認することだとわかります。指示に従って次のコマンドを実行して、シェル内の OWA.Proxy プロキシ正常性セットの現在の状態を確認します。

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

このコマンドを実行すると、次の出力が得られます。

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

Rob は問題が OWA アプリケーション プールにあることを確認しました。次の手順は、正常状態にないモニターに関連するプローブを再実行することです。「OWA.Proxy 正常性セットのトラブルシューティング」の表を使って、再実行しなければならないプローブが OWAProxyTestProbe であることを特定します。次のコマンドを実行します。

    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List

ResultType の値の出力をスキャンして、プローブに障害があることを確認します。

    ResultType : Failed

記事の「OWAProxyTestMonitor の回復操作」セクションに進みます。IIS マネージャーを使って Server1 に接続し、IIS Server で MSExchangeOWAAppPool が実行されているかを確認します。実行されていることを確認した後、次の手順で MSExchangeOWAAppPool をリサイクルするように指示されます。

    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool

MSExchangeOWAAppPool が正常にリサイクルされたことを確認した後、Invoke-MonitoringProbe コマンドレットを使用してプローブを再実行し、問題がまだ存在しているかを確認します。今度は結果は問題なしでした。次のコマンドを実行して、以前のように、正常性セットによって **\[正常\]** な状態が報告されることを確認します。

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

今回は、問題が解決したことがわかりました。

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

SCOM コンソールに戻り、問題が解決したことを確認します。

![サーバーの正常性](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "サーバーの正常性")

上で説明したシナリオは、SCOM コンソールに警告が表示された場合のトラブルシューティング ワークフローを簡単に示したものです。詳細は異なりますが、通常は、コンソールで報告された問題ごとに、同様のトラブルシューティング ワークフローに従ってください。

