---
title: 'Exchange 2013 のテレフォニー アドバイザー: Exchange 2013 Help'
TOCTitle: Exchange 2013 のテレフォニー アドバイザー
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50555891
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 のテレフォニー アドバイザー

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2017-07-25_

ユニファイド メッセージング (UM) では、Microsoft Exchange を組織の既存のテレフォニー システムに統合する必要があります。展開を成功させるには、既存のテレフォニー インフラストラクチャを慎重に分析し、ユニファイド メッセージングを展開するための正しい計画手順を実行する必要があります。

テレフォニー ネットワークに関する経験がほとんどないか、まったくない Exchange 管理者にとっては、計画段階は大きな課題になる可能性があります。この課題に対処する方法については、このトピックの「Resources to Help with Your UM Deployment」を参照してください。

ユニファイド メッセージングでサポートされている VoIP ゲートウェイを確認したり、PBX が特定の VoIP ゲートウェイ モデルまたは製造元でサポートされているかどうかや、直接 SIP 接続で IP PBX がサポートされているかどうかを判断したり、Exchange Online UM でサポートされているセッション ボーダー コントローラー (SBC) を確認したりするには、次のリンクのいずれかをクリックしてください。

  - Supported VoIP gateways

  - Supported PBXs when using an AudioCodes VoIP gateway

  - Supported PBXs when using a dialogic VoIP gateway
    
      - PBXs supported when using a DMG1000 series Media Gateway
    
      - PBXs supported when using a DMG 2000 series Media Gateway
    
      - PBXs supported when using a DMG3000 series Media Gateway

  - Supported IP PBXs

  - Supported IP PBXs when using SIP media gateways

  - Exchange Unified Messaging, Office Communications Server 2007 R2, and Microsoft Lync Server

## UM の展開に役立つリソース

テレフォニー ネットワークを展開するためのガイドラインを作成するのは困難です。テレフォニー ネットワークには異なる構成設定、ファームウェア、および要件を持つ VoIP ゲートウェイ、IP PBX、および PBX が含まれる場合があるため、それぞれがまったく異なるものである可能性があります。ただし、ユニファイド メッセージングの展開を成功させるために、次のようなリソースを利用することができます。

  - **ユニファイド メッセージング スペシャリスト   **UM スペシャリストは、Exchange エンジニアリング チームが実施する、Exchange ユニファイド メッセージングに関する技術的なトレーニングを受けたシステム インテグレーターです。従来のボイス メール システムから ユニファイド メッセージングへのスムーズな移行を行うために、Microsoft では、すべてのお客様が UM スペシャリストの支援を受けることをお勧めします。問い合わせ方法の詳細については、「[Microsoft Exchange Server 2013 ユニファイド メッセージング (UM) の専門家に関するページ](https://go.microsoft.com/fwlink/p/?linkid=262708)」または「[ユニファイド メッセージング向けの Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)」を参照してください。

  - **サポートされる VoIP ゲートウェイ、IP PBX、および PBX の構成に関する注意事項**   これらの構成に関する注意事項には、VoIP ゲートウェイ、IP PBX、および PBX を構成してネットワーク上のユニファイド メッセージング サーバーとの通信を行うために役立つ、設定およびその他の情報が記載されています。詳細については、「[サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)」を参照してください。

  - **サポートされるセッション ボーダー コントローラーの構成に関する注意事項**   これらの構成に関する注意事項には、セッション ボーダー コントローラー (SBC) を構成して、ハイブリッド展開および Exchange Online ユニファイド メッセージング (UM) 展開で UM サーバーとの通信を行う際に非常に役立つ、設定およびその他の情報が記載されています。詳細については、「[サポートされているセッション ボーダー コントローラーの構成に関する注意事項](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > SBCs の運営、顧客からの直接接続を使用してサード パーティの PBX システムのサポート オンライン UM は、2018年 7 月で終了します。 詳細については Exchange チームのブログ<A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">で Exchange のオンライン セッションの枠線のコント ローラーのサポートの提供中止はユニファイド メッセージング</A>を参照してください。



ユニファイド メッセージング スペシャリストの支援を受ける前に、主要な質問に答えられるよう準備をしておく必要があります。以下の質問に対する答えを準備しておくことで、UM スペシャリストとの話し合いが生産的なものになります。

  - 電話またはボイス メール、あるいはその両方のユーザーは、組織内に現在何人いますか。

  - 何人のユーザーにユニファイド メッセージングを提供しますか。

  - ユニファイド メッセージングとの統合に使用するのは、どの PBX ですか。

  - 組織内に PBX はいくつありますか。ベンダー、種類 (回線ベースまたは IP ベース)、モデル、ファームウェアのバージョンを記入してください。

  - PBX はネットワーク化されていますか。それらは集中管理されていますか、あるいは複数の場所に置かれていますか。

  - 組織では現在どのようなボイス メール システムを使用していますか。ベンダー、種類、モデル、ファームウェアのバージョンを記入してください。

  - ボイス メール システムは PBX にどのように統合されていますか (アナログ、T1/E1、PRI、Digital Set Emulation、VoIP など)。

  - 音声ネットワークを現在使用していますか。

  - 組織ではどのような種類の FAX システムを使用していますか。その FAX システムでは Exchange への受信 FAX ルーティングがサポートされていますか。

  - 自動応答機能を使用していますか。

  - 電話のみのユーザー、つまり電子メールでのアクセスを行わないユーザーに対するサポートを必要としますか。

## サポートされている VoIP ゲートウェイ

ユニファイド メッセージングと PBX を統合するには、1 つ以上の VoIP ゲートウェイを使用して、TDM ベースの PBX で使用される回線交換プロトコルを、ユニファイド メッセージで使用される IP ベースのパケット交換プロトコルに変換する必要があります。複数のモデルの VoIP ゲートウェイおよびメディア ゲートウェイを提供する VoIP ゲートウェイ ベンダーがテストされ、ユニファイド メッセージングでサポートされています。

ユニファイド メッセージングと VoIP ゲートウェイ、IP PBX、および SBC との相互運用性テストは Microsoft Unified Communications Open Interoperability Program に統合されました。詳細については、「[Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722)」 を参照してください。

VoIP ゲートウェイ、IP PBX、および高度な VoIP ゲートウェイ用の「[Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722)」の資格プログラムにより、対象のテレフォニー VoIP ゲートウェイと IP-PBX を Microsoft ユニファイド コミュニケーション ソフトウェアと共に使用する場合に、シームレスなセットアップおよびサポート サービスを受けることができます。厳しく広範囲のテスト要件を満たし、仕様とテスト プランに準拠する製品のみ資格を受けます。

サポートされる VoIP ゲートウェイ、IP PBX、PBX、および SBC の構成の詳細については、次のリソースのいずれかを参照してください。

  - [サポートされる VoIP ゲートウェイ、IP Pbx、および PBX の構成に関する注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [サポートされているセッション ボーダー コントローラーの構成に関する注意事項](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

次の VoIP ゲートウェイ ベンダーの相互運用性が検証されました。

  - AudioCodes

  - Dialogic

  - 次の表 1 に、VoIP ゲートウェイ ベンダー、VoIP ゲートウェイのモデル、および各モデルでサポートされているプロトコルを示します。

### ユニファイド メッセージングでサポートされている VoIP ゲートウェイ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ベンダー</th>
<th>モデル</th>
<th>サポートされるプロトコル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>インバンド DTMF を使用したアナログ</p></li>
<li><p>SMDI を使用したアナログ</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>インバンド DTMF を使用したアナログ</p></li>
<li><p>SMDI を使用したアナログ</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>Digital Set Emulation</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>インバンド DTMF を使用したアナログ</p></li>
<li><p>SMDI を使用したアナログ</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 以上</p></td>
<td><ul>
<li><p>TDM シグナリング (ISDN): AT&amp;T 4ESS/5ESS、Nortel DMS- 100、Euro ISDN (ETSI 300-102)、QSIG、NTT InsNet (日本)、ANSI National ISDN-2 (NI-2)</p></li>
<li><p>TDM Signaling (CAS): T1 CAS (E&amp;M、ループ スタート)、E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Tenor DX Series</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## AudioCodes VoIP ゲートウェイでサポートされている PBX

次の表に、MediaPack-114 FXO、MediaPack-118 FXO、Mediant 2000 などの AudioCodes VoIP ゲートウェイでサポートされている PBX を示します。

### AudioCodes VoIP ゲートウェイでサポートされている PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX の製造元</th>
<th>PBX モデル/種類</th>
<th>AudioCodes のモデル (&quot;x&quot; は、4 または 8、&quot;y&quot; は、1、2、4、8、または 16)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000、M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000/IP-to-IP</p></li>
<li><p>Mediant2000/IP-to-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra Elite</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Communication Server-1000M、1000S、1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 11c、51c、61c、81c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824、KX-TEA308</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30、KX-TDA100、KX-TDA200、KX-TDA600</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>IP テレフォニー システム</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran Telecom</p></td>
<td><p>Coral Flexicom、Coral IPX</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Dialogic VoIP ゲートウェイでサポートされている PBX

Dialogic VoIP ゲートウェイの各モデルでは、異なる PBX がサポートされています。次の表では、Dialogic VoIP ゲートウェイが使用できる PBX の製造元とモデルを示しています。各 VoIP ゲートウェイでは、異なる信号方式、密度、プロトコルが使用されます。

## DMG1000 Series Media Gateway でサポートされている PBX

次の表に、低密度 Dialogic Media Gateway (DMG1000) でサポートされている PBX を示します。ただし、アナログ DMG1000 を使用している場合は、補足信号 (RS232 SMDI、MD110、MCI プロトコル、またはインバンド DTMF 信号) が必要になります。

### 低密度 Dialogic DMG1000 Series VoIP ゲートウェイでサポートされている PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX の製造元</th>
<th>PBX モデル/種類</th>
<th>DMG のモデルと追加の信号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (以前の Ericsson MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>MD110 RS232 プロトコルを使用したアナログ接続</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100、S8300、S8700、および S8710 (Communications Mgr SW V2.0 以降)</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>SMDI シリアル プロトコルを使用したアナログ接続</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200D、SX-200 Light、SX-2000 Light、SX-2000 S、SX-2000 VS、SX-200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000、2400、2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - オプション 11、21、21A、51、61、71、および 81</p>
<p>Meridian SL1 - Generic X11、リリース 15 以降のバージョン</p>
<p>Nortel Communication Server - 1000M、1000S、1000E with V3.0 以降のバージョン</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>SMDI シリアル プロトコルを使用したアナログ接続</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E (European)</p></td>
<td><p>DMG1008LSW</p>
<p>インバンド DTMF 信号を使用したアナログ接続</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 (SW リリース 80003 以降のバージョン)<br />
9000 (すべてのバージョン)</p>
<p>9751 (SW リリース 9005 のすべてのバージョン)</p>
<p>9751 (SW リリース 9006.4 以降のバージョン)</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX (SW バージョン AR1ME021.00)</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>その他</p></td>
<td><p>各種</p></td>
<td><p>DMG1008LSW</p>
<p>インバンド DTMF または SMDI を使用したアナログ接続</p></td>
</tr>
</tbody>
</table>


## DMG 2000 Series Media Gateway でサポートされている PBX

次の表に、T1/E1 Dialogic Media Gateway (DMG2000) でサポートされている PBX を示します。Single Span (DMG2030DTIQ)、Dual Span (DMG2060DTIQ)、または Quad Span (DMG2120DTIQ) 密度の DMG2000 ゲートウェイでは、以下のプロトコルがサポートされています。

  - T1 CAS

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

回線個別信号方式 (CAS) を使用している場合は、補足信号 (RS232 SMDI、MD110、MCI プロトコル、またはインバンド DTMF 信号) が必要になります。Q.SIG 信号を使用している場合、PBX では呼び出し側および受信側の情報に関連する補足サービスに加えて、ユニファイド メッセージングで要求される通話転送機能がサポートされている必要があります。

### DMG2000 Media Gateway でサポートされている PBX

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX の製造元</th>
<th>PBX モデル/種類</th>
<th>必要なソフトウェアのバージョン</th>
<th>プロトコルおよび追加の信号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>Version 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>Version 3 以降</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>Manager SW V2.0 以降のバージョン</p></td>
<td><p>T1 CAS</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>Release MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS (SMDI シリアル プロトコル使用)</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>Release 5200 Dec. 92 1b 以降のバージョン</p></td>
<td><p>CAS (MCI シリアル プロトコル使用)</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 Release 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Meridian 1- オプション 11</p></td>
<td><p>Release 15 以降のバージョン、オプション 19 および 46 が必要</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Communication Server 1000</p></td>
<td><p>Version 2121、Release 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>Release 9006.4 以降 (注 : 北アメリカ仕様ソフトウェアの読み込みのみ)</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX-2000 S、SX-2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>Version 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## DMG4008BRI Series Media Gateway でサポートされている PBX

DMG4000 シリーズの Media Gateway には、複数の TDM インターフェイス オプションが付属します。DMG4008BRI は、4 ポート/8 チャネルの密度をサポートし、次のプロトコルをサポートします。

  - ISDN BRI Q.SIG

  - ETSI-DSS1 (Euro ISDN)

  - NET 3 (ベルギー)

  - VN3 (フランス)

  - 1TR6 (ドイツ)

  - INS-64 (日本)

  - 5ESS Custom (北米 - AT\&T)

  - National ISDN (NI1 - 北米)

以下の表に、Dialogic 4000 Media Gateway Series (DMG4008) でサポートされている PBX を示します。

### DMG4008BRI Media Gateway でサポートされている PBX

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX の製造元</th>
<th>PBX モデル/種類</th>
<th>必要なソフトウェアのバージョン</th>
<th>プロトコルおよび追加の信号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## サポートされる IP PBX

IP PBX は、ユニファイド メッセージングでもサポートされています。次の表に、ユニファイド メッセージングへの直接 SIP 接続でサポートされている IP PBX を示します。

### 直接 SIP 接続でサポートされている IP PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX の製造元</th>
<th>PBX モデル/種類</th>
<th>必要なソフトウェアのバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX-ONE</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Aura</p></td>
<td><p>5.2.1 と Service Pack 5 (SP5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Communication Server 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>Call Manager、Unified Communications Manager</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## SIP メディア ゲートウェイでサポートされている IP PBX

ユニファイド メッセージングでは、SIP メディア ゲートウェイを使用する IP PBX もサポートされています。次の表に、ユニファイド メッセージングに接続するため、SIP メディア ゲートウェイの IP to IP でサポートされている IP PBX を示します。

### SIP メディア ゲートウェイでサポートされている IP PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX の製造元</th>
<th>PBX モデル/種類</th>
<th>SIP ゲートウェイ モデル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>Call Manager 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (IP-to-IP 対応)</p></td>
</tr>
</tbody>
</table>


## Exchange ユニファイド メッセージング、Office Communications Server 2007 R2 および Microsoft Lync Server

社内展開およびハイブリッド展開の場合、Exchange ユニファイド メッセージング、Microsoft Office Communications Server 2007 R2、および Microsoft Lync Server 2010 または Lync Server 2013 を一緒に展開することによって、組織内のユーザーにボイス メッセージング、インスタント メッセージング (IM)、強化されたユーザー プレゼンス、音声会議、および電子メールとメッセージングが統合された操作性を提供することができます。詳細については、次のトピックを参照してください。

  - [Exchange 2013 UM および Lync Server の展開の概要](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

資格のある SIP PSTN ゲートウェイと IP PBX の検索、テレフォニー インフラストラクチャ ベンダーがプログラムに参加するプロセスなど、エンタープライズ テレフォニー インフラストラクチャに対する Microsoft Unified Communications Open Interoperability Program の詳細については、「[Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071)」 を参照してください。

