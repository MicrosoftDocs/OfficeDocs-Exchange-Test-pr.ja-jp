---
title: 'POP3 および IMAP4 のプロトコル ログ出力の構成: Exchange 2013 Help'
TOCTitle: POP3 および IMAP4 のプロトコル ログ出力の構成
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50555770
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 および IMAP4 のプロトコル ログ出力の構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-27_

シェルを使用して、POP3 および IMAP4 のプロトコル ログ設定を有効または無効にしたり、変更したりすることができます。既定では、プロトコル ログは無効になっています。

プロトコル ログ出力を使用すると、Exchange 環境で POP3 接続と IMAP4 接続を確認できます。これは、POP3 または IMAP4 のパフォーマンスに関する問題のトラブルシューティングする際に便利です。詳細については、「[POP3 および IMAP4 のプロトコル ログ出力](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)」を参照してください。POP3 および IMAP4 に関連する詳細については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 の設定」および「IMAP4 の設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して POP3 または IMAP4 のプロトコル ログ出力を有効化する

この例では、クライアント アクセス サーバー CAS01 で IMAP4 または POP3 のプロトコル ログ出力を有効にします。

    Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true


> [!NOTE]
> POP3 または IMAP4 のプロトコル ログ設定を変更した後、使用するサービスとして POP3 または IMAP4 のいずれかを再開する必要があります。POP3 サービスおよび IMAP4 サービスを再起動する方法の詳細については、「<A href="start-and-stop-the-pop3-services-exchange-2013-help.md">POP3 サービスの開始および停止</A>」および「<A href="start-and-stop-the-imap4-services-exchange-2013-help.md">IMAP4 サービスの開始および停止</A>」を参照してください。



構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」と「[Set-PopSettings](https://technet.microsoft.com/ja-jp/library/aa997154\(v=exchg.150\))」を参照してください。

## シェルを使用して POP3 または IMAP4 のプロトコル ログ出力を無効化する

この例では、クライアント アクセス サーバー CAS01 で IMAP4 または POP3 のプロトコル ログ出力を無効にします。

    Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
    Set-PopSettings -Server "CAS01" -protocolLogEnabled $false


> [!NOTE]
> POP3 または IMAP4 のプロトコル ログ設定を変更した後、使用するサービスとして POP3 または IMAP4 のいずれかを再開する必要があります。POP3 サービスおよび IMAP4 サービスを再起動する方法の詳細については、「<A href="start-and-stop-the-pop3-services-exchange-2013-help.md">POP3 サービスの開始および停止</A>」および「<A href="start-and-stop-the-imap4-services-exchange-2013-help.md">IMAP4 サービスの開始および停止</A>」を参照してください。



構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」と「[Set-PopSettings](https://technet.microsoft.com/ja-jp/library/aa997154\(v=exchg.150\))」を参照してください。

## シェルを使用して POP3 または IMAP4 のプロトコル ログ出力を変更する

POP3 および IMAP4 設定を変更するには、次のパラメーターを 1 つまたは複数設定して **Set-ImapSettings** または **Set-PopSettings**コマンドレットを実行します。

  - *LogFileLocation*   このパラメーターには、POP3 または IMAP4 プロトコル ログ ファイルの場所を指定します。既定では、POP3 プロトコル ログ ファイルは C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3 ディレクトリにあります。この例では、クライアント アクセス サーバー CAS01 で POP3 プロトコル ログ出力をオンにします。また、POP3 プロトコル ログ出力のディレクトリを C:\\Pop3Logging に変更します。
    
    ```powershell
Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"
```

  - *LogFileRollOverSettings*   このパラメーターには、POP3 または IMAP4 プロトコル ログ出力で新しいログ ファイルを作成する頻度を指定します。既定では、新しいログ ファイルが毎日作成されます。値は次のいずれかです。
    
    Hourly (1 時間ごと)
    
    Daily (毎日)
    
    Weekly (毎週)
    
    Monthly (毎月)
    
    この設定は、パラメーター *LogPerFileSizeQuota* の値がゼロに設定されている場合にのみ適用されます。この例では、新しいログ ファイルを 1 時間ごとに作成するように、クライアント アクセス サーバー CAS01 の POP3 プロトコル ログを変更します。
    
    ```powershell
Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly
```

  - *LogPerFileSizeQuota*   このパラメーターには、POP3 または IMAP4 プロトコル ログ ファイルの最大サイズをバイト単位で指定します。既定では、この値はゼロに設定されます。この値がゼロに設定されている場合、新しいプロトコル ログ ファイルは *LogFileRollOverSettings* パラメーターによって指定されている頻度で作成されます。
    
    この例では、ログ ファイルが 2 メガバイト (MB) に達したときに新しいログ ファイルを作成するように、クライアント アクセス サーバー CAS01 の POP3 プロトコル ログを変更します。
    
    ```powershell
Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
```
    
    この例では、クライアント アクセス サーバー CAS01 の POP3 プロトコル ログ出力を変更し、ログ ファイルの作成日時およびサイズに関係なく同じログ ファイルを作成します。
    
    ```powershell
Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited
```


> [!NOTE]
> POP3 または IMAP4 のプロトコル ログ設定を変更した後、使用するサービスとして POP3 または IMAP4 のいずれかを再開する必要があります。POP3 サービスおよび IMAP4 サービスを再起動する方法の詳細については、「<A href="start-and-stop-the-pop3-services-exchange-2013-help.md">POP3 サービスの開始および停止</A>」および「<A href="start-and-stop-the-imap4-services-exchange-2013-help.md">IMAP4 サービスの開始および停止</A>」を参照してください。



構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」と「[Set-PopSettings](https://technet.microsoft.com/ja-jp/library/aa997154\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

シェルで次のコマンドを実行して、POP3 のプロトコル ログ設定を確認します。POP3 のプロトコル ログが有効になっている場合、*ProtocolLogEnabled* パラメーターの値は `True` です。POP3 のプロトコル ログが無効になっている場合、値は `False` です。*LogFileLocation*、*LogPerFileSizeQuota*、および *LogFileRollOverSettings* の値が正しいことを確認することもできます。

```powershell
Get-PopSettings | format-list
```

シェルで次のコマンドを実行して、IMAP4 のプロトコル ログ設定を確認します。IMAP4 のプロトコル ログが有効になっている場合、*ProtocolLogEnabled* パラメーターの値は `True` です。IMAP4 のプロトコル ログが無効になっている場合、値は `False` です。*LogFileLocation*、*LogPerFileSizeQuota*、および *LogFileRollOverSettings* の値が正しいことを確認することもできます。

```powershell
Get-ImapSettings | format-list
```

## 詳細情報

POP3 および IMAP4 のプロトコル ログ出力設定を構成した後に、以下の作業も実行できます。

[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)

[POP3 サービスの開始および停止](start-and-stop-the-pop3-services-exchange-2013-help.md)

