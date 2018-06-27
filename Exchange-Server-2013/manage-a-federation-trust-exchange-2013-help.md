---
title: 'フェデレーション信頼の管理: Exchange 2013 Help'
TOCTitle: フェデレーション信頼の管理
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 49895220
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション信頼の管理

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-01-01_

フェデレーションの信頼は、Microsoft Exchange 2013 の組織と Azure Active Directory 認証システムの間に信頼関係を確立し、その他のフェデレーションされた Exchange 組織とのフェデレーションされた共有をサポートします。通常は、フェデレーションの信頼を作成した後に管理または変更する必要はありません。ただし、フェデレーション ドメインの追加や削除、またはフェデレーションの信頼の組織識別子 (OrgID) を構成するために使用されるドメインの再設定が必要になる状況もあります。


> [!NOTE]
> 既存のフェデレーションの信頼を変更すると、特に OrgID の定義に使用されるプライマリ共有ドメインの場合、フェデレーション Exchange 組織間または Office 365 組織とのハイブリッド展開のためのフェデレーションの共有を中断させる可能性があります。



フェデレーションに関連する追加の管理タスクについては、「[フェデレーションの手順](federation-procedures-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 30 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「*Federation and certificates* パーミッション」。

  - フェデレーションの信頼に追加された新しいフェデレーション ドメインごとに、パブリック DNS に TXT レコードを追加することが必要になります。パブリック DNS レコードをホストする組織とともに TXT レコードを追加する要件を確認します。

  - このトピックの目的上、既存のフェデレーションの信頼は次の設定で構成されました。
    
      - **\[Contoso.com\]** はフェデレーションの信頼のプライマリ共有ドメインです。(このドメインは変更されません)
    
      - フェデレーション ドメイン **\[service.contoso.com\]** および **\[sales.contoso.com\]** は、既存のフェデレーションの信頼に含まれます。
    
      - **Marketing.contoso.com** は Exchange 組織の承認済みドメインです。

  - このトピックは、フェデレーションの信頼に使用される証明書の表示および管理、シェル内のフェデレーションの信頼のパラメーター情報の表示など、他のフェデレーション管理タスクも対象とします。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

## 必要な作業

## EAC を使用してフェデレーション信頼を管理する

1.  社内組織の Exchange 2013 サーバーで、**\[組織\]** \> **\[共有\]** に移動します。

2.  **\[フェデレーションの信頼\]** セクションで、**\[変更\]** をクリックします。

3.  **\[共有が有効なドメイン\]** で、プライマリ共有ドメインが変わっていないので **\[ステップ 1\]** をスキップします。

4.  **\[ステップ 2\]** で、**\[service.contoso.com\]** ドメインを選択してから **\[削除\]**![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックして、フェデレーションの信頼からドメインを削除します。

5.  **\[ステップ 2\]** で、**\[追加\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

6.  **\[承認済みドメインの選択\]** で、承認済みドメインのリストから **\[marketing.contoso.com\]** を選択して、**\[OK\]** をクリックし、フェデレーションの信頼にドメインを追加します。
    

    > [!IMPORTANT]
    > フェデレーション ドメインの証明文字列は、<STRONG>[marketing.contoso.com]</STRONG> ドメインに作成されます。このドメインのパブリック DNS に別の TXT レコードを作成する必要があります。



7.  **\[marketing.contoso.com\]** ドメインに作成されたフェデレーション ドメインの証明文字列を使用して、パブリック DNS サーバー上に TXT レコードを作成します。パブリック DNS ホストの更新スケジュールによっては、DNS 変更のレプリケーションに 15 分以上かかる場合があります。

8.  TXT レコードを作成および複製した後、**\[更新\]** をクリックします。

## シェルを使用してフェデレーションの信頼を管理する

1.  この例では、フェデレーションの信頼からから service.contoso.com ドメインを削除します。
    
        Remove-FederatedDomain -DomainName service.contoso.com

2.  この例では、marketing.contoso.com ドメインをフェデレーションの信頼に追加します。
    
        Add-FederatedDomain -DomainName marketing.contoso.com

構文およびパラメーターの詳細については、「[Remove-FederatedDomain](https://technet.microsoft.com/ja-jp/library/dd298128\(v=exchg.150\))」と「[Add-FederatedDomain](https://technet.microsoft.com/ja-jp/library/dd351208\(v=exchg.150\))」を参照してください。

次のシェル コマンドを実行して、フェデレーションの信頼の他の側面を管理します。

1.  **フェデレーション OrgID とフェデレーション ドメインを表示する**
    
    この例では、Exchange 組織のフェデレーション OrgID と、フェデレーション ドメインや状態などの関連情報を表示します。
    
        Get-FederatedOrganizationIdentifier

2.  **フェデレーション信頼証明書を表示する**
    
    この例では、フェデレーションの信頼 "Azure AD authentication" で使用される前の証明書、現在の証明書、および次の証明書を表示します。
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **フェデレーション証明書の状態を確認する**
    
    この例では、組織内のすべてのメールボックス サーバーおよびクライアント アクセス サーバー上のフェデレーション証明書の状態を表示します。
    
        Test-FederationTrustCertificate

4.  **フェデレーション信頼が、証明書を次の証明書として使用するよう構成する**
    
    この例では、提供された拇印付き証明書を次の証明書として使用するようにフェデレーションの信頼 "Azure AD authentication" を構成します。組織内のすべての Exchange サーバーで証明書を展開した後、*PublishCertificate* スイッチを使用し、この証明書を現在の証明書として使用されるようにフェデレーション信頼を構成できます。
    
        Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17

5.  **次の証明書を現在の証明書として使用するようにフェデレーション信頼を構成する**
    
    この例では、フェデレーション信頼 Azure AD 認証が次の証明書を現在の証明書として使用し、それを Azure AD 認証システムに発行するように構成します。
    
        Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    

    > [!NOTE]
    > 次の証明書を現在の証明書として使用するようにフェデレーション信頼を構成する前に、証明書が組織内のすべての Exchange サーバーに展開されていることを確認してください。証明書の展開状態を確認するには、<A href="https://technet.microsoft.com/ja-jp/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</A> コマンドレットを使用します。



6.  **フェデレーション メタデータと証明書を Azure AD 認証システムから更新する**
    
    この例では、フェデレーション信頼 Azure AD 認証に関する Azure AD 認証システムのフェデレーション メタデータと証明書を更新します。
    
        Set-FederationTrust "Azure AD authentication" -RefreshMetadata

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/ja-jp/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/ja-jp/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd298034\(v=exchg.150\))

## 正常な動作を確認する方法

**\[共有が有効なドメイン\]** ウィザードが正常に完了することは、まず予期したとおりにフェデレーション信頼を構成したことで判断できます。

正常実行を詳細に確認するには、次を実行します。

1.  次のシェル コマンドを実行して、フェデレーション信頼情報を確認します。
    
        Get-FederationTrust | format-list

2.  次のシェル コマンドを実行して、フェデレーション情報を組織から取得できることを確認します。たとえば、sales.contoso.com ドメインおよび marketing.contoso.com ドメインが *DomainNames* パラメーターで返されることを確認します。
    
        Get-FederationInformation -DomainName <your primary sharing domain>


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


