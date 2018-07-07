﻿---
title: 'フェデレーション: Exchange 2013 Help'
TOCTitle: フェデレーション
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 48269117
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

インフォメーション ワーカーは、外部の受信者、ベンダー、パートナー、および顧客との共同作業、および空き時間 (予定表の空き時間とも言う) 情報の共有を頻繁に行う必要があります。Microsoft Exchange Server 2013 のフェデレーションは、このような共同作業の取り組みに役立ちます。*フェデレーション*とは、ユーザーが他の外部のフェデレーション組織の受信者と予定表情報を共有するための簡単な方法である*フェデレーション共有*をサポートする、基礎となる信頼インフラストラクチャを意味します。フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



**目次**

主要な関連用語

Azure AD 認証システム

フェデレーション信頼

フェデレーション組織識別子

フェデレーションの例

フェデレーションのための証明書の要件

新しい証明書への切り替え

フェデレーションのファイアウォールの検討事項

## 主要な関連用語

次の表に、Exchange 2013 のフェデレーションに関連付けられたコア コンポーネントの定義を示します。

  - **アプリケーション識別子 (AppID)**  
    Exchange 組織を識別するために Azure Active Directory 認証システムによって生成された一意の番号。AppID は、Azure Active Directory 認証システムでフェデレーション信頼を作成するときに自動生成されます。

<!-- end list -->

  - **委任トークン**  
    Azure Active Directory 認証システムによって発行される SAML (Security Assertion Markup Language) トークンです。このトークンによって、あるフェデレーション組織のユーザーが、別のフェデレーション組織によって信頼されることが可能になります。委任トークンには、ユーザーの電子メール アドレス、不変の ID、アクションのためにトークンが発行されるオファーに関連付けられている情報が含まれています。

<!-- end list -->

  - **外部フェデレーション組織**  
    Azure Active Directory 認証システムとのフェデレーション信頼を確立した Exchange の外部組織。

<!-- end list -->

  - **フェデレーションの共有**  
    Azure Active Directory 認証システムとのフェデレーション信頼を活用して、クロスプレミスの Exchange 展開を含む Exchange 組織全体で動作する Exchange 機能のグループ。さらに、これらの機能は、複数の Exchange 組織にわたってユーザーの代わりに、サーバー間の認証済みの要求を作成するために使用されます。

<!-- end list -->

  - **フェデレーション ドメイン**  
    Exchange 組織の組織識別子 (OrgID) に追加される、権限のある承認済みドメイン。

<!-- end list -->

  - **ドメインの証明暗号化文字列**  
    Exchange 組織が Azure Active Directory 認証システムで使用するドメインを所有していることを証明するために使用する、暗号で保護された文字列。文字列は、**\[フェデレーションの信頼を有効にする\]** ウィザードを使用して自動生成するか、**Get-FederatedDomainProof** コマンドレットを使用して生成できます。

<!-- end list -->

  - **フェデレーションの共有ポリシー**  
    ユーザーによって設定される、予定表情報の個人間共有を可能にして制御する組織レベルのポリシー。

<!-- end list -->

  - **フェデレーション**  
    共通の目的を実現するための 2 つの Exchange 組織間の信頼ベースの合意。フェデレーションでは、両方の組織が、互いに相手の組織による認証アサーションの認識を必要とします。

<!-- end list -->

  - **フェデレーション信頼**  
    Exchange 組織の次のコンポーネントを定義する Azure Active Directory 認証システムとの関係。
    
      - アカウント名前空間
    
      - アプリケーション識別子 (AppID)
    
      - 組織識別子 (OrgID)
    
      - フェデレーション ドメイン
    
    他の Exchange フェデレーション組織とのフェデレーション共有を構成するには、Azure Active Directory 認証システムでフェデレーション信頼を確立する必要があります。

<!-- end list -->

  - **フェデレーション外の組織**  
    Azure Active Directory 認証システムとのフェデレーション信頼が確立されていない組織。

<!-- end list -->

  - **組織識別子 (OrgID)**  
    組織内で構成された権限のある承認済みドメインの中で、どのドメインがフェデレーションが有効であるかを定義します。電子メール アドレスに OrgID で構成されたフェデレーション ドメインが含まれる受信者のみが、Azure Active Directory 認証システムによって認識され、フェデレーション共有の機能を使用できます。OrgID は、定義済みの文字列と、**\[フェデレーションの信頼を有効にする\]** ウィザードでフェデレーション用に選択された最初の承認済みドメインの組み合わせです。たとえば、フェデレーション ドメイン contoso.com を組織のプライマリ SMTP ドメインとして指定すると、アカウントの名前空間 FYDIBOHF25SPDLT.contoso.com がフェデレーション信頼の OrgID として自動的に作成されます。

<!-- end list -->

  - **組織上の関係**  
    受信者が空き時間 (予定表の空き時間) 情報を共有できる、2 つの Exchange フェデレーション組織間の一対一の関係。組織の関係では、Azure Active Directory 認証システムとのフェデレーション信頼が必要となり、Exchange 組織間で Active Directory のフォレストまたはドメインの信頼を使用する必要がなくなります。

<!-- end list -->

  - **Azure Active Directory 認証システム**  
    Microsoft Exchange フェデレーション組織間の信頼ブローカーとして機能する無償のクラウドベースの ID サービス。このゲートウェイは、Exchange 受信者から他の Exchange フェデレーション組織の受信者の情報を要求されたときに、委任トークンを要求した受信者に発行します。詳細については、「[Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)」を参照してください。

## Azure AD 認証システム

Microsoft が提供する無料のクラウドベース サービスである Azure Active Directory 認証システムは、オンプレミスの Exchange 2013 組織と、その他のフェデレーション Exchange 2010 組織および Exchange 2013 組織の間で信頼ブローカーとして機能します。Exchange 組織でフェデレーションを構成するには、 認証システムとのワンタイム フェデレーション信頼を確立し、Azure Active Directory 認証システムがその組織のフェデレーション パートナーになれるようにする必要があります。この信頼の確立により、Active Directory (*ID プロバイダー*) により認証されたユーザーは、Azure AD 認証システムによって SAML (Security Assertion Markup Language) 委任トークンを発行されます。これらの委任トークンによって、特定のフェデレーション Exchange 組織のユーザーは、別のフェデレーション Exchange 組織によって信頼されるようになります。信頼ブローカーとして機能する Azure AD 認証システムを使用することで、組織は他の組織と複数の信頼関係を個別に確立する必要がなくなり、ユーザーはシングル サインオン (SSO) 操作によって外部のリソースにアクセスできます。詳細については、「[Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)」を参照してください。

主要な関連用語

## フェデレーション信頼

Exchange 2013 のフェデレーション共有機能を使用するには、Exchange 2013 組織と Azure AD 認証システムの間でフェデレーションの信頼を確立する必要があります。Azure AD 認証システムとのフェデレーション信頼を確立すると、組織のデジタル セキュリティ証明書が Azure AD 認証システムに置き換えられ、Azure AD 認証システムの証明書とフェデレーション メタデータが取得されます。フェデレーション信頼を確立するには、Exchange 管理コンソール (EAC) で **\[フェデレーションの信頼を有効にする\]** ウィザードを使用するか、Exchange 管理シェルで **New-FederationTrust** コマンドレットを実行します。自己署名証明書が **\[フェデレーションの信頼を有効にする\]** ウィザードによって自動的に作成され、ユーザーが外部のフェデレーション組織によって信頼されるようにする Azure AD 認証システムからの委任トークンを署名および暗号化するために使用されます。証明書の要件の詳細については、後の「フェデレーションのための証明書の要件」を参照してください。

Azure AD 認証システムとのフェデレーション信頼を作成すると、*アプリケーション識別子* (AppID) が Exchange 組織に対して自動的に生成され、**Get-FederationTrust** コマンドレットの出力に提供されます。AppID は、Azure AD 認証システムが Exchange 組織を一意に識別するために使用されます。また、Exchange 組織によって、Azure AD 認証システムで使用するドメインを組織が所有していることを証明するためにも使用されます。これは、各フェデレーション ドメインのパブリック ドメイン ネーム システム (DNS) ゾーンにテキスト (TXT) レコードを作成することによって行われます。

主要な関連用語

## フェデレーション組織識別子

*フェデレーション組織識別子* (OrgID) は、組織内で構成された権限のある承認済みドメインの中で、どのドメインがフェデレーションを使用可能であるかを定義します。電子メール アドレスに OrgID で構成された承認済みドメインが含まれる受信者のみが、Azure AD 認証システムによって認識され、フェデレーション共有の機能を使用できます。フェデレーション信頼を新規作成すると、OrgID が Azure AD 認証システムで自動的に作成されます。この OrgID は、定義済みの文字列と、ウィザードでプライマリ共有ドメインとして選択された承認済みドメインの組み合わせです。たとえば、共有有効ドメインの編集ウィザードで、フェデレーション ドメイン **contoso.com** を組織のプライマリ共有ドメインとして指定した場合、Exchange 組織のフェデレーション信頼の OrgID として **FYDIBOHF25SPDLT.contoso.com** アカウントの名前空間が自動的に作成されます。

Exchange 組織のプライマリ SMTP ドメインであっても、このドメインを Exchange 組織で承認済みのドメインとする必要はなく、ドメイン ネーム システム (DNS) の所有権の証明のための TXT レコードは必要ありません。唯一の要件は、フェデレーション対象として選択した承認済みドメインは、最長で 32 文字に制限されるということです。このサブドメインの唯一の目的は、Azure AD 認証システム用のフェデレーション名前空間として機能し、SAML 委任トークンを要求する受信者の一意の識別子を維持することです。SAML トークンの詳細については、「[SAML トークンとクレーム](https://go.microsoft.com/fwlink/?linkid=198561)」を参照してください。

承認されたドメインは、いつでもフェデレーション信頼に追加または削除できます。組織内ですべてのフェデレーション共有機能を有効または無効にするには、フェデレーション信頼の OrgID を有効または無効にするだけで済みます。


> [!IMPORTANT]
> フェデレーション信頼で使用する OrgID、承認済みドメイン、または AppID を変更すると、組織内のすべてのフェデレーションの共有機能に影響します。また、このような変更は、Exchange Online およびハイブリッド展開の構成などの外部のフェデレーション Exchange 組織にも影響します。これらのフェデレーション信頼構成の設定に対して変更を行った場合は、すべての外部フェデレーション パートナーに通知することをお勧めします。



主要な関連用語

## フェデレーションの例

Contoso, Ltd. と Fabrikam, Inc. という 2 つの Exchange 組織では、ユーザーが互いに予定表の空き時間情報を共有できるようにしようとしています。それぞれの組織で Azure AD 認証システムとのフェデレーション信頼を作成し、そのアカウント名前空間を、ユーザーの電子メール アドレス ドメインに使用するドメインを含むように構成します。

Contoso の従業員は、contoso.com、contoso.co.uk、contoso.ca のいずれかの電子メール アドレス ドメインを使用します。Fabrikam の従業員は、fabrikam.com、fabrikam.org、fabrikam.net のいずれかの電子メール アドレス ドメインを使用します。いずれの組織も、それぞれの Azure AD 認証システムとのフェデレーション信頼のアカウント名前空間に、すべての承認済み電子メール ドメインを含めるようにします。2 つの組織間で複雑な Active Directory フォレストまたはドメイン信頼構成を必要とはせずに、両方の組織が互いの組織の関係を構成して、予定表の空き時間情報の共有を可能にします。

次の図は、Contoso, Ltd. と Fabrikam, Inc. の間のフェデレーション構成を示します。

**フェデレーションの共有例**

![フェデレーションの信頼とフェデレーションの共有](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "フェデレーションの信頼とフェデレーションの共有")

## フェデレーションのための証明書の要件

Azure AD 認証システムとのフェデレーション信頼を確立するには、自己署名証明書、または証明機関 (CA) によって署名された X.509 証明書を作成し、信頼の作成に使用する Exchange 2013 サーバーにインストールする必要があります。EAC で **\[フェデレーションの信頼を有効にする\]** ウィザードを使用して自動的に作成およびインストールできる、自己署名証明書の使用を強くお勧めします。この証明書は、フェデレーションの共有に使用される委任トークンの署名および暗号化のみに使用されます。フェデレーション信頼に必要な証明書は 1 つだけです。この証明書は、Exchange 2013 によって組織内の他のすべての Exchange 2013 サーバーに自動的に配布されます。

外部 CA によって署名された X.509 証明書を使用する場合は、証明書が以下の要件を満たしている必要があります。

  - **信頼済み証明機関**   可能であれば、X.509 SSL (Secure Sockets Layer) 証明書は Windows Live により、信頼済み証明機関から発行する必要があります。現在、Microsoft が認定していない証明機関が発行した証明書も使用できます。信頼済み証明機関の一覧については、「[フェデレーション信頼のための信頼されたルート証明機関](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md)」を参照してください。

  - **サブジェクトのキー識別子**   証明書にはサブジェクト キー識別子フィールドが必要です。商用 CA によって発行された X.509 証明書のほとんどには、この識別子が含まれています。

  - **CryptoAPI 暗号化サービス プロバイダー (CSP)** 証明書は CryptoAPI CSP を使用する必要があります。Cryptography API:Next Generation (CNG) プロバイダーを使用する証明書は、フェデレーションではサポートされません。Exchange を使用して証明書要求を作成する場合は、CryptoAPI プロバイダーを使用します。詳細については、「[Cryptography API:Next Generation](https://go.microsoft.com/fwlink/?linkid=187890)」を参照してください (このサイトは英語の場合があります)。

  - **RSA 署名アルゴリズム**   証明書は署名アルゴリズムとして RSA を使用する必要があります。

  - **エクスポート可能な秘密キー**   証明書を生成するために使用される秘密キーは、エクスポート可能である必要があります。EAC で **\[Exchange 証明書の新規作成\]** ウィザードを使用するか、シェルで [New-ExchangeCertificate](https://technet.microsoft.com/ja-jp/library/aa998327\(v=exchg.150\)) コマンドレットを実行することで証明書要求を作成する場合に、秘密キーをエクスポート可能に指定します。

  - **現在の証明書**   証明書は現在のものにする必要があります。有効期限が切れた証明書や失効した証明書を使用して、フェデレーション信頼を作成することはできません。

  - **拡張キー使用法**   証明書には、拡張キー使用法 (EKU) タイプ **クライアント認証 (1.3.6.1.5.5.7.3.2)** を含める必要があります。この使用法タイプは、リモート コンピューターに自分の ID を提供するために使用されます。EAC またはシェルを使用して証明書要求を生成する場合に、既定でこの使用法タイプが含まれます。


> [!NOTE]
> 認証のために証明書が使用されることがないため、証明書にはサブジェクト名やサブジェクトの別名についての要件はありません。ホスト名、ドメイン名、または他の何らかの名前と同じサブジェクト名を持つ証明書を使用することができます。



主要な関連用語

## 新しい証明書への切り替え

フェデレーション信頼を作成するために使用する証明書は、現在の証明書として指定されます。ただし、定期的にフェデレーション信頼の新しい証明書をインストールして使用しなければならない場合があります。たとえば、現在の証明書の期限が切れた場合、組織のビジネスやセキュリティの要件を満たす必要がある場合などに、新しい証明書を使用する必要があります。新しい証明書への移行をシームレスに実行するには、Exchange 2013 サーバー上に新しい証明書をインストールし、その証明書を新しい証明書として指定するようにフェデレーション信頼を構成する必要があります。Exchange 2013 によって、新しい証明書は組織内の他のすべての Exchange 2013 サーバーに自動的に配布されます。Active Directory トポロジによっては、証明書の配布に時間がかかる場合があります。シェルで [Test-FederationTrustCertificate](https://technet.microsoft.com/ja-jp/library/dd335228\(v=exchg.150\)) コマンドレットを使用すると、証明書の状態を確認できます。

証明書の配布状態を確認したら、新しい証明書を使用するように信頼を構成します。証明書の切り替えを実行すると、現在の証明書は以前の証明書として指定され、新しい証明書が現在の証明書として指定されます。新しい証明書は Azure AD 認証システムに公開され、Azure AD 認証システムと交換されたすべての新しいトークンが新しい証明書を使用して暗号化されます。


> [!NOTE]
> この証明書の切り替え処理は、フェデレーションによってのみ使用されます。証明書を必要とする Exchange 2013 の他の機能に同じ証明書を使用する場合は、新しい証明書の入手、インストール、および移行を計画する際にその機能の要件を考慮する必要があります。



主要な関連用語

## フェデレーションのファイアウォールの検討事項

フェデレーション機能は、組織内のメールボックスおよびクライアント アクセス サーバーによる HTTPS を使用したインターネットへの送信アクセスを必要とします。組織内のすべての Exchange 2013 メールボックスおよびクライアント アクセス サーバーからの送信 HTTPS アクセス (TCP ポート 443) を許可する必要があります。

外部組織が組織の空き時間情報にアクセスするには、クライアント アクセス サーバーをインターネットに公開する必要があります。これには、インターネットからクライアント アクセス サーバーへの受信 HTTPS アクセスが必要です。クライアント アクセス サーバーをインターネットに公開していない Active Directory サイトのクライアント アクセス サーバーは、インターネットからアクセスできるその他の Active Directory サイトのクライアント アクセス サーバーを使用できます。インターネットに公開されていないクライアント アクセス サーバーは、外部組織から可視の URL で設定された Web サービス仮想ディレクトリの外部 URL が必要です。

[ページのトップへ](sharing-exchange-2013-help.md)
