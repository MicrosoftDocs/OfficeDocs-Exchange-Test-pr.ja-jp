---
title: 'Exchange 2016 で IMAP4 を有効にする: Exchange 2013 Help'
TOCTitle: Exchange 2016 で IMAP4 を有効にする
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 49896455
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2016 で IMAP4 を有効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-06-02_

Microsoft 管理コンソール (MMC) または Exchange 管理シェル (EMS) を使用して、Exchange 2016 で IMAP4 クライアント接続を有効にする方法について説明します。

Exchange Server 2016 をインストールした時点では、IMAP4 クライアント接続は有効になっていません。IMAP4 クライアント接続を有効にするには、2 つの IMAP サービスを開始する必要があります。Microsoft Exchange IMAP4 サービス、および Microsoft Exchange IMAP4 バックエンド サービスです。IMAP4 を有効にすると、Exchange 2016 はセキュリティで保護されていない IMAP4 クライアントの通信をポート 143 で、SSL (Secure Sockets Layer) を使用する場合はポート 993 で受信します。

メールボックス サーバーの役割を実行している同じ Exchange 2016 コンピューターで、IMAP4 バックエンドと IMAP4 バックエンド両方のサービスを管理します。Exchange 2016 では、クライアント アクセス サービスは、メールボックス サーバーの役割の一部であるため、サービスを個別に管理する必要はなくなります。

POP3 および IMAP4 を設定する方法の詳細については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 および IMAP4 のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## Microsoft 管理コンソール (MMC) を使用して IMAP4 を有効にする

メールボックス サーバーの役割を実行しているコンピューター上:

1.  **\[サービス\]** スナップインのコンソール ツリーで、**\[サービス (ローカル)\]** をクリックします。

2.  結果ウィンドウで、**\[Microsoft Exchange IMAP4\]** を右クリックし、**\[プロパティ\]** をクリックします。

3.  結果ウィンドウで、**\[Microsoft Exchange IMAP4 Backend\]** を右クリックし、**\[プロパティ\]** をクリックします。

4.  **\[全般\]** タブの **\[スタートアップの種類\]** で **\[自動\]** を選択し、**\[適用\]** をクリックします。

5.  **\[サービスの状態\]** の下の **\[開始\]** をクリックし、**\[OK\]** をクリックします。

## Exchange 管理シェル を使用して IMAP4 を有効にする

メールボックス サーバーの役割を実行しているコンピューター上:

1.  Microsoft Exchange IMAP4 サービスが自動的に開始するよう設定します。
    
        Set-service msExchangeIMAP4 -startuptype automatic

2.  Microsoft Exchange IMAP4 サービスを開始します。
    
        Start-service msExchangeIMAP4

3.  Microsoft Exchange IMAP4 バックエンド サービスが自動的に開始するよう設定します。
    
        Set-service msExchangeIMAP4BE -startuptype automatic

4.  Microsoft Exchange IMAP4 バックエンド サービスを開始します。
    
        Start-service msExchangeIMAP4BE

## 正常な動作を確認する方法

Exchange 2016 メールボックス サーバーで、Windows タスク マネージャーを開きます。**\[サービス\]** タブで、IMAP4 が有効になっていれば **\[MSExchangeIMAP4\]** と **\[MSExchangeIMAP4BE\]** の状態が **\[実行中\]** となります。

