---
title: 'Exchange 2013 UM および Lync Server の展開の概要: Exchange 2013 Help'
TOCTitle: Exchange 2013 UM および Lync Server の展開の概要
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 49896381
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 UM および Lync Server の展開の概要

 

_**適用先:** Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2016-12-09_

ユニファイド メッセージング (UM) と Microsoft Lync Server を一緒に展開することによって、組織内のユーザーにボイス メッセージング、インスタント メッセージング、強化されたユーザーのプレゼンス、音声ビデオ会議、および電子メールとメッセージングが統合された環境を提供できます。ユニファイド メッセージングを使用して、通話応答、Outlook Voice Access、および自動応答サービスを提供します。Microsoft Lync Server により、インスタント メッセージング (IM)、会議、および着信と受信の呼び出しなど、エンタープライズ VoIP に見られる数多くの先進機能が利用可能になります。ここでは、これらの機能をサポートするためユニファイド メッセージングと Microsoft Lync Server を構成する方法について説明します。


> [!TIP]
> Microsoft Office Communications Server 2007 R2 をユニファイド メッセージングと一緒に展開することもできます。ここでは、"Microsoft Lync Server" は Microsoft Lync Server 2010 または Microsoft Lync Server 2013 のことを指します。



Microsoft Lync Server に関する詳細情報は、「[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)」を参照してください。

**目次**

Exchange UM と Lync Server の展開の概要

証明書構成に関する推奨事項

展開手順

詳細情報

## Exchange UM と Lync Server の展開の概要

ユニファイド メッセージングは、ボイス メッセージングと電子メール メッセージングを単一のメッセージング インフラストラクチャに統合します。Microsoft Lync Server のエンタープライズ VoIP は UM インフラストラクチャを駆使し、ボイス メール、Outlook Voice Access、呼び出し通知、および自動応答を提供します。

以下の表に UM と Lync Server の展開ステップの概要を示します。各ステップの詳細は、このトピックに含まれています。

1.  クライアント アクセス サーバーが Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行し、メールボックス サーバーが Microsoft Exchange ユニファイド メッセージング サービスを実行するのと同じトポロジに Microsoft Lync Server をインストールします。少なくとも 1 つの Lync プールが作成されることを確認します。

2.  有効でプライベートまたは公的な証明機関 (CA) により署名され、Lync Server により信頼される証明書をインストールします。

3.  クライアント アクセス サーバーとメールボックス サーバーをインストールします。インストールを確認します。

4.  Lync Server にインストールした証明書と同じ CA により署名された、有効な証明書をインストールします。

5.  セッション開始プロトコル (SIP) URI ダイヤル プランを作成して構成します。

6.  すべてのクライアント アクセス サーバーおよびメールボックス サーバーを SIP URI ダイヤル プランに追加します。ただし、複数の SIP URI ダイヤル プランが存在する場合、すべての SIP URI ダイヤル プランにすべてのクライアント アクセス サーバーとメールボックス サーバーを追加する必要があります。

7.  メールボックス サーバーの \<Exchange インストール フォルダー\>\\Exchange Server\\Script フォルダーにある ExchUcUtil.ps1 スクリプトを実行します。
    

    > [!IMPORTANT]
    > ExchUcUtil.ps1 スクリプトは、Lync の統合のための 1 つまたは複数の UM IP ゲートウェイを作成します。スクリプトで作成した 1 つのゲートウェイを除き、すべての UM IP ゲートウェイでの発信呼び出しを無効にする必要があります。これにはスクリプトを実行する前に作成した UM IP ゲートウェイでの発信呼び出しを無効にすることが含まれます。UM IP ゲートウェイでの発信呼び出しを無効にするには、「<A href="disable-outgoing-calls-on-https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateways">UM IP ゲートウェイで送信呼び出しを無効にする</A>」を参照してください。



8.  Lync Server の %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support フォルダーにある **OcsUmUtil.exe** を実行します。

9.  仲介サーバーとメディア ゲートウェイを展開します。

10. Lync Server にインストールした証明書と同じ CA により署名された、有効な証明書を仲介サーバーにインストールします。

11. ユーザーの UM とエンタープライズ VoIP を有効にします。

## 証明書構成に関する推奨事項

Exchange を実行するコンピューターと Lync Server を実行するコンピューターの両方に信頼された証明書が必要です。Lync Server とユニファイド メッセージングがある環境では、信頼できる証明書を展開する際に以下のガイドラインに従ってください。

  - Lync Server、クライアント アクセス サーバー、メールボックス サーバー、仲介サーバー、およびメディア ゲートウェイに、有効でプライベートまたは公的な CA により署名された証明書をインポートします。これは、信頼できる第三者の商用証明書、または公開鍵基盤 (PKI) による証明書である必要があります。

  - 各 Exchange サーバーに同一の第三者の商用証明書または PKI 証明書をインポートすると、作業を簡素化できます。また、この信頼できる証明書を Microsoft Lync Server と仲介サーバーを実行する各コンピューターにインストールします。これにより、証明書の展開を簡素化し、証明書の展開に関連する管理負担を軽減できます。ただし、サブジェクト代替名 (SAN) をサポートする信頼できる証明書を取得する必要があります。
    
    UM と一緒にトランスポート層セキュリティ (TLS) を展開する場合、クライアント アクセス サーバーとメールボックス サーバーの両方で使用される証明書で、証明書のサブジェクト名にローカル コンピューターの完全修飾ドメイン名 (FQDN) が含まれる必要があります。この問題を回避するには、公的証明書を使用して、すべてのクライアント アクセス サーバーとメールボックス サーバー、任意の VoIP ゲートウェイ、およびすべての Lync Server にインストールします。
    
    展開に VoIP ゲートウェイまたは IP PBX が含まれ、セキュリティで保護された SIP ダイヤル プランかセキュリティで保護されたダイヤル プランを使用する場合、クライアント アクセス サーバーとメールボックス サーバー、および VoIP ゲートウェイまたは IP PBX 間に信頼できる証明書が必要です。直接 SIP 接続を使用している場合にも、信頼できる証明書が必要です。セキュリティで保護された SIP ダイヤル プランかセキュリティで保護されたダイヤル プランを使用する場合、Lync Server および Exchange サーバーに VoIP ゲートウェイまたは IP PBX で使用するのと同じ信頼できる証明書を使用できます。

  - Exchange クライアント アクセス サーバーとメールボックス サーバーを、Microsoft Lync Server またはサードパーティの SIP ゲートウェイ、または構内交換機 (PBX) テレフォニー装置と接続する場合は、内部、公共、または第三者の証明機関によって署名された有効な証明書を使用して、セキュリティで保護されたセッションを確立する必要があります。証明書の SAN 一覧にすべてのクライアント アクセス サーバーとメールボックス サーバーの FQDN が含まれている場合は、すべてのクライアント アクセス サーバーとメールボックス サーバーで 1 つの証明書を使用できます。または、各クライアント アクセス サーバーとメールボックス サーバーに異なる証明書を生成できます。これには、そのサーバーの証明書のサブジェクトの共通名 (CN) または SAN 一覧にローカル コンピューターの FQDN を記述します。Exchange UM は、Microsoft Lync Server のワイルドカード証明書をサポートしません。
    
    Lync Server と Exchange が連携するには、非ワイルドカードのサブジェクト名が必要です。UM および Lync Server は、信頼できる SIP ピアであることを示すのにサブジェクト名を使用します。Lync Server では、一部の呼び出しルーティング シナリオでワイルドカード サブジェクト名も必要です。FQDN は、「発行先」の値として使用する必要があります。
    
    Exchange UM では、証明書名にワイルドカードを記述することはサポートされません。ただし、SAN にはワイルドカードを記述できます。

以下の表は、Exchange UM の証明書をインストールして構成するための証明書の要件を示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>トポロジ</th>
<th>証明書の構成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>同じサーバー上のクライアント アクセスおよびメールボックス (Lync Server 2010 または 2013 はなし。SIP 以外のダイヤル プラン)</p></td>
<td><p>クライアント アクセス サーバーおよびメールボックス サーバー間に証明書が必要です。これは、クライアント アクセス サーバーとメールボックス サーバー、および VoIP ゲートウェイ、IP PBX、SBC 間で使用するのと同じ証明書です。</p></td>
</tr>
<tr class="even">
<td><p>異なるサーバー上のクライアント アクセスおよびメールボックス (Lync Server 2010 または 2013 はなし。SIP 以外のダイヤル プラン)</p></td>
<td><p>証明書が必要です。証明書は、クライアント アクセス サーバーおよびメールボックス サーバーで一致する必要があります。クライアント アクセス サーバーとメールボックス サーバー、および VoIP ゲートウェイ、IP PBX、SBC 間でも証明書が必要です。これは、クライアント アクセス サーバーとメールボックス サーバー間で使用される証明書と同じでも異なってもかまいません。クライアント アクセス サーバーとメールボックス サーバーでは、いずれかのサーバーからでも <strong>Create-ExchangeCertificate</strong> コマンドレットを実行できます。</p></td>
</tr>
<tr class="odd">
<td><p>同じサーバー上のクライアント アクセスおよびメールボックス (Lync Server 2010 または 2013 あり。SIP ダイヤル プラン)</p></td>
<td><p>証明書が必要です。クライアント アクセスとメールボックス サーバーには、Lync 2010 または 2013 サーバーと同じルート証明書が必要です。</p></td>
</tr>
<tr class="even">
<td><p>異なるサーバー上のクライアント アクセスおよびメールボックス (Lync Server 2010 または 2013 あり。SIP ダイヤル プラン)</p></td>
<td><p>証明書が必要です。クライアント アクセスとメールボックス サーバーには、Lync 2010 または 2013 サーバーと同じルート証明書が必要です。</p></td>
</tr>
</tbody>
</table>


ページのトップへ

## 展開手順

組織に必要なサーバーをインストールした後に実行する、Exchange ユニファイド メッセージング サーバーと Lync Server 展開で実行する必要がある一連の推奨手順があります。これにより、ユーザー向けにエンタープライズ VoIP が正しく展開されます。

Microsoft Lync Server の詳細については、「[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)」を参照してください。

以下のステップを実行して、Lync Server のエンタープライズ VoIP 機能と連携するようにユニファイド メッセージングを構成します:

1.  それぞれが対応する Lync Server の場所プロファイルにマップする、1 つまたは複数のユニファイド メッセージング SIP URI ダイヤル プランを作成します。エンタープライズ VoIP の場所のプロファイルは、Exchange UM ダイヤル プランごとに作成する必要があります。**Get-UMDialPlan** コマンドレットを使用して、SIP URI ダイヤル プランの FQDN を取得できます。SIP URI ダイヤル プランを作成する方法の詳細については、「[UM ダイヤル プランを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)」を参照してください。
    

    > [!IMPORTANT]
    > Exchange UM と Lync Server を統合していると、多くの場合 Exchange UM でダイヤル情報やダイヤル情報グループを構成する必要がありません。Lync Server は、組織内のユーザー向けに呼び出しのルーティングと番号の変換を実行するよう設計されており、ユニファイド メッセージングがユーザーの代理で呼び出しを行った場合も同じように実行します。



2.  有効で、プライベートまたは公的な CA により署名された証明書をクライアント アクセス サーバーとメールボックス サーバーにインストールします。これは、Lync Server で使用したのと同じ CA です。

3.  ボイス オーバー IP (VoIP) トラフィックを暗号化するには、SIP URI ダイヤル プランを \[セキュリティで保護された SIP\] または \[セキュリティで保護\] として構成します。
    

    > [!NOTE]
    > SIP トラフィックにのみ暗号化を必要とするためにセキュリティ設定を [セキュリティで保護された SIP] に設定する場合、暗号化を必要とするようにフロント エンド プールが構成されている (つまり、プールが SIP および RTP トラフィックの両方に暗号化を必要とする) のであれば、この設定はダイヤル プランには不十分です。ダイヤル プランとプールのセキュリティ設定が互換ではない場合、フロント エンド プールから Exchange UM へのすべての呼び出しが失敗し、「セキュリティ設定に互換性がありません」というエラーが表示されます。

    
    UM ダイヤル プランは \[セキュリティで保護された SIP\] または \[セキュリティで保護\] として構成できますが、\[セキュリティで保護\] として構成して、Lync Phone Edition デバイスが正しく機能できるようにすることをお勧めします。Lync Server で構成された既定の暗号化レベル設定のため、この設定を推奨します。Lync Phone Edition デバイスは、次の表のように暗号化設定が構成されている場合のみ機能します。この表に、Lync Server と UM ダイヤル プランの両方に対する暗号化設定の関係を示します。
    
    **Lync Phone Edition の暗号化設定**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Lync Server</th>
    <th>UM ダイヤル プラン</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>暗号化が必要 (既定)</p></td>
    <td><p>セキュリティで保護</p></td>
    </tr>
    <tr class="even">
    <td><p>暗号化は任意</p></td>
    <td><p>セキュリティで保護された SIP/セキュリティで保護</p></td>
    </tr>
    <tr class="odd">
    <td><p>暗号化なし</p></td>
    <td><p>セキュリティで保護された SIP</p></td>
    </tr>
    </tbody>
    </table>


4.  すべてのクライアント アクセス サーバーおよびメールボックス サーバーを SIP ダイヤル プランに追加します。サーバーを受信呼び出しに応答できるようにし、Lync Server からの呼び出しに応答するには、すべての Exchange サーバーをダイヤル プランに追加する必要があります。

5.  SIP URI ダイヤル プランに追加するクライアント アクセス サーバーとメールボックス サーバーのスタートアップ モードと TLS ポートを \[デュアル\] に設定し、各メールボックス サーバー上の MicrosoftExchange ユニファイド メッセージング サービスと、各クライアント アクセス サーバー上の MicrosoftExchange ユニファイド メッセージング呼び出しルーター サービスを再起動します。

6.  UM 自動応答を作成して構成します。詳細については、「[UM 自動応答の設定](set-up-a-um-auto-attendant-exchange-2013-help.md)」を参照してください。

7.  ユーザーのボイス メールを有効にするには、エンタープライズ VoIP を使用するユーザーの SIP アドレスを作成します。通常この SIP アドレスは、ユーザーのエンタープライズ VoIP を有効にするときに使用するのと同じ SIP アドレスです。詳細については、「[ボイス メール用にユーザーを有効にする](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)」を参照してください。
    

    > [!IMPORTANT]
    > SIP URI ダイヤル プランに関連付けられたユーザーは、着信 FAX を受信できません。これは、着信の音声呼び出しおよび FAX 呼び出しが仲介サーバーによってルーティングされていて、仲介サーバーの使用中は FAX 機能がサポートされないためです。



8.  Exchange 管理シェルを開き、%Program Files%\\Microsoft\\Exchange Server\\V15\\Scripts フォルダーにある exchucutil.ps1 スクリプトを実行します。exchucutil.ps1 スクリプトは次の処理を行います。
    
      - Lync Server に対し、Exchange UM Active Directory コンポーネント、特に前のタスクで作成された SIP URI ダイヤル プランを読み取るためのアクセス許可を与えます。Active Directory でアクセス許可を構成する方法の詳細については、「[ADSI Edit を使用してアクセス許可を適用する方法についてのページ](https://go.microsoft.com/fwlink/p/?linkid=82751)」を参照してください (このサイトは英語の場合があります)。
    
      - 各 Lync Server プール、またはエンタープライズ VoIP が有効なユーザーをホストする Lync Server Standard Edition を実行している各サーバーに UM IP ゲートウェイを作成します。詳細については、「[UM IP ゲートウェイを作成する](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)」を参照してください。
    
      - 各 IP ゲートウェイの Exchange UM ハント グループを作成します。ハント グループのパイロット ID は、対応する UM IP ゲートウェイに関連付けられたダイヤル プランの名前です。ハント グループは、UM IP ゲートウェイに使用される UM SIP ダイヤル プランを指定する必要があります。

9.  ユーザーのボイス メールを有効にします。ユーザーのボイス メールを有効にするには、ユーザーに有効な SIP アドレスを入力し、SIP ダイヤル プランにリンクします。詳細については、「[ボイス メール用にユーザーを有効にする](https://docs.microsoft.com/ja-jp/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)」を参照してください。

また、Lync Server を Exchange UM と協調して動作するように構成するには、次の作業を完了する必要があります。

  - 場所のプロファイルまたは Lync のダイヤル プランを作成します。場所のプロファイル名は、対応する UM ダイヤル プランの FQDN と一致する必要はありません。

  - 場所のプロファイルを Lync Server プールを割り当てます。

  - メディア ゲートウェイまたは仲介サーバーを展開および構成します。クライアント アクセス サーバー、メールボックス サーバー、および Lync Server 上の証明書と同じ信頼できる CA から発行された証明書をインポートする必要もあります。

  - 電話の使用法を定義し、音声ポリシーおよび発信呼び出しのルートを作成して割り当てます。

  - エンタープライズ VoIP を使用できるようにユーザーを構成し、TEL URI および SIP ID を追加します。

  - **ocsumutil.exe** コマンドを実行します。このコマンドは、Outlook Voice Access 用および自動応答用の連絡先オブジェクトを作成します。
    

    > [!NOTE]
    > Lync Server をインストールすると、Active Directory に <STRONG>msRTC-SIPLine</STRONG> 属性が追加されます。環境に Lync Server をインストールしていない場合は、Active Directory&nbsp;にこの属性が追加されていないため、UM が有効でないユーザーに対してユニファイド メッセージング プロキシ アドレスを構成しない限り、単一フォレストおよびフォレスト間のシナリオでダイヤル プラン全体にわたる呼び出し ID の名前解決が正しく機能しません。



Lync Server およびユニファイド メッセージング サーバーを構成した後、ユーザーが Lync Server を使用できるようにし、ユーザーのクライアント コンピューターに Lync をインストールできるようにする必要があります。


> [!IMPORTANT]
> ユニファイド メッセージングと Lync Server を統合した場合、Exchange 2007 または Exchange 2010 メールボックス サーバーに配置されたメールボックスを持つユーザーは、不在着信通知を使用できません。不在着信通知は、通話がメールボックス サーバーに送信される前に切断された場合に生成されます。



ページのトップへ

## 詳細情報

Microsoft Lync Server 用に実行が必要なタスクの実行方法の詳細については、「[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)」を参照してください。

