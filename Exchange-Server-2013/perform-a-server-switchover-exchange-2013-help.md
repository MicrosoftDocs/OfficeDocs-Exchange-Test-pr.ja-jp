---
title: 'サーバー切り替えを実行する: Exchange 2013 Help'
TOCTitle: サーバー切り替えを実行する
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523726
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# サーバー切り替えを実行する

 

_**適用先:** Exchange Server 2013 SP1_

_**トピックの最終更新日:** 2014-06-23_

サーバー切り替えは、すべてのアクティブなメールボックス データベースのコピーを、現在のメールボックス サーバーからデータベース可用性グループ (DAG) 内にある他の 1 台以上のメールボックス サーバーへ移動するタスクです。このタスクは、現在のメールボックス サーバーのスケジュールされた停止に対する準備の一部として実行されます。

## 始める前に把握しておくべき情報

  - 推定完了時間: データベース 1 つあたり 30 秒

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「データベース可用性グループ」。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## EAC を使用してサーバー切り替えを実行する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[高可用性とサイト復元のアクセス許可](high-availability-and-site-resilience-permissions-exchange-2013-help.md)」の「メールボックス データベースのコピー」。

1.  EAC で、**\[サーバー\]** \> **\[サーバー\]** に移動します。

2.  切り替えるメールボックス サーバーを選択します。

3.  詳細ウィンドウで、**\[サーバーの切り替え\]** を選択します。

4.  **\[サーバーの切り替え\]** ページで、以下のいずれかの操作を行います。
    
    1.  **\[対象サーバーを自動的に選択します\]** の既定の設定を変更せずに (この結果、システムによって切り替え対象の各データベースに最適なメールボックス サーバーが自動的に選択されます)、**\[保存\]** をクリックします。
    
    2.  **\[指定のサーバーを切り替え先として使用する\]** をクリックし、**\[参照\]** をクリックしてメールボックス サーバーを選択した後、**\[保存\]** をクリックします。

5.  切り替えが完了したら、**\[閉じる\]** をクリックして **\[サーバーの切り替え\]** ページを終了します。

## シェルを使用してサーバー切り替えを実行する

この例では、MBX1 というサーバーのサーバー切り替えを実行します。システムによって、MBX1 上のアクティブなデータベースに最適なメールボックス サーバーが自動的に選択されます。

    Move-ActiveMailboxDatabase -Server MBX1

この例では、MBX4 というメールボックス サーバーのサーバー切り替えを実行します。コマンドが完了すると、以前 MBX4上 でアクティブだったデータベースのアクティブ コピーが MBX5 によってホストされます。

    Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5

構文およびパラメーターの詳細については、「[Move-ActiveMailboxDatabase](https://technet.microsoft.com/ja-jp/library/dd298068\(v=exchg.150\))」を参照してください。

