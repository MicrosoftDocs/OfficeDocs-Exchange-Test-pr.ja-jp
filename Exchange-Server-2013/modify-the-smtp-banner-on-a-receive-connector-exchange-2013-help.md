---
title: '受信コネクタで SMTP バナーを変更する: Exchange 2013 Help'
TOCTitle: 受信コネクタで SMTP バナーを変更する
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52057865
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 受信コネクタで SMTP バナーを変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

*SMTP バナー*とは、リモートの SMTP メッセージング サーバーが、Microsoft Exchange Server 2013 を実行しているコンピューター上に構成されている受信コネクタに接続したときに受信する SMTP 接続応答です。

これは、リモートの SMTP メッセージング サーバーが受信コネクタに接続したときに受信する既定の応答です。

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

受信コネクタの SMTP バナーにカスタム値を指定した場合、その SMTP 受信コネクタに接続するリモート SMTP メッセージング サーバーは、次の応答を受信します。

    220 <Banner Text>

サーバー名やメッセージング サーバー ソフトウェアが SMTP バナーによって外部に知られないように、インターネット側の SMTP 受信コネクタの SMTP バナーを変更できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「受信コネクタ」。

  - この手順を実行するには、シェルを使用する必要があります。

  - 置換する SMTP バナー テキストの文字列は "`220`" で始まる必要があります。RFC 2821 で定義されているように、準備完了であることを示す既定の SMTP 応答コードは 220 です。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して受信コネクタの SMTP バナーを変更する

次のコマンドを実行します。

    Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"

この例では、既存の From the Internet という名前の受信コネクタの SMTP バナーを変更して、SMTP バナーで `220 Contoso Corporation` が表示されるようにします。

    Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"

この例では、From the Internet という名前の受信コネクタからカスタムの SMTP バナーを削除して、SMTP バナーを既定の値に戻します。

    Set-ReceiveConnector "From the Internet" -Banner $null

## 正常な動作を確認する方法

SMTP バナーの変更が正しく行われたことを確認するには、以下の手順を実行します。

1.  受信コネクタにアクセスできるコンピューター上で Telnet クライアントを開き、次のコマンドを実行します。
    
        open <Connector FQDN or IP address> <Port>

2.  受信コネクタの応答に構成した SMTP バナーが含まれていることを確認します。

この手順は、匿名認証または基本認証を許可している受信コネクタのみで実行できる点に注意してください。詳細については、「[Telnet を使用した SMTP 通信のテスト](use-telnet-to-test-smtp-communication-exchange-2013-help.md)」を参照してください。

