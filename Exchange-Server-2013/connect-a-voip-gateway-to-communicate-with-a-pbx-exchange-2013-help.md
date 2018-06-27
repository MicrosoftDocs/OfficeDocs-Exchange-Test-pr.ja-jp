---
title: 'VoIP ゲートウェイを PBX と通信するために接続する: Exchange 2013 Help'
TOCTitle: VoIP ゲートウェイを PBX と通信するために接続する
ms:assetid: 76bcdc54-3ec2-408a-bdbe-37826580dd62
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998872(v=EXCHG.150)
ms:contentKeyID: 50555815
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# VoIP ゲートウェイを PBX と通信するために接続する

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2016-12-15_

Microsoft Exchange Server 2013 でユニファイド メッセージング (UM) のテレフォニーおよびデータ ネットワークを構成する場合は、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバーおよび Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーと通信できるように、VoIP ゲートウェイを構成する必要があります。また、組織内の構内交換機 (PBX) と通信するように VoIP ゲートウェイを構成する必要もあります。このトピックの情報およびリンクを使用して、PBX と通信するように IP ゲートウェイを構成できます。

## VoIP ゲートウェイを構成する

VoIP ゲートウェイを構成するときは、VoIP ゲートウェイ デバイスがアナログか、デジタルか、またはアナログとデジタルの両方かを考慮する必要があります。PBX に接続する VoIP ゲートウェイ インターフェイスがアナログの場合は、VoIP ゲートウェイが PBX と通信できるようにするための適切な設定を正しく構成する必要があります。PBX に接続する VoIP ゲートウェイ インターフェイスがデジタルの場合は、デジタル インターフェイスが PBX と通信できるようにするために必要な追加の構成は不要である可能性があります。

Exchange TechCenter の次の推奨リソースには、VoIP ゲートウェイおよび PBX を正しく構成するのに役立つ情報が含まれています。

  - **サポートされる VoIP ゲートウェイ、IP PBX、および PBX のドキュメント**   「[Exchange 2013 のテレフォニー アドバイザー](telephony-advisor-for-exchange-2013-exchange-2013-help.md)」には、VoIP ゲートウェイ および PBX を構成するときに使用できる構成ファイルとセットアップ情報が記載されています。

  - **構成および技術的な注記**   「[サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)」には、VoIP ゲートウェイ および PBX を構成するときに使用できる構成ファイルとセットアップ情報が記載されています。

  - **AudioCodes ベースの VoIP ゲートウェイの構成**  「[Microsoft Exchange Server リソース ページ](https://www.audiocodes.com/solutions/microsoft/exchange-server)」には、ユニファイド メッセージングで使用するための AudioCodes ベースの VoIP ゲートウェイの構成に役立つ最新のサポート情報および構成情報が記載されています。

  - **Dialogic ベースの VoIP ゲートウェイの構成** [Dialogic の Web サイト](https://www.dialogic.com/) には、Dialogic ベースの VoIP ゲートウェイに関する最新のサポートと構成の情報が記載されています。

ユニファイド メッセージングの展開を計画するすべてのお客様は、ユニファイド メッセージングの専門家の支援を受けることをお勧めします。Exchange ユニファイド メッセージングの専門家は、従来の、またはサードパーティ製のボイス メール システムからユニファイド メッセージングへのスムーズなアップグレードが実行されることを確保し、Exchange ユニファイド メッセージングを使用した新しいボイス メール システムの計画および展開を支援します。新しいボイス メール システムの展開または従来のボイス メール システムのアップグレードを行うには、VoIP ゲートウェイ、PBX、およびユニファイド メッセージングについての多くの知識が必要です。ユニファイド メッセージングの専門家に問い合わせる方法の詳細については、「[Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists](https://go.microsoft.com/fwlink/p/?linkid=262708)」(Microsoft Exchange Server 2013 ユニファイド メッセージング (UM) の専門家) を参照してください。または、「[Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)」の認定 UM パートナーにお問い合わせください。

## 詳細情報

[サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

[UM をサポートされる VoIP ゲートウェイに接続する](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)

