﻿---
title: 'クライアント アクセス サーバー: Exchange 2013 Help'
TOCTitle: クライアント アクセス サーバー
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 48269746
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセス サーバー

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2014-07-02_

Microsoft Exchange 2013 では、Exchange サーバーの役割に関してアーキテクチャが大幅に変更されました。Exchange 2010 と Exchange 2007 では、5 つのサーバーの役割が存在していましたが、Exchange 2013 では、サーバーの役割がクライアント アクセス サーバーの役割、メールボックス サーバーの役割、およびサービス パック 1 の場合はエッジ トランスポート サーバーの役割の 3 つに削減されました。


> [!NOTE]
> Exchange 2013 は、Exchange 2010 エッジ トランスポート サーバーの役割で動作することも可能です。



Exchange 2013 メールボックス サーバーには、Exchange 2010 に存在する、次のすべてのサーバー コンポーネントが含まれます。クライアント アクセス プロトコル、トランスポート サービス、メールボックス データベース、およびユニファイド メッセージング サービス (クライアント アクセス サーバーは、着信呼び出しから生成された SIP トラフィックをメールボックス サーバーにリダイレクトします)。Exchange 2013 メールボックス サーバーの詳細については、「[メールボックス サーバー](mailbox-server-exchange-2013-help.md)」を参照してください。

クライアント アクセス サーバーは、認証、プロキシ、および制限付きリダイレクト サービスを提供し、次のような通常のクライアント アクセス プロトコルをすべて提供します。HTTP、POP、IMAP、SMTP。クライアント アクセス サーバーは最小限の機能を備えたステートレス サーバーで、データのレンダリングを実行しません。クライアント アクセス サーバーにはキューまたは格納されるものは何もありません。Exchange 2013 の新しいアーキテクチャの詳細については、「[Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md)」を参照してください。


> [!WARNING]
> クライアント アクセス サーバーは境界ネットワークではサポートされておらず、内部 Active&nbsp;Directory 環境内に展開する必要があります。メールボックス サーバーを含むすべての Active Directory サイトは、クライアント アクセス サーバーも含んでいる必要があります。



こうしたアーキテクチャ変更の結果、クライアントの接続にいくつかの変更点があります。まず、RPC/TCP はサポートされている直接アクセス プロトコルではなくなりました。つまり、すべての Outlook 接続は、RPC over HTTPS (Outlook Anywhere とも呼ばれる)、または Exchange 2013 SP1 および Outlook 2013 SP1 では MAPI over HTTP を使用して行う必要があります。これらの変更の結果、クライアント アクセス サーバーに RPC クライアント アクセス サービスを配置する必要はなくなりました。さらに、Exchange 2010 でサイト復元ソリューションに必要であったいくつかの名前空間が削減され、RPC クライアント アクセス サービスに類似性を用意する要件もなくなりました。また、Outlook クライアントは、以前のすべてのバージョンの Exchange で行っていたような、サーバーの完全修飾ドメイン名 (FQDN) への接続は行いません。Outlook は、自動検出を使用して、新しい接続ポイント (ユーザーのメールボックス GUID + @ + ユーザーのプライマリ SMTP アドレスのドメイン部分で構成される) を検索します。この変更により、「管理者がメールボックスを変更しました。再起動してください。」という好ましくないメッセージはほぼ表示されなくなります。Exchange 2013 では、Outlook 2007 以降のバージョンのみがサポートされます。

## クライアント アクセス サーバーの機能

Exchange 2013 のクライアント アクセス サーバーは、すべてのクライアント要求を受け入れ、正しいアクティブなメールボックス データベースにルーティングし、まさにフロント ドアのように機能します。クライアント アクセス サーバーは、Secure Sockets Layer (SSL) やクライアント認証などのネットワーク セキュリティ機能を提供し、リダイレクトとプロキシ機能を通じてクライアント接続を管理します。クライアント アクセス サーバーは、クライアント接続を認証し、ほとんどの場合、ユーザーのメールボックスを含むデータベースのアクティブなコピーが格納されているメールボックス サーバーに要求を転送します。クライアント アクセス サーバーは、別の場所にあるか、より新しいバージョンの Exchange Server を実行しているより適切なクライアント アクセス サーバーに要求をリダイレクトすることもあります。

クライアント アクセス サーバーには、次の機能があります。

  - **ステートレス サーバー** 以前のバージョンの Exchange では、多くのクライアント アクセス プロトコルでセッション類似性が必要でした。たとえば、Outlook Web App では、特定のクライアントからのすべての要求を、クライアント アクセス サーバーの負荷分散アレイ内で特定のクライアント アクセス サーバーが処理する必要がありました。Exchange 2013 では、クライアント アクセス サーバーはステートレスです。つまり、メールボックスのすべての処理はメールボックス サーバーで行われるため、クライアント アクセス サーバーのアレイ内のどのクライアント アクセス サーバーが個々のクライアント要求を受信しようと問題ではありません。この機能の変更は、セッション類似性が負荷分散装置レベルでは必要ないことを意味します。これにより、クライアント アクセス サーバーへの受信接続を、DNS ラウンド ロビンなどの負荷分散テクノロジで提供される単純な手法を使用してバランスさせることができます。また、ハードウェア負荷分散デバイスではるかに多くの同時接続をサポートすることもできます。

  - **接続プール** クライアント アクセス サーバーはクライアント認証を処理し、AuthN データをメールボックス サーバーに送信します。クライアント アクセス サーバーによってメールボックス サーバーに接続するために使用されるアカウントは、Exchange Servers グループのメンバーである特権アカウントです。これにより、クライアント アクセス サーバーは接続をメールボックス サーバーに効率的にプールすることができます。クライアント アクセス サーバーのアレイは、インターネットからの何百万ものクライアント接続を処理できますが、要求をメールボックス サーバーに転送する際、以前のリリースの Exchange に比べてはるかに少ない接続しか使用しません。これにより、処理の効率性とエンド ツー エンドの待機時間が改善されます。

## クライアント アクセス サーバー上の管理タスク

Exchange 2013 では、クライアント アクセス サーバー上で実行できるいくつかの主要なタスクがあります。デジタル証明書の管理は、主にクライアント アクセス サーバーで実行され、Exchange ActiveSync、POP3、および IMAP4 のクライアント プロトコル管理の一部もクライアント アクセス サーバー上で処理されます。
