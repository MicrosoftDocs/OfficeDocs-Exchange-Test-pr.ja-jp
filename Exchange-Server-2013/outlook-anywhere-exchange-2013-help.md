---
title: 'Outlook Anywhere: Exchange 2013 Help'
TOCTitle: Outlook Anywhere
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 48269791
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Anywhere

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Microsoft Exchange Server 2013 では、Outlook Anywhere 機能 (以前は RPC over HTTP と呼ばれていました) により、MicrosoftOutlook 2013、Outlook 2010、または Outlook 2007 を使用するクライアントが、企業ネットワークの外から、または RPC over HTTP Windows ネットワーク コンポーネントを使用してインターネット経由で、Exchange サーバーに接続できます。ここでは、Outlook Anywhere の機能について説明し、Outlook Anywhere を使用することによる利点を一覧表示します。

**目次**

Outlook Anywhere と Exchange 2013

Outlook Anywhere を使用することによる利点

Outlook Anywhere の展開

Outlook Anywhere の管理

Outlook Anywhere の共存

Outlook Anywhere 接続のテスト

## Outlook Anywhere と Exchange 2013

Windows RPC over HTTP Proxy コンポーネントは、Outlook Anywhere クライアントが接続に使用するコンポーネントであり、HTTP 層でリモート プロシージャ コール (RPC) をラップします。これにより、RPC ポートを開くことなく、トラフィックはネットワークのファイアウォールを通過することができます。Exchange 2013 では、Exchange 2013 が直接 RPC 接続を許可しないため、この機能は既定で有効になっています。

## Outlook Anywhere を使用することによる利点

Outlook Anywhere を使用すると、Outlook 2013、Outlook 2010、または Outlook 2007 を使用する Exchange メッセージング インフラストラクチャにアクセスするクライアントは、次の利点を得ることができます。

  - ユーザーは、インターネットから Exchange サーバーへのリモート アクセスが可能になります。

  - Outlook Web App および Microsoft Exchange ActiveSync に使用しているものと同じ URL および名前空間を使用できます。

  - Outlook Web App および Exchange ActiveSync に使用しているものと同じ SSL (Secure Sockets Layer) サーバー証明書を使用できます。

  - Outlook からの認証されていない要求は Exchange サーバーにアクセスできません。

  - インターネット経由で Exchange サーバーにアクセスするために、仮想プライベート ネットワーク (VPN) を使用する必要がありません。

  - Outlook Web App with SSL または Exchange ActiveSync with SSL を既に使用している場合は、インターネットから追加のポートを開く必要はありません。

  - **Test-OutlookConnectivity** コマンドレットを使用することで、Outlook Anywhere および TCP ベース接続のエンド ツー エンド クライアント接続をテストできます。

## Outlook Anywhere の展開

Exchange 2013 では、すべての Outlook 接続が Outlook Anywhere を介して行われるため、Outlook Anywhere は既定で有効になっています。Outlook Anywhere を成功裡に使用するために実行する必要がある展開後のタスクは、有効な SSL 証明書をクライアント アクセス サーバーにインストールすることだけです。組織内のメールボックス サーバーでは、既定の自己署名 SSL 証明書のみが必要です。

## Outlook Anywhere の管理

Exchange 管理センターまたは Exchange 管理シェルを使用して、Outlook Anywhere を管理できます。

## Outlook Anywhere の共存

Exchange Server の以前のバージョンと共存させるシナリオで Exchange 2013 のインストールを計画している場合、組織内にまだ Outlook 2003 クライアントが存在する可能性があります。Outlook 2003 は、Exchange 2013 でサポートされているクライアントではありません。

名前空間を Exchange 2013 に移動する前に、サポートされる最小バージョンにすべての Outlook クライアントをアップグレードする必要があります。移動先のメールボックスが Exchange 2007 または Exchange 2010 上にある場合も、Outlook Anywhere で Exchange 2013 に接続するには、Outlook 2007 以降が必要になります。

Exchange 2007 または 2010 環境で現在 Outlook Anywhere を使用している場合、Exchange 2013 クライアント アクセス サーバーが Exchange 2007/2010 サーバーへの接続をプロキシできるようにするには、組織内のすべての Exchange 2007/2010 CAS で Outlook Anywhere を有効にして構成しなければなりません。しかし、Exchange 2007/2010 環境で現在 Outlook Anywhere を使用しておらず、Outlook Anywhere を使用して開始しようとしていない場合は、従来型の環境で Outlook Anywhere を有効にする必要はありません。Exchange Server 2007 で実行するクライアント アクセス サーバーの Outlook Anywhere を有効にする方法については、「[Outlook Anywhere を有効にする方法](https://go.microsoft.com/fwlink/p/?linkid=510497)」を参照してください。Exchange Server 2010 で実行するクライアント アクセス サーバーの Outlook Anywhere を有効にする方法については、「[Outlook Anywhere を有効にする](https://go.microsoft.com/fwlink/p/?linkid=510502)」を参照してください。

Outlook Anywhere をクライアント アクセス サーバーで有効にするときには、IIS 認証に NTLM を選択してください。

最後に、Exchange 2013 Outlook Anywhere のホスト名を示すように Outlook Anywhere 外部ホスト名を構成します。Exchange Server 2007 での手順について詳しくは、「[Outlook Anywhere のために外部ホスト名を構成する方法](https://go.microsoft.com/fwlink/p/?linkid=510530)」を参照してください。Exchange Server 2010 での手順について詳しくは、「[Outlook Anywhere のために外部ホスト名を構成する](https://go.microsoft.com/fwlink/p/?linkid=510531)」を参照してください。

## Outlook Anywhere 接続のテスト

Outlook のエンド ツー エンド クライアント接続をテストするには、次のいずれかの操作を行います。

  - **Test-OutlookConnectivity** コマンドレットの実行。コマンドレットで、Outlook Anywhere (RPC over HTTP) 接続をテストします。コマンドレット テストが失敗した場合は、その失敗したステップを出力で確認できます。構文およびパラメーターの詳細については、「[Test-OutlookConnectivity](https://technet.microsoft.com/ja-jp/library/dd638082\(v=exchg.150\))」を参照してください。

  - Exchange リモート接続アナライザー (ExRCA) を使用した Outlook Anywhere 接続テストの実行。このテストを実行すると、テストが失敗した箇所と問題を修正するのに実行できる手順が記載された、詳細なサマリーが得られます。詳細については、「[Exchange リモート接続アナライザー](exchange-remote-connectivity-analyzer-exchange-2013-help.md)」を参照してください。

いずれのテストも、自動検出サービスからサーバー設定を取得した後、Outlook Anywhere 経由でサインインを試みます。エンド ツー エンドの検証としては、次が挙げられます。

  - 自動検出の接続のテスト

  - DNS の検証

  - 証明書の検証 (証明書の名前が Web サイトと一致するかどうか、証明書の有効期限が切れているかどうか、および信頼済みかどうか)

  - ファイアウォールが正しくセットアップされているかの確認 (ExRCA がファイアウォールの全体のセットアップを確認します。コマンドレットで Windows のファイアウォール構成をテストします)

  - ユーザーのメールボックスへのサインインによるクライアント接続の確認

