---
title: 'POP3、IMAP4、SMTP サーバーの設定を Outlook Web App のエンド ユーザーが表示できるようにする: Exchange 2013 Help'
TOCTitle: POP3、IMAP4、SMTP サーバーの設定を Outlook Web App のエンド ユーザーが表示できるようにする
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50555863
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3、IMAP4、SMTP サーバーの設定を Outlook Web App のエンド ユーザーが表示できるようにする

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-11-28_

POP3 や IMAP4 を使用して MicrosoftExchange Server 2013 メールボックスに接続するユーザーがいる場合、ユーザーは接続するための正しいサーバー設定を知る必要があります。Exchange 2013 の既定のインストール後には、ユーザーは自分の着信 POP3/IMAP4 サーバー設定または送信 SMTP サーバー設定を確認できません。ただし、ユーザーが MicrosoftOutlook Web App を使用して自分の設定を確認できるように、Exchange を構成できます。

これらの手順を実行すると、ユーザーは Outlook Web App で以下の方法でサーバー設定を確認できるようになります。

1.  Outlook Web App で、**\[設定\]** \> **\[オプション\]** をクリックします。

2.  **\[オプション\]** で、**\[アカウント\]** \> **\[マイ アカウント\]** \> **\[POP または IMAP アクセスの設定\]** をクリックします。

POP3 および IMAP4 に関連する詳細情報については、「[Exchange Server 2013 での POP3 と IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## シェルを使用して、POP3 ユーザーおよび IMAP4 ユーザーによる Outlook Web App での着信 POP3 設定および IMAP4 設定の表示を可能にする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」の「POP3 の設定」および「IMAP4 の設定」。

この例では、エンド ユーザーが外部 POP3 サーバー設定を表示できるようにします。

    Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}

構文およびパラメーターの詳細については、「[Set-PopSettings](https://technet.microsoft.com/ja-jp/library/aa997154\(v=exchg.150\))」を参照してください。

この例では、エンド ユーザーが外部 IMAP4 サーバー設定を表示できるようにします。

    Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}

構文およびパラメーターの詳細については、「[Set-ImapSettings](https://technet.microsoft.com/ja-jp/library/aa998252\(v=exchg.150\))」を参照してください。

これらの変更を適用するには、IIS を再起動する必要があります。POP3 サービスを再起動する必要はありません。IIS を再起動するには、コマンド プロンプトから次を入力します。

    iisreset

## 正常な動作を確認する方法

ユーザーが POP3 サーバー設定を表示できるように正常に構成されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-PopSettings | format-list

2.  *ExternalConnectionSettings* プロパティが設定されていることを確認します。

ユーザーが IMAP4 サーバー設定を表示できるように正常に構成されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-ImapSettings | format-list

2.  *ExternalConnectionSettings* プロパティが設定されていることを確認します。

## シェルを使用して、POP3 ユーザーおよび IMAP4 ユーザーによる Outlook Web App での送信 SMTP 設定の表示を可能にする

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「受信コネクタ」。

この例では、エンド ユーザーが Outlook Web App を使用して内部および外部の SMTP サーバー設定を表示できるようにします。

    Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 

構文およびパラメーターの詳細については、「[Set-ReceiveConnector](https://technet.microsoft.com/ja-jp/library/bb125140\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

ユーザーが SMTP サーバー設定を表示できるように正常に構成されたことを確認するには、次の手順を実行します。

1.  シェルで、次のコマンドを実行します。
    
        Get-ReceiveConnector | format-list

2.  *AdvertiseClientSettings* プロパティを `true` に設定した場合、ユーザーは Outlook Web App で SMTP サーバー設定を表示できます。*AdvertiseClientSettings* を `false` に設定した場合、ユーザーは Outlook Web App で SMTP サーバー設定を表示できません。

## 詳細情報

エンド ユーザーが POP3、IMAP4、および SMTP 設定を表示できるようにした後、以下の操作も実行できます。

[ユーザーの POP3 アクセスを有効または無効にする](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[ユーザーの IMAP4 アクセスを有効または無効にする](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

