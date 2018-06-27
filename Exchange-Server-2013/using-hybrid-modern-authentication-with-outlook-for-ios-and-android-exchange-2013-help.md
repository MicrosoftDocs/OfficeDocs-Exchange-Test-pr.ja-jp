---
title: 'Using hybrid Modern Authentication with Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Using hybrid Modern Authentication with Outlook for iOS and Android
ms:assetid: 0e701643-1f18-4cc3-8595-4fd4b15caf6c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt846639(v=EXCHG.150)
ms:contentKeyID: 74520284
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Using hybrid Modern Authentication with Outlook for iOS and Android

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2018-04-19_

**概要**:オンプレミスのメールボックスの移動を管理する iOS および Android 用の Outlook のサポートを有効にするために、管理者がハイブリッド先進認証および Enterprise Mobility + Security の各機能を Exchange のオンプレミス メールボックスに展開する方法。

iOS および Android 用の Outlook アプリは、Microsoft サービスを利用して毎日の生活や仕事を検索、計画、および優先順位付けするために、モバイル デバイスで Office 365 を活用する最良の方法として設計されています。Outlook は、Azure Active Directory の条件付きアクセスおよび Intune アプリ保護ポリシーなどの機能を使用して、会社のデータを保護している間必要となるセキュリティ、プライバシー、およびサポートを提供します。次のセクションは、ハイブリッド先進認証アーキテクチャの概要を示します。展開に必要な前提条件や、iOS および Android 用の Outlook を Exchange のオンプレミス メールボックスに安全に展開する方法について説明します。

## ハイブリッド Exchange Server 利用者向けの Microsoft Cloud アーキテクチャ

iOS および Android 用の Outlook は、クラウドベースのアプリケーションです。つまり、ユーザーが操作するのはローカルにインストールされたアプリですが、Microsoft Cloud で実行されている安全で拡張性のあるサービスを利用して実行されています。

Exchange Server のメールボックスでは、iOS および Android 用の Outlook の新しいアーキテクチャは従来のアーキテクチャと同様の設計を使用しています。ただし、サービスが Microsoft Cloud (Office 365 と Microsoft Azure を使用) に直接組み込まれるようになったため、お客様は [Office 365 セキュリティ センター](https://products.office.com/business/office-365-trust-center-welcome)および[Azure セキュリティ センター](https://www.microsoft.com/trustcenter/cloudservices/azure)で Microsoft が取り組んでいるセキュリティ、プライバシー、組み込みコンプライアンス、および透明性のある運用などの他のメリットを経験できます。

![iOS および Android 用の Outlook でのハイブリッド先進認証のアーキテクチャ図](images/Mt846639.20a7e963-916d-47e0-bffb-4d86c4777bea(EXCHG.150).png "iOS および Android 用の Outlook でのハイブリッド先進認証のアーキテクチャ図")

Exchange Online から Outlook アプリに渡されるデータは、TLS によって保護された接続を通して渡されます。Azure で実行されているプロトコル トランスレーターは、データ、コマンド、および通知をルーティングしますが、データ自体を読み取ることはできません。

Exchange Online とオンプレミス環境間の Exchange ActiveSync 接続を使用すると、ユーザーのオンプレミス データを同期でき、それには 4 週間分のメール、すべての予定表データ、すべての連絡先データ、Exchange Online テナントの不在時のステータスが含まれます。このデータは、Azure Active Directory でアカウントが削除されてから 30 日後に Exchange Online から自動的に削除されます。

オンプレミス環境と Exchange Online 間でのデータの同期は、ユーザーの動作とは関係なく行われます。これにより、新しいメッセージをデバイスに高速で送信できます。

Microsoft Cloud で情報を処理すると、優先受信トレイでのメールの分類、旅行と予定表のカスタマイズされたエクスペリエンス、および高速な検索などの高度な機能を利用できます。負荷の高い処理にクラウドを利用し、ユーザーのデバイスで必要となるリソースを最小限に抑えることによって、アプリのパフォーマンスと安定性が向上します。最後に、基になっているサーバー (さまざまなバージョンの Exchange Server や Office 365 など) の技術的な機能に関係なく、すべてのメール アカウントで動作する機能を Outlook で構築できます。

具体的には、新しいアーキテクチャでは次の機能が強化されました。

1.  **Enterprise Mobility + Security のサポート**:お客様は Microsoft Intune および Azure Active Directory Premium を含む Microsoft Enterprise Mobility + Security (EMS) を活用して、条件付きアクセスや Intune アプリ保護ポリシーを有効にし、モバイル デバイス上で会社のメッセージ データを制御し保護できます。

2.  **Microsoft Cloud による機能強化**:オンプレミスのメールボックス データは Exchange Online に同期され、[Office 365 セキュリティ センター](https://products.office.com/business/office-365-trust-center-welcome)で Microsoft が取り組んでいるセキュリティ、プライバシー、組み込みコンプライアンス、および透明性のある運用などのメリットを提供します。

3.  **OAuth によるユーザーのパスワードの保護**:Outlook ではハイブリッド先進認証 (OAuth) を使ってユーザーの資格情報を保護します。ハイブリッド先進認証は、ユーザーの資格情報を変更したり保存したりすることなく、Exchange データにアクセスするためのセキュリティで保護されたメカニズムを Outlook に提供します。サインイン時に、ユーザーは ID プラットフォーム (Azure Active Directory または ADFS などのオンプレミス ID プロバイダー) に対して直接認証を行い、代わりに、Outlook でユーザーのメールボックスまたはファイルにアクセスできるようアクセス トークを受け取ります。すぐにサービスでユーザーのパスワードにアクセスできるようになります。

4.  **固有のデバイス ID の提供**:Outlook の各接続は、Microsoft Intune で一意に登録されるため、一意の接続として管理できます。

5.  **iOS および Android の新機能のロック解除**:この更新プログラムにより、Exchange Online の全文検索や優先受信トレイの利用など、現在 Exchange オンプレミスではサポートされていない Office 365 のネイティブ機能を Outlook アプリで利用できます。これらの機能は、iOS および Android 用の Outlook を使用する場合にのみ使用できます。


> [!NOTE]
> オンプレミスの Exchange 管理センター経由でデバイスを管理することはできません。モバイル デバイスを管理するには、Intune が必要です。



## データのセキュリティ、アクセス、および監査の制御

オンプレミス データが Exchange Online と同期されているため、Exchange Online でデータがどのように保護されているかについてお客様から質問があげられています。ホワイト ペーパー「[Encryption in the Microsoft Cloud](http://aka.ms/office365ce)」は、BitLocker がボリュームレベルの暗号化に使用される方法を取り上げています。ホワイト ペーパーで取り上げられている顧客キー オプションを使ったサービスの暗号化は iOS および Android 用の Outlook アーキテクチャでサポートされていますが、暗号化ポリシーが割り当てられるには、ユーザーには Office 365 Enterprise E5 ライセンス (または政府機関向けまたは教育機関向けのそれらのプランに対応するバージョン) が必要です。

既定では、Microsoft のエンジニアには継続的な管理者権限も、Office 365 の顧客コンテンツへのアクセス権もありません。ホワイト ペーパー「[Office 365 Administrative Access Controls](http://aka.ms/office365aac)」は、個人調査、背景の確認、ロックボックスおよびカスタマー ロックボックスなどについて取り上げています。

[サービス アシュアランスの ISO 監査対象のコントロール](https://sip.protection.office.com/)に関するドキュメントは、Office 365 によって実装されたグローバル情報のセキュリティ標準および規制からの監査対象のコントロールの状態について説明します。

## 接続フロー

ハイブリッド先進認証によって iOS および Android 用の Outlook が有効にされている場合、接続フローは次のとおりです。

![ハイブリッド先進認証での認証フロー](images/Mt846639.d6e20ddb-cf8e-4154-8a17-95657ef696d1(EXCHG.150).png "ハイブリッド先進認証での認証フロー")

1.  ユーザーがメール アドレスを入力すると、iOS および Android 用の Outlook が AutoDetect サービスに接続されます。AutoDetect は、AutoDiscover クエリを Exchange Online に初期化することによって、メールボックスの種類を判断します。Exchange Online はユーザーのメールボックスがオンプレミスであると判断し、オンプレミス Autodiscover URL を使って AutoDetect に 302 リダイレクトを返します。AutoDetect はオンプレミス AutoDiscover サービスに対するクエリを開始して、メール アドレスの ActiveSync エンドポイントを決定します。URL 試行オンプレミスは、https://autodiscover.contoso.com/autodiscover/autodiscover.json?Email=test%40contoso.com\&Protocol=activesync\&RedirectCount=3 の例と類似しています。

2.  AutoDetect は、上記のステップ 1 で空のベアラー チャレンジによって返されたオンプレミス ActiveSync URL への接続を開始します。空のベアラー チャレンジは、クライアントが先進認証をサポートしていることをオンプレミス ActiveSync に知らせます。オンプレミス ActiveSync は、401 チャレンジ応答で応答し、*WWW-Authenticate:Bearer* ヘッダーを含めます。WWW-Authenticate:Bearer ヘッダーは、OAuth トークンを取得するのに使用する必要のある Azure Active Directory (AAD) エンドポイントを識別する authorization\_uri 値です。

3.  AutoDetect は AAD エンドポイントをクライアントに返します。クライアントがログイン フローを開始すると、Web フォームが表示され (または Microsoft Authenticator アプリにリダイレクトされ)、資格情報を入力できます。ID の構成によっては、オンプレミスの ID プロバイダーへのフェデレーション エンドポイント リダイレクトは含まれない場合があります。最終的に、クライアントは AT1/RT1 という名前のアクセス トークンと更新トークンのペアを取得します。このアクセス トークンのスコープは、Exchange Online エンドポイントの対象ユーザーが存在する iOS および Android 用の Outlook クライアントです。

4.  iOS および Android 用の Outlook は、ステートレス プロトコル トランスレーターへの接続を確立します。このトランスレーターで、クライアントの専用デバイス プロトコルが Exchange Online で認識できるプロトコルに変換されます。

5.  プロビジョニング要求が Exchange Online に渡されます。これには、ユーザーのアクセス トークン (AT1) と、オンプレミスの ActiveSync エンドポイントが含まれます。

6.  Exchange Online 内の MRS プロビジョニング API は入力として AT1 を利用し、2 番目のアクセス トークンと更新トークンのペア (名前は AT2/RT2) を取得して、Azure Active Directory への代理呼び出しによってオンプレミスのメールボックスにアクセスします。この 2 番目のアクセス トークンのスコープは、Exchange Online であるクライアントと、オンプレミスの ActiveSync 名前空間エンドポイントの対象ユーザーです。

7.  メールボックスがプロビジョニングされていない場合、プロビジョニング API によりメールボックスが作成されます。

8.  MRS プロビジョニング API は、オンプレミスの ActiveSync エンドポイントに対してセキュリティで保護された接続を確立し、AT2 アクセス トークンを認証方法として使用して、ユーザーのメッセージング データを同期します。ユーザーが操作しなくてもバックグラウンドでデータを同期できるように、RT2 が定期的に使用されて新しい AT2 が生成されます。

## 技術要件とライセンス要件

ハイブリッド先進認証アーキテクチャには、次の技術要件があります。

1.  **Exchange On-Premises のセットアップ**:
    
      - すべての Exchange サーバーで、Exchange Server 2016 CU8 または Exchange Server 2013 CU19 以上の累積的な更新プログラム (CU) が展開されている必要があります。Exchange がオンプレミスとクラウドに展開されているハイブリッド展開のお客様や、オンプレミスの Exchange 展開で Exchange Online Archiving (EOA) を使用しているお客様は、最新の CU かその 1 つ前の CU を展開する必要があることにご注意ください。
    
      - Exchange 2007 サーバーや Exchange 2010 サーバーは、環境からすべて削除する必要があります。Exchange Server 2010 SP3 はメインストリーム サポートの対象外となっており、Intune で管理される iOS および Android 用の Outlook では動作しません。このアーキテクチャでは、iOS および Android 用の Outlook は認証方法として OAuth を使用します。行われるオンプレミス構成変更の 1 つにより、既定の承認エンドポイントとして Microsoft Cloud に対する OAuth エンドポイントが有効になります。この変更により、クライアントは OAuth の使用をネゴシエーションできるようになります。これは組織全体に関わる変更であるので、Exchange 2013 または 2016 によってアクセスされる Exchange 2010 メールボックスは OAuth を実行できると誤って認識し、接続が切断された状態になります。これは、Exchange 2010 では、認証方法として OAuth がサポートされていないためです。

2.  **Active Directory の同期**Azure Active Directory を使用して、Azure AD Connect 経由でオンプレミス ディレクトリ全体の Active Directory 同期を実行します。次の属性が同期されることを確認する必要があります。
    
      - Office 365 ProPlus
    
      - Exchange Online
    
      - Exchange ハイブリッドのライトバック
    
      - Azure RMS
    
      - Intune

3.  **Exchange ハイブリッドのセットアップ**:Exchange On-Premises と Exchange Online との間に完全なハイブリッド関係が必要です。
    
      - ハイブリッドの Office 365 テナントは完全なハイブリッド構成モードで構成されており、「[Exchange Server 展開アシスタント](http://technet.microsoft.com/exdeploy)」で指定されているとおりにセットアップされます。
    
      - Office 365 Enterprise、Business、Education のいずれかのテナントが必要です。
    
      - オンプレミスのメールボックス データは、Office 365 テナントがセットアップされるのと同じデータセンター リージョンで同期されます。Office 365 のデータ保存場所の詳細については、Office 365 セキュリティ センターの「[データの保存場所](http://o365datacentermap.azurewebsites.net/)」セクションをご覧ください。
    
      - Office 365 US Government Community テナント、US Government Defense テナント、Office 365 Germany テナント、21Vianet が運用する Office 365 China テナントの使用はサポートされていません。
    
      - Exchange ActiveSync および AutoDiscover の外部 URL ホスト名は、Azure Active Directory に対するサービス プリンシパルとして、ハイブリッド構成ウィザードから発行される必要があります。
    
      - AutoDiscover 名前空間と Exchange ActiveSync 名前空間は、インターネットからアクセスできる必要があり、事前認証ソリューションによるアクセスは許可されません。
    
      - ロード バランサーと Exchange サーバーの間で SSL オフロードや TLS オフロードが使用されていないことを確認します。使用されていると、OAuth トークンの使用に影響します。SSL ブリッジと TLS ブリッジ (終了と再暗号化) はサポートされています。

4.  **Intune のセットアップ**:Intune は、クラウドのみの展開とハイブリッド展開の両方がサポートされています (Office 365 用 MDM はサポート対象外)。

5.  **Office 365 のライセンス\***:ユーザーごとに次の Office 365 のライセンスのいずれかが必要です。
    
      - 商用:Enterprise E3、Enterprise E5、ProPlus、または Business ライセンス
    
      - 政府機関:U.S.Government Community G3、U.S.Government Community G5
    
      - 教育機関:Office 365 Education E3、Office 365 Education E5
    
    さらに、上記のライセンスに、iOS および Android 用の Outlook を商用利用するのに必要な Office クライアント アプリケーションを含める必要があります。

6.  **EMS のライセンス\***:オンプレミスのユーザーごとに次のライセンスのいずれかが必要です。
    
      - Intune スタンドアロン + Azure Active Directory Premium スタンドアロン
    
      - Enterprise Mobility + Security E3、Enterprise Mobility + Security E5

**\*** Microsoft Secure Productive Enterprise (SPE) には、Office 365 および EMS に必要なすべてのライセンスが含まれています。

## 実装の手順

組織でハイブリッド先進認証のサポートを有効にするには、次の手順を実行する必要があります。詳細については、以降のセクションで説明します。

1.  条件付きアクセス ポリシーを作成する

2.  Intune アプリ保護ポリシーを作成する

3.  ハイブリッド先進認証を有効にする

4.  Microsoft に問い合わせる

## 条件付きアクセス ポリシーを作成する

エンドユーザー用の電子メール アプリとして iOS および Android 用の Outlook のみを使用し、ユーザーが Exchange データにアクセスする方法を標準化することを組織で決定した場合は、他のモバイル アクセス方法をブロックする条件付きアクセス ポリシーを構成できます。iOS および Android 用の Outlook は、Azure Active Directory の ID オブジェクト経由で認証して Exchange Online に接続します。したがって、Azure Active Directory の条件付きアクセス ポリシーを作成し、モバイル デバイスによる Exchange Online への接続を制限する必要があります。これを行うには、それぞれ使用する可能性のあるすべてのユーザーを対象にした 2 つの条件付きアクセス ポリシーが必要です。これらのポリシーの作成の詳細については「[Azure Active Directory アプリベースの条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-mam#exchange-online-policy)」を参照してください。

1.  最初のポリシーは、iOS および Android 用の Outlook を許可し、OAuth 対応 Exchange ActiveSync クライアントによる Exchange Online への接続はブロックします。「手順 1 - Exchange Online 用の Azure AD 条件付きアクセス ポリシーを構成する」を参照してください。

2.  2 番目のポリシーは、Exchange ActiveSync クライアントが基本認証を活用して Exchange Online に接続するのを防ぎます。「手順 2 - Active Sync (EAS) を使用する Exchange Online 用の Azure AD 条件付きアクセス ポリシーを構成する」を参照してください。

ポリシーは、[承認されたクライアント アプリの要件](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference)の制御の付与を活用し、これにより、Intune SDK を統合している Microsoft アプリだけにアクセスを許可します。


> [!IMPORTANT]
> アプリベースの条件付きアクセス ポリシーを活用するには、iOS デバイスに Microsoft Authenticator アプリをインストールする必要があります。Android デバイスには、Intune ポータル サイト アプリを利用します。詳細については、「<A href="https://docs.microsoft.com/intune/app-based-conditional-access-intune">Intune でのアプリベースの条件付きアクセス</A>」を参照してください。



他のモバイル デバイス クライアント (モバイル オペレーティング システムに含まれているネイティブ メール クライアントなど) が (オンプレミスの Active Directory に対して基本認証で認証する) オンプレミスの環境に接続できないようにブロックするには、次の 2 つのオプションがあります。

1.  組み込みの Exchange モバイル デバイス アクセス ルールを利用して、Exchange 管理シェルで次を設定することにより、すべてのモバイル デバイスが接続できないようにブロックできます。
    
        Set-ActiveSyncOrganizationSettings -DefaultAccessLevel Block

2.  オンプレミスの Exchange Connector をインストールした後で、オンプレミスの条件付きアクセス ポリシーを Intune 内で利用できます。詳細については、「[Exchange On-Premises と従来の Exchange Online Dedicated の条件付きアクセス ポリシーを作成する](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access)」を参照してください。


> [!NOTE]
> 上記のオンプレミスのオプションのいずれかを実装する場合、モバイル デバイスで Exchange に接続するユーザーに影響を及ぼす可能性があることにご注意ください。



## Intune アプリ保護ポリシーを作成する

ハイブリッド先進認証を有効にすると、オンプレミスのモバイル ユーザーは全員、Office 365 ベースのアーキテクチャを使用して iOS および Android 用の Outlook を利用できます。そのため、Intune アプリ保護ポリシーを使用して会社のデータを保護することが重要です。

「[アプリ保護ポリシーを作成して割り当てる方法](https://docs.microsoft.com/intune/app-protection-policies)」で説明されている手順を使用して、iOS と Android 両方の Intune アプリ保護ポリシーを作成する必要があります。少なくとも、各ポリシーに次のものが含まれている必要があります。

1.  Word、Excel、PowerPoint などすべての Microsoft モバイル アプリケーションを含み、ユーザーは安全な方法で任意の Microsoft アプリ内で会社のデータにアクセスし、操作できる。

2.  Exchange がモバイル デバイスに対して提供する次のようなセキュリティ機能を模倣する。
    
      - アクセスに PIN を要求する (種類の選択、PIN の長さ、単純な PIN を許可する、指紋を要求する、など)
    
      - アプリのデータを暗号化する
    
      - 脱獄およびルート化されたデバイスで管理対象アプリが実行されないようにブロックする

3.  すべてのユーザーに割り当てられる。これにより、iOS および Android 用の Outlook を使用しているかどうかに関係なくすべてのユーザーを保護することができる。

上記の最低限のポリシー要求に加えて、**他のアプリへの切り取り、コピー、貼り付けを制限する**などの高度な保護ポリシーの設定を展開して、会社のデータの漏洩をよりしっかり防ぐことを考慮する必要があります。利用可能な設定の詳細については、「[Microsoft Intune の Android アプリ保護ポリシー設定](https://docs.microsoft.com/intune/app-protection-policy-settings-android)」と「[iOS アプリ保護ポリシー設定](https://docs.microsoft.com/intune/app-protection-policy-settings-ios)」を参照してください。


> [!IMPORTANT]
> Intune に登録していない Android デバイスでアプリに対して Intune App Protection ポリシーを適用するには、Intune ポータル サイトもインストールする必要があります。詳細については、「<A href="https://docs.microsoft.com/ja-jp/intune/app-protection-enabled-apps-android">アプリ保護ポリシーを使用して Android アプリを管理するときの注意点</A>」を参照してください。



## ハイブリッド先進認証を有効にする

ハイブリッド先進認証を有効にしていない場合は、「[ハイブリッドの先進認証の概要、およびオンプレミスの Skype for Business と Exchange サーバーで使用するための前提条件](https://support.office.com/article/hybrid-modern-authentication-overview-and-prerequisites-for-using-it-with-on-premises-skype-for-business-and-exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d?)」で説明されている手順を確認し実装します。

「[Exchange Server オンプレミスを構成してハイブリッド先進認証を使用する方法](https://support.office.com/article/how-to-configure-exchange-server-on-premises-to-use-hybrid-modern-authentication-cef3044d-d4cb-4586-8e82-ee97bd3b14ad?)」で説明されているとおりにハイブリッド先進認証を有効にして、Outlook for Mac などの他のバージョンの Outlook をオンプレミスのユーザーに対してサポートしている場合は、あといくつかの手順を実行するだけで済みます。

1.  Exchange デバイスのアクセス許可ルールを作成し、Exchange Online が ActiveSync プロトコルを使用して、オンプレミスの環境に接続できるようにします。
    
        If ((Get-ActiveSyncOrganizationSettings).DefaultAccessLevel -ne "Allow") {New-ActiveSyncDeviceAccessRule -Characteristic DeviceType -QueryString "OutlookService" -AccessLevel Allow}
    
    オンプレミスの Exchange 管理センター経由では、デバイスを管理できないことにご注意ください。モバイル デバイスを管理するには、Intune が必要です。

2.  Exchange ActiveSync プロトコルでは iOS および Android 用の Outlook によるオンプレミスの環境への基本認証を使用したユーザー接続を行えないようにする、Exchange デバイス アクセス ルールを作成します。
    
        New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
    

    > [!NOTE]
    > このルールを作成すると、基本認証で iOS および Android 用の Outlook を使用しているユーザーがブロックされます。



3.  EAS maxRequestLength が、トランスポート構成の MaxSendSize/MaxReceiveSize と一致するように構成されていることを確認します。
    
      - パス: `%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config`
    
      - プロパティ: `maxRequestLength`
    
      - 値: KB サイズで設定 (10 MB は 10240 など)

## Microsoft に問い合わせる

iOS および Android 用の Outlook でハイブリッド先進認証のサポートを有効にするには、Microsoft アカウント チーム、カスタマー セールス & サービス (CSS) コンタクト、またはお客様のテクニカル アカウント マネージャーにお問い合わせください。すべての SMTP ドメイン (UPN ドメインが SMTP アドレスと一致しない場合は UPN ドメインも) を提供する必要があります。ドメインが提供され有効になると、iOS および Android 用の Outlook を使用するオンプレミスのメールボックスでハイブリッド先進認証がサポートされるようになります。

## サポートされていないクライアント機能

iOS および Android 用の Outlook でハイブリッド先進認証を使用するオンプレミスのメールボックスでは、次の機能はサポートされていません。

  - 下書きフォルダーと下書きメッセージの同期

  - 共有の予定表へのアクセスと代理人の予定表へのアクセス

  - Cortana 出発時刻

  - 予定表の添付ファイル

  - Microsoft To-Do を使用したタスク管理

## 接続フローに関する FAQ

**Q**:組織で、許可されている IP アドレスか FQDN にインターネットの受信接続を制限する必要のあるセキュリティ ポリシーを採用しています。このアーキテクチャでも同じことができますか。

**A**:Microsoft では、AutoDiscover プロトコルと ActiveSync プロトコル用のオンプレミスのエンドポイントが、インターネットに対して開かれており、インターネットから制限なくアクセス可能であることを推奨しています。特定の状況では、それができない場合があります。たとえば、別の MDM ソリューションが共存する期間には、お客様が Intune や iOS および Android 用の Outlook に移行する間、ActiveSync プロトコルに制限を設定し、ユーザーがサード パーティの MDM ソリューションをバイパスできないようにする必要がある場合があります。オンプレミスのファイアウォールまたはゲートウェイのエッジ デバイスに制限を設定する必要がある場合、FQDN エンドポイントに基づくフィルター処理をお勧めします。FQDN エンドポイントが使用できない場合は、IP アドレスでフィルター処理します。次の IP サブネットと FQDN がホワイトリストに登録されていることを確認します。

  - 「[Office 365 URL および IP アドレス範囲](https://support.office.com/article/office-365-urls-and-ip-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」で定義されているすべての Exchange Online URL および IP サブネット範囲。

  - 「[Office 365 ProPlus およびモバイルでのネットワーク要求](https://support.office.com/article/network-requests-in-office-365-proplus-and-mobile-eb73fcd1-ca88-4d02-a74b-2dd3a9f3364d?)」で定義されているすべての Outlook iOS および Android アプリ FQDN。

  - 「[Microsoft Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653)」で定義されているすべての Azure US および EUR データセンター リージョン IP サブネット。「接続フロー」で概説されているように AutoDetect サービスがオンプレミスのインフラストラクチャへの接続を確立するために、これが必要になります。現時点では、AutoDetect サービスは Azure 内で IP 予約を利用しません。

**Q**:組織で、モバイル デバイスの接続を管理するサード パーティの MDM ソリューションが使用されています。Exchange ActiveSync 名前空間をインターネットに公開すると、ユーザーは、共存期間中にサード パーティの MDM ソリューションをバイパスすることができるようになります。これを防ぐにはどうすればよいですか。

**A**:この問題を解決するために使用可能なソリューションは 3 つあります。

1.  接続を承認されるデバイスを制御する Exchange モバイル デバイス アクセス ルールを実装します。

2.  一部のサード パーティの MDM ソリューションは、Exchange モバイル デバイス アクセス ルールと統合して未承認のアクセスをブロックする一方、承認されたデバイスをユーザーの ActiveSyncAllowedDeviceIDs プロパティに追加します。

3.  Exchange ActiveSync 名前空間に IP 制限を実装します。

**Q**:Microsoft Cloud とオンプレミスの環境の間のトラフィックを管理する目的で Azure ExpressRoute を利用できますか。

**A**:Microsoft Cloud に接続するにはインターネット接続が必要です。ただし、Office 365 ネットワーク トラフィックのサブセットは、Azure ExpressRoute 経由でルーティングされる場合があります。詳細については、「[Office 365 向け Azure ExpressRoute](https://support.office.com/article/azure-expressroute-for-office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)」を参照してください。

ExpressRoute には、ExpressRoute 接続用のプライベート IP 領域も、"プライベート" な DNS 解決もありません。このため、会社が ExpressRoute で使用するすべてのエンドポイントは、パブリック DNS で解決される必要があります。エンドポイントが、ExpressRoute 回線に関連付けられているアドバタイズされたプレフィックスに含まれている IP に解決される場合 (ExpressRoute 接続で Microsoft ピアリングを有効にする場合、その会社はこれらのプレフィックスを Azure Portal で構成する必要があります)、Exchange Online からオンプレミス環境への送信接続は ExpressRoute 回線を経由します。会社は、これらの接続に関連付けられているリターン トラフィックが (非対称ルーティングを回避して) ExpressRoute 回線を経由することを確認する必要があります。


> [!NOTE]
> 会社は、ExpressRoute 回線内のアドバタイズされたプレフィックスに Exchange ActiveSync 名前空間を追加することになるので、Exchange ActiveSync エンドポイントに到達する唯一の方法は ExpressRoute 経由になります。つまり、ActiveSync 名前空間経由でオンプレミスに接続できる唯一のモバイル デバイスは、iOS および Android 用の Outlook になります。他のすべての ActiveSync クライアント (モバイル デバイスのネイティブ メール クライアントなど) は、Microsoft Cloud から接続が確立されないので、オンプレミス環境には接続できません。これは、ExpressRoute 回線で Microsoft にアドバタイズされるパブリック IP 領域と、使用しているインターネット回線でアドバタイズされるパブリック IP 領域とが一切重複していないためです。



**Q**:4 週間分のメッセージ データのみが Exchange Online に同期される場合、iOS および Android 用の Outlook で実行される検索クエリはそのローカル デバイス上で利用可能なデータ以上の情報は返せないということになりますか。

**A**:iOS および Android 用の Outlook で検索クエリが実行されると、検索クエリに一致し、そのデバイス上にあるアイテムが返されます。また、検索クエリは Exchange Online 経由で Exchange On-Premises に渡されます。Exchange On-Premises は、オンプレミスのメールボックスに対して検索クエリを実行し、結果を Exchange Online に返します。その結果を、Exchange Online がクライアントにリレーします。オンプレミスのクエリ結果は、Exchange Online に 1 日保存されてから削除されます。

**Q**:iOS および Android 用の Outlook にメール アカウントが正常に追加されたか、どうすれば確認できますか。

**A**:ハイブリッド先進認証を介して追加されたオンプレミスのメールボックスには、iOS および Android 用の Outlook のアカウント設定で、以下の例に示すような **\[Exchange (ハイブリッド)\]** というラベルが付けられます。

![ハイブリッド先進認証のために構成された iOS および Android 用の Outlook のアカウントの例](images/Mt846639.79887a65-e5e1-4501-a274-008393dbb6c9(EXCHG.150).png "ハイブリッド先進認証のために構成された iOS および Android 用の Outlook のアカウントの例")

## 認証に関する FAQ

**Q**:ハイブリッド先進認証と iOS および Android 用の Outlook ではどのような ID 構成がサポートされますか。

**A**:ハイブリッド先進認証では、Azure Active Directory を使用した以下の ID 構成がサポートされています。

  - Azure Active Directory でサポートされている任意のオンプレミス ID プロバイダーが指定されたフェデレーション ID

  - Azure Active Directory Connect を介したパスワード ハッシュ同期

  - Azure Active Directory Connect を介したパススルー認証

**Q:** iOS および Android 用の Outlook ではどのような認証メカニズムが使用されていますか。Office 365 に資格情報は格納されますか。

**A:** iOS および Android 用の Outlook は、Active Directory 認証ライブラリ (ADAL) ベースの認証を使用して、Exchange Online と同期されているオンプレミスのメールボックス データにアクセスします。ADAL 認証はデスクトップ版とモバイル デバイス版の両方の Office アプリで使用され、この認証ではユーザーは Outlook に資格情報を提供する代わりに、Office 365 の ID プロバイダーである Azure Active Directory に直接サインインします。

ADAL ベースのサインインにより、ハイブリッド Exchange オンプレミス アカウントに対して OAuth が有効になり、ユーザー資格情報へのアクセスなしで電子メールにアクセスするためのセキュリティで保護されたメカニズムが iOS および Android 用の Outlook に提供されます。サインイン時に、ユーザーは直接 Microsoft クラウドで認証を受け、アクセス トークンを受け取ります。このトークンにより、該当するメールボックスへのアクセス権が iOS および Android 用の Outlook に付与されます。OAuth は、ユーザー資格情報を必要とすることも格納することもなく、Office 365 と Outlook クラウド サービスにアクセスするためのセキュリティで保護されたメカニズムを Outlook に提供します。

詳しくは、「[Outlook for iOS と Outlook for Android の新しいアクセスとセキュリティの制御](https://blogs.office.com/2015/06/10/new-access-and-security-controls-for-outlook-for-ios-and-android/)」を参照してください。

**Q:** iOS および Android 用の Outlook やその他の Microsoft Office モバイル アプリはシングル サインオンをサポートしていますか。

**A:** Azure Active Directory 認証ライブラリ (ADAL) を認証に利用するすべての Microsoft アプリでシングル サインオンがサポートされています。さらに、アプリを Microsoft Authenticator または Microsoft ポータル サイト アプリのいずれかと組み合わせて使用する場合にもシングル サインオンがサポートされます。

次のシナリオでは、トークンを他の Microsoft アプリ (Word モバイルなど) で共有および再利用できます。

1.  それらのアプリが同じ署名証明書によって署名され、同じサービス エンドポイントまたは対象の URL (Office 365 URL など) を使用する場合。この例では、トークンは、アプリ共有ストレージに格納されます。

2.  アプリがブローカー アプリによるシングル サインオンを活用またはサポートしている場合。ブローカー アプリ内にトークンが格納されます。Microsoft Authenticator は、ブローカー アプリの一例です。ブローカー アプリのシナリオでは、iOS および Android 用の Outlook にサインインしようとすると、ADAL によって Microsoft Authenticator アプリが起動されます。これにより、Azure Active Directory への接続が確立され、トークンを取得することができます。次いでトークンは保持され、構成されているトークンの有効期間中に他のアプリからの認証要求があった場合に再利用されます。

詳細については、「[iOS で ADAL を使用してクロス アプリ SSO を有効にする方法](https://docs.microsoft.com/ja-jp/azure/active-directory/develop/active-directory-sso-ios)」を参照してください。

**Q:** iOS および Android 用の Outlook で Active Directory Authentication Library (ADAL) によって生成および使用されるトークンの有効期間とは何のことですか。

**A**:iOS および Android 用の Outlook、Authenticator アプリ、ポータル サイト アプリといった ADAL 対応アプリを通じてオンプレミスのユーザーが認証を受ける場合、複数のトークンが生成されます。最初のアクセス トークンと更新トークンのペアは Exchange Online に同期されるデータにアクセスするために使用され、2 番目のアクセス トークンと更新トークンのペアは、Exchange ActiveSync プロトコル経由でオンプレミスのメールボックスにアクセスするために Exchange Online によって使用されます。アクセス トークンは、リソース (Exchange メッセージ データなど) にアクセスするために使用され、更新トークンは、現在のアクセス トークンの有効期限が切れたときに新しいアクセス トークンまたは更新トークンのペアを取得するために使用されます。

既定では、アクセス トークンの有効期間は 1 時間、更新トークンの有効期間は 14 日間です。これらの値は調整できます。詳細については、「[Azure Active Directory における構成可能なトークンの有効期間](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)」を参照してください。これらの有効期間を短縮することを選択した場合、iOS および Android 用の Outlook のパフォーマンスも低下することにご注意ください。これは、有効期間が短くなると、アプリケーションが新しいアクセス トークンを取得しなければならない回数が増えるためです。

**Q:** ユーザーのパスワードが変更されると、アクセス トークンはどうなりますか。

**A**:以前に付与されたアクセス トークンは、期限が切れるまで有効です。認証で利用する ID モデルは、パスワードの有効期限の処理方法に影響を及ぼします。次の 3 つのシナリオがあります。

1.  フェデレーション ID モデルでは、オンプレミスの ID プロバイダーが Azure Active Directory にパスワードの有効期限要求を送信するようにする必要があります。そうしないと、Azure Active Directory はパスワードの有効期限を処理できません。詳細については、「[パスワードの有効期限要求を送信する AD FS を構成する](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims)」を参照してください。

2.  パスワード ハッシュ同期はパスワードの有効期限をサポートしていません。したがって、以前にアクセス トークンと更新トークンのペアを取得していたアプリは、そのトークンのペアの有効期限を超えるか、ユーザーが自分のパスワードを変更するまで機能し続けます。詳細については、「[Azure AD Connect 同期を使用したパスワード ハッシュ同期の実装](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-hash-synchronization#how-password-synchronization-works)」を参照してください。

3.  パススルー認証では、パスワード ライトバックを AAD Connect で有効にする必要があります。詳細については、「[Azure Active Directory パススルー認証:よく寄せられる質問](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-faq#what-happens-if-my-users-password-has-expired-and-they-try-to-sign-in-by-using-pass-through-authentication)」を参照してください。

トークンの有効期限が切れると、クライアントは更新トークンを使用して新しいアクセス トークンを取得しようとしますが、ユーザーのパスワードが変更されたため、更新トークンは無効になります (オンプレミスと Azure Active Directory の間でディレクトリ同期が発生したと仮定した場合)。更新トークンが無効になると、ユーザーは新しいアクセス トークンと更新トークンのペアを取得するために強制的に再認証させられます。

**Q**:iOS および Android 用の Outlook にユーザーが自分のアカウントを追加するときに、AutoDetect をバイパスする方法はありますか。

**A**:はい。ユーザーはいつでも AutoDetect をバイパスして、Exchange ActiveSync プロトコルで基本認証を使用して接続を手動で構成できます。ユーザーが Azure Active Directory の条件付きアクセスや Intune のアプリ保護ポリシーをサポートしていないメカニズムを使用してオンプレミス環境への接続を確立しないようにするには、オンプレミスの Exchange 管理者が、ActiveSync 接続をブロックする Exchange デバイス アクセス ルールを構成する必要があります。これを行うには、Exchange 管理シェルで次のコマンドを入力します。

``` 
 New-ActiveSyncDeviceAccessRule -Characteristic DeviceModel -QueryString "Outlook for iOS and Android" -AccessLevel Block
```

