---
title: 'POP3 および IMAP4 アクセスの IP アドレスとポートを構成する: Exchange 2013 Help'
TOCTitle: POP3 および IMAP4 アクセスの IP アドレスとポートを構成する
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50555821
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 および IMAP4 アクセスの IP アドレスとポートを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-28_

EAC および シェルを使用して、既定の設定とは異なる IP アドレスおよびポートを使用するように Microsoft Exchange POP3 サービスおよび IMAP4 サービスを構成できます。


> [!NOTE]
> インターネット プロトコル Version 4 (IPv4) 形式、インターネット プロトコル Version 6 (IPv6) 形式、または両方の形式の IP アドレスおよび IP アドレスの範囲を入力できます。Windows Server 2008&nbsp;の既定のインストールでは、IPv4 と IPv6 がサポートされています。



POP3 および IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 の設定」および「IMAP4 の設定」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## POP3 の IP アドレスおよびポートを構成する

## EAC を使用して POP3 の IP アドレスおよびポートを構成する

1.  EAC で **\[サーバー\]\>\[サーバー\]** に移動します。

2.  サーバーのリストでクライアント アクセス サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバー プロパティ ページで、**\[POP3\]** をクリックします。

4.  **\[TLS 接続または非暗号化接続\]** で、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  **\[IP アドレスの追加\]** ページの **\[IP アドレス\]** で、次のいずれかを選択します。
    
      - **\[利用可能なすべての IPv4 アドレス\]**   サーバーで利用可能なすべての IPv4 IP アドレスを使用します。
    
      - **\[利用可能なすべての IPv6 アドレス\]**   サーバーで利用可能なすべての IPv6 IP アドレスを使用します。
    
      - **\[IP アドレスの指定\]**   特定の IP アドレスを使用します。

6.  **\[ポート\]** でポート番号を入力するか、または既定のポートを承認します。

7.  **\[保存\]** をクリックして変更を保存します。

設定を有効にするには、POP3 の IP アドレスおよびポートを設定した後、POP3 サービスを再起動する必要があります。POP3 サービスを再起動する方法の詳細については、「[POP3 サービスの開始および停止](start-and-stop-the-pop3-services-exchange-2013-help.md)」を参照してください。

## シェルを使用して POP3 の IP アドレスおよびポートを構成する

この例では SSL (Secure Sockets Layer) と共に POP3 を使用して Exchange と通信するための IP アドレスとポートを設定します。

    Set-PopSettings -SSLBindings: IPaddress:Port

この例では暗号化なしまたは TLS (Transport Layer Security) 暗号化と共に POP3 を使用して Exchange と通信するための IP アドレスとポートを設定します。

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

設定を有効にするには、POP3 の IP アドレスおよびポートを設定した後、POP3 サービスを再起動する必要があります。POP3 サービスを再起動する方法の詳細については、「[POP3 サービスの開始および停止](start-and-stop-the-pop3-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-PopSettings](https://technet.microsoft.com/ja-jp/library/aa997154\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

サーバー上での POP3 の IP アドレス/ポート設定が変更されたことを確認するには、次の操作を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-PopSettings | format-list

2.  *UnencryptedOrTLSBindings* および *SSLBindings* の設定が正しいことを確認します。

## IMAP4 の IP アドレスおよびポートを構成する

## EAC を使用して IMAP4 の IP アドレスおよびポートを構成する

1.  EAC で **\[サーバー\]\>\[サーバー\]** に移動します。

2.  サーバーのリストでクライアント アクセス サーバーを選択し、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  サーバー プロパティ ページで、**\[IMAP4\]** をクリックします。

4.  TLS 接続または非暗号化接続設定を設定する場合は、**\[TLS 接続または非暗号化接続\]** で **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。Secure Sockets Layer (SSL) 接続設定を変更する場合は、**\[Secure Sockets Layer (SSL) 接続\]** で **\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

5.  **\[IP アドレスの追加\]** ページの **\[IP アドレス\]** で、次のいずれかを選択します。
    
      - **\[利用可能なすべての IPv4 アドレス\]**   サーバーで利用可能なすべての IPv4 IP アドレスを使用します。
    
      - **\[利用可能なすべての IPv6 アドレス\]**   サーバーで利用可能なすべての IPv6 IP アドレスを使用します。
    
      - **\[IP アドレスの指定\]**   特定の IP アドレスを使用します。

6.  **\[ポート\]** でポート番号を入力するか、または既定のポートを承認します。

7.  **\[保存\]** をクリックして変更を保存します。

設定を有効にするには、IMAP4 の IP アドレス/ポート設定を設定した後、IMAP4 サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

## シェルを使用して IMAP4 の IP アドレスおよびポートを構成する

この例では IMAP4 を使用して Exchange と通信するための IP アドレスとポートを設定します。

    Set-ImapSettings -SSLBindings: IPaddress:Port

この例では暗号化なしまたは TLS 暗号化と共に IMAP4 を使用して Exchange と通信するための IP アドレスとポートを設定します。

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

設定を有効にするには、IMAP4 の IP アドレス/ポート設定を設定した後、IMAP4 サービスを再起動する必要があります。IMAP4 サービスを再起動する方法の詳細については、「[IMAP4 サービスの開始および停止](start-and-stop-the-imap4-services-exchange-2013-help.md)」を参照してください。

構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

サーバー上での IMAP4 の IP アドレス/ポート設定が変更されたことを確認するには、次の操作を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-ImapSettings | format-list

2.  *UnencryptedOrTLSBindings* および *SSLBindings* の設定が正しいことを確認します。

## 詳細情報

POP3 または IMAP4 で使用する IP アドレスとポートを構成した後で、次の操作も実行できます。

[Exchange 2016 で IMAP4 を有効にする](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 で POP3 を有効にする](enable-pop3-in-exchange-2013-exchange-2013-help.md)

