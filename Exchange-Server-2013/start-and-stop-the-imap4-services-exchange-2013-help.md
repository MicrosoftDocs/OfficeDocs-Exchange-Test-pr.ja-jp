---
title: 'IMAP4 サービスの開始および停止: Exchange 2013 Help'
TOCTitle: IMAP4 サービスの開始および停止
ms:assetid: a52db4bd-69a6-47b2-acf3-d9d8571c7a87
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124022(v=EXCHG.150)
ms:contentKeyID: 49896396
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IMAP4 サービスの開始および停止

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-10-05_

既定では、Microsoft Exchange IMAP4 サービスおよび Microsoft Exchange IMAP4 バックエンド サービスの 2 つの IMAP4 サービスは、MicrosoftExchange Server 2013 を実行するコンピューター上で開始されていません。 電子メール クライアントが IMAP4 を使用して Exchange に接続できるようにするためには、これら 2 つのサービスを開始する必要があります。 これらサービスが実行しているとき、Exchange 2013 はセキュリティで保護されていない IMAP4 クライアントの通信をポート 143 で、SSL (Secure Sockets Layer) を使用する場合はポート 993 で受信します。

Microsoft Exchange IMAP4 サービスは、クライアント アクセス サーバーの役割を実行している Exchange 2013 コンピューターで動作します。 Microsoft Exchange IMAP4 バックエンド サービスは、メールボックス サーバーの役割を実行している Exchange 2013 コンピューターで動作します。 クライアント アクセスの役割とメールボックス サーバーの役割を同じコンピューター上で実行している環境では、両方のサービスを同じコンピューター上で管理します。

POP3 および IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 および IMAP4 のアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## Microsoft 管理コンソールのスナップインを使用して IMAP4 サービスを開始および停止する

IMAP4 サービスを開始するには:

1.  クライアント アクセス サーバーの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。 <strong>Microsoft Exchange IMAP4</strong> を右クリックし、<strong>開始</strong> をクリックします。

2.  メールボックスの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。 <strong>Microsoft Exchange IMAP4 バックエンド</strong> を右クリックし、<strong>開始</strong> をクリックします。

IMAP4 サービスを停止するには:

1.  クライアント アクセス サーバーの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。 <strong>Microsoft Exchange IMAP4</strong> を右クリックし、<strong>停止</strong> をクリックします。

2.  メールボックスの役割を実行しているコンピューターで、<strong>スタート</strong> ボタンをクリックし、<strong>プログラム</strong> をポイントします。次に <strong>管理ツール</strong> をポイントし、<strong>サービス</strong> をクリックします。<strong>Microsoft Exchange IMAP4 バックエンド</strong> を右クリックし、<strong>停止</strong> をクリックします。

## シェルを使用して IMAP4 サービスを開始または停止する

IMAP4 サービスを開始するには:

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange IMAP4 サービスを開始します。
    
    ```powershell
Start-service msExchangeIMAP4
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange IMAP4 バックエンド サービスを開始します。
    
    ```powershell
Start-service msExchangeIMAP4BE
```

IMAP4 サービスを停止するには:

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange IMAP4 サービスを停止します。
    
    ```powershell
Stop-service msExchangeIMAP4
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、シェルから次のコマンドを実行して Microsoft Exchange IMAP4 Backend サービスを停止します。
    
    ```powershell
Stop-service msExchangeIMAP4BE
```

## net start コマンドを使用して IMAP4 サービスを開始または停止する

IMAP4 サービスを開始するには:

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange IMAP4 サービスを開始します。
    
    ```powershell
net start msExchangeIMAP4
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange IMAP4 Backend サービスを開始します。
    
    ```powershell
net start msExchangeIMAP4BE
```

IMAP4 サービスを停止するには:

1.  クライアント アクセス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange IMAP4 サービスを停止します。
    
    ```powershell
Net Stop MSExchangeIMAP4
```

2.  メールボックス サーバーの役割を実行しているコンピューター上で、コマンド プロンプトで次のコマンドを実行して Microsoft Exchange IMAP4 Backend サービスを停止します。
    
    ```powershell
Net Stop MSExchangeIMAP4BE
```

## 正常な動作を確認する方法

1.  Exchange クライアント アクセス サーバーで、Windows タスク マネージャーを開きます。 Microsoft Exchange IMAP4 サービスが実行中である場合、<strong>サービス</strong> タブで、<strong>MSExchangeIMAP4</strong> の状態が <strong>実行中</strong> と表示されます。

2.  Exchange メールボックス サーバーで、Windows タスク マネージャーを開きます。 Microsoft Exchange IMAP4 Backend サービスが実行中である場合、<strong>サービス</strong> タブで、<strong>MSExchangeIMAP4BE</strong> の状態が <strong>実行中</strong> と表示されます。

