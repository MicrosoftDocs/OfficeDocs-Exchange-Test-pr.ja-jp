---
title: 'ハイブリッド構成ウィザードを使用してハイブリッド展開を作成する: Exchange 2013 Help'
TOCTitle: ハイブリッド構成ウィザードを使用してハイブリッド展開を作成する
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 48267605
ms.date: 03/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ハイブリッド構成ウィザードを使用してハイブリッド展開を作成する

このトピックは処理中です。  

_<strong>適用先:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>トピックの最終更新日:</strong>2016-12-09_

ハイブリッド展開を確立すると、既存の社内 Exchange Server 組織で実現されている多機能性と管理制御能力をクラウドにまで拡大できます。また、ハイブリッド展開は、社内メールボックスのクラウドベース アーカイブ ソリューションを Exchange Online Archiving でサポートし、社内メールボックスから Exchange Online への完全な移行の中間ステップにもなります。

このトピックでは、ハイブリッド構成ウィザードを使用して、企業のオンプレミスの Exchange 組織と Office 365 内の Exchange Online 組織向けのハイブリッド展開を構成します。このトピックでは、次の組織構成でハイブリッド展開を作成します。

  - オンプレミス組織は単一フォレストのオンプレミスの Exchange 組織です。

  - 社内組織は、社内を保護するために既存の Microsoft Exchange Online Protection (EOP) サービスを使用しません。

  - 社内組織にはエッジ トランスポート サーバーは導入されていません。ハイブリッド構成ウィザードは、ハイブリッド展開の一部としてエッジ トランスポート サーバーの構成をサポートしていますが、ウィザードでのエッジ トランスポート サーバーの構成はこのトピックの対象外です。


> [!IMPORTANT]
> ハイブリッド構成ウィザードでハイブリッド展開を構成するには、ウィザードが正常に完了し、ハイブリッド展開が正常に機能するように、いくつかの重要な前提条件を満たす必要があります。ハイブリッド構成ウィザードでハイブリッド展開を作成し構成する前に、「<A href="hybrid-deployment-prerequisites-exchange-2013-help.md">ハイブリッド展開の前提条件</A>」に記載された前提条件をすべて満たす必要があります。<BR>さらに、<A href="http://technet.microsoft.com/exdeploy2013">Exchange Server 展開アシスタント</A>は、無料の Web ベース ツールで、社内組織と Office 365 間のハイブリッド展開の構成、または Office 365 への完全移行を支援します。このツールによる簡単な一連の質問に回答すると、その答えに基づき、ハイブリッド展開を構成する指示が記された専用のチェックリストが作成されます。展開アシスタントを使用して、組織独自の必要に合った専用のハイブリッド展開チェックリストを生成することを強くお勧めします。



ハイブリッド展開に関連する追加の管理タスクについては、「[ハイブリッド展開の手順](hybrid-deployment-procedures-exchange-2013-help.md)」をご覧ください。

ハイブリッド展開の詳細については、「[Exchange Server のハイブリッド展開](exchange-server-hybrid-deployments-exchange-2013-help.md)」を参照してください。Office 365 の詳細については、「[Office 365 とは](http://go.microsoft.com/fwlink/?linkid=266712)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 30 分
    

    > [!IMPORTANT]
    > ハイブリッド展開の要件の構成には、このトピックで概説したハイブリッド構成ウィザードを完了するまでの推定時間よりかなり長い時間がかかることがあります。たとえば、Office 365 for enterprises のサインアップ、Active Directory 同期の構成、および Exchange Online ライセンスの割り当てには、長い時間を費やす必要があり、ネットワーク トポロジの変更が含まれる場合もあります。エンドツーエンドのハイブリッド展開の構成を完了するまでの全体的な時間については、この手順の完了に必要とされる時間より多めに計画する必要があります。



  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](https://technet.microsoft.com/ja-jp/library/dd638114\(v=exchg.150\))」の「ハイブリッド構成」。

  - ハイブリッド構成ウィザードは、Exchange のサポートされているバージョンの最新リリースを実行しているコンピューターから実行する必要があります。ハイブリッド構成ウィザードで Exchange OAuth 認証を構成する最後のステップは、オンプレミスの Exchange から、またはドメインに参加しているサーバーまたはワークステーションのいずれかから実行する必要があります。また、OAuth 認証プロセスにはデスクトップ バージョンの Internet Explorer 11 以上を使用するのが最適です。

  - 「[Exchange Server のハイブリッド展開](exchange-server-hybrid-deployments-exchange-2013-help.md)」を参照し、ハイブリッド展開の構成によって影響を受ける領域を必ず確認しておいてください。

  - 「[ハイブリッド展開の前提条件](hybrid-deployment-prerequisites-exchange-2013-help.md)」に示されたすべてのハイブリッド展開要件を確認し、満たしておく必要があります。

  - Microsoft リモート接続アナライザー ツールは、社内の Exchange 組織の外部接続をチェックし、ハイブリッド展開を構成する準備が整っているか確認します。ハイブリッド構成ウィザードを使用してハイブリッド展開を構成する前に、リモート接続アナライザー ツールを使用して社内組織をチェックすることを強くお勧めします。詳細については、「[リモート接続アナライザー ツール](http://go.microsoft.com/fwlink/p/?linkid=167905)」を参照してください。

  - Azure Active Directory Connect パスワード同期を使用することにより、シングル サインオンを構成することを強くお勧めします。シングル サインオンによりユーザーは、1 つのユーザー名とパスワードで、オンプレミスと Exchange Online の両方の組織にアクセスすることができます。シングル サインオンは、Exchange Online Archiving を使用している場合に、ユーザーが Exchange Online 組織内のアーカイブされたコンテンツにアクセスする際の資格情報の入力を回避します。パスワード同期について詳しくは、「[Azure AD Connect Sync:パスワード同期の実装](http://go.microsoft.com/fwlink/p/?linkid=723513)」をご覧ください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](https://technet.microsoft.com/ja-jp/library/jj150484\(v=exchg.150\))」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## Exchange 管理センターとハイブリッド構成ウィザードを使用してハイブリッド展開を作成する

ハイブリッド展開を作成および構成するには、次の手順に従います。

1.  オンプレミス組織の Exchange サーバー上の EAC で、<strong>ハイブリッド</strong> ノードに移動します。

2.  <strong>ハイブリッド</strong> ノードで <strong>構成</strong> をクリックし Office 365 資格情報を入力します。
    

    > [!IMPORTANT]
    > 社内組織が中国にあり、Office 365 テナントが 21Vianet でホストされている場合は、<STRONG>[Office 365 組織は 21Vianet でホストされています]</STRONG> チェックボックスを選択する必要があります。Office 365 テナントが 21Vianet でホストされているのに、このチェックボックスを選択しない場合、ハイブリッド構成ウィザードは 21Vianet サービスに接続せず、Office 365 アカウント資格情報が認識されないため、ウィザードが正常に完了しません。



3.  Office 365 にログインするプロンプトで、<strong>Office 365 にサインイン</strong> を選択して、アカウント資格情報を入力します。ログインするアカウントは、Office 365 のグローバル管理者であることが必要です。

4.  もう一度 <strong>構成</strong> をクリックして、ハイブリッド構成ウィザードを起動します。

5.  <strong>Microsoft Office 365 ハイブリッド構成ウィザードのダウンロード</strong> ページで、<strong>ここをクリック</strong> をクリックしてウィザードをダウンロードします。プロンプトが表示されたら、<strong>アプリケーションのインストール</strong> ダイアログの <strong>インストール</strong> をクリックします。

6.  <strong>次へ</strong> をクリックし、<strong>オンプレミスの Exchange Server 組織</strong> セクションで <strong>Exchange 2013 CAS または Exchange 2016 の実行されているサーバーを検出</strong> を選択します。ウィザードにより、オンプレミスの Exchange サーバーの検出が試みられます。ウィザードにより Exchange サーバーが検出されない場合、または別のサーバーを使用する場合は、<strong>Exchange 2013 CAS または Exchange 2016 が実行されているサーバーを指定する</strong> を選択し、Exchange メールボックス サーバーの内部 FQDN を指定します。

7.  <strong>Office 365 Exchange Online</strong> セクションで、<strong>Microsoft Office 365</strong> を選択し、<strong>次へ</strong> をクリックします。

8.  <strong>資格情報</strong> ページの <strong>オンプレミスのアカウント資格情報の入力</strong> セクションで <strong>現在の Windows 資格情報を使用する</strong> を選択し、ウィザードが現在のログイン アカウントを使用してオンプレミスの Active Directory および Exchange サーバーへアクセスするようにします。別の資格情報セットを指定する場合は、<strong>現在の Windows 資格情報を使用する</strong> の選択を解除し、使用する Active Directory アカウントのユーザー名とパスワードを指定します。どちらを選択する場合も、使用するアカウントは、Enterprise Admins セキュリティ グループのメンバーであることが必要です。

9.  <strong>Office 365 資格情報の入力</strong> セクションで、グローバル管理者のアクセス許可を付与された Office 365 アカウントのユーザー名とパスワードを指定します。<strong>次へ</strong> をクリックします。

10. <strong>接続と資格情報の検証</strong> ページで、ウィザードは、オンプレミス組織と Office 365 組織の両方に接続して資格情報を検証し、両方の組織の現在の構成を調べます。終了したら、<strong>次へ</strong> をクリックします。

11. <strong>ハイブリッド ドメイン</strong> で、ハイブリッド展開に含めるドメインを選択します。ほとんどの展開では、各ドメインの <strong>自動検出</strong> 列を <strong>False</strong> のままにすることができます。特定のドメインからの自動検出情報をウィザードで使用させることが必要な場合にのみ、そのドメインの横の <strong>True</strong> を選択します。<strong>次へ</strong> をクリックします。
    

    > [!IMPORTANT]
    > ハイブリッド構成ウィザードの実行時に、このウィザードのドメイン選択手順は表示されない場合があります。<BR>次のような場合、このステップは表示されません。 
    > <UL>
    > <LI>
    > <P>社内の承認済みドメインを 1 つだけ Office 365 テナントに追加した場合。ハイブリッド展開構成に使用できるドメインはこれだけなので、ドメインは自動的に選択され、ウィザードのこの手順はスキップされます。</P>
    > <LI>
    > <P>社内の承認済みドメインが Office&nbsp;365 テナントに追加されていない場合。この場合はエラーが発生し、最低 1 つのドメインを Office&nbsp;365 テナントに追加してから続行する必要があります。これを実行するには、Office&nbsp;365 の管理ポータルを使用するか、Active Directory フェデレーション サービス (AD&nbsp;FS) を社内組織で任意に構成します。</P></LI></UL>この手順は、複数の社内の承認済みドメインが Office&nbsp;365 テナントに追加されている場合に表示されます。



12. <strong>フェデレーション信頼</strong> ページで、<strong>有効にする</strong> をクリックした後、<strong>次へ</strong> をクリックします。

13. <strong>ドメイン所有者</strong> ページで <strong>クリックしてクリップボードにコピー</strong> をクリックして、ハイブリッド展開に含めるために選択したドメインのドメイン証明トークン情報をコピーします。メモ帳などのテキスト エディターを開き、これらのドメインのトークン情報を貼り付けます。ハイブリッド構成ウィザードを続行する前に、この情報を使用してパブリック DNS 内の各ドメインの TXT レコードを作成する必要があります。TXT レコードをご使用の DNS ゾーンに追加する方法については、ご使用の DNS ホストのヘルプをご覧ください。TXT レコードを作成し、DNS レコードをレプリケートしたら、<strong>次へ</strong> をクリックします。

14. <strong>トランスポート証明書</strong> ページの <strong>参照サーバーの選択</strong> フィールドで、以前にチェックリストで構成した証明書のある Exchange サーバーを選択します。

15. <strong>証明書を選択する</strong> フィールドで、メール トランスポートのセキュリティ保護に使用する証明書を選択します。この一覧には、前の手順で選択したメールボックス サーバーにインストールされているサードパーティの証明機関 (CA) によって発行されたデジタル証明書が表示されます。<strong>次へ</strong> をクリックします。

16. <strong>組織 FQDN</strong> ページで、インターネットにつながっている Exchange サーバーの外部アクセス可能な FQDN を入力します。Office 365 は、この FQDN を使用して、Exchange 組織間のセキュリティ保護されたメール トランスポートのサービス コネクタを構成します。たとえば、「mail.contoso.com」と入力します。<strong>次へ</strong> をクリックします。

17. ハイブリッド展開の構成の選択を更新し、Exchange サービスの変更とハイブリッド展開の構成を開始する準備をします。<strong>更新</strong> をクリックして、構成プロセスを開始します。ハイブリッド構成プロセスが実行されている間、ウィザードは、更新されるとともにハイブリッド展開用に構成されている機能とサービス領域を表示します。

18. ウィザードは完了メッセージを表示し、<strong>閉じる</strong> ボタンが表示されます。<strong>閉じる</strong> をクリックして、ハイブリッド展開構成プロセスを完了し、ウィザードを閉じます。

## Exchange と Exchange Online 組織の間の OAuth 認証の構成

Exchange 2013/2010 や Exchange 2013/2007 といった混在するハイブリッド展開の場合、Office 365 と社内 Exchange 組織の間の新しいハイブリッド展開 OAuth ベースの認証接続はハイブリッド構成ウィザードでは構成されません。これらの展開は、既定では、引き続きフェデレーション信頼プロセスを使用します。しかし、メッセージ レコード管理 (MRM)、Exchange インプレース アーカイブ、インプレース eDiscovery などの特定の Exchange 2013 機能は、新しい Exchange OAuth 認証プロトコルを使うことによってのみ、組織で完全に利用可能になります。Exchange 2013/2010 および Exchange 2013/2007 が混合するすべての組織で Exchange Online による新しいハイブリッド展開の一部としてこれらの機能を実装する場合は、ハイブリッド構成ウィザードでハイブリッド展開を構成した後に、Exchange OAuth 認証を構成するようお勧めします。

構成の手順の詳細については、「[Exchange と Exchange Online 組織の間の OAuth 認証の構成](https://technet.microsoft.com/ja-jp/library/dn594521\(v=exchg.150\))」を参照してください。

OAuth 認証を使用する Exchange のセキュリティとコンプライアンスの機能の詳細については、以下を参照してください。

  - [OAuth 認証を使用する Exchange ハイブリッド展開での Archiving のサポート](https://technet.microsoft.com/ja-jp/library/dn689104\(v=exchg.150\))

  - [Exchange ハイブリッド展開において電子情報開示をサポートするための OAuth 認証の使用](https://technet.microsoft.com/ja-jp/library/dn497703\(v=exchg.150\))

## 正常な動作を確認する方法

ハイブリッド構成ウィザードが正常に完了すると、最初に、ハイブリッド構成手順が予期したとおりに動作し完了したことが示されます。

ハイブリッド展開が正常に作成および構成されたことをさらに詳しく確認するには、次の手順を実行します。

  - 社内組織の Exchange 管理シェルで次のコマンドを実行します。このコマンドは、ハイブリッド展開の構成の値と設定、ハイブリッド機能、およびトランスポート エンドポイントを表示します。これらの値が正しいことを確認します。
    
        Get-HybridConfiguration

  - ハイブリッド構成ログを調べ、ハイブリッド構成ウィザードがすべての構成手順を完了したことを確認します。既定のログの場所は、社内メールボックス サーバーの C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration です。

  - 既存の社内メールボックスを Exchange Online 組織に移動してメールボックス移動機能のサポートをテストするか、または Exchange Online 組織に新しいユーザー メールボックスを作成して 2 つの組織間の空き時間情報の共有をテストします。どちらのメールボックスの操作でも、社内組織と Exchange Online 組織との間のメッセージ配信が既存のメールボックスで正常に機能しており、メッセージ配信がセキュリティ保護され、Exchange 組織への内部メッセージとして処理されていることをテストできます。
    
      - Exchange Online に新しいリモート メールボックスを作成するには、EAC を使用して、<strong>エンタープライズ</strong> \> <strong>受信者</strong> \> <strong>メールボックス</strong> の順に選択します。
    
      - Exchange Online に既存のメールボックスを移動するには、EAC を使用して、<strong>Office 365</strong> \> <strong>受信者</strong> \> <strong>移行</strong> の順に選択します。

