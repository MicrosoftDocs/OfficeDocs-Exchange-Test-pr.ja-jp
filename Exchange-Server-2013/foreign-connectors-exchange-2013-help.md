---
title: '外部コネクタ: Exchange 2013 Help'
TOCTitle: 外部コネクタ
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 49895290
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 外部コネクタ

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2012-09-25_

外部コネクタは、プライマリ トランスポート機構に SMTP を使用しないサーバーや外部システムにメッセージを配信します。例としては、fax ゲートウェイ サーバーがあります。 外部システム コネクタはローカル ディレクトリや共有ドロップ ディレクトリを使用してファイル転送で送信メッセージを外部システムに送信します。 外部コネクタは、Microsoft Exchange Server 2013 メールボックス サーバーのトランスポート サービスに作成します。

外部ゲートウェイ サーバーは、メールボックス サーバーのトランスポート サービスにあるピックアップ ディレクトリや再生ディレクトリを利用して Exchange 2013 組織にメッセージを送信できます。 形式の正しい電子メール メッセージ ファイルを各ディレクトリにコピーすると、そのメッセージ ファイルは Exchange への配信のために送信されます。


> [!TIP]
> 送信メッセージを SMTP 以外のシステムに配信する必要があるほとんどの場合で、配信エージェント コネクタの使用をお勧めします。配信エージェント コネクタではメッセージのキューを管理することができ、メッセージをファイル システムに書き込む必要がないなど、他にも利点があるためです。詳細は、「<A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">配信エージェントと配信エージェント コネクタ</A>」を参照してください。



## 詳細情報

[外部コネクタを作成して SMTP Fax ゲートウェイ以外にメッセージを配信する](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[配信エージェントと配信エージェント コネクタ](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/ja-jp/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/ja-jp/library/bb123789\(v=exchg.150\))

