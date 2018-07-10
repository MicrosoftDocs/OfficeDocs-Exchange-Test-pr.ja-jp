---
title: 'UM プロトコル、ポート、およびサービス: Exchange 2013 Help'
TOCTitle: UM プロトコル、ポート、およびサービス
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54652966
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM プロトコル、ポート、およびサービス

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2015-03-09_

MicrosoftExchange 2013 ユニファイド メッセージング (UM) では、Exchange 2013 を実行中のサーバーとその他のデバイス間で通信を確立するために使用される複数の TCP ポートとユーザーデータグラム プロトコル (UDP) ポートが必要になります。これらの IP ポートを使用したアクセスを許可することにより、ユニファイド メッセージングを正しく機能させることができます。ここでは、Exchange 2013 ユニファイド メッセージングで使用される TCP ポートと UDP ポートについて説明します。

## ユニファイド メッセージングのプロトコルおよびサービス

Exchange 2013 ユニファイド メッセージングの機能とサービスは、静的と動的な TCP ポートと UDP ポートを使用して、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバーと Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーの正しい動作を保証します。Exchange 2013 をインストールすると、Exchange に静的な受信 Windows ファイアウォール ルールが追加されます。クライアント アクセス サーバーとメールボックス サーバーで使用される TCP ポートを変更する場合は、ユニファイド メッセージングが正しく機能するように Windows ファイアウォール ルールを再構成する必要もあります。


> [!IMPORTANT]
> UM コンポーネントとサービスを実行している Exchange 2013 クライアント アクセス サーバーとメールボックス サーバーでは、Exchange セットアップ プログラムが TCP ポートの制限なしで受信通信を許可する受信ファイアウォール ルールを作成します。UM サービス用の以下の受信ルールが追加されます。



1.  **SESWorker (GFW) (TCP-In)**

2.  **UMCallRouter (GFW) (TCP-In)**

3.  **UMCallRouter (TCP-In)**

4.  **UMService (GFW) (TCP-In)**

5.  **UMService (TCP-In)**

6.  **UMWorkerProcess – RPC (TCP-In)**

7.  **UMWorkerProcess (GFW) (TCP-In)**

8.  **UMWorkerProcess (TCP-In)**

## セッション開始プロトコル

セッション開始プロトコル (SIP) は、ビデオ、音声、インスタント メッセージング、オンライン ゲーム、仮想現実などのマルチメディア要素を含む対話型ユーザー セッションの開始、変更、および終了に使用されるプロトコルです。これは、H.323 と共に、ボイス オーバー IP (VoIP) の代表的な信号プロトコルの 1 つです。ほとんどの VoIP 標準ベースのソリューションは、H.323 または SIP のいずれかを使用します。ただし、独自の設計およびプロトコルもいくつか存在します。VoIP プロトコルは、通常、キャッチホン、電話会議、通話の転送などの機能をサポートします。

VoIP ゲートウェイや IP 構内交換機 (PBX) などの SIP クライアントは、TCP と UDP ポート 5060 を使用して、Microsoft Exchange ユニファイド メッセージング呼び出しルータ サービスを実行しているクライアント アクセス サーバーなどの SIP サーバーに接続します。SIP は、音声またはビデオ通話の確立または破棄のためだけに使用されます。すべての音声およびビデオ通信は、リアルタイム転送プロトコル (RTP) を介して実行されます。

## リアルタイム転送プロトコル

RTP は、インターネットなどの特定ネットワークを介してオーディオおよびビデオを配信するための標準パケット形式を定義します。RTP は、ネットワークを介して音声またはビデオのデータのみを伝送します。通話の確立および破棄は一般的に、SIP により実行されます。

RTP は、通信のために標準のまたは静的な TCP ポートまたは UDP ポートを必要としません。RTP 通信は、偶数の UDP ポート上で行われ、その偶数の次に大きい奇数のポートが TCP 通信で使用されます。標準のポート範囲割り当ては存在しませんが、通常は、RTP が 1024 ～ 65535 の範囲のポートを使用するように構成され、Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーはこの慣例に従います。RTP は動的なポート範囲を使用するため、ファイアウォールを通過するのは困難です。

## ユニファイド メッセージング Web サービス

メールボックス サーバー上にインストールされたユニファイド メッセージング Web サービスは、クライアント、メールボックス サーバー、およびその他の Exchange 2013 サーバー役割を実行しているコンピューター間のネットワーク通信に IP を使用します。一部の Exchange 2013Outlook Web App と Outlook 2013 のクライアント機能は、ユニファイド メッセージング Web サービスを使用して正しく動作します。

ユニファイド メッセージング Web サービスを使用するユニファイド メッセージング クライアント機能は次のとおりです。

  - 電話での再生機能および PIN のリセット機能を含む、Exchange 2013Outlook Web App で使用可能なボイス メール オプション

  - Outlook クライアントの電話での再生機能

## UM ポート

クライアント アクセス サーバーの Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスは、伝送制御プロトコル (TCP) または相互トランスポート層セキュリティ (相互 TLS) のいずれかを経由する SIP を使用して、Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーと通信します。TCP/ユーザー データグラム プロトコル (UDP) ポートの競合を回避するために、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスおよび Microsoft Exchange ユニファイド メッセージング サービスは、既定では別の TCP ポートに設定され、その TCP ポート上で待機します。それらは、SIP および RTP トラフィックで相互 TLS が使用されているかどうかによって、セキュリティで保護されていない接続とセキュリティで保護された接続の両方を受け付けます。相互 TLS が使用されている場合、既定ではクライアント アクセス サーバーは、TCP ポート 5060 (セキュリティで保護されないモード) および TCP ポート 5061 (SIP セキュリティで保護されたモード) の両方で SIP 要求を待機します。これらのポートは **Set-UMCallRouterSettings** コマンドレットを使用して構成します。クライアント アクセス サーバーの Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスはメディア (RTP または SRTP) トラフィックを処理しないので、TCP ポートだけを使用して UDP ポートは使用しません。相互 TLS が使用されている場合、既定ではメールボックス サーバーは、TCP ポート 5062 (セキュリティで保護されないモード) および TCP ポート 5063 (SIP セキュリティで保護されたモード) の両方で SIP 要求を待機します。これらのポートは、Exchange 管理シェル コマンドレットでは構成できません。メールボックス サーバー上の Microsoft Exchange ユニファイド メッセージング サービスは、SIP ポート 5062 および 5063 でクライアント アクセス サーバーからの接続を受け付けます。クライアント アクセス サーバーが SIP 要求をメールボックス サーバーにリダイレクトした後、VoIP ゲートウェイ、IP PBX、または SBC、およびメールボックス サーバー上の Microsoft Exchange ユニファイド メッセージング ワーカー プロセスを使用して、RTP または SRTP メディア チャネルが作成されます。

次の表は、Exchange 2013 のポートとプロトコル、そしてポートを変更できるかどうかをまとめたものです。

### UM のリスニング ポート

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロトコル</th>
<th>TCP ポート</th>
<th>UDP ポート</th>
<th>ポートを変更できるかどうか</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP (クライアント アクセス サーバー - Microsoft ユニファイド メッセージング呼び出しルーター サービス)</p></td>
<td><p>5060 (セキュリティ保護なし)、5061 (セキュリティ保護あり)。サービスは両方のポートで待機します。</p></td>
<td><p>該当なし</p></td>
<td><p>変更可能。<strong>Set-UMCallRouterSettings</strong> コマンドレットを使用。</p></td>
</tr>
<tr class="even">
<td><p>SIP (メールボックス サーバー - Microsoft Exchange Unified Messaging サービス)</p></td>
<td><p>5062 (セキュリティ保護なし)、5063 (セキュリティ保護あり)。サービスは両方のポートで待機します。</p></td>
<td><p>該当なし</p></td>
<td><p>ポートの変更は不可。</p></td>
</tr>
<tr class="odd">
<td><p>SIP (メールボックス サーバー - UM ワーカー プロセス)</p></td>
<td><p>TCP の場合、5065 および 5067 (セキュリティで保護されない)。相互 TLS の場合、5065 および 5067 (セキュリティで保護される) が含まれます。デュアル モードに設定する場合は、5066 および 5068 も使用されます。</p></td>
<td><p>該当なし</p></td>
<td><p>ポートの変更は不可。</p></td>
</tr>
<tr class="even">
<td><p>RTP (メールボックス サーバー - UM ワーカー プロセス)</p></td>
<td><p>該当なし</p></td>
<td><p>ポートの範囲は 1024 ～ 65535 です。</p></td>
<td><p>ポートは、msexchangeum.config 構成ファイルで変更できます。msexchangeum.config ファイルは、Exchange 2013 ユニファイド メッセージング サーバー上の \Program Files\Microsoft\Exchange\V15\bin フォルダーにあります。</p></td>
</tr>
</tbody>
</table>


## Lync Server と UM ポート

Exchange 2013 ユニファイド メッセージングは、ネットワーク アドレス変換 (NAT) トラバーサルをサポートし、RTP メディアとメールボックス サーバー間での NAT ファイアウォール経由のトンネリングを許可します。ただし、これが機能するためには、Microsoft Office Communications Server 2007 R2 と Microsoft Lync Server 2010 または Microsoft Lync 2013 を環境内に展開する必要もあります。Exchange 2013 と Communications Server 2007 R2、Microsoft Lync Server 2010、または Lync 2013 の両方をネットワーク上に展開した場合は、Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーと NAT ファイアウォール外部のエンドポイントの通信が可能になります。メールボックス・サーバーは、Communications Server 2007 R2、Microsoft Lync Server 2010、または Lync 2013 プールが関連付けられ、特定の Communications Server 2007 または Lync Server プールを提供しているコンピューター上の A/V 認証サービスから適切な認証トークンを取得します。

A/V 認証サービスを使用すると、RTP 音声メディアが NAT デバイスとファイアウォールを通過することができます。メディア ゲートウェイは信号だけを処理し、NAT デバイスやファイアウォール経由で音声を安全に転送できないため、これが必要になります。Communications Server 2007、Lync Server 2010、または Lync 2013 で仲介サーバーを構成するときに、仲介サーバーが受信メディア パケットの転送先を認識するように、A/V 認証サービスが実行されている A/V エッジ サーバーを指定します。

Communications Server 2007 または Lync Server 2010/2013と Exchange 2013 ユニファイド メッセージングの展開方法については、以下を参照してください。

  - [Exchange 2013 UM および Lync Server の展開の概要](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [チェックリスト: Exchange 2013 UM と Lync Server の統合](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

