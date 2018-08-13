---
title: 'Exchange 2013 をインストールしたときの Active Directory の変更内容: Exchange 2013 Help'
TOCTitle: Exchange 2013 をインストールしたときの Active Directory の変更内容
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371325
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 をインストールしたときの Active Directory の変更内容

 

_**適用先:** Exchange Server, Exchange Server 2013_

_**トピックの最終更新日:** 2014-05-26_

Exchange 2013 をインストールすると、Active Directory フォレストとドメインが変更されます。Exchange がこの変更を行うのは、組織内の Exchange サーバー、メールボックス、およびその他の Exchange 関連オブジェクトに関する情報を保存するためです。この変更は、Exchange 2013 セットアップ ウィザードを実行したとき、または、Exchange 2013 コマンドライン セットアップ中に *PrepareSchema* コマンド、*PrepareAD* コマンド、および *PrepareDomains* コマンド (これらのコマンドの使用方法については「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照) を実行したときに実施されます。Exchange が Active Directory に加える変更内容を知りたい場合に、このトピックが役に立ちます。ここでは、Exchange が Active Directory の各準備段階で行う変更内容について説明します。

Active Directory を Exchange 用に準備するために実行する必要のある手順は次の 3 つです。

  - Active Directory スキーマを拡張する

  - Active Directory コンテナー、オブジェクト、およびその他の項目を準備する

  - Active Directory ドメインを準備する

3 つすべての手順が完了したら、Active Directory フォレストを Exchange 2013 に使用することができます。Exchange 2013 のインストール方法については、「[セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)」を参照してください。

## Active Directory スキーマを拡張する

Active Directory スキーマを拡張すると、クラス、属性、およびその他の項目が追加され、更新されます。これらの変更は、Exchange が Exchange 組織に関する情報を保存するためのコンテナーとオブジェクトを作成できるようにするために必要です。Exchange は Active Directory スキーマに多数の変更を加えるため、この手順専用のトピックが用意されています。スキーマに対するすべての変更を確認するには、「[Exchange 2013 Active Directory スキーマの変更](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)」を参照してください。

この手順は、Active Directory フォレスト内の最初の Exchange 2013 サーバー上で Exchange 2013 セットアップ ウィザードを実行したときに自動的に実行されます。また、フォレスト内の最初の Exchange 2013 サーバー上で *PrepareSchema* コマンド (またはオプションで *PrepareAD* コマンド) を使用して Exchange 2013 コマンド ライン セットアップを実行したときにも実行されます。スキーマの拡張方法に関する詳細については、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」の「[Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照してください。

Exchange がスキーマの拡張を終了すると、スキーマ バージョンが設定され、**ms-Exch-Schema-Version-Pt** 属性に保存されます。Active Directory スキーマが正常に拡張されたことを確認するには、この属性内に保存された値をチェックします。属性内の値が、インストールした Exchange 2013 のリリースの列挙されたスキーマ バージョンと一致していれば、スキーマの拡張は成功しています。Exchange リリースの一覧とこの属性値のチェック方法については、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」の「[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照してください。

## Active Directory コンテナー、オブジェクト、およびその他の項目を準備する

拡張されたスキーマを使用する次の手順は、Exchange が Active Directory に情報を保存するために使用するコンテナー、オブジェクト、属性、およびその他の項目を追加することです。この手順で加えられる変更のほとんどが Active Directory フォレスト全体に適用されます。セットアップ中に *PrepareAD* コマンドが実行されるローカル Active Directory ドメインにはもっと小規模な変更が加えられます。

Active Directory フォレストに加えられる変更は次のとおりです。

  - CN=Services,CN=Configuration,DC=\<*root domain*\> の下に Microsoft Exchange コンテナーが作成されます (存在しない場合)。

  - また、CN=\<*organization name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> の下に次のコンテナーとオブジェクトが作成されます (存在しない場合)。
    
      - CN=Address Lists Container
    
      - CN=AddressBook Mailbox Policies
    
      - CN=Addressing
    
      - CN=Administrative Groups
    
      - CN=Approval Applications
    
      - CN=Auth Configuration
    
      - CN=Availability Configuration
    
      - CN=Client Access
    
      - CN=Connections
    
      - CN=ELC Folders Container
    
      - CN=ELC Mailbox Policies
    
      - CN=ExchangeAssistance
    
      - CN=Federation
    
      - CN=Federation Trusts
    
      - CN=Global Settings
    
      - CN=Hybrid Configuration
    
      - CN=Mobile Mailbox Policies
    
      - CN=Mobile Mailbox Settings
    
      - CN=Monitoring Settings
    
      - CN=OWA Mailbox Policies
    
      - CN=Provisioning Policy Container
    
      - CN=Push Notification Settings
    
      - CN=RBAC
    
      - CN=Recipient Policies
    
      - CN=Remote Accounts Policies Container
    
      - CN=Retention Policies Container
    
      - CN=Retention Policy Tag Container
    
      - CN=ServiceEndpoints
    
      - CN=System Policies
    
      - CN=Team Mailbox Provisioning Policies
    
      - CN=Transport Settings
    
      - CN=UM AutoAttendant Container
    
      - CN=UM DialPlan Container
    
      - CN=UM IPGateway Container
    
      - CN=UM Mailbox Policies
    
      - CN=Workload Management Settings

  - CN=Transport Settings,CN=\<*Organization Name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> の下に次のコンテナーとオブジェクトが作成されます (存在しない場合)。
    
      - CN=Accepted Domains
    
      - CN=ControlPoint Config
    
      - CN=DNS Customization
    
      - CN=Interceptor Rules
    
      - CN=Malware Filter
    
      - CN=Message Classifications
    
      - CN=Message Hygiene
    
      - CN=Rules
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - Active Directory の構成パーティション全体にアクセス許可が設定されます。

  - Rights.ldf ファイルがインポートされます。このファイルは、Exchange のインストールと Active Directory の構成に必要なアクセス許可を追加します。

  - フォレストのルート ドメインに MicrosoftExchange セキュリティ グループ組織単位 (OU) が作成され、それにアクセス許可が割り当てられます。

  - Microsoft Exchange セキュリティ グループ OU 内に次の管理役割グループが作成されます (存在しない場合)。
    
      - Compliance Management
    
      - Delegated Setup
    
      - Discovery Management
    
      - Help Desk
    
      - Hygiene Management
    
      - Organization Management
    
      - Public Folder Management
    
      - Recipient Management
    
      - Records Management
    
      - Server Management
    
      - UM Management
    
      - View-Only Organization Management

  - MicrosoftExchange セキュリティ グループ OU 内に作成された新しい管理役割グループ (Active Directory にはユニバーサル セキュリティ グループとして表示される) が、CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> コンテナーに保存された **otherWellKnownObjects** 属性に追加されます。

  - ルート ドメインの Microsoft Exchange システム オブジェクト コンテナーにユニファイド メッセージング音声発信者の連絡先が作成されます。

  - *PrepareAD* コマンドが実行されたドメインが Exchange 2013 に使用できるようになります。Exchange 用の Active Directory ドメインの準備方法については、「Active Directory ドメインを準備する」を参照してください。

  - Exchange 組織オブジェクトの **msExchProductId** プロパティが設定されます。Active Directory スキーマが正常に拡張されたことを確認するには、このプロパティ内に保存された値をチェックします。プロパティ内の値が、インストールした Exchange 2013 のリリースの列挙されたスキーマ バージョンと一致していれば、スキーマの拡張が成功しています。Exchange リリースの一覧とこのプロパティ値のチェック方法については、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」の「[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照してください。

## Active Directory ドメインを準備する

Active Directory を Exchange 用に準備するための最後の手順は、Exchange サーバーがインストールされる、または、メールボックスを使用できるユーザーが配置されるすべての Active Directory ドメインを準備することです。この手順は、*PrepareAD* コマンドが実行されたドメイン内で自動的に実行されます。

Active Directory ドメインに加えられる変更は次のとおりです。

  - Active Directory 内のルート ドメイン パーティション内に Microsoft Exchange システム オブジェクト コンテナーが作成されます (存在しない場合)。

  - Microsoft Exchange システム オブジェクト コンテナー上で、Exchange サーバー、Organization Management セキュリティ グループ、および Authenticated Users セキュリティ グループに対するアクセス許可が設定されます。

  - 現在のドメイン内に Exchange Install Domain Servers ドメイン グローバル グループが作成され、Microsoft Exchange システム オブジェクト コンテナーに配置されます。

  - Exchange Install Domain Servers グループがルート ドメイン内の Exchange Servers USG に追加されます。

  - Exchange Servers USG と Organization Management USG に対するアクセス許可がドメイン レベルで割り当てられます。

  - DC=\<*root domain*\> の下にある Microsoft Exchange システム オブジェクト コンテナーの **objectVersion** プロパティが設定されます。Active Directory スキーマが正常に拡張されたことを確認するには、このプロパティ内に保存された値をチェックします。プロパティ内の値が、インストールした Exchange 2013 のリリースの列挙されたスキーマ バージョンと一致していれば、スキーマの拡張が成功しています。Exchange リリースの一覧とこのプロパティ値のチェック方法については、「[Active Directory とドメインを準備する](prepare-active-directory-and-domains-exchange-2013-help.md)」の「[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)」を参照してください。

