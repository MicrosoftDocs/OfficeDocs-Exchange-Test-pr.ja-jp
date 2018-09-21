---
title: 'Exchange 2013 で POP3 を有効にする: Exchange 2013 Help'
TOCTitle: POP3 を有効にする
ms:assetid: e226a5f1-429d-4046-b925-da6cc151709e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124934(v=EXCHG.150)
ms:contentKeyID: 49896525
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 で POP3 を有効にする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-03-28_

Microsoft 管理コンソール (MMC) または Exchange 管理シェル (EMS) を使用して、Exchange 2016 で POP3 クライアント接続を有効にする方法について説明します。

Exchange Server 2016 をインストールした時点では、POP3 クライアント接続は有効になっていません。POP3 クライアント接続を有効にするには、Microsoft Exchange POP3 サービスと Microsoft Exchange POP3 Backend サービスの 2 つのサービスを開始する必要があります。POP3 が有効な場合、Exchange 2016 はセキュリティで保護されていない POP3 クライアントの通信をポート 110 で、SSL (Secure Sockets Layer) を使用する場合はポート 995 で受信します。

メールボックス サーバーの役割を実行している同じ Exchange 2016 コンピューターで、POP3 バックエンドと POP3 バックエンド両方のサービスを管理します。Exchange 2016 では、クライアント アクセス サービスは、メールボックス サーバーの役割の一部であるため、サービスを個別に管理する必要はなくなります。

POP3 および IMAP4 を設定する方法の詳細については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間:2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 および IMAP4 のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## Microsoft 管理コンソール (MMC) を使用して POP3 を有効にする

メールボックス サーバーの役割を実行しているコンピューター上:

1.  <strong>サービス</strong> スナップインのコンソール ツリーで、<strong>サービス (ローカル)</strong> をクリックします。

2.  結果ウィンドウで、<strong>Microsoft Exchange POP3</strong> を右クリックし、<strong>プロパティ</strong> をクリックします。

3.  結果ウィンドウで、<strong>Microsoft Exchange POP3 バックエンド</strong> を右クリックし、<strong>プロパティ</strong> をクリックします。

4.  <strong>全般</strong> タブの <strong>スタートアップの種類</strong> で <strong>自動</strong> を選択し、<strong>適用</strong> をクリックします。

5.  <strong>サービスの状態</strong> の下の <strong>開始</strong> をクリックし、<strong>OK</strong> をクリックします。

## Exchange 管理シェル を使用して POP3 を有効にする

メールボックス サーバーの役割を実行しているコンピューター上:

1.  Microsoft Exchange POP3 サービスを自動で開始されるように設定します。
    
    ```powershell
Set-service msExchangePOP3 -startuptype automatic
```

2.  Microsoft Exchange POP3 サービスを開始します。
    
    ```powershell
Start-service msExchangePOP3
```

3.  Microsoft Exchange POP3 Backend サービスを自動で開始されるように設定します。
    
    ```powershell
Set-service msExchangePOP3BE -startuptype automatic
```

4.  Microsoft Exchange POP3 Backend サービスを開始します。
    
    ```powershell
Start-service msExchangePOP3BE
```

## 正常な動作を確認する方法

Exchange 2016 メールボックス サーバーで、Windows タスク マネージャーを開きます。POP3 が有効な場合は、<strong>サービス</strong> タブに、<strong>MSExchangePOP3</strong> および <strong>MSExchangePOP3BE</strong> のステータスが <strong>実行中</strong> と表示されます。

