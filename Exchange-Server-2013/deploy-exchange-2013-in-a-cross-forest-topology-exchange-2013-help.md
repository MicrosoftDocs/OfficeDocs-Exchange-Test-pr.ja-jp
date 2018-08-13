---
title: 'フォレスト間のトポロジで Exchange 2013 を展開する: Exchange 2013 Help'
TOCTitle: フォレスト間のトポロジで Exchange 2013 を展開する
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51407539
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フォレスト間のトポロジで Exchange 2013 を展開する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

ここでは、Microsoft Forefront Identity Manager 2010 R2 SP1 を使用してフォレスト間トポロジに Exchange 2013 を展開する方法を説明します。フォレスト間のトポロジで Exchange 2013 を展開するには、ユーザーがフォレスト間でアドレスや使用可能なデータを確認できるように、最初に各フォレストに Exchange 2013 をインストールしてから、フォレストを接続する必要があります。

次の図に、2 つの Exchange 2013 フォレスト間のユーザー同期を示します。

**Exchange 2013 のフォレスト間同期の例**

![Exchange 2010 の複数のフォレストの例](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Exchange 2010 の複数のフォレストの例")

ここでは、専用の Exchange フォレスト (またはリソース フォレスト) トポロジ内に Exchange 2013 を展開する方法は説明*しません*。Exchange 2013 をリソース フォレストのトポロジで展開する方法の詳細については、「[Exchange リソース フォレストのトポロジに Exchange 2013 を展開する](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

Exchange 2013 で次の手順を実行するには、以下の点を確認してください。

  - 組織内の複数のフォレストにわたって名前解決のためのドメイン ネーム システム (DNS) が正しく構成されている。DNS が正しく構成されていることを確認するには、Ping ツールを使用して、組織内の他のフォレストと GALSync エージェントを実行するサーバーから各フォレストへの接続をテストします。

  - GALSync 管理エージェント (MA) は Exchange 2013 PowerShell V2.0 RTM を使用して Windows フォレストと通信します。\[コントロール パネル\] から \[プログラムと機能\] をクリックして、このコンピューターに Windows PowerShell v1.0 がインストールされていないことを確認します。

  - Windows リモート管理が、Windows Update によってインストールされていないことを確認します。

  - Windows PowerShell と Windows リモート管理をインストールします。詳細については、Microsoft サポート技術情報の文書番号 968930「[Windows 管理フレームワークのコア パッケージ (Windows PowerShell 2.0 および WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)」を参照してください。

  - Forefront Identity Manager 2010 R2 SP1 をダウンロードします。「[Microsoft Forefront Identity Manager 2010 R2 SP1 のダウンロード](https://go.microsoft.com/fwlink/p/?linkid=279868)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Forefront Identity Manager 2010 R2 SP1 を使用してフォレスト間トポロジに Exchange 2013 を展開する

1.  各フォレストに、Exchange 2013 を個別にインストールします。Exchange 2013 をインストールするには、単一フォレストのトポロジで Exchange 2013 をインストールする場合と同じ手順を実行します。詳細については、以下のいずれかのトピックを参照してください。
    
      - [Exchange 2013 の新規インストールの展開](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        

        > [!NOTE]
        > ここでは、既存の Exchange&nbsp;2007 トポロジまたは Exchange 2010 トポロジが存在しないことを前提としています。既存の Exchange トポロジが存在し、アップグレードを行う場合は、「<A href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Exchange 2010 から Exchange 2013 へのアップグレード</A>」または「<A href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Exchange 2007 から Exchange 2013 へのアップグレード</A>」を参照してください。



2.  各フォレストの Active Directory ユーザーとコンピューターで、FIM 2010 R2 SP1 が他のフォレストのメールボックスごとに連絡先を作成するコンテナーを作成します。このコンテナーを **"FromFIM"** という名前にすることをお勧めします。コンテナーを作成するには、コンテナーを作成するドメインを選択し、そのドメインを右クリックして **\[新規作成\]** \> **\[組織単位\]** の順に選択します。**\[新しいオブジェクト - 組織単位\]** に「**FromFIM**」と入力し、**\[OK\]** をクリックします。

3.  Forefront Identify Manager を使用して、各フォレストに GALSync 管理エージェントを作成します。これにより、各フォレストのユーザー名を同期したり、共通の GAL を作成したりすることができるようになります。詳細な手順については、以下のリソースを参照してください。
    
      - [Forefront Identity Manager (FIM) 2010 を使用したグローバル アドレス一覧 (GAL) 同期の構成](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [管理エージェントを操作する](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [Forefront Identity Manager 2010 R2 のドキュメント ロードマップ](https://go.microsoft.com/fwlink/p/?linkid=279871)
    

    > [!IMPORTANT]
    > これらのリソースは Exchange 2010 について説明していますが、FIM 2010 R2 SP1 は Exchange 2013 もサポートしています。FIM 2010 R2 SP1 で Exchange 2013 用の <STRONG>[拡張機能]</STRONG> を構成していることを確認してください。

    
    1.  **\[拡張機能の構成\]** ページで、**\[パーティション表示名の構成\]** の **\[以下のプロビジョニング\]** の横にある **\[Exchange 2013\]** を選択します。**\[Exchange 2013 RPS URI\]** フィールドが表示されます。Exchange 2013 クライアント アクセス サーバーの URI を入力し、リモート PowerShell 接続が機能していることを確認します。**\[Exchange 2013 RPS URI\]** は次の形式にする必要があります:http://CAS\_Server\_FQDN/Powershell。**\[OK\]** をクリックします。
        

        > [!NOTE]
        > Exchange 2013 フォレストへの接続に使用する管理者の資格情報が、フォレストへのリモート PowerShell 接続にも使用できることを確認します。<BR>次の図では、Exchange 2013 のプロビジョニングの選択方法を示します。

        
        **Provision GalSync Management Agent for Exchange 2013**
        
        ![管理エージェントの Exchange 2010 プロビジョニング](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "管理エージェントの Exchange 2010 プロビジョニング")  

4.  各フォレストに SMTP 送信コネクタを作成します。詳細な手順については、「[フォレスト間の送信コネクタを構成する](configure-a-cross-forest-send-connector-exchange-2013-help.md)」を参照してください。

5.  各フォレストで可用性サービスを有効にして、フォレスト内のユーザーが別のフォレストのユーザーに関する空き時間情報データを参照できるようにします。詳細については、「[Exchange 2013 の可用性サービス](availability-service-in-exchange-2013-exchange-2013-help.md)」を参照してください。

6.  組織の任意のフォレストを介してメールを中継する場合は、そのフォレスト内のドメインを権限のあるドメインとして構成する必要があります。詳細な手順については、「[複数の権限のあるドメインのメールを受け付けるように Exchange を構成する](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)」を参照してください。

