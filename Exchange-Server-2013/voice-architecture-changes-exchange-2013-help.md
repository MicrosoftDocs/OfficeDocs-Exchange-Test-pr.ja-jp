---
title: 'ボイスのアーキテクチャの変更: Exchange 2013 Help'
TOCTitle: ボイスのアーキテクチャの変更
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 48269515
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイスのアーキテクチャの変更

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2015-03-09_

Microsoft Exchange Server 2013 のアーキテクチャは、Exchange Server 2007 および Exchange Server 2010 のアーキテクチャとは異なっています。Exchange 2007 および Exchange 2010 では、サーバーの種類は複数のサーバーの役割に分かれていました。クライアント アクセス、メールボックス、ハブ トランスポート、ユニファイド メッセージングです。Exchange 2013 では、サーバーの役割が 2 つのサーバーの種類に集約されました。それらのサーバー役割から派生したコンポーネントやサービスはいずれも、同一の物理サーバー上で実行されるか、2 種類の別々のサーバー ("クライアント アクセス" と "メールボックス") 上で実行されます。新しいモデルでは、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバーは、着信呼び出しによって生成されるセッション開始プロトコル (SIP) トラフィックをメールボックス サーバーにリダイレクトします。次に、VoIP ゲートウェイまたは IP 構内交換機 (PBX) から、ユーザーのメールボックスをホストしているメールボックス サーバーに対して、メディア (リアルタイム転送プロトコル (RTP) またはセキュリティで保護された RTP (SRTP)) チャネルが確立されます。Exchange 2013 では、メールボックス サーバーは Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバーの役割と同じ処理を行います。メールボックス サーバーは、Microsoft Exchange ユニファイド メッセージング サービスと UM ワーカー プロセスの両方を実行します。クライアント アクセス サーバーは、着信呼び出しを受信してメールボックス サーバーへと転送する Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行します。

**目次**

新しい Exchange アーキテクチャのサポート

UM ポート

UM ダイヤル プラン

UM 呼び出しルーターのパフォーマンス カウンター

## 新しい Exchange アーキテクチャのサポート

Exchange 2013 では、クライアント アクセス サーバーは、自動検出、SSL (Secure Sockets Layer)、認証、リダイレクト、プロキシを担当します。クライアント アクセス サーバーは、すべての着信呼び出しまたはユニファイド メッセージング (UM) に対する SIP 要求のエントリ ポイントです。ルーティングのロジックおよび SIP REDIRECT は、クライアント アクセス サーバーに自動的に含まれているサービスとして実装されています。このサービスは、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスと呼ばれます。これは、組織の各クライアント アクセス サーバーにインストールされて実行されます。クライアント アクセス サーバーが着信呼び出しに対する SIP INVITE を受信すると、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスは、着信呼び出しをメールボックス サーバーにリダイレクトします。次に、VoIP ゲートウェイ、IP PBX、またはセッション ボーダー コントローラー (SBC) とメールボックス サーバーの間にメディア チャネル (RTP または SRTP) が作成されます。クライアント アクセス サーバーは SIP リダイレクターとして動作しますが、VoIP ゲートウェイ、IP PBX、または SBC からの SIP 要求だけを処理します。メディア トラフィックは受信しません。RTP または SRTP を使用するメディア トラフィックは、メールボックス サーバーと SIP ピア (VoIP ゲートウェイ、IP PBX、SBC など) の間でのみ受け渡しされ、クライアント アクセス サーバーには渡されません。Exchange 2013 および UM を展開する場合、VoIP ゲートウェイ、IP PBX、または SBC が、インストールしたクライアント アクセス サーバーを指し示して、着信呼び出しが UM に対して正しくルーティングされるように構成する必要があります。

場合によっては、複数のクライアント アクセス サーバーを展開することが要件で、クライアント アクセス サーバーはメールボックス サーバーとは別の物理ハードウェア上に展開されます。L4 または L5 ハードウェアを使用するか、ソフトウェア負荷分散装置を使用して、複数のクライアント アクセス サーバーをアレイにグループ化できます。ただし、Active Directory の Exchange オブジェクト ベースのクライアント アクセス サーバー アレイはありません。クライアント アクセス サーバーの前段階にハードウェアまたはソフトウェアの負荷分散装置を使用することは、大規模な Exchange 展開における一般的に認められたプラクティスです。

クライアント アクセス サーバーをインストールすると、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスが実行されます。サービスは、次のような操作を行います。

  - 初期化時に、msexchangeumcallrouter.config という名前のローカル構成ファイルを読み込みます。

  - 組織の調停メールボックスを使用して、音声認識文章校正の生成を実行します。

  - 伝送制御プロトコル (TCP) またはトランスポート層セキュリティ (TLS) 接続をサポートします。この設定は構成可能です。

  - 構成エラーがある場合または必要なポートを登録できない場合にだけ停止します。

Exchange 2013 では、メールボックス サーバーは着信呼び出しの SIP 要求に対する返答を担当しません。クライアント アクセス サーバーからの SIP トラフィックの受信だけを担当し、VoIP ゲートウェイ、IP PBX、または SBC に対して RTP または SRTP 接続を確立します。

クライアント アクセス サーバーが着信呼び出しをメールボックス サーバーにリダイレクトした後、VoIP ゲートウェイ、IP PBX、または SBC とメールボックス サーバーの間でメディア チャネルが確立します。メディア チャネルの確立後、メールボックス サーバー上の Microsoft Exchange ユニファイド メッセージング サービスは、ユーザーのボイス メール案内応答を再生し、ユーザーの通話応答ルールの処理後に、発信者に音声メッセージを残すよう促します。その後、メールボックス サーバーは音声メッセージを記録し、メッセージのトランスクリプションを作成して、ユーザーのメールボックスに音声メッセージを置きます。ただし、Exchange を Office Communications Server 2007 R2 または Lync Server と統合している場合は、着信呼び出しの SIP および RTP または SRTP メディア チャネルの両方は、Lync サーバーおよびメールボックス サーバーによって処理されます。Lync 統合環境には VoIP ゲートウェイ、IP PBX、または SBC はありません。Lync にとって、Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーは単なる Exchange 2010 UM サーバーとして見えます。メールボックス サーバーと Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバーは、両方のサーバーとも SIP ダイヤル プランに追加する必要があるので、信頼済みピアと見なされます。Lync は受信ルーティング コンポーネントを使用して受信呼び出しをルーティングします。受信ルーティング コンポーネントは、SIP を使用してクライアント アクセス サーバーと通信し、呼び出しをメールボックス サーバーにルーティングします。

Exchange 2010 UM 管理者は、各 UM サーバー上にユニファイド メッセージング用のプロパティのセットを構成できます。Exchange 2013 では、UM コンポーネントおよび UM の構成の設定は、クライアント アクセスとメールボックス サーバーの両方に存在します。Exchange 2010 のユニファイド メッセージング サーバーの役割を実行している、単一コンピューターに適用された構成設定はすべて引き続き利用可能です。ただし、これらのプロパティおよび構成設定の一部は、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行しているクライアント アクセス サーバー上で設定され、その他は Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバー上で利用できます。場合によっては、両方で同じ設定を利用できます。次の表に、クライアント アクセス サーバーおよびメールボックス サーバーで利用できるコマンドレットとパラメーター、および以前のバージョンのユニファイド メッセージングで展開シナリオをサポートするためにコマンドレットで変更が行われた箇所を示します。

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**   Exchange 2013 メールボックス サーバー上で利用でき、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上でも動作します。

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**   Exchange 2013 クライアント アクセス サーバー上では利用できますが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では利用できません。

  - **Set-UMService -MaxCallsAllowed \<Int32\>**   Exchange 2013 メールボックス サーバー上で利用でき、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上でも動作します。

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   Exchange 2013 クライアント アクセス サーバー上で利用できず、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上でも利用できません。

  - **Set-UMService -SipTcpListeningPort \<Int32\>**   Exchange 2013 メールボックス サーバー上で構成できませんが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作します。

  - **Set-UMService -SipTlsListeningPort \<Int32\>**   Exchange 2013 メールボックス サーバー上で構成できませんが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作します。

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**   Exchange 2013 クライアント アクセス サーバー上では利用できますが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作しません。

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**   Exchange 2013 クライアント アクセス サーバー上では利用できますが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作しません。

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   Exchange 2013 メールボックス サーバー上で利用できませんが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作します。

  - **Set-UMCallRouterSettings - Status \<Enabled | Disabled | NoNewCalls\>**   Exchange 2013 クライアント アクセス サーバー上で利用できず、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上でも動作しません。

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**   Exchange 2013 メールボックス サーバー上で利用でき、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上でも動作します。

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Dual\>**   Exchange 2013 クライアント アクセス サーバー上では利用できますが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作しません。

  - **Enable-UMService**   Exchange 2013 メールボックス サーバー上で利用できませんが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作します。

  - **Disable-UMService**   Exchange 2013 メールボックス サーバー上で利用できませんが、Exchange 2007 および Exchange 2010 のユニファイド メッセージング サーバー上では動作します。

メールボックス サーバーについては、**Set/Get/Enable/Disable-UMService** コマンドレットを使用して、Exchange 2013 メールボックス サーバーあるいは Exchange 2007 または Exchange 2010 のユニファイド メッセージング サーバー上の Microsoft Exchange ユニファイド メッセージング サービスの UM プロパティを表示または構成します。クライアント アクセス サーバー上の Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスのプロパティを表示または構成するには、異なるセットのコマンドレット、**Set/Get-UMCallRouterSettings** を使用します。これにより、Exchange 2007 および Exchange 2010 の既存のコマンドレット、**Get-UMServer**、**Set-UMServer**、**Enable-UMServer**、および **Disable-UMServer** は、Exchange 2013 メールボックス サーバーとの共存展開において確実に機能します。また、メールボックス サーバーおよびクライアント アクセス サーバーが同じサーバーまたは別のサーバーにインストールされている場合でもコマンドレットが確実に機能するようにもなります。

新しい Exchange アーキテクチャのサポート

## UM ポート

クライアント アクセス サーバーの Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスは、伝送制御プロトコル (TCP) または相互トランスポート層セキュリティ (相互 TLS) のいずれかを経由する SIP を使用して、Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバーと通信します。TCP/ユーザー データグラム プロトコル (UDP) ポートの競合を回避するために、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスおよび Microsoft Exchange ユニファイド メッセージング サービスは、既定では別の TCP ポートに設定され、その TCP ポート上で待機します。それらは、SIP および RTP トラフィックで相互 TLS が使用されているかどうかによって、セキュリティで保護されていない接続とセキュリティで保護された接続の両方を受け付けます。相互 TLS が使用されている場合、既定ではクライアント アクセス サーバーは、TCP ポート 5060 (セキュリティで保護されないモード) および TCP ポート 5061 (SIP セキュリティで保護されたモード) の両方で SIP 要求を待機します。これらのポートは **Set-UMCallRouterSettings** コマンドレットを使用して構成します。クライアント アクセス サーバーの Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスはメディア (RTP または SRTP) トラフィックを処理しないので、TCP ポートだけを使用して UDP ポートは使用しません。相互 TLS が使用されている場合、既定ではメールボックス サーバーは、TCP ポート 5062 (セキュリティで保護されないモード) および TCP ポート 5063 (SIP セキュリティで保護されたモード) の両方で SIP 要求を待機します。これらのポートは、Exchange 管理シェル コマンドレットでは構成できません。Microsoft Exchange ユニファイド メッセージング サービスを実行しているメールボックス サーバー上では、Exchange サーバーの TCP ポートはシェルを使用したりレジストリの設定を構成しても構成できません。メールボックス サーバー上の Microsoft Exchange ユニファイド メッセージング サービスは、SIP ポート 5062 および 5063 でクライアント アクセス サーバーからの接続を受け付けます。クライアント アクセス サーバーが SIP 要求をメールボックス サーバーにリダイレクトした後、VoIP ゲートウェイ、IP PBX、または SBC、およびメールボックス サーバー上の Microsoft Exchange ユニファイド メッセージング ワーカー プロセスを使用して、RTP または SRTP メディア チャネルが作成されます。

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
<td><p>SIP (クライアント アクセス サーバー - Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービス)</p></td>
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
<td><p>TCP の場合、5065 および 5067 (セキュリティで保護されない)。相互 TLS の場合、5066 および 5068 (セキュリティで保護される) が含まれます。この状況に該当する場合、<em>UMStartupMode</em> は <em>Dual</em> に設定されています。<em>UMStartUpMode</em> が <em>TCP</em> または <em>TLS</em> に設定されている場合、ポート 5065 および 5066 が使用されます。既定の <em>UMStartupMode</em> は <em>TCP</em> です。</p></td>
<td><p>該当なし</p></td>
<td><p>ポートの変更は不可。</p></td>
</tr>
<tr class="even">
<td><p>RTP (メールボックス サーバー - UM ワーカー プロセス)</p></td>
<td><p>該当なし</p></td>
<td><p>ポートの範囲は 1024 ～ 65535 です。</p></td>
<td><p>ポートの範囲はレジストリを介して変更できますが、これはサポートされている構成ではありません。</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


新しい Exchange アーキテクチャのサポート

## UM ダイヤル プラン

Exchange 2007 および Exchange 2010 で行ったような、UM ダイヤル プランの UM サーバーへのマッピングまたは関連付けは Exchange 2013 では必要ありません。UM サービスを実行しているクライアント アクセス サーバーまたはメールボックス サーバーは、ダイヤル プランにリンクする必要はありません。なぜなら、すべてのクライアント アクセス サーバーおよびメールボックス サーバーは VoIP ゲートウェイ、IP PBX、または SBC からすべての受信呼び出しを受け付けるはずだからです。例外は Lync 2013、Lync Server 2010、および Office Communications Server 2007 R2 で使用される SIP ダイヤル プランで、展開したクライアント アクセス サーバーおよびメールボックス サーバーと関連付ける必要があります。両方の種類の Exchange サーバーを、Communications Server 2007 R2 または Lync Server からの信頼済みピアとして含めるよう、各 SIP ダイヤル プランに追加する必要があります。そうしないと、Communications Server 2007 R2 または Lync Server はユーザーからの発信呼び出しを拒否します。

次の表に、クライアント アクセス サーバーとメールボックス サーバーと UM ダイヤル プランの関係をまとめます。

### UM ダイヤル プランのリンク

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>トポロジ</th>
<th>ダイヤル プラン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>同じサーバー上のクライアント アクセスおよびメールボックス (Communications Server 2007 R2 または Lync Server 2010 の SIP 以外のダイヤル プラン)</p></td>
<td><p>クライアント アクセス サーバーとメールボックス サーバーにダイヤル プランを関連付ける必要がなくなりました。クライアント アクセス サーバーまたはメールボックス サーバーをダイヤル プランに追加することは許可されません。<strong>Set-UMService</strong> コマンドレットを実行したときに、メールボックス サーバーを SIP 以外のダイヤル プランに関連付けようとすると、エラーが生成されます。</p></td>
</tr>
<tr class="even">
<td><p>異なるサーバー上のクライアント アクセスおよびメールボックス (Communications Server 2007 R2 または Lync Server 2010 の SIP 以外のダイヤル プラン)</p></td>
<td><p>クライアント アクセス サーバーとメールボックス サーバーにダイヤル プランを関連付ける必要がなくなりました。クライアント アクセス サーバーまたはメールボックス サーバーをダイヤル プランに追加することは許可されません。<strong>Set-UMService</strong> コマンドレットを実行したときに、メールボックス サーバーを SIP 以外のダイヤル プランに関連付けようとすると、エラーが生成されます。</p></td>
</tr>
<tr class="odd">
<td><p>同じ物理サーバー上のクライアント アクセス サーバーとメールボックス サーバー (Communications Server 2007 R2 および Lync Server 2010 で SIP ダイヤル プランを使用)</p></td>
<td><p>単一 SIP のダイヤル プランの場合、対象の SIP ダイヤル プランにすべてのクライアント アクセス サーバーとメールボックス サーバーを追加します。複数 SIP のダイヤル プランの場合、各 SIP のダイヤル プランにすべてのクライアント アクセス サーバーとメールボックス サーバーを追加します。この結果、両方のサーバーが Office Communications Server 2007 R2 または Lync Server の信頼済みピアになります。Office Communications Server 2007 R2 または Lync Server 展開には、各クライアント アクセス サーバーおよびメールボックス サーバーで使用するのと同じ証明書を使用する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>別の物理サーバー上のクライアント アクセス サーバーとメールボックス サーバー (Communications Server 2007 R2 および Lync Server 2010 で SIP ダイヤル プランを使用)</p></td>
<td><p>単一 SIP のダイヤル プランの場合、対象の SIP ダイヤル プランにすべてのクライアント アクセス サーバーとメールボックス サーバーを追加します。複数 SIP のダイヤル プランの場合、各 SIP のダイヤル プランにすべてのクライアント アクセス サーバーとメールボックス サーバーを追加します。この結果、両方のサーバーが Office Communications Server 2007 R2 または Lync Server の信頼済みピアになります。クライアント アクセス サーバーおよびメールボックス サーバーで使用される証明書が異なる場合、Office Communications Server 2007 R2 または Lync Server 展開には、組織の各クライアント アクセス サーバーおよびメールボックス サーバーで使用するのと同じ証明書を使用する必要があります。</p></td>
</tr>
</tbody>
</table>


新しい Exchange アーキテクチャのサポート

## UM 呼び出しルーターのパフォーマンス カウンター

過去のバージョンの Exchange には、Microsoft Exchange ユニファイド メッセージング サービスを実行するユニファイド メッセージング サーバーの役割が含まれていました。Exchange 2013 ではアーキテクチャが変更されたため、クライアント アクセス サーバーが Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行し、メールボックス サーバーが Microsoft Exchange ユニファイド メッセージング サービスを実行します。以前のバージョンの Exchange UM と同じ Microsoft Exchange ユニファイド メッセージング サービス用のパフォーマンス カウンターを管理者が利用できます。ただし、クライアント アクセス サーバー上で使用して Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの状態を確認したりトラブルシューティングのために使用できる追加のパフォーマンス カウンターもあります。

Exchange 2013 の新しいクライアント アクセス ユニファイド メッセージング呼び出しルーター サービスをサポートするために、次のパフォーマンス カウンターが使用可能になりました。

### パフォーマンス カウンター

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>パフォーマンス カウンターのカテゴリ</th>
<th>カウンター名</th>
<th>説明</th>
<th>しきい値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>過去 1 時間に Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって拒否された着信呼び出しの割合</p></td>
<td><p>過去 1 時間に Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって拒否された着信呼び出しの割合を示します。</p></td>
<td><p>常に 5% 未満である必要があります (ただし、必ず 0 でなければならない場合を除きます)。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスの回復不能な内部エラーで切断された呼び出し</p></td>
<td><p>内部システム エラーが発生した後で切断された呼び出しの数を示します。</p></td>
<td><p>常に 0 である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって拒否された着信呼び出しの合計数</p></td>
<td><p>サービスの開始以降に Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって拒否された着信呼び出しの合計数を示します。</p></td>
<td><p>常に 0 である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって受信された呼び出しの合計数</p></td>
<td><p>サービスの開始以降に Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって受信された着信呼び出しの合計数を示します。</p></td>
<td><p>0 以上である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>過去 1 時間に Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって拒否された着信呼び出しの割合</p></td>
<td><p>過去 1 時間に Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスによって拒否された着信呼び出しの割合を示します。</p></td>
<td><p>5% 未満である必要があります。</p></td>
</tr>
</tbody>
</table>


新しい Exchange アーキテクチャのサポート

