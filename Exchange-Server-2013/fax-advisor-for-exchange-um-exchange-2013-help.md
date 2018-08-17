---
title: 'Exchange UM の FAX アドバイザー: Exchange Online Help'
TOCTitle: Exchange UM の FAX アドバイザー
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52057461
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange UM の FAX アドバイザー

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

Microsoft ユニファイド メッセージング (UM) は、送信 FAX や FAX ルーティングなどの拡張された FAX 機能のための認定された FAX パートナー ソリューションに依存します。既定では、ユーザーは、着信 FAX メッセージが UM が有効なユーザーに配信されるように構成されていません。Exchange サーバーは、FAX 要求を認定 FAX パートナー ソリューションに送信します。FAX パートナーのサーバーは FAX データを受信し、FAX が.tif 添付ファイルとして含まれている電子メール メッセージ内の受信者のメールボックスにその FAX データを送信します。詳細については、「[ボイス メール ユーザーが FAX を受信できるようにする](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> ユニファイド メッセージングの展開を計画するすべてのお客様は、ユニファイド メッセージングの専門家の支援を受けることをお勧めします。ユニファイド メッセージングの専門家は、従来のボイス メール システムからユニファイド メッセージングへの円滑な移行を遂行するための支援を行います。新しい展開、または従来のボイス メール システムのアップグレードを行うには、PBX とユニファイド メッセージングについての多くの知識が必要です。ユニファイド メッセージングの専門家への問い合わせ方法の詳細については、「<A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 ユニファイド メッセージング (UM) の専門家</A>」または「<A href="https://go.microsoft.com/fwlink/p/?linkid=261951">ユニファイド メッセージング用の Microsoft Pinpoint</A>」を参照してください。



## Exchange ユニファイド メッセージング FAX パートナー プログラム

Exchange UM と相互運用が可能と認定された FAX パートナーになるには、パートナーが FAX パートナーの相互運用性の仕様で規定されている要件を満たし、FAX ソリューションが独立認証機関から認定を受ける必要があります。Exchange ユニファイド メッセージングで使用する FAX 製品の認定の詳細については、「[ユニファイド メッセージングの FAX パートナー](mailto:fax-part@microsoft.com)」までご請求ください。

## ユニファイド メッセージングと相互運用が可能と認定された FAX パートナー ソリューション

Exchange ユニファイド メッセージングを既に展開しており、組織内で着信 FAX を有効にする FAX パートナーを検索している場合は、「[Microsoft Pinpoint の FAX パートナー](https://go.microsoft.com/fwlink/p/?linkid=190238)」を参照してください。これらのソフトウェア ベンダーは、Exchange Server との相互運用が可能と認定されており、ユニファイド メッセージング用の認定されたソフトウェア ソリューションを対象に加えています。

## VoIP、メディア ゲートウェイ、および IP PBX のサポート

組織の VoIP ゲートウェイを正しく構成することは、困難な展開作業ですが、着信 FAX 処理を行うために Exchange ユニファイド メッセージングを正常に展開するために必要となる作業です。質問がある場合や、最新の VoIP ゲートウェイの構成に関する情報を得るには、「[Exchange 2013 のテレフォニー アドバイザー](telephony-advisor-for-exchange-2013-exchange-2013-help.md)」を参照してください。「[サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)」には、VoIP ゲートウェイの構成に関する注意事項と、組織の VoIP ゲートウェイ、IP PBX、および SBC が Exchange ユニファイド メッセージングで動作するよう正しく構成するために必要となるファイルが掲載されています。

Exchange ユニファイド メッセージングと VoIP ゲートウェイとの相互運用性テストは Microsoft Unified Communications Open Interoperability Program に統合されました。詳細については、「[Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722)」 を参照してください。

VoIP ゲートウェイおよび IP PBX 用の「[Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722)」により、対象のテレフォニー ゲートウェイと IP PBX を Microsoft ユニファイド コミュニケーション ソフトウェアと共に使用する場合に、シームレスなセットアップおよびサポート サービスを受けることができます。


> [!IMPORTANT]
> T.38 または G.711 を使用した FAX の送受信は、ユニファイド メッセージングと Communications Server 2007 R2 または Microsoft Lync Server が統合されている環境ではサポートされていません。



## FAX 送受信の展開と構成

UM は、受信 FAX 呼び出しを専門の FAX パートナー ソリューションに転送します。この FAX パートナー ソリューションは、FAX 送信者と FAX 通話を確立し、UM が有効なユーザーの代わりに FAX を受信します。ただし、UM が有効なユーザーが FAX メッセージをメールボックスで受信できるようにするには、FAX パートナー サーバーを構成した後、UM ダイヤル プラン、UM メールボックス ポリシーを構成し、UM が有効なユーザーの FAX の受信を有効にする必要があります。詳細については、「[着信 FAX の設定](setting-up-incoming-faxing-exchange-2013-help.md)」を参照してください。

