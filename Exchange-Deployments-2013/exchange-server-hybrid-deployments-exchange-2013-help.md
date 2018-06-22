---
title: 'Exchange Server のハイブリッド展開: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 48267600
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server のハイブリッド展開

 

_<strong>適用先:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>トピックの最終更新日:</strong>2018-04-16_

**概要**:Exchange ハイブリッド展開を計画する前に把握しておく必要のあること。

ハイブリッド展開により組織は、既存の社内 Microsoft Exchange 組織で実現されている多機能性と管理制御能力をクラウドにまで拡大することができます。ハイブリッド展開は、社内 Exchange 組織と Microsoft Office 365 内の Exchange Online との間が単一の Exchange 組織に見えるシームレスな概観を提供します。さらに、ハイブリッド展開は、Exchange Online 組織へ完全に移行するための中間段階としても機能します。

**目次**

Exchange ハイブリッド展開の機能

Exchange ハイブリッド展開の考慮事項

Exchange ハイブリッド展開のコンポーネント

Exchange ハイブリッド展開の例

Exchange ハイブリッド展開を構成する前の考慮事項

主要な関連用語

Exchange ハイブリッド展開のドキュメント

## Exchange ハイブリッド展開の機能

ハイブリッド展開では次の機能が有効になります。

  - 社内組織および Exchange Online 組織間の安全なメール ルーティング。

  - 共有ドメイン名前空間によるメール ルーティング。たとえば、社内組織と Exchange Online 組織の両方で、SMTP ドメインとして @contoso.com を使用できます。

  - 統一されたグローバル アドレス一覧 (GAL)。"共有アドレス帳" とも呼ばれます。

  - 社内組織と Exchange Online 組織間での空き時間情報や予定表の共有。

  - 受信および送信メール フロー制御の集中管理。すべての受信および送信 Exchange Online メッセージを、社内 Exchange 組織経由でルーティングされるように構成できます。

  - オンプレミスの組織と Exchange Online 組織の両方に対応した単一の Web 上の Outlook URL。

  - 既存の社内メールボックスを Exchange Online 組織に移動する機能。必要な場合に、Exchange Online メールボックスを移動して社内組織に戻すこともできます。

  - 社内 Exchange 管理センター (EAC) を使用した、メールボックスの集中管理。

  - メッセージ追跡、メール ヒント、および社内組織と Exchange Online 組織間での複数のメールボックスの検索。

  - クラウドベースでの社内 Exchange メールボックスのメッセージ アーカイブ。Exchange Online Archiving は、ハイブリッド展開と併用できます。Exchange Online Archiving の詳細については、「[Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=233231)」を参照してください。

## Exchange ハイブリッド展開の考慮事項

Exchange ハイブリッド展開を実装する前に、以下を考慮する必要があります。

  - **ハイブリッド展開の要件** ハイブリッド展開を構成する前に、正常に展開を完了するために必要な前提条件すべてをオンプレミスの組織が満たしていることを確認する必要があります。詳しくは、「[ハイブリッド展開の前提条件](hybrid-deployment-prerequisites-exchange-2013-help.md)」をご覧ください。

  - **Exchange ActiveSync クライアント**  メールボックスをオンプレミスの Exchange 組織から Exchange Online に移動するときに、メールボックスにアクセスするすべてのクライアントが Exchange Online を使うように更新する必要があります。その中には Exchange ActiveSync デバイスが含まれます。メールボックスを Exchange Online に移動する際に、ほとんどの Exchange ActiveSync クライアントは自動的に再構成されるようになりましたが、一部の古いデバイスが正しく更新されないことがあります。詳しくは、「[Exchange ハイブリッド展開での Exchange ActiveSync デバイスの設定](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md)」をご覧ください。

  - **メールボックス アクセス許可の移行**  メールボックスに明示的に適用されるオンプレミスのメールボックス アクセス許可 (メールボックス所有者として送信する、フルアクセス、代理人として送信する、など) およびフォルダー アクセス許可は、Exchange Online に移行されます。継承された (明示的でない) メールボックス アクセス許可と、Exchange Online でメールに対応していないオブジェクトに付与されたアクセス許可は移行されません。すべてのアクセス許可が明示的に付与されていて、すべてのオブジェクトがメールに対応していることを、移行前に確認する必要があります。そのため、自分の組織に該当する場合は、Office 365 でのこれらのアクセス許可の構成を計画する必要があります。送信者のアクセス許可では、送信しようとしているユーザーとリソースが同時に移動されなかった場合、**Add-RecipientPermission** コマンドレットを使用して Exchange Online に送信者のアクセス許可を明示的に追加する必要があります。

  - **クロスプレミスのメールボックス アクセス許可のサポート** Exchange ハイブリッド展開では、オンプレミスの Exchange 組織にあるメールボックスと Office 365 にあるメールボックスとの間で、フル アクセスおよび代理人として送信する権限の使用がサポートされます。送信者アクセス許可には追加の手順が必要です。さらに、オンプレミス組織にインストールされている Exchange のバージョンによっては、クロスプレミス メールボックス アクセス許可をサポートするために追加の構成が必要な場合があります。詳細については、「[Exchange ハイブリッド展開のアクセス許可](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)」の「[メールボックスのアクセス許可の委任](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)」および「[ハイブリッド展開で委任されたメールボックスへのアクセス許可をサポートするように Exchange を構成する](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > フォレスト間のフル アクセス、代理送信、フォルダー権限をサポートする機能は、2018 年 2 月時点では展開中であり、2018 年 4 月までに完了する見込みです。



  - **オフボード**  継続受信者管理の一環として、Exchange Online メールボックスを社内環境に戻さなければならない場合があります。
    
    Exchange 2010 ベースのハイブリッド展開でのメールボックスの移動方法については、「[社内組織への Exchange Online メールボックスの移動](https://technet.microsoft.com/ja-jp/library/hh882527\(v=exchg.150\))」を参照してください。
    
    Exchange 2013 以降におけるハイブリッド展開でのメールボックスの移動方法については、「[ハイブリッド展開においてオンプレミスの組織と Exchange Online 組織間でメールボックスを移動する](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)」をご覧ださい。

  - **メールボックスの転送設定** 送られてきたメールを別のメールボックスに自動的に転送するようにメールボックスを設定できます。Exchange Online では、メールボックスの転送がサポートされていますが、メールボックスを移行する際に、転送構成は Exchange Online にコピーされません。Exchange Online にメールボックスを移行する前に、忘れずに各メールボックスの転送構成をエクスポートしてください。転送構成は、各メールボックスの `DeliverToMailboxAndForward`、`ForwardingAddress`、および `ForwardingSmtpAddress` プロパティに格納されます。

## Exchange ハイブリッド展開のコンポーネント

ハイブリッド展開には、次のようないくつかの種類のサービスおよびコンポーネントが含まれます。

  - **Exchange サーバー**  ハイブリッド展開を構成する場合、オンプレミスの組織で少なくとも 1 つの Exchange サーバーが構成されていることが必要です。Exchange 2013 以前のバージョンを実行している場合、メールボックスとクライアント アクセスの役割を実行するサーバーを少なくとも 1 つインストールする必要があります。Exchange 2016 以降のバージョンを実行している場合、メールボックスの役割を実行するサーバーを、少なくとも 1 つインストールする必要があります。必要に応じて、Exchange エッジ トランスポート サーバーを境界ネットワークにインストールし、Office 365 でのセキュリティ保護されたメール フローをサポートすることもできます。
    

    > [!NOTE]
    > 境界ネットワーク内において、メールボックスやクライアント アクセスのサーバー役割を実行する Exchange サーバーのインストールはサポートされていません。



  - **Microsoft Office 365**   Office 365 サービスには、そのサブスクリプション サービスの一部として Exchange Online 組織が含まれています。ハイブリッド展開を構成する組織では、Exchange Online 組織に移行されるか、その中で作成されるメールボックスごとにライセンスを購入する必要があります。

  - **ハイブリッド構成ウィザード**Exchange には、社内 Exchange 組織および Exchange Online 組織間のハイブリッド展開を効率的に構成するハイブリッド構成ウィザードが含まれています。
    
    詳細については、「[ハイブリッド構成ウィザード](hybrid-configuration-wizard-exchange-2013-help.md)」を参照してください。

  - **Azure AD 認証システム**   Azure Active Directory (AD) 認証システムは、オンプレミスの Exchange 2016 組織と Exchange Online 組織間の信頼ブローカーとして機能する、無料のクラウドベースのサービスです。ハイブリッド展開を構成するオンプレミスの組織には、Azure AD 認証システムとのフェデレーション信頼が必要になります。フェデレーション信頼は、オンプレミスの Exchange 組織とその他のフェデレーション Exchange 組織との間にフェデレーション共有機能を構成する一環として、またはハイブリッド構成ウィザードでハイブリッド展開を構成する一環として、手動で作成できます。Office 365 テナントの Azure AD 認証システムとのフェデレーション信頼は、Office 365 サービス アカウントをアクティブにすると自動的に構成されます。
    
    詳細情報:[Azure AD 認証システム](https://go.microsoft.com/fwlink/p/?linkid=135986)

  - **Azure Active Directory 同期**   Azure AD 同期では、Azure AD Connect を使うことにより、メール対応オブジェクトのオンプレミスの Active Directory 情報が Office 365 組織にレプリケートされ、統一グローバル アドレス リスト (GAL) とユーザー認証がサポートされます。ハイブリッド展開を構成する組織では、Office 365 でオンプレミスの Active Directory と同期するために、Azure AD Connect を別個のオンプレミスのサーバー上に展開する必要があります。
    
    詳細情報:[Azure AD Connect - 概要](https://go.microsoft.com/fwlink/p/?linkid=203007)

主要な関連用語

## ハイブリッド展開の例

以下のシナリオをご覧ください。これは、典型的な Exchange 2016 展開の概要を示したトポロジの例です。Contoso, Ltd. は、単一フォレスト、単一ドメインの組織で、2 つのドメイン コントローラーと 1 つの Exchange 2016 サーバーがインストールされています。リモートの Contoso ユーザーは、Web 上の Outlook を使ってインターネット経由で Exchange 2016 に接続することにより、メールボックスをチェックしたり、Outlook の予定表にアクセスしたりします。

![Office 365 とのハイブリッド展開を構成する前に、オンプレミスの Exchange を展開する](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "Office 365 とのハイブリッド展開を構成する前に、オンプレミスの Exchange を展開する")

Contoso 社のネットワーク管理者が、ハイブリッド展開を構成する場合を考えてみましょう。必要な Azure AD Connect サーバーを展開して構成し、ユーザーが使う資格情報を、オンプレミスのネットワーク アカウントと Office 365 アカウントの両方で同じになるようにするため、Azure AD Connect パスワード同期機能を使うことにします。ハイブリッド展開の前提条件を満たしたら、ハイブリッド構成ウィザードを使ってハイブリッド展開のオプションを選択すると、新しいトポロジの構成は次のようになります。

  - ユーザーは、オンプレミスの組織と Exchange Online 組織のどちらにログオンする際にも、同じユーザー名とパスワードを使います (「シングル サインオン」)。

  - 社内組織に配置されたユーザー メールボックスと Exchange Online 組織に配置されたユーザー メールボックスは、同じ電子メール アドレス ドメインを使用します。たとえば、社内組織に配置されたメールボックスと Exchange Online 組織に配置されたメールボックスは、どちらもユーザー電子メール アドレスに @contoso.com を使用します。

  - すべての送信メールは社内組織によってインターネットに配信されます。社内組織は、すべてのメッセージ トランスポートを制御し、Exchange Online 組織の中継として機能します (「メール トランスポートの集中管理」)。

  - 社内組織のユーザーと Exchange Online 組織のユーザーは、予定表の空き時間情報を互いに共有できます。両方の組織に構成された組織上の関係により、社内外にまたがるメッセージ追跡、メール ヒント、メッセージ検索も利用できます。

  - 社内ユーザーおよび Exchange Online ユーザーは、同じ URL を使用して、それぞれのメールボックスにインターネット経由で接続します。

![Office 365 とのハイブリッド展開を構成した後に、オンプレミスの Exchange を展開する](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "Office 365 とのハイブリッド展開を構成した後に、オンプレミスの Exchange を展開する")

Contoso の既存の組織構成とハイブリッド展開構成を比較すると、ハイブリッド展開の構成では、追加の通信をサポートするサーバーとサービス、および社内組織と Exchange Online 組織間で共有される機能が追加されていることがわかります。以下は、ハイブリッド展開によって初期の社内 Exchange 組織に加えられた変更の概要を示しています。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>構成</th>
<th>ハイブリッド展開前</th>
<th>ハイブリッド展開後</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メールボックスの場所</p></td>
<td><p>社内組織のメールボックスのみ。</p></td>
<td><p>オンプレミスのメールボックスと Office 365 のメールボックス。</p></td>
</tr>
<tr class="even">
<td><p>メッセージ トランスポート</p></td>
<td><p>オンプレミスのメールボックス サーバーがすべての受信と送信メッセージのルーティングを処理します。</p></td>
<td><p>オンプレミスのメールボックス サーバーは、オンプレミスの組織と Office 365 組織の間での内部メッセージのルーティングを処理します。</p></td>
</tr>
<tr class="odd">
<td><p>Web 上の Outlook</p></td>
<td><p>オンプレミスのメールボックス サーバーが、すべての Web 上の Outlook 要求を受信し、メールボックス情報を表示します。</p></td>
<td><p>オンプレミスのメールボックス サーバーは、Web 上の Outlook 要求をオンプレミスの Exchange 2016 メールボックス サーバーにリダイレクトするか、Office 365 にログオンするためのリンクを提供します。</p></td>
</tr>
<tr class="even">
<td><p>両方の組織の統合 GAL</p></td>
<td><p>該当なし、単一組織のみ。</p></td>
<td><p>オンプレミスの Active Directory 同期サーバーが、メール対応オブジェクトの Active Directory 情報を Office 365 にレプリケートします。</p></td>
</tr>
<tr class="odd">
<td><p>両方の組織で使用されるシングル サインオン</p></td>
<td><p>該当なし、単一組織のみ。</p></td>
<td><p>オンプレミスの Active Directory と Office 365 は、オンプレミスか Office 365 のいずれかにあるメールボックスで同じユーザー名とパスワードを使います。</p></td>
</tr>
<tr class="even">
<td><p>確立された組織上の関係と、Azure AD 認証システムによるフェデレーションの信頼</p></td>
<td><p>Azure AD 認証システムとの信頼関係と、他のフェデレーション Exchange 組織との組織上の関係を構成できます。</p></td>
<td><p>Azure AD 認証システムとの信頼関係は必須です。組織上の関係は、オンプレミスと Office 365 の間で確立されます。</p></td>
</tr>
<tr class="odd">
<td><p>空き時間情報の共有</p></td>
<td><p>社内ユーザーの間でのみ空き時間情報を共有。</p></td>
<td><p>オンプレミスと Office 365 の両方のユーザーの間で空き時間情報を共有。</p></td>
</tr>
</tbody>
</table>


## ハイブリッド展開を構成する前の考慮事項

ここまでで、ハイブリッド展開についてある程度理解を深めることができましたが、今度はいくつかの重要な問題について慎重に考慮する必要があります。ハイブリッド展開を構成すると、現在のネットワークの複数の領域と Exchange 組織に影響することがあります。

## ディレクトリ同期とシングル サインオン

オンプレミスの組織と Office 365 組織の間の Active Directory 同期は、Azure Active Directory Connect を実行するサーバーで 3 時間ごとに実行されます。これは、ハイブリッド展開を構成するために必要です。ディレクトリ同期により、どちらの組織の受信者も、グローバル アドレス リストの中で互いを認識できるようになります。また、ユーザー名とパスワードも同期されるため、ユーザーは、オンプレミスの組織と Office 365 の両方で同じ資格情報を使ってログインすることができます。


> [!NOTE]
> AD FS を使って Azure AD Connect を構成する場合、オンプレミスのユーザーのユーザー名とパスワードは、既定で Office 365 に同期されます。しかし、ユーザーの主要な認証方法は、AD FS を使ったオンプレミスの Active Directory での認証になります。AD FS が何らかの理由でオンプレミスの Active Directory に接続できない場合、クライアントはフォールバックを試み、Office 365 と同期されたユーザー名とパスワードに対して認証を行います。



Azure Active Directory と Office 365 のすべてのお客様のオブジェクト (ユーザー、メールが有効な連絡先、グループ) 数の上限の既定値は 50,000 です。この制限により、Office 365 組織で作成できるオブジェクトの数が決まります。最初のドメインを確認すると、このオブジェクト数の上限は自動的に 300,000 に増えます。ドメインの確認が終わっており、300,000 を超えるオブジェクトの同期が必要な場合や、確認するドメインがなく、50,000 を超えるオブジェクトの同期が必要な場合は、Azure Active Directory サポートに連絡して、オブジェクトのクォータ制限値を大きくしてもらうように依頼する必要があります。

AD FS を構成する場合、Azure AD Connect が実行されているサーバーに加えて、Web アプリケーション プロキシ サーバーを展開することも必要です。これは、境界ネットワーク内に配置する必要があり、内部 Azure AD Connect サーバーとインターネットとの間の中継サーバーとして機能します。Web アプリケーション プロキシ サーバーは、TCP ポート 443 を使って、インターネット上のクライアントとサーバーからの接続を受け入れる必要があります。

## ハイブリッド展開の管理

ハイブリッド展開は、Exchange 2016 で単一の統合管理コンソールによって管理します。これにより、オンプレミスの組織と Exchange Online 組織の両方を管理できます。Exchange 管理コンソールと Exchange コントロール パネルに代わる *Exchange 管理センター* (EAC) では、両方の組織の機能を接続して構成できます。ハイブリッド構成ウィザードを初めて実行すると、Exchange Online 組織に接続するように求められます。Organization Management 役割グループのメンバーである Office 365 アカウントを使って、Exchange Online 組織に EAC を接続することが必要です。

## 証明書

Secure Sockets Layer (SSL) デジタル証明書には、ハイブリッド展開の構成において重要な役割があります。これらの証明書により、社内ハイブリッド サーバーと Exchange Online 組織間の通信をセキュリティで保護できます。証明書は、いくつかの種類のサービスを構成するための要件です。Exchange 組織内で既にデジタル証明書を使用している場合は、追加のドメインを含めるように証明書を変更するか、信頼された証明機関 (CA) から追加の証明書を購入する必要が生じることがあります。まだ証明書を使用していない場合は、信頼された CA から 1 つまたは複数の証明書を購入する必要があります。

詳細情報:[ハイブリッド展開の証明書要件](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## 帯域幅

インターネットへのネットワーク接続は、オンプレミスの組織と Office 365 組織との間の通信パフォーマンスに直接影響します。これは特に、メールボックスをオンプレミスの Exchange 2016 サーバーから Office 365 組織に移動するときに該当します。使用可能なネットワーク帯域幅の量と、並行して移動されるメールボックスのサイズと数によって、メールボックスの移動が完了するまでに要する時間は異なります。また、SharePoint Server 2016 や Skype for Business などの他の Office 365 のサービスも、メッセージング サービスの使用可能な帯域幅に影響することがあります。

メールボックスを Office 365 に移動する前に、次のことを実行してください。

  - Office 365 に移動するメールボックスの平均サイズを確認します。

  - 社内組織からインターネットへの接続の平均的な接続速度とスループット速度を決定します。

  - 平均予想転送速度を計算して、それに従ってメールボックスの移動を計画します。

詳細情報:[ネットワーク](https://go.microsoft.com/fwlink/p/?linkid=280178)

## ユニファイド メッセージング

ユニファイド メッセージング (UM) は、オンプレミスの組織と Office 365 組織間のハイブリッド展開でサポートされます。オンプレミスのテレフォニー ソリューションでは、Office 365 組織と通信できるようにする必要があります。この場合、追加のハードウェアとソフトウェアの購入が必要になる場合があります。

オンプレミスの組織から Office 365 にメールボックスを移動して、これらのメールボックスを UM 用に構成する場合は、メールボックスを移動する前にハイブリッド展開で UM を構成する必要があります。ハイブリッド展開で UM を構成する前にメールボックスを移動すると、メールボックスは UM 機能にアクセスできなくなります。

詳細情報:[ユニファイド メッセージングの共存の設定](https://go.microsoft.com/fwlink/p/?linkid=842271)

## Information Rights Management

Information Rights Management (IRM) を使用すると、ユーザーは、送信するメッセージに Active Directory Rights Management サービス (AD RMS) テンプレートを適用できます。AD RMS テンプレートを使用すると、ユーザーは、権利が保護されたメッセージを開くことができる人物、およびメッセージを開いた後にそのメッセージに対して実行できる操作を制御でき、情報漏洩を防止することができます。

ハイブリッド展開で IRM を使うには、計画、Office 365 組織の手動での構成の実行が必要です。また、メールボックスがオンプレミスの組織か Exchange Online 組織内のどちらに存在するかに応じて、クライアントが AD RMS サーバーを使う方法を理解する必要があります。

詳細情報:[Exchange ハイブリッド展開での IRM](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## モバイル デバイス

ハイブリッド展開では、モバイル デバイスがサポートされています。Exchange ActiveSync が既存のサーバーですでに有効な場合は、引き続き、モバイル デバイスからオンプレミスのメールボックス サーバー上のメールボックスに要求がリダイレクトされます。オンプレミスの組織から Office 365 に移動した既存のメールボックスに接続しているモバイル デバイスの場合は、ほとんどの電話で Office 365 に接続するように Exchange ActiveSync プロファイルが自動的に更新されます。Exchange ActiveSync をサポートするすべてのモバイル デバイスは、ハイブリッド展開との互換性が必要です。

詳細情報:[モバイル機器](https://go.microsoft.com/fwlink/p/?linkid=206387)

## クライアント要件

ハイブリッド展開で最適なエクスペリエンスとパフォーマンスを得るために、クライアントで Outlook 2016 や Outlook 2013 を使うことをお勧めします。Outlook 2010 より前のクライアントは、ハイブリッド展開でも Office 365 でもサポートされていません。

## Office 365 のライセンス

Office 365 内でメールボックスを作成したり、Office 365 にメールボックスを移動したりするには、Office 365 for enterprises にサインアップし、ライセンスを使用可能にする必要があります。Office 365 にサインアップすると、新しいメールボックスかオンプレミスの組織から移動したメールボックスに割り当てることのできる特定の数のライセンスを受け取ります。Office 365 サービスではメールボックスごとにライセンスが必要です。

## ウイルス対策とスパム対策サービス

Office 365 に移動されたメールボックスには、Office 365 で提供されるサービスである Exchange Online Protection (EOP) によってウイルス対策とスパム対策の保護機能が自動的に提供されます。すべての受信インターネット メールを EOP サービスを経由してルーティングする場合、オンプレミスのユーザー用に追加の EOP ライセンスを購入する必要があります。Office 365 の EOP 保護が、オンプレミスの組織のウイルス対策とスパム対策のニーズも十分満たしているかどうかを評価することをお勧めします。オンプレミスの組織が保護されている場合は、組織全体を最大限に保護するようにオンプレミスのウイルス対策とスパム対策ソリューションをアップグレードしたり構成したりすることが必要になる可能性があります。

詳細情報:[スパム対策とマルウェア対策の保護](https://technet.microsoft.com/ja-jp/library/jj200731\(v=exchg.150\))

## パブリック フォルダー

パブリック フォルダーが Office 365 でサポートされている場合、オンプレミスのパブリック フォルダーを Office 365 に移行できます。また、Office 365 のパブリック フォルダーをオンプレミスの Exchange 2016 組織に移動することもできます。オンプレミスのユーザーと Office 365 ユーザーはいずれも、Web 上の Outlook、Outlook 2016、Outlook 2013、Outlook 2010 SP2 以降を使って、どちらかの組織に存在するパブリック フォルダーにアクセスできます。ハイブリッド展開を構成しても、既存のオンプレミスのパブリック フォルダー構成とオンプレミスのメールボックスへのアクセス権は変更されません。

詳細情報:[パブリック フォルダー](https://technet.microsoft.com/ja-jp/library/jj150538\(v=exchg.150\))

## ユーザー補助

このチェックリストの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](https://technet.microsoft.com/ja-jp/library/jj150484\(v=exchg.150\))」を参照してください。

## 主要な関連用語

次の一覧では、Exchange 2013 でのハイブリッド展開に関連するコア コンポーネントについて定義します。

  - **メール トランスポートの集中管理**  
    その内部で、すべてのExchange オンライン受信および送信インターネット メッセージが社内 Exchange 組織経由でルーティングされるハイブリッド構成オプション。このルーティング オプションは、ハイブリッド構成ウィザードで構成されます。詳細については、「[Exchange ハイブリッド展開でのトランスポート オプション](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)」を参照してください。

<!-- end list -->

  - **共存ドメイン**  
    Office 365 サービス用のハイブリッド メール フローおよび自動検出要求に対応するために社内組織に追加される承認済みドメイン。このドメインは、ハイブリッド構成ウィザードで選択されたドメインに対応する*PrimarySmtpAddress* テンプレートが存在する、電子メール アドレス ポリシーにセカンダリのプロキシ ドメインとして追加されます。既定では、このドメインは \<ドメイン\>.mail.onmicrosoft.com です。

<!-- end list -->

  - ***HybridConfiguration* Active Directory オブジェクト**  
    ハイブリッド構成ウィザードで選択された項目で定義される必要なハイブリッド展開構成パラメーターを含む、社内組織内の Active Directory オブジェクト。ハイブリッド構成エンジンは、社内および Exchange Online 設定を構成してハイブリッド機能を有効にする際に、これらのパラメーターを使用します。*HybridConfiguration* オブジェクトの内容は、ハイブリッド構成ウィザードが実行されるたびにリセットされます。

<!-- end list -->

  - **ハイブリッド構成エンジン**  
    ハイブリッド構成エンジン (HCE) は、ハイブリッド展開の構成と更新に必要な中心的な操作を実行します。HCE は、*HybridConfiguration* Active Directory オブジェクトの状態と現在のオンプレミスの Exchange と Exchange Online 構成設定を比較して、タスクを実行し、*HybridConfiguration* Active Directory オブジェクトで定義されたパラメーターに展開構成設定を一致させます。詳しくは、「[ハイブリッド構成エンジン](hybrid-configuration-wizard-exchange-2013-help.md)」をご覧ください。

<!-- end list -->

  - **ハイブリッド構成ウィザード (HCW)**  
    Exchange で提供される適応型ツールで、オンプレミスの組織と Exchange Online 組織間のハイブリッド展開の構成について管理者に順を追って説明します。ウィザードは、*HybridConfiguration* オブジェクトのハイブリッド展開構成パラメーターを定義し、ハイブリッド構成エンジンに必要な構成タスクを実行して定義されたハイブリッド機能を有効にするように指示します。詳しくは、「[ハイブリッド構成ウィザード](hybrid-configuration-wizard-exchange-2013-help.md)」をご覧ください。

<!-- end list -->

  - **Exchange 2010 ベースのハイブリッド展開**  
    Office 365 と Exchange Online サービスの接続エンドポイントとして、Exchange Server 2010 用 Service Pack 3 (SP3) オンプレミス サーバーを使って構成されたハイブリッド展開。オンプレミスの Exchange 2010、Exchange Server 2007、Exchange Server 2003 組織のハイブリッド展開オプション。

<!-- end list -->

  - **Exchange 2013 ベースのハイブリッド展開**  
    Office 365と Exchange Online サービスの接続エンドポイントとして、Exchange 2013 オンプレミス サーバーを使って構成されたハイブリッド展開。オンプレミスの Exchange 2013、Exchange 2010、Exchange 2007 組織のハイブリッド展開オプション。

<!-- end list -->

  - **Exchange 2016 ベースのハイブリッド展開**  
    Office 365 と Exchange Online サービスの接続エンドポイントとして、Exchange 2016 オンプレミス サーバーを使って構成されたハイブリッド展開。オンプレミスの Exchange 2016、Exchange 2013、Exchange 2010 組織のハイブリッド展開オプション。

<!-- end list -->

  - **セキュリティ保護されたメール トランスポート**  
    ハイブリッド展開の自動構成された機能で、オンプレミスの組織と Exchange Online 組織間のセキュリティ保護されたメッセージングを使用可能にします。メッセージは暗号化され、ハイブリッド構成ウィザードで選択された証明書と組み合わされた、トランスポート層セキュリティ (TLS) を使って認証されます。Office 365 テナントは、オンプレミスの組織を接続元とするハイブリッド トランスポート接続のエンドポイントであり、Exchange Online からオンプレミスの組織へのハイブリッド トランスポート接続のソースです。

主要な関連用語

## Exchange ハイブリッド展開のドキュメント

次の表には、Microsoft Exchange のハイブリッド展開の詳細と管理方法の理解に役立つトピックへのリンクが含まれています。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">ハイブリッド構成ウィザード</a></p></td>
<td><p>ハイブリッド構成ウィザードとハイブリッド構成エンジンでハイブリッド展開を構成する方法について。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">ハイブリッド展開の前提条件</a></p></td>
<td><p>互換性のある Exchange Server 組織、Office 365 の要件、社内構成のその他の要件をはじめとする、ハイブリッド展開の前提条件について。</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">ハイブリッド展開の証明書要件</a></p></td>
<td><p>ハイブリッド展開でのデジタル証明書の要件について</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange ハイブリッド展開でのトランスポート オプション</a></p></td>
<td><p>ハイブリッド展開での送受信メッセージのトランスポート オプションについて。</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange ハイブリッド展開でのトランスポート ルーティング</a></p></td>
<td><p>ハイブリッド展開での送受信メッセージのルーティングについて。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange ハイブリッド展開でのハイブリッド管理</a></p></td>
<td><p>Exchange 管理センターおよび Exchange 管理シェルによるハイブリッド展開の管理について。</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange ハイブリッド展開における空き時間情報の共有</a></p></td>
<td><p>ハイブリッド展開における社内組織と Exchange Online 組織間の予定表の空き時間情報の共有について。</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange ハイブリッド展開のサーバー役割</a></p></td>
<td><p>ハイブリッド展開における Exchange サーバー役割の機能について。</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange ハイブリッド展開での IRM</a></p></td>
<td><p>Information Rights Management がハイブリッド展開でどのように機能するかについて。</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange ハイブリッド展開のアクセス許可</a></p></td>
<td><p>ハイブリッド展開で役割ベースのアクセス制御 (RBAC) を使用してアクセス許可を制御する方法について。</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">ハイブリッド展開でのエッジ トランスポート サーバー</a></p></td>
<td><p>Exchange エッジ トランスポート サーバーと、それがハイブリッド展開でどのように展開され動作するかについて。</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">ハイブリッド展開でのシングル サインオン</a></p></td>
<td><p>ハイブリッド展開におけるパスワード同期と AD FS 機能を使ったシングル サインオンの方法について。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">ハイブリッド展開の手順</a></p></td>
<td><p>Exchange オンプレミスの組織と Exchange Online 組織用にハイブリッド展開を作成、変更する手順について。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">Exchange 2013 および Exchange 2010 を使用するハイブリッド展開</a></p></td>
<td><p>Exchange 2007 組織との Exchange 2010 ベースのハイブリッド展開について。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">Exchange 2013 および Exchange 2007 を使用するハイブリッド展開</a></p></td>
<td><p>Exchange 2007 組織との Exchange 2013 ベースのハイブリッド展開について。</p></td>
</tr>
</tbody>
</table>


## Office 365 を初めて使用する場合


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning の小さいアイコン" alt="LinkedIn Learning の小さいアイコン" /> <strong>Office 365 を初めて使用する場合は、</strong><br />
LinkedIn Learning が提供する <a href="https://support.office.com/ja-jp/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> のための無料のビデオ コースをご覧ください。</p></td>
</tr>
</tbody>
</table>

