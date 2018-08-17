---
title: 'フェデレーション信頼の構成: Exchange 2013 Help'
TOCTitle: フェデレーション信頼の構成
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 49896332
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション信頼の構成

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2017-07-26_

フェデレーションの信頼は、Microsoft Exchange 2013 組織と Azure Active Directory 認証システムの間に信頼関係を確立します。フェデレーション信頼を構成すると、他の Exchange フェデレーション組織とのフェデレーション共有を構成して、受信者間で予定表の空き時間情報を共有できます。フェデレーション共有は、2 つの Exchange 2013 フェデレーション組織間、または 1 つの Exchange 2013 フェデレーション組織と複数の Exchange 2010 フェデレーション組織との間で構成できます。また、Office 365 組織との共有を設定することもできます。


> [!NOTE]
> フェデレーション信頼の作成は、Exchange 組織内でフェデレーション共有を設定する際の、複数の手順の 1 つです。すべての手順を確認するには、「<A href="configure-federated-sharing-exchange-2013-help.md">フェデレーション共有の構成</A>」を参照してください。



フェデレーションに関連する追加の管理タスクについては、「[フェデレーションの手順](federation-procedures-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 30 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。: 「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」トピックの「フェデレーションと証明書のアクセス許可」。

  - フェデレーション信頼の確立に使用されるドメインは、インターネットから解決可能である必要があります。これには、ドメイン登録業者によってドメインが登録されていること、およびドメインのドメイン ネーム システム (DNS) ゾーンがインターネットからアクセス可能な DNS サーバーによってホストされていることが必要です。組織がドメイン宛てのインターネット電子メールを受信できるようであれば、それらの前提条件は既に満たしています。

  - TXT レコードをパブリック DNS に追加する必要があります。パブリック DNS レコードをホストする組織とともに TXT レコードを追加する要件を確認します。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

  - フェデレーション共有関係にある両方の Exchange 組織は、フェデレーション信頼のために同じ Azure AD 認証システムを使用する必要があります。この要件が適用されるのは、2 つの社内 Exchange 組織間、または社内 Exchange 組織と [Office 365](https://go.microsoft.com/fwlink/?linkid=392576) によってホストされる Exchange 組織の間にフェデレーション共有を構成する場合です。

  - Exchange 2013 組織のために Azure AD 認証システムとのフェデレーション信頼を作成する場合、そのフェデレーション信頼では Azure AD 認証システムのビジネス インスタンスが使用されます。ただし、以前のバージョンの Exchange を使用しているその他の Exchange フェデレーション組織および既存のフェデレーション信頼では、Azure AD 認証システムのビジネス インスタンスまたはコンシューマー インスタンスのいずれかを使用している可能性があります。
    
    以下の Exchange 組織において既定では、Azure AD 認証システムのビジネス インスタンスを使用します。
    
      - フェデレーション信頼に対して**フェデレーション信頼の有効化**ウィザードと自己署名証明書を使用する Exchange 2013 組織。
    
      - フェデレーション信頼に対して**フェデレーション信頼の新規作成**ウィザードと自己署名証明書を使用する Exchange 2010 SP1 以降の組織。
    
      - Office 365 によってホストされている Exchange 組織 (Exchange Online など)。
    
    以下の Exchange 組織において既定では、Azure AD 認証システムのコンシューマー インスタンスを使用します。
    
      - サード パーティの証明機関が発行する証明書を使用する、RTM (Release To Manufacturing) 版の Exchange 2010 組織。
    
    すべての Exchange 組織で、フェデレーション信頼に Azure AD 認証システムのビジネス インスタンスを使用することをお勧めします。2 つの Exchange 組織間でフェデレーション共有を構成する前に、各 Exchange 組織で既存のフェデレーション信頼に Azure AD 認証システムのどちらのインスタンスが使用されているかを確認する必要があります。Exchange 組織で既存のフェデレーション信頼に使用されている Azure AD 認証システムのインスタンスを判別するには、次のシェル コマンドを実行します。
    
        Get-FederationInformation -DomainName <hosted Exchange domain namespace>
    
    ビジネス インスタンスは、*TokenIssuerURIs* パラメーターに `<uri:federation:MicrosoftOnline>` という値を返します。
    
    コンシューマー インスタンスは、*TokenIssuerURIs* パラメーターに `<uri:WindowsLiveID>` という値を返します。
    
    Azure AD 認証システムのビジネス インスタンスを使用している既存のフェデレーション信頼を所有する Exchange 組織にフェデレーション共有を構成するには、このトピックの手順を実行します。これらの手順を実行しさえすれば、フェデレーション信頼を作成して、それを使用して 2 つの Exchange 2013 組織の間、または Exchange 2013 組織と既に Azure AD 認証システムのビジネス インスタンスを使用している Exchange 2010 組織の間でフェデレーション共有を有効にすることができます。
    
    Exchange 2013 組織と Azure AD 認証システムのコンシューマー インスタンスを使用している既存のフェデレーション信頼を所有する Exchange 組織の間にフェデレーション共有を構成するには、コンシューマー インスタンスを使用している Exchange 組織が、Exchange 2010 SP2 以降をインストールするか、Exchange 2013 にアップグレードする必要があります。Exchange 2010 SP2 以降をインストールする場合は、**フェデレーション信頼の新規作成**ウィザードを使用して、既存のフェデレーション ドメインとフェデレーション信頼を削除し、再作成します。フェデレーション信頼の再作成時に、Azure AD 認証システムのビジネス インスタンスが使用されます。

## EAC を使用してフェデレーション信頼を作成および構成する

1.  社内組織の Exchange 2013 サーバーで、<strong>組織</strong> \> <strong>共有</strong> に移動します。

2.  <strong>有効にする</strong> をクリックして、**フェデレーション信頼の有効化**ウィザードを起動します。

3.  ウィザードが完了したら、<strong>閉じる</strong> をクリックします。

4.  <strong>共有</strong> タブの <strong>フェデレーション信頼</strong> で、<strong>変更</strong> をクリックします。

5.  <strong>共有が有効なドメイン</strong> の <strong>ステップ 1</strong> の横にある <strong>参照</strong> をクリックします。

6.  <strong>承認済みドメインの選択</strong> で、リストからプライマリ共有ドメインを選択し、<strong>OK</strong> をクリックします。
    

    > [!NOTE]
    > 選択したドメインは、フェデレーション信頼の OrgID の構成に使用されます。OrgID の詳細については、「<A href="federation-exchange-2013-help.md">フェデレーション</A>」を参照してください。



7.  プライマリ共有ドメイン用に生成されたフェデレーション ドメインの証明をメモしておきます。この文字列を使用して、パブリック DNS サーバー上で TXT レコードを作成します。
    

    > [!IMPORTANT]
    > フェデレーション ドメインの証明は、アルファベット文字列です。入力エラーを避けるために、EAC からこの文字列をコピーし、メモ帳などのテキスト エディターに貼り付けます。その後、テキスト エディターからクリップボードにコピーし、TXT レコードの作成時に <STRONG>[テキスト]</STRONG> フィールドに貼り付けます。正確でないフェデレーション ドメインの証明文字列を使用して TXT レコードを作成すると、Azure AD 認証システムが、ドメインの所有権の証明を確認できなくなり、この TXT レコードをフェデレーションの組織識別子に追加できません。



8.  **ステップ 2** で、<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、フェデレーション共有機能を必要とする組織内のユーザーが使用する電子メール アドレスのフェデレーション信頼にドメインを追加します。たとえば、その電子メール アドレスで sales.contoso.com などのサブドメインを使用するユーザーがいる場合、sales.contoso.com ドメインをフェデレーション信頼に追加します。
    

    > [!NOTE]
    > フェデレーション ドメインの証明文字列は、選択された追加ドメインごとに作成されます。追加ドメインごとにパブリック DNS 上で別個の TXT レコードを作成する必要があります。



9.  各ドメイン用に作成されたフェデレーション ドメインの証明文字列を使用して、パブリック DNS サーバー上でこれらの各ドメインに TXT レコードを作成します。パブリック DNS ホストの更新スケジュールによっては、DNS 変更のレプリケーションに 15 分以上かかる場合があります。

10. TXT レコードを作成およびレプリケートしたら、<strong>更新</strong> をクリックします。

## シェルを使用してフェデレーション信頼を作成および構成する

1.  次のコマンドを実行して、フェデレーション信頼で使用する証明書用の一意のサブジェクト キー識別子を作成します。
    
        $ski = [System.Guid]::NewGuid().ToString("N")

2.  フェデレーション信頼で使用する自己署名証明書を作成するには、次の構文を使用します。
    
        New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    
    この例では、Azure AD 認証システムとのフェデレーション信頼で使用する自己署名証明書を作成します。証明書はフレンドリ名の値 Exchange Federated Sharing を使用し、ドメイン値は **USERDNSDOMAIN** 環境変数から取得されます。
    
        New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski

3.  フェデレーションの信頼を作成し、前の手順で作成した自己署名証明書を組織の Exchange サーバーに自動的に展開するには、次の構文を使用します。
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    
    この例では、Azure AD Authentication という名前のフェデレーション信頼を作成し、Exchange Federated Sharing という名前の自己署名証明書を展開します。
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"

4.  この構文を使用して、フェデレーション信頼用に構成するドメインに必要な、ドメイン所有権の証明の TXT レコードを返します。
    
        Get-FederatedDomainProof -DomainName <domain>
    
    この例では、プライマリ共有ドメイン contoso.com に必要なドメイン所有権の証明の TXT レコードを返します。
    
        Get-FederatedDomainProof -DomainName contoso.com
    
    **メモ:** 
    
      - フェデレーション信頼用に構成された各ドメインまたはサブドメインには、ドメイン所有権の証明の TXT レコードが必要です。そのため、異なる *DomainName* 値を使用してこのコマンドを何回か実行する必要があります。
    
      - シェルで右クリックして、ドメインの証明文字列をコピーし、<strong>Mark</strong>、<strong>Proof</strong> 値の順に選択し後に Enter キーを押すと、TXT レコード作成時にドメインの証明文字列を使用できます。正確でないフェデレーション ドメインの証明文字列を使用して TXT レコードを作成すると、Azure AD 認証システムがドメインの所有権の証明を確認できないため、この TXT レコードをフェデレーションの組織識別子に追加できません。

5.  前の手順の情報に基づいて、フェデレーション信頼に含めるすべてのドメインのパブリック DNS サーバーに TXT レコードを作成します。パブリック DNS ホストの更新スケジュールによっては、DNS 変更のレプリケーションに 15 分以上かかる場合があります。新しい TXT レコードが使用できることを確認したら、次に進みます。

6.  次のコマンドを実行して、Azure AD からメタデータおよび証明書を取得します。
    
        Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"

7.  この構文を使用して、ステップ 3 で作成したフェデレーション信頼のプライマリ共有ドメインを構成します。指定したドメインは、フェデレーション信頼の組織識別子 (OrgID) を構成するために使用されます。OrgID の詳細については、「[フェデレーション組織識別子](federation-exchange-2013-help.md)」を参照してください。
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    
    この例では、承認済みドメイン contoso.com を、Azure AD Authentication というフェデレーション信頼のプライマリ共有ドメインとして構成します。
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true

8.  フェデレーション信頼に他のドメインを追加するには、次の構文を使用します。
    
        Add-FederatedDomain -DomainName <AdditionalDomain>
    
    sales.contoso.com ドメインのメール アドレスを持つユーザーにフェデレーション共有機能が必要なため、この例では、サブドメイン sales.contoso.com をフェデレーション信頼に追加します。
    
        Add-FederatedDomain -DomainName sales.contoso.com
    
    フェデレーション信頼に追加するドメインまたはサブドメインには、ドメイン所有権の証明の TXT レコードが必要です。

構文およびパラメーターの詳細については、「[New-ExchangeCertificate](https://technet.microsoft.com/ja-jp/library/aa998327\(v=exchg.150\))」、「[New-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd351047\(v=exchg.150\))」、「[Get-FederatedDomainProof](https://technet.microsoft.com/ja-jp/library/ff717833\(v=exchg.150\))」、「[Set-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd298034\(v=exchg.150\))」、「[Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/ja-jp/library/dd351037\(v=exchg.150\))」、「[Add-FederatedDomain](https://technet.microsoft.com/ja-jp/library/dd351208\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

**フェデレーション信頼の有効化**および**共有が有効なドメイン** ウィザードが正常に完了すると、フェデレーション信頼が期待どおりに構成されたことが初めてわかります。

フェデレーション信頼が正常に作成および構成されたことをさらに詳しく確認するには、次の手順を実行します。

1.  次のシェル コマンドを実行して、フェデレーション信頼情報を確認します。
    
        Get-FederationTrust | Format-List

2.  *\<PrimarySharedDomain\>* をプライマリ共有ドメインに置き換え、次のシェル コマンドを実行し、フェデレーション情報を組織から取得できることを確認します。
    
        Get-FederationInformation -DomainName <PrimarySharedDomain>

構文およびパラメーターの詳細については、「[Get-FederationTrust](https://technet.microsoft.com/ja-jp/library/dd351262\(v=exchg.150\))」と「[Get-FederationInformation](https://technet.microsoft.com/ja-jp/library/dd351221\(v=exchg.150\))」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。


