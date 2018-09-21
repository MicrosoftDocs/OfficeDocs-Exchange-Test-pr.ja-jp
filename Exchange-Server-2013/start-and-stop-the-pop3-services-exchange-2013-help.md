---
title: 'POP3 サービスの開始および停止: Exchange 2013 Help'
TOCTitle: POP3 サービスの開始および停止
ms:assetid: 3d543921-d8c9-4d4b-99a1-82446b585ceb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997475(v=EXCHG.150)
ms:contentKeyID: 49896212
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 サービスの開始および停止

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-03-13_

既定では、Microsoft Exchange POP3 サービスと Microsoft Exchange POP3 バックエンド サービスの 2 つの POP3 サービスは、MicrosoftExchange Server 2013 を実行するコンピューター上で開始されていません。電子メール クライアントが POP3 を使用して Exchange に接続できるようにするためには、これら 2 つのサービスを開始する必要があります。これらサービスが実行しているとき、Exchange 2013 はセキュリティで保護されていない POP3 クライアントの通信をポート 110 で、SSL (Secure Sockets Layer) を使用する場合はポート 995 で受信します。

Microsoft Exchange POP3 サービスは、クライアント アクセス サーバーの役割を実行する Exchange 2013 コンピューターで実行します。Microsoft Exchange POP3 バックエンド サービスは、メールボックス サーバーの役割を実行する Exchange 2013 コンピューターで実行します。クライアント アクセスの役割とメールボックスの役割を同じコンピューター上で実行している環境では、両方のサービスを同じコンピューター上で管理します。

POP3 および IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 および IMAP4 のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## Microsoft 管理コンソール サービス スナップインを使用して POP3 サービスを開始または停止する

POP3 サービスを開始するには、次の手順を実行します。

1.  クライアント アクセス サーバーの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。<strong>Microsoft Exchange POP3</strong> を右クリックし、<strong>開始</strong> をクリックします。

2.  メールボックスの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。結果ウィンドウで、<strong>Microsoft Exchange POP3 バックエンド</strong> を右クリックし、<strong>開始</strong> をクリックします。

POP3 サービスを停止するには、次の手順を実行します。

1.  クライアント アクセス サーバーの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。<strong>Microsoft Exchange POP3</strong> を右クリックし、<strong>停止</strong> をクリックします。

2.  メールボックスの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。<strong>Microsoft Exchange POP3 バックエンド</strong> を右クリックし、<strong>停止</strong> をクリックします。

## シェルを使用して POP3 サービスを開始または停止する

POP3 サービスを開始するには、次の手順を実行します。

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange POP3 サービスを開始します。
    
    ```powershell
Start-service MSExchangePOP3
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange POP3 バックエンド サービスを開始します。
    
    ```powershell
Start-service MSExchangePOP3BE
```

POP3 サービスを停止するには、次の手順を実行します。

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange POP3 サービスを停止します。
    
    ```powershell
Stop-service MSExchangePOP3
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange POP3 バックエンド サービスを停止します。
    
    ```powershell
Stop-service MSExchangePOP3BE
```

## net start コマンドを使用して POP3 サービスを開始または停止する

POP3 サービスを開始するには、次の手順を実行します。

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange POP3 サービスを開始します。
    
    ```powershell
Net Start msExchangePOP3
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange POP3 バックエンド サービスを開始します。
    
    ```powershell
Net Start msExchangePOP3BE
```

POP3 サービスを停止するには、次の手順を実行します。

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange POP3 サービスを停止します。
    
    ```powershell
Net Stop MSExchangePOP3
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange POP3 バックエンド サービスを停止します。
    
    ```powershell
Net Stop MSExchangePOP3BE
```

## 正常な動作を確認する方法

1.  Exchange クライアント アクセス サーバーで、Windows タスク マネージャーを開きます。Microsoft Exchange POP3 サービスが実行中である場合、<strong>サービス</strong> タブで、<strong>MSExchangePOP3</strong> の状態が <strong>実行中</strong> と表示されます。

2.  Exchange メールボックス サーバーで、Windows タスク マネージャーを開きます。Microsoft Exchange POP3 バックエンド サービスが実行中である場合、<strong>サービス</strong> タブで、<strong>MSExchangePOP3BE</strong> の状態が <strong>実行中</strong> と表示されます。

