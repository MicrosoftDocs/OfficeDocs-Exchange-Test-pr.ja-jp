---
title: 'メールボックス サーバー: Exchange 2013 Help'
TOCTitle: メールボックス サーバー
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 48269227
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス サーバー

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-19_

Microsoft Exchange Server 2010 では、メールボックス サーバーの役割がメールボックス データベースとパブリック フォルダー データベースの両方をホストし、電子メール メッセージ記憶域も提供していました。今、Exchange Server 2013 では、メールボックス サーバーの役割には、クライアント アクセス プロトコル、トランスポート サービス、メールボックス データベース、ユニファイド メッセージング コンポーネントも含まれるようになりました。

Exchange 2013 では、メールボックス サーバーの役割は、以下のプロセスで、Active Directory、クライアント アクセス サーバー、Microsoft Outlook クライアントと直接対話します。

  - メールボックス サーバーは、LDAP を使用して、Active Directory から受信者、サーバー、組織の構成情報にアクセスします。

  - クライアント アクセス サーバーは、クライアントからメールボックス サーバーに要求を送信し、メールボックス サーバーからクライアントにデータを返します。また、クライアント アクセス サーバーは、NetBIOS ファイル共有で、メールボックス サーバーのオンライン アドレス帳 (OAB) ファイルにアクセスします。クライアント アクセス サーバーは、クライアントとメールボックス サーバー間で、メッセージ、空き時間情報、クライアント プロファイル設定、OAB データを送信します。

  - ファイアウォールの内側にある Outlook クライアントは、メッセージを送受信するためにクライアント アクセス サーバーにアクセスします。ファイアウォール外の Outlook クライアントは、(RPC over HTTP プロキシ コンポーネントを使用する) Outlook Anywhere でクライアント アクセス サーバーにアクセスできます。

  - パブリック フォルダー メールボックスは、クライアントがファイアウォールの内外のどちらにあっても、RPC over HTTP でアクセスできます。

  - 管理者用コンピューターは、Microsoft Exchange Active Directory トポロジ サービスから Active Directory トポロジ情報を取得します。また、メール アドレス ポリシー情報とアドレス一覧情報も取得します。

  - クライアント アクセス サーバーは、LDAP または Name Service Provider Interface (NSPI) を使用して Active Directory サーバーと通信し、ユーザーの Active Directory 情報を取得します。

**メールボックスとクライアント アクセス サーバーの対話とアーキテクチャ**

![クライアント アクセス サーバーとメールボックス サーバーのやり取り](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "クライアント アクセス サーバーとメールボックス サーバーのやり取り")

詳細については、「[Exchange 2013 の新機能](what-s-new-in-exchange-2013-exchange-2013-help.md)」の「Exchange 2013 アーキテクチャ」を参照してください。

## メールボックスの新機能

以下の一覧では、Exchange 2013 のメールボックス役割の一部の新機能と強化機能について説明します。

  - Exchange 2010 データベース可用性グループ (DAG) の進化:
    
      - トランザクション ログ コードは、パッシブ データベース コピーのチェックポイントの深度を大きくして、高速フェールオーバーのためにリファクタリングしました。
    
      - 強化されたサイトの復元をサポートするために、サーバーはさまざまな場所に配置できます。

  - Exchange 2013 は、一部のクライアント アクセスのコンポーネント、トランスポートのコンポーネント、およびユニファイド メッセージングのコンポーネントをホストするようになりました。

  - Exchange Store は、マネージコードの記述を変更して、I/O をさらに削減し、信頼性を高めてパフォーマンスを強化しました。

  - Exchange 2013 データベースは、それぞれ専用のプロセスで実行するようになりました。

  - Exchange 2010 の複数メールボックス検索インフラストラクチャは、スマート検索に置き換わりました。

## メールボックス サーバーのセキュリティ保護

既定では、メールボックス サーバーとその他の Exchange サーバーの役割、ドメイン コントローラー、およびグローバル カタログ サーバーとの間の HTTP、Microsoft Exchange ActiveSync、POP3、IMAP4 の通信は暗号化されます。また、メールボックス サーバーがインターネットにアクセスできないことを確認してください。

## 詳細情報

[ユニファイド メッセージング](unified-messaging-exchange-2013-help.md)

[メール フロー](mail-flow-exchange-2013-help.md)

[高可用性とサイトの復元](high-availability-and-site-resilience-exchange-2013-help.md)

[メッセージングのポリシーと準拠](messaging-policy-and-compliance-exchange-2013-help.md)

[Exchange 2013 でのメールボックスの移動](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 のメールボックス データベースの管理](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[メッセージングのポリシーと準拠](messaging-policy-and-compliance-exchange-2013-help.md)

[受信者](recipients-exchange-2013-help.md)

[グループ作業](collaboration-exchange-2013-help.md)

