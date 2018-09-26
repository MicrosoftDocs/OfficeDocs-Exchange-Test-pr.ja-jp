---
title: '優先度キューを有効化および構成する: Exchange 2013 Help'
TOCTitle: 優先度キューを有効化および構成する
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51407506
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 優先度キューを有効化および構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-12-16_

*優先度キュー*は Microsoft Exchange Server 2013 の機能です。この機能を使用すると、Microsoft Outlook または Outlook Web Access で送信者が構成したメッセージ優先度に従って、メールボックス サーバーのトランスポート サービスでメッセージが処理されるようになります。優先度キューが有効になっている場合、高優先度のメッセージは標準優先度のメッセージの前に送信先に送信され、標準優先度のメッセージは低優先度のメッセージの前に送信先に送信されます。詳細については、「[優先度キュー](priority-queuing-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 15 分

  - Exchange のアクセス許可は、このトピックの手順には適用されません。これらの手順は、Exchange Server のオペレーティング システムで実行されます。

  - EdgeTransport.exe.config アプリケーション構成ファイルに保存した変更は、Microsoft Exchange Transport サービスを再起動した後に適用されます。

  - Microsoft Exchange Transport サービスを再起動すると、サーバー上のメール フローは一時的に中断されます。

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_Upgrade\_WebConfigFiles)

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## コマンド プロンプトを使用して、EdgeTransport.exe.config ファイルで優先度キューを有効化および構成する

1.  コマンド プロンプト ウィンドウで、次のコマンドを実行して、EdgeTransport.exe.config アプリケーション構成ファイルをメモ帳で開きます。
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2.  `<appSettings>` セクションで以下のキーを検索します。
    
    ```powershell
    <add key="PriorityQueuingEnabled" value="false" />
    <add key="MaxPerDomainHighPriorityConnections" value="3" />
    <add key="MaxPerDomainNormalPriorityConnections" value="15" />
    <add key="MaxPerDomainLowPriorityConnections" value="2" />
    <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
    <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
    <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
    <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
    <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
    <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
    <add key="MaxHighPriorityMessageSize" value="250KB" />
    ```
    
    メールボックス サーバーの Microsoft Exchange Transport サービスで優先度キューを有効にするには、次の値を使用します。
    
    ```command line
    <add key="PriorityQueuingEnabled" value="true" />
    ```
    
    残りの優先度キューの値を構成するか、既定値のままにしておきます。

3.  完了したら、EdgeTransport.exe.config ファイルを保存して閉じます。

4.  次のコマンドを実行して、Microsoft Exchange Transport サービスを再起動します。
    
    ```powershell
    net stop MSExchangeTransport && net start MSExchangeTransport
    ```

## 正常な動作を確認する方法

優先度キューが正常に有効になって構成されたことを確認するには、次の操作を行います。

1.  EdgeTransport.exe.config ファイルの **PriorityQueueinEnabled** キーの値が `"true"` になっていることを確認します。

2.  Outlook を使用して、**MaxHighPriorityMessageSize** キーで指定した値よりも大きい、高優先度のテスト メッセージを作成し、そのメッセージが通常の優先度のメッセージとして届くことを確認します。

3.  同じ受信者や送信先に送信された優先度が低いメッセージの前に、優先度が高いメッセージが届くことを確認するようにします。また、複数のメールボックスを使用し、類似する複数のテスト メッセージを優先度を変えて同じ受信者に同時に送信してみてください。

