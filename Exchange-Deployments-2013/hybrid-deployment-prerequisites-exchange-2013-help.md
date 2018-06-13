---
title: 'ハイブリッド展開の前提条件: Exchange 2013 Help'
TOCTitle: ハイブリッド展開の前提条件
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 48267609
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ハイブリッド展開の前提条件

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2017-07-25_

**概要**:ハイブリッド展開をセットアップするために必要な Exchange 環境について説明します。

ハイブリッド構成ウィザードを使用してハイブリッド展開を作成し構成する前に、既存のオンプレミスの Exchange 組織が特定の要件を満たしている必要があります。要件を満たしていない場合、ハイブリッド構成ウィザードで手順を完了することができず、オンプレミスの Exchange 組織と Exchange Online との間でハイブリッド展開を構成できません。

## ハイブリッド展開の前提条件

ハイブリッド展開を構成するには、次の前提条件を満たすことが必要です。

  - **オンプレミスの Exchange 組織**   ハイブリッド展開は、Exchange 2007 以降をベースとするオンプレミスの組織に対して構成できます。
    
    オンプレミス組織にインストールした Exchange のバージョンによって、インストール可能なハイブリッド展開のバージョンが決まります。通常、組織でサポートされている最新バージョンのハイブリッド展開を構成する必要があります。たとえば、オンプレミス組織で Exchange 2007 を実行中の場合は、Exchange 2013 ベースのハイブリッド展開を構成する必要があります。エンタープライズ ハイブリッド展開の互換性に関する Exchange Server および Office 365 の完全な一覧は、次の表に掲載されています。
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>社内環境</th>
    <th>Exchange 2016 ベースのハイブリッド展開</th>
    <th>Exchange 2013 ベースのハイブリッド展開</th>
    <th>Exchange 2010 ベースのハイブリッド展開</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>サポートされている</p></td>
    <td><p>サポート対象外</p></td>
    <td><p>サポートされていない</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>サポートされている</p></td>
    <td><p>サポートされている</p></td>
    <td><p>サポート対象外</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>サポートされている</p></td>
    <td><p>サポートされている</p></td>
    <td><p>サポートされている</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>非サポート</p></td>
    <td><p>サポートされている</p></td>
    <td><p>サポートされている</p></td>
    </tr>
    </tbody>
    </table>


  - **オンプレミスの Exchange のリリース** ハイブリッド展開には、オンプレミスの組織にインストールした Exchange のバージョンで利用できる最新の累積更新プログラムまたは更新プログラムのロールアップが必要です。最新の累積更新プログラムまたは更新プログラムのロールアップをインストールできない場合でも、直前のリリースがサポートされます。それ以前の累積更新プログラムまたは更新プログラムのロールアップはサポートされません。
    
    たとえば、オンプレミスの組織に Exchange 2013 累積更新プログラム 8 がインストールされていて、Exchange 2013 で利用できる最新リリースは累積更新プログラム 10 であるとします。ハイブリッド構成がサポートされている状態を維持するには、Exchange 2013 サーバーを少なくとも累積更新プログラム 9 にアップグレードする必要があります。ただし、累積更新プログラム 10 にアップグレードすることをぜひお勧めします。
    
    累積更新プログラムと更新プログラムのロールアップは四半期ごとにリリースされます。サーバーにいつでも最新の累積更新プログラムまたは更新プログラムのロールアップを適用しておくと、アップグレードを完了するために定期的に余分な時間が必要となる場合でも、より高い柔軟性が得られます。

  - **オンプレミスのサーバーの役割** オンプレミスの組織にインストールするために必要なサーバ―の役割は、インストールされている Exchange のバージョンによって異なります。
    
      - **Exchange 2010** メールボックス サーバー、ハブ トランスポート サーバー、およびクライアント アクセス サーバーの役割をインストールされているサーバーが少なくとも 1 つなければなりません。メールボックス、ハブ トランスポート、およびクライアント アクセスの各役割を別々のサーバーにインストールすることもできますが、信頼性を高め、パフォーマンスの向上を図るには、サーバーにすべての役割をインストールすることを強くお勧めします。
    
      - **Exchange 2013** メールボックス サーバーの役割とクライアント アクセス サーバーの役割をインストールされているサーバーが少なくとも 1 つなければなりません。メールボックスの役割とクライアント アクセスの役割を別々のサーバーにインストールすることもできますが、信頼性を高め、パフォーマンスの向上を図るには、サーバーにどちらの役割もインストールすることを強くお勧めします。
    
      - **Exchange 2016 以降** メールボックス サーバーの役割をインストールされているサーバーが少なくとも 1 つ必要です。
    
    ハイブリッド展開では、エッジ トランスポート サーバーの役割を実行している Exchange サーバーもサポートします。エッジ トランスポート サーバーも、インストールされている Exchange のバージョンで利用できる最新の累積更新プログラムまたは更新プログラムのロールアップに更新する必要があります。境界ネットワークにエッジ トランスポート サーバーを配置することを強くお勧めします。メールボックス サーバーおよびクライアント アクセス サーバーは境界ネットワークに展開できません。

  - **Office 365**   ハイブリッド展開は、Azure Active Directory 同期 をサポートするすべての Office 365 のプランでサポートされています。Office 365 の企業向け、行政機関向け、教育機関向け、中規模企業向けのすべてのプランで、ハイブリッド展開がサポートされています。小規模企業向けの Office 365 Business プランおよび Office 365 Home プランではハイブリッド展開はサポートされていません。
    
    詳細については、「[Office 365 で最新の高度な機能を手に入れよう](https://go.microsoft.com/fwlink/p/?linkid=203981)」を参照してください。

  - **カスタム ドメイン** ハイブリッド展開で Office 365 とともに使用するカスタム ドメインを登録します。これは、Office 365 管理ポータルを使用するか、オプションで社内組織に Active Directory フェデレーション サービス (AD FS) を構成することで実行できます。
    
    詳細については、「[ドメインとユーザーを Office 365 に追加する](https://go.microsoft.com/fwlink/p/?linkid=229238)」を参照してください。

  - **Active Directory 同期**Active Directory 同期を有効にするための Azure Active Directory Connect ツールをオンプレミス組織に展開します。
    
    詳細については、「[Azure AD Connect ユーザーのサインオン オプション](http://go.microsoft.com/fwlink/p/?linkid=723514)」をご覧ください。

  - **自動検出 DNS レコード**   社内の Exchange 2013 クライアント アクセス サーバーをポイントするように、既存の SMTP ドメイン向けに自動検出パブリック DNS レコードを構成します。

  - **Exchange 管理センター (EAC) 内の Office 365 組織**   既定では Office 365 組織ノードはオンプレミス EAC に含まれますが、ハイブリッド構成ウィザードを使用するには、Office 365 管理者の資格情報を使用して EAC を Office 365 組織に接続する必要があります。これにより、1 つの管理コンソールからオンプレミス組織と Exchange Online 組織の両方を管理できます。
    
    詳細については、「[Exchange ハイブリッド展開でのハイブリッド管理](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md)」を参照してください。

  - 
    
    **証明書**   Exchange サービスをインストールし、信頼されたパブリック証明機関 (CA) から購入した有効なデジタル証明書に割り当てます。Microsoft Federation Gateway を使用したオンプレミスのフェデレーション信頼には自己署名証明書を使用することが必要ですが、自己署名証明書はハイブリッド展開での Exchange サービスに使用できません。ハイブリッド展開で構成された Exchange サーバー上のインターネット インフォメーション サービス (IIS) インスタンスには、信頼できる CA から購入した有効なデジタル証明書がインストールされている必要があります。さらに、パブリック DNS で指定されている EWS 外部 URL と自動検出エンドポイントが証明書の別名 (SAN) に記載されている必要があります。ハイブリッド展開でメール トランスポートに使用する Exchange サーバーにインストールする証明書には、すべて同じ証明書 (つまり、同じ CA によって発行され、サブジェクトが同じ) を使用する必要があります。
    
    詳細については、「[ハイブリッド展開の証明書要件](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)」を参照してください。

  - **EdgeSync**   オンプレミス組織にエッジ トランスポート サーバーを展開して、ハイブリッドのセキュリティ保護されたメール トランスポート用にエッジ トランスポート サーバーを構成する場合は、ハイブリッド構成ウィザードを使用する前に EdgeSync を構成する必要があります。また、新しい累積的な更新プログラムまたは更新プログラムのロールアップをエッジ トランスポート サーバーに適用するたびに、EdgeSync を実行することも必要です。
    

    > [!IMPORTANT]
    > エッジ トランスポート サーバーでの展開には EdgeSync が必要ですが、ハイブリッドのセキュリティ保護されたメール トランスポート用にエッジ トランスポート サーバーを構成する場合は、トランスポート構成をさらに手動で設定する必要があります。

    
    詳細については、「[ハイブリッド展開でのエッジ トランスポート サーバー](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md)」を参照してください。

  - **ユニファイド メッセージング (UM) が有効になっているメールボックス** UM が有効なメールボックスがあり、それらを Office 365 に移動する場合は、Exchange ハイブリッド展開に加えて、次のことが必要です。UM が有効になっているメールボックスを Office 365 に移動する**前**に、これらの要件を満たす必要があります。
    
      - オンプレミスのテレフォニー システムと統合された Lync Server 2010、Lync Server 2013、または Skype for Business Server 2015 以降、**または**
    
      - オンプレミスのテレフォニー システムと統合された Skype for Business Online、**または**
    
      - 従来のオンプレミスの PBX または IP-PBX ソリューション。
    
      - オンプレミスの組織の UM メールボックス ポリシーの名前を反映する、Exchange Online で作成された UM メールボックス ポリシー。
        

        > [!NOTE]
        > 複数のオンプレミスの UM メールボックス ポリシーを、Exchange Online の 1 つの UM メールボックス ポリシーにマップすることができます。これを行う場合は、Exchange 管理シェルを使用して、それぞれのオンプレミスの UM メールボックス ポリシーを Exchange Online ポリシーに手動でマップする必要があります。

    
    詳細については、「[電話システムの UM との統合](https://technet.microsoft.com/ja-jp/library/jj673558\(v=exchg.150\))」、「[Exchange 2013 のテレフォニー アドバイザー](https://technet.microsoft.com/ja-jp/library/ee364753\(v=exchg.150\))」、および「[Cloud PBX ボイスメールのセットアップ - Admin ヘルプ](https://go.microsoft.com/fwlink/p/?linkid=826207)」を参照してください。

## ハイブリッド展開のプロトコル、ポート、エンドポイント

ハイブリッド展開機能とコンポーネントが正しく機能するには、特定の着信プロトコル、ポート、接続エンドポイントが Office 365 にアクセスできなければなりません。ハイブリッド展開を構成する前に、オンプレミスのネットワークとセキュリティの構成が、次の表の機能とコンポーネントをサポートすることをご確認ください。特定の受信プロトコル、ポート、エンドポイントを許可することに加えて、ネットワーク上のコンピューターが、「[Office 365 URL および IP アドレス範囲](https://go.microsoft.com/fwlink/?linkid=823100)」の一覧に示された IP アドレス、ポート、URL にアクセスできるようにする必要もあります。


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>トランスポート プロトコル</th>
<th>上位レベル プロトコル</th>
<th>機能/コンポーネント</th>
<th>社内エンドポイント</th>
<th>社内パス</th>
<th>認証プロバイダ</th>
<th>認証メソッド</th>
<th>事前認証のサポート</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25 (SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Office 365 と社内間のメール フロー</p></td>
<td><p>Exchange 2016 メールボックス/エッジ</p>
<p>Exchange 2013 CAS/エッジ</p>
<p>Exchange 2010 ハブ/エッジ</p></td>
<td><p>該当なし</p></td>
<td><p>該当なし</p></td>
<td><p>証明書ベース</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>自動検出</p></td>
<td><p>自動検出</p></td>
<td><p>Exchange 2016 メールボックス</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Azure AD 認証システム</p></td>
<td><p>WS-Security 認証</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>空き時間情報、メール ヒント、メッセージ追跡</p></td>
<td><p>Exchange 2016 メールボックス</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Azure AD 認証システム</p></td>
<td><p>WS-Security 認証</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>複数のメールボックスの検索</p></td>
<td><p>Exchange 2016 メールボックス</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>認証サーバー</p></td>
<td><p>WS-Security 認証</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>メールボックスの移行</p></td>
<td><p>Exchange 2016 メールボックス</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>Basic</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>自動検出</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Exchange 2016 メールボックス</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>認証サーバー</p></td>
<td><p>WS-Security 認証</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>該当なし</p></td>
<td><p>AD FS (Windows に含まれている)</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 認証システム</p></td>
<td><p>構成ごとに異なります。</p></td>
<td><p>2 要素</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>該当なし</p></td>
<td><p>Azure Active Directory Connect (AD FS を使用)</p></td>
<td><p>Windows 2012 R2 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 認証システム</p></td>
<td><p>構成ごとに異なります。</p></td>
<td><p>2-factor</p></td>
</tr>
</tbody>
</table>


## 推奨されるツールおよびサービス

ハイブリッド構成ウィザードを使用してハイブリッド展開を構成する場合、前述した必要な前提条件に加えて、その他のツールとサービスが役立ちます。

  - **Exchange Server 展開アシスタント**   Exchange Server 展開アシスタントは、無料の Web ベース ツールで、オンプレミス組織への Exchange の展開、オンプレミス組織と Office 365 間のハイブリッド展開の構成、または Office 365 への完全移行を支援します。このツールによる簡単な一連の質問に回答すると、その答えに基づき、Exchange Server を展開または構成する指示が記されたカスタマイズされたチェックリストが作成されます。展開アシスタントは、ハイブリッド展開を構成するために必要な情報を正確に提供します。
    
    詳細については、「[Exchange Server 展開アシスタント](https://technet.microsoft.com/exdeploy2013)」を参照してください。
    
     

  - **リモート接続アナライザー ツール**   Microsoft リモート接続アナライザー ツールは、社内の Exchange 組織の外部接続をチェックし、ハイブリッド展開を構成する準備が整っているか確認します。ハイブリッド構成ウィザードを使用してハイブリッド展開を構成する前に、リモート接続アナライザー ツールを使用して社内組織をチェックすることを強くお勧めします。
    
    詳細については、「[Microsoft リモート接続アナライザー](https://testconnectivity.microsoft.com/)」を参照してください。
    
     

  - **シングル サインオン**   シングル サインオンを使用することで、ユーザーが 1 つのユーザー名とパスワードでオンプレミス組織と Exchange Online 組織の両方にアクセスすることができます。シングル サインオンは、ユーザーにとってなじみのあるサインオン エクスペリエンスであり、これにより管理者は、オンプレミスの Active Directory 管理ツールを使用して Exchange Online 組織のメールボックスのアカウント ポリシーを簡単に制御できます。
    
    シングル サインオンを展開する場合、パスワード同期と Active Directory フェデレーション サービスの 2 つのオプションがあります。Azure Active Directory Connect では、両方のオプションが用意されています。パスワード同期を使用すると、サイズに関係なく、ほぼすべての組織で簡単にシングル サインオンを実装できます。これに加え、シングル サインオンを有効にすると、ハイブリッド展開でのユーザー エクスペリエンスが大幅に改善されるため、これを実装することを強くお勧めします。Active Directory フェデレーション サービスが必要なのは、複数の Active Directory フォレストがハイブリッド展開に参加する必要があるような、非常に大規模な組織の場合です。
    
    詳細については、「[ハイブリッド展開でのシングル サインオン](single-sign-on-with-hybrid-deployments-exchange-2013-help.md)」をご覧ください。

