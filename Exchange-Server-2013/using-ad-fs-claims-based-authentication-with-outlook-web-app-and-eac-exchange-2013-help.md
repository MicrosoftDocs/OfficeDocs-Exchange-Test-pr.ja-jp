---
title: 'AD FS のクレームベース認証を Outlook Web App および EAC で使用する: Exchange 2013 Help'
TOCTitle: AD FS のクレームベース認証を Outlook Web App および EAC で使用する
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61204840
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AD FS のクレームベース認証を Outlook Web App および EAC で使用する

 

_**適用先:** Exchange Server 2013 SP1_

_**トピックの最終更新日:** 2017-04-14_

**概要:** 

Exchange 2013 Service Pack 1 (SP1) のオンプレミス展開では、Active Directory フェデレーション サービス (AD FS) をインストールして構成すると、AD FS クレームベース認証を使用して Outlook Web App と EAC に接続できるようになります。また Exchange 2013 SP1 を使用して AD FS とクレームベース認証を統合することができます。クレームベース認証を、次のような従来の認証方式を置き換えるものとして使用できます。

  - Windows 認証

  - フォーム認証

  - ダイジェスト認証

  - 基本認証

  - Active Directory クライアント証明書の認証

認証は、ユーザーの識別情報を確認するプロセスです。認証は、ユーザーが主張しているとおりの人物であることを確認します。クレームベース ID は、認証のためのもう 1 つの方式です。クレームベースの認証は、認証の管理処理をアプリケーション (この場合は Outlook Web App および EAC) から取り去ることにより、認証を一元化してアカウントの管理を容易にします。Outlook Web App および EAC は、ユーザーの認証、ユーザー アカウントおよびパスワードの保管、ユーザー ID の詳細の検索、他の ID システムとの統合に関与しません。認証を一元化すると、将来、認証の方式をアップグレードする作業が容易になります。


> [!NOTE]
> OWA for Devices は、AD FS クレームベース認証をサポートしていません。



使用できる AD FS のバージョンはいくつかあります。次の表にまとめたとおりです。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Server のバージョン</th>
<th>インストール</th>
<th>AD FS のバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2008 R2</p></td>
<td><p>Windows のアドオン コンポーネントである AD FS 2.0 を<strong>ダウンロードしてインストール</strong>します。</p></td>
<td><p>AD FS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p><strong>組み込み</strong> AD FS サーバーの役割をインストールします。</p></td>
<td><p>AD FS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p><strong>組み込み</strong> AD FS サーバーの役割をインストールします。</p></td>
<td><p>AD FS 3.0</p></td>
</tr>
</tbody>
</table>


これから実行する作業は、AD FS 役割サービスを組み込んだ Windows Server 2012 R2 に基づくものです。

**必要な手順の概要**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

ステップ 3: Outlook Web App と EAC に対する証明書利用者信頼とカスタム要求規則を作成する

ステップ 4: Web アプリケーション プロキシの役割サービスをインストールする (省略可能)

ステップ 5: Web アプリケーション プロキシの役割サービスを構成する (省略可能)

ステップ 6: Web アプリケーション プロキシを使用して Outlook Web App と EAC を発行する (省略可能)

ステップ 7: AD FS 認証を使用するように Exchange 2013 を構成する

ステップ 8: OWA と ECP の仮想ディレクトリ上で AD FS 認証を有効にする

ステップ 9: インターネット インフォメーション サービス (IIS) を再起動またはリサイクルする

ステップ 10: Outlook Web App と EAC の AD FS 要求をテストする

Additional information you might want to know

## 始める前に把握しておくべき情報

  - 最低限、次のような別個の Windows Server 2012 R2 サーバーをインストールする必要があります。Active Directory ドメイン サービス (AD DS) を使用するドメイン コントローラーとしてのサーバー、Exchange 2013 サーバー、Web アプリケーション プロキシ サーバー、および Active Directory フェデレーション サービス (AD FS) サーバー。すべての更新がインストールされていることを確認してください。

  - 組織内の適切な数の Windows Server 2012 R2 サーバーに AD DS をインストールします。あるいは、<strong>サーバー マネージャー</strong> \> <strong>ダッシュボード</strong> の <strong>通知</strong> に対して <strong>このサーバーをドメイン コントローラーに昇格する</strong> を使用することもできます。

  - 組織に適切な数のクライアント アクセス サーバーおよびメールボックス サーバーをインストールします。組織内のすべての Exchange 2013 サーバーにすべての更新 (SP1 を含む) をインストールしたことを確認します。SP1 をダウンロードするには、「[Exchange 2013 の更新プログラム](updates-for-exchange-2013-exchange-2013-help.md)」を参照してください。

  - Web アプリケーション プロキシをサーバーに展開するために、ローカル管理者のアクセス許可が必要です。Web アプリケーション プロキシを展開する前に、Windows Server 2012 R2 を実行しているサーバーに AD FS を展開しておく必要があります。

  - Windows Server 2012 R2 上に AD FS の役割をインストールして構成し、証明書利用者信頼と要求規則を作成します。これを実行するには、Domain Admins、Enterprise Admins、またはローカルの Administrators グループのメンバーであるユーザー アカウントでログオンする必要があります。

  - 「[機能のアクセス許可](feature-permissions-exchange-2013-help.md)」を参照して、Exchange 2013 に必要なアクセス許可を判別します。

  - Outlook Web App を管理するためのアクセス許可を割り当てられている必要があります。必要なアクセス許可については、「[クライアントおよびモバイル デバイスのアクセス許可](clients-and-mobile-devices-permissions-exchange-2013-help.md)」トピックの「Outlook Web App のアクセス許可」を参照してください。

  - EAC を管理するためのアクセス許可を割り当てられている必要があります。必要なアクセス許可については、「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」トピックの「Exchange 管理センターの接続」を参照してください。

  - シェルだけを使用していくつかの手順を実行できる場合があります。社内 Exchange 組織でシェルを開く方法について学習するには、「[シェルを開く](https://technet.microsoft.com/ja-jp/library/dd638134\(v=exchg.150\))」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## ステップ 1: AD FS の証明書要件の確認

証明書は、Exchange 2013 SP1 サーバー、Outlook Web App などの Web クライアント、EAC、Windows Server 2012 R2 サーバー (Active Directory フェデレーション サービス (AD FS) サーバーや Web アプリケーション プロキシ サーバーを含む) との間の通信をセキュリティで保護する面で重要な役割を果たします。証明書の要件は、AD FS サーバー、AD FS プロキシ サーバー、または Web アプリケーション プロキシ サーバーのうちどれを設定しているかに応じて異なります。AD FS サービスで使用される証明書 (SSL 証明書とトークン署名証明書を含む) は、すべての Exchange サーバー、AD FS サーバー、および Web アプリケーション プロキシ サーバー上の信頼されたルート証明機関ストアにインポートする必要があります。インポートされた証明書の拇印は、[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\)) コマンドレットを使用するときに Exchange 2013 SP1 サーバーでも使用されます。

どのような AD FS 設計でも、インターネットおよび AD FS サーバー上のユーザー間の通信をセキュリティで保護するためにさまざまな証明書を使用する必要があります。AD FS サーバー、Active Directory ドメイン コントローラー、および Exchange 2013 サーバーで通信と認証を実行するには、事前に各フェデレーション サーバーがサービス通信証明書または Secure Socket Layer (SSL) 証明書と、トークン署名証明書を保有している必要があります。セキュリティと予算の要件に応じて、どの証明書をパブリック CA またはエンタープライズ CA から取得するかを注意深く検討してください。エンタープライズ ルート CA または下位 CA をインストールして構成する場合は、Active Directory 証明書サービス (AD CS) を使用できます。AD CS の詳細については、「[Active Directory 証明書サービスの概要](https://go.microsoft.com/fwlink/?linkid=392697)」を参照してください。

AD FS は証明書が CA から発行されたものであることを必要としませんが、SSL 証明書 (既定でサービス通信証明書としても使用される SSL 証明書) は AD FS クライアントから信頼されている必要があります。自己署名証明書は使用しないことをお勧めします。フェデレーション サーバーは、Web クライアントおよびフェデレーション サーバー プロキシとの SSL 通信について SSL 証明書を使用して Web サービス トラフィックをセキュリティで保護します。SSL 証明書はクライアント コンピューターによって信頼されている必要があるため、信頼された CA によって署名された証明書を使用することをお勧めします。選択するすべての証明書は、対応する秘密キーを持っている必要があります。CA (エンタープライズまたはパブリック) から証明書を受け取ったら、必ずすべての証明書をすべてのサーバーの信頼されたルート証明機関ストアにインポートしてください。<strong>証明書</strong> MMC スナップインを使用して証明書をストアにインポートしたり、Active Directory 証明書サービスを使用して証明書を配布したりできます。重要な点として、インポートした証明書の有効期限が切れている場合は、別の有効な証明書を手動でインポートする必要があります。


> [!IMPORTANT]
> 自己署名したトークン署名証明書を AD FS から使用する場合は、この証明書をすべての Exchange 2013 サーバー上の信頼されたルート証明機関ストアにインポートする必要があります。自己署名したトークン署名証明書を使用せずに Web アプリケーション プロキシを展開した場合は、Web アプリケーション プロキシ構成およびすべての AD FS 証明書利用者信頼に含まれる公開キーを更新する必要があります。



Exchange 2013 SP1、AD FS、および Web アプリケーション プロキシを設定するときには、証明書について以下の推奨事項に従ってください。

  - **メールボックス サーバー:**  メールボックス サーバーで使用される証明書は、Exchange 2013 のインストール時に作成される自己署名証明書です。Exchange 2013 メールボックス サーバーに接続するすべてのクライアントは Exchange 2013 クライアント アクセス サーバーを経由するため、管理する必要のある証明書はクライアント アクセス サーバー上にあるものだけです。

  - **クライアント アクセス サーバー:**  サービス通信に使用する SSL 証明書が必要です。既存の SSL 証明書に、証明書利用者信頼エンドポイントを設定するために使用する FQDN が既に組み込まれている場合は、追加の証明書は不要です。

  - **AD FS**: AD FS には次の 2 種類の証明書が必要です。
    
      - サービス通信に使用する SSL 証明書
        
          - サブジェクト名: **adfs.contoso.com** (AD FS 展開名)
        
          - サブジェクトの別名 (SAN):なし
    
      - トークン署名証明書
        
          - サブジェクト名: **tokensigning.contoso.com**
        
          - サブジェクトの別名 (SAN):なし
        

        > [!NOTE]
        > AD FS 上のトークン署名証明書を置き換える場合は、新しいトークン署名証明書を使用するように既存のすべての証明書利用者信頼を更新する必要があります。



  - **Web アプリケーション プロキシ**
    
      - サービス通信に使用する SSL 証明書
        
          - サブジェクト名: **owa.contoso.com**
        
          - サブジェクトの別名 (SAN):なし
        

        > [!NOTE]
        > Web アプリケーション プロキシの外部 URL が内部 URL と同じである場合は、Exchange の SSL 証明書をここで再利用できます。

    
      - AD FS プロキシ SSL 証明書
        
          - サブジェクト名: **adfs.contoso.com** (AD FS 展開名)
        
          - サブジェクトの別名 (SAN):なし
    
      - トークン署名証明書: これは、以下のステップの中で AD FS から自動的に上書きコピーされます。この証明書を使用する場合は、それが組織内の Exchange 2013 サーバーによって信頼されている必要があります。

証明書の詳細については、「[AD FS を配置するための要件を確認する](https://go.microsoft.com/fwlink/?linkid=392699)」にある証明書の要件に関するセクションを参照してください。


> [!NOTE]
> AD FS 用の SSL 証明書がある場合でも、Outlook Web App および EAC には SSL 暗号証明書が必要です。SSL 証明書は、OWA および ECP の仮想ディレクトリで使用されます。



## ステップ 2: Active Directory フェデレーション サービス (AD FS) のインストールと構成

Windows Server 2012 R2 の AD FS は、簡素化され、セキュリティで保護された ID フェデレーションと Web シングル サインオン (SSO) 機能を提供します。AD FS には、ブラウザー ベースの Web SSO、多要素認証、およびクレームベース認証を可能にするフェデレーション サービスが含まれています。AD FS では、クレームベース認証およびアクセス承認のメカニズムを使用してアプリケーションのセキュリティが維持されるため、システムおよびアプリケーションへのアクセスが簡素化されます。

AD FS を Windows Server 2012 R2 上にインストールするには、以下の手順を実行します。

1.  <strong>スタート</strong> 画面で <strong>サーバー マネージャー</strong> を開くか、デスクトップのタスクバーで <strong>サーバー マネージャー</strong> を開きます。<strong>管理</strong> メニューの <strong>役割と機能の追加</strong> をクリックします。

2.  <strong>始める前に</strong> ページで、<strong>次へ</strong> をクリックします。

3.  <strong>インストールの種類の選択</strong> ページで、<strong>役割ベースまたは機能ベースのインストール</strong> をクリックしてから、<strong>次へ</strong> をクリックします。

4.  <strong>対象サーバーの選択</strong> ページで、<strong>サーバー プールからサーバーを選択</strong> をクリックし、ローカル コンピューターが選択されていることを確認してから、<strong>次へ</strong> をクリックします。

5.  <strong>サーバーの役割の選択</strong> ページで、<strong>Active Directory フェデレーション サービス</strong> をクリックしてから、<strong>次へ</strong> をクリックします。
    
    <strong>機能の選択</strong> ページで、<strong>次へ</strong> をクリックします。必要な前提条件または機能が既に自動的に選択されています。それ以外の機能を選択する必要はありません。

6.  <strong>Active Directory フェデレーション サービス (AD FS)</strong> ページで、<strong>次へ</strong> をクリックします。

7.  <strong>インストール オプションの確認</strong> ページで、<strong>必要に応じて対象サーバーを自動的に再起動する</strong> を選択してから、<strong>インストール</strong> をクリックします。
    

    > [!NOTE]
    > インストール処理の実行中、ウィザードは閉じないでください。



必要な AD FS サーバーをインストールし、必要な証明書を生成した後は、AD FS を構成し、AD FS が正常に機能することをテストする必要があります。次のトピックにあるチェックリストは、AD FS のセットアップと構成の際に役立ちます:「[チェックリスト: フェデレーション サーバーを設定します。](https://go.microsoft.com/fwlink/?linkid=392700)」。

Active Directory フェデレーション サービスを構成するには、以下の手順を実行します。

1.  <strong>インストールの進行状況</strong> ページで、<strong>Active Directory フェデレーション サービス</strong> の下にあるウィンドウから、<strong>このサーバーにフェデレーション サービスを構成します</strong> をクリックします。Active Directory フェデレーション サービス構成ウィザードが開きます。

2.  **「ようこそ」**ページで、<strong>フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成します</strong> をクリックしてから、<strong>次へ</strong> をクリックします。

3.  <strong>AD DS に接続</strong> ページで、このコンピューターの参加先になる正しい Active Directory ドメインに対してドメイン管理者権限を持つアカウントを指定し、<strong>次へ</strong> をクリックします。異なるユーザーを選択する必要がある場合は、<strong>変更</strong> をクリックします。

4.  <strong>サービスのプロパティの指定</strong> ページで以下の操作を実行してから、<strong>次へ</strong> をクリックします。
    
      - 前のステップで AD CS またはパブリック CA から入手した SSL 証明書をインポートします。この証明書は、必須のサービス認証証明書です。SSL 証明書のある場所を参照します。SSL 証明書の作成およびインポートの詳細については、「[サーバー証明書](https://go.microsoft.com/fwlink/?linkid=392703)」を参照してください。
    
      - フェデレーション サービスの名前を入力します。たとえば、**adfs.contoso.com** と入力します。
    
      - フェデレーション サービスに表示名を指定する場合は、組織の名前を入力します。たとえば、**Contoso, Ltd.** と入力します。

5.  <strong>サービス アカウントの指定</strong> ページで、<strong>既存のドメイン ユーザー アカウントまたはグループの管理されたサービス アカウントを使用してください</strong> を選択してから、ドメイン コントローラーを作成したときに作成した GMSA アカウント (FsGmsa) を指定します。アカウントのパスワードを組み込んでから、<strong>次へ</strong> をクリックします。
    

    > [!NOTE]
    > グローバルに管理されたサービス アカウント (GMSA) は、ドメイン コントローラーを構成するときに作成する必要のあるアカウントです。GMSA アカウントは、AD FS のインストールおよび構成中に必要です。このアカウントをまだ作成していない場合は、次の Windows PowerShell コマンドを実行してください。contoso.com ドメインおよび AD FS サーバー用のアカウントが作成されます。



6.  次のコマンドを実行します。
    
    ```powershell
    Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)
    ```  

7.  この例では、adfs.contoso.com をという名前のフェデレーション サービスの FsGmsa をという名前の新しい GMSA アカウントを作成します。フェデレーション サービス名は、クライアントに表示されている値です。
    
    ```powershell
    New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com
    ```  

8.  <strong>構成データベースの指定</strong> ページで、<strong>Windows Internal Database を使用してサーバーにデータベースを作成します</strong> を選択してから、<strong>次へ</strong> をクリックします。

9.  <strong>オプションの確認</strong> ページで、選択した構成の内容を確認します。オプションとして、<strong>スクリプトの表示</strong> ボタンを使用すると、追加の AD FS のインストールを自動化できます。<strong>次へ</strong> をクリックします。

10. <strong>前提条件の確認</strong> ページで、すべての前提条件の確認が正常に完了したことを確認してから、<strong>構成</strong> をクリックします。

11. <strong>インストールの進行状況</strong> ページで、すべてが正常にインストールされたことを確認してから、<strong>閉じる</strong> をクリックします。

12. <strong>結果</strong> ページで、結果を確認し、構成が正常に完了したことをチェックしてから、<strong>フェデレーション サービス展開を完了するために必要な次の手順</strong> をクリックします。

Windowsの次の PowerShell コマンドは、上記の手順と同じです。
    
```powershell
Import-Module ADFS
```
```powershell
Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"
```

詳細と構文については、「[Install-AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704)」を参照してください。

インストールを検証するには、以下の手順を実行します。AD FS サーバーで、Web ブラウザーを開き、フェデレーション メタデータの URL (例: **https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**) を参照します。

## ステップ 3: Outlook Web App と EAC に対する証明書利用者信頼とカスタム要求規則を作成する

Web アプリケーション プロキシを介して発行するすべてのアプリケーションとサービスの場合、AD FS サーバーで証明書利用者信頼を構成する必要があります。独立した名前空間を使用する複数の Active Directory サイトで展開する場合は、Outlook Web App と EAC の証明書利用者信頼を各名前空間に追加する必要があります。

EAC は、ECP 仮想ディレクトリを使用します。EAC の設定を表示または構成するには、[Get-EcpVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dd351058\(v=exchg.150\)) および [Set-EcpVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dd297991\(v=exchg.150\)) コマンドレットを使用することができます。EAC にアクセスするには、Web ブラウザーを使用して **http://server1.contoso.com/ecp** にアクセスします。


> [!NOTE]
> 以下に示す URL の例に含まれている末尾のスラッシュ <STRONG>/</STRONG> は、意図的なものです。AD FS 証明書利用者信頼と Exchange Audience URI の両方が必ず<STRONG>同一であること</STRONG>が重要です。これは、AD FS 証明書利用者信頼と Exchange Audicence URI の両方の URL の末尾にスラッシュが<STRONG>あるか</STRONG>または<STRONG>ないか</STRONG>のどちらかでなければならないことを意味します。このセクションの例では、"owa" または "ecp" で終わる URL のすべての末尾に <STRONG>/</STRONG> が含まれています ( /owa/ または /ecp/)。



Outlook Web App に対して Windows Server 2012 R2 で AD FS 管理スナップインを使用して証明書利用者信頼を作成するには、以下のようにします。

1.  <strong>サーバー マネージャー</strong> で、<strong>ツール</strong> をクリックして、<strong>AD FS 管理</strong> を選択します。

2.  <strong>AD FS スナップイン</strong> の **AD FS\\信頼関係** の下で、<strong>証明書利用者信頼</strong> を右クリックしてから、<strong>証明書利用者信頼の追加</strong> をクリックして <strong>証明書利用者信頼の追加</strong> ウィザードを開きます。

3.  <strong>ようこそ</strong> ページで、<strong>開始</strong> をクリックします。

4.  <strong>データ ソースの選択</strong> ページで、<strong>証明書利用者に関するデータを手動で入力します</strong> をクリックしてから、<strong>次へ</strong> を入力します。

5.  <strong>表示名の指定</strong> ページの <strong>表示名</strong> ボックスに **Outlook Web App** と入力し、<strong>メモ</strong> の下にこの証明書利用者信頼の説明 (例: **This is a trust for https://mail.contoso.com/owa**) を入力してから、<strong>次へ</strong> をクリックします。

6.  <strong>プロファイルの選択</strong> ページで、<strong>AD FS プロファイル</strong> をクリックしてから、<strong>次へ</strong> をクリックします。

7.  <strong>証明書の構成</strong> ページで、<strong>次へ</strong> をクリックします。

8.  <strong>URL の構成</strong> ページで、<strong>WS-Federation パッシブ プロトコルのサポートを有効にします</strong> をクリックし、<strong>証明書利用者の WS-Federation パッシブ プロトコル URL</strong> の下に **type https://mail.contoso.com/owa** と入力してから、<strong>次へ</strong> をクリックします。

9.  <strong>ID の構成</strong> ページで、この証明書利用者の 1 つ以上の ID を指定し、<strong>追加</strong> をクリックしてそれらの ID を一覧に追加してから、<strong>次へ</strong> をクリックします。

10. <strong>多要素認証を今すぐ構成しますか?</strong> ページで、<strong>この証明書利用者信頼に対して多要素認証の設定を構成します</strong> を選択します。

11. <strong>多要素認証の構成</strong> ページで、<strong>この証明書利用者信頼に対して多要素認証の設定を今は構成しません</strong> を選択してから、<strong>次へ</strong> をクリックします。

12. <strong>発行承認規則の選択</strong> ページで、<strong>すべてのユーザーがこの証明書利用者にアクセスすることを許可します</strong> を選択してから、<strong>次へ</strong> をクリックします。

13. <strong>信頼の追加の準備完了</strong> ページで、設定を確認してから、<strong>次へ</strong> をクリックして証明書利用者信頼の情報を保存します。

14. <strong>完了</strong> ページで、<strong>ウィザードを閉じるときにこの証明書利用者の \[要求規則の編集\] ダイアログを開きます</strong> が選択されていないことを確認してから、<strong>閉じる</strong> をクリックします。

EAC に対して証明書利用者信頼を作成するために上記の手順を再び実行しますが、次の点が違います。表示名に **Outlook Web App** を入力する代わりに、**EAC** と入力します。説明として **This is a trust for the Exchange Admin Center** を入力し、<strong>証明書利用者の WS-Federation パッシブ プロトコル URL</strong> は **https://mail.contoso.com/ecp** です。

クレームベースの ID モデルでは、Active Directory フェデレーション サービス (AD FS) のフェデレーション サービスとしての機能は、要求のセットを含むトークンを発行することです。要求規則は、AD FS がどのクレームを発行するかの決定に影響を与えます。要求規則およびすべてのサーバー構成データは、AD FS 構成データベースに格納されます。

次の 2 つの要求規則を作成する必要があります。

  - Active Directory ユーザー SID

  - Active Directory UPN

必要な要求規則を追加するには、以下の手順を実行します。

1.  <strong>サーバー マネージャー</strong> で、<strong>ツール</strong> をクリックしてから、<strong>AD FS 管理</strong> をクリックします。

2.  コンソール ツリーの **AD FS\\信頼関係** の下で、<strong>要求プロバイダー信頼</strong> または <strong>証明書利用者信頼</strong> のどちらかをクリックしてから、Outlook Web App の証明書利用者信頼をクリックします。

3.  <strong>証明書利用者信頼</strong> ウィンドウで、Outlook Web App 信頼を右クリックしてから、<strong>要求規則の編集</strong> をクリックします。

4.  <strong>要求規則の編集</strong> ウィンドウの <strong>発行変換規則</strong> タブで、<strong>規則の追加</strong> をクリックして、変換要求規則の追加ウィザードを開始します。

5.  <strong>ルール テンプレートの選択</strong> ページの <strong>要求規則テンプレート</strong> の下にあるリストで <strong>カスタム規則を使用した要求の送信</strong> を選択してから、<strong>次へ</strong> をクリックします。

6.  <strong>規則の構成</strong> ページの <strong>規則の種類の選択</strong> ステップで、<strong>要求規則名</strong> の下に要求規則の名前を入力します。要求規則には説明的な名前 (例: **ActiveDirectoryUserSID**) を付けてください。<strong>カスタム規則</strong> の下に、この規則について次のような要求規則言語の構文を入力します。
    
    ```powershell
    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);
    ```  

7.  <strong>規則の構成</strong> ページで、<strong>完了</strong> をクリックします。

8.  <strong>要求規則の編集</strong> ウィンドウの <strong>発行変換規則</strong> タブで、<strong>規則の追加</strong> をクリックして、変換要求規則の追加ウィザードを開始します。

9.  <strong>ルール テンプレートの選択</strong> ページの <strong>要求規則テンプレート</strong> の下にあるリストで <strong>カスタム規則を使用した要求の送信</strong> を選択してから、<strong>次へ</strong> をクリックします。

10. <strong>規則の構成</strong> ページの <strong>規則の種類の選択</strong> ステップで、<strong>要求規則名</strong> の下に要求規則の名前を入力します。要求規則には説明的な名前 (例: **ActiveDirectoryUPN**) を付けてください。<strong>カスタム規則</strong> の下に、この規則について次のような要求規則言語の構文を入力します。
    
    ```powershell
    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);
    ```  

11. <strong>終了</strong> をクリックします。

12. <strong>要求規則の編集</strong> ウィンドウで、<strong>適用</strong> をクリックしてから、<strong>OK</strong> をクリックします。

13. EAC の証明書利用者信頼の場合は、この手順のステップ 3-12 を繰り返します。

または、Windows PowerShell を使用して、証明書利用者信頼と要求規則を作成できます。

1.  IssuanceAuthorizationRules.txt および IssuanceTransformRules.txt の 2 つの .txt ファイルを作成します。

2.  それらの内容を 2 つの変数にインポートします。

3.  次の 2 つのコマンドレットを実行して、証明書利用者信頼を作成します。これらを実行すると、この例では要求規則の構成も行われます。

**IssuanceAuthorizationRules.txt の内容:** 

```powershell
@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");
```  

**IssuanceTransformRules.txt の内容:** 

```powershell
@RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 

@RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);
```  

**次のコマンドを実行します。**

```powershell
[string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt

[string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt

Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules

Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
```  

## ステップ 4: Web アプリケーション プロキシの役割サービスをインストールする (省略可能)


> [!NOTE]
> ステップ 4、ステップ 5、ステップ 6 は、Web アプリケーション プロキシを使用して Exchange OWA と ECP を発行するユーザーと、Web アプリケーション プロキシに AD FS 認証を実行させるユーザーに必要な手順です。ただし、Web アプリケーション プロキシを使用して Exchange を発行することは必須ではありません。そのため、Web アプリケーション プロキシを使用せず、Exchange 自体が AD FS 認証を実行するように構成する場合は、ステップ 7 までスキップできます。



Web アプリケーション プロキシは、Windows Server 2012 R2 の新しいリモート アクセス役割サービスです。Web アプリケーション プロキシは、企業ネットワークの内側にある Web アプリケーションに企業ネットワークの外側から多くのデバイスでユーザーがアクセスできるようにするためのリバース プロキシの機能を Web アプリケーションに提供します。Web アプリケーション プロキシは、Active Directory フェデレーション サービス (AD FS) を使用して Web アプリケーションへのアクセスを事前に認証し、さらに AD FS プロキシとしても機能します。Web アプリケーション プロキシは必須ではありませんが、AD FS を外部クライアントからアクセス可能にする場合に推奨されます。ただし、Outlook Web App のオフライン アクセスは、Web アプリケーション プロキシを介した AD FS 認証の使用時にはサポートされません。Web アプリケーション プロキシとの統合に関する詳細は、「[Web アプリケーション プロキシを使用してアプリケーションを公開することを計画する](https://go.microsoft.com/fwlink/?linkid=392705)」を参照してください。


> [!WARNING]
> AD FS がインストールされているのと同じサーバー上に Web アプリケーション プロキシをインストールすることはできません。



Web アプリケーション プロキシを展開するには、Web アプリケーション プロキシ サーバーとして機能させる予定のサーバー上に、リモート アクセス サーバーの役割を Web アプリケーション プロキシの役割サービスと一緒にインストールする必要があります。Web アプリケーション プロキシの役割サービスをインストールするには、以下の手順を実行します。

1.  Web アプリケーション プロキシ サーバーの <strong>サーバー マネージャー</strong> で、<strong>管理</strong> をクリックしてから、<strong>役割と機能の追加</strong> をクリックします。

2.  役割と機能の追加ウィザードで <strong>次へ</strong> を 3 回クリックして、<strong>サーバーの役割</strong> ページに進みます。

3.  <strong>サーバーの役割</strong> ページの一覧から <strong>リモート アクセス</strong> を選択し、<strong>次へ</strong> をクリックします。

4.  <strong>機能</strong> ページで <strong>次へ</strong> をクリックします。

5.  <strong>リモート アクセス</strong> ページで情報を確認してから、<strong>次へ</strong> をクリックします。

6.  <strong>役割サービス</strong> ページで <strong>Web アプリケーション プロキシ</strong> を選択します。次に、<strong>役割と機能の追加ウィザード</strong> ウィンドウで <strong>機能の追加</strong> をクリックして、<strong>次へ</strong> をクリックします。

7.  <strong>確認</strong> ウィンドウで <strong>インストール</strong> をクリックします。また、<strong>必要に応じて対象サーバーを自動的に再起動する</strong> を選択することもできます。

8.  <strong>インストールの進行状況</strong> ダイアログ ボックスで、インストールが成功したことを確認し、<strong>閉じる</strong> をクリックします。

次の Windows PowerShell コマンドレットは、上記の手順と同じ操作を実行します。

```powershell
Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools
```

## ステップ 5: Web アプリケーション プロキシの役割サービスを構成する (省略可能)

Web アプリケーション プロキシは、AD FS サーバーに接続するように構成する必要があります。Web アプリケーション プロキシ サーバーとして展開するすべてのサーバーに対して、この手順を繰り返します。

Web アプリケーションの役割サービスを構成するには、以下の手順を実行します。

1.  Web アプリケーション プロキシ サーバーの <strong>サーバー マネージャー</strong> で、<strong>ツール</strong> をクリックし、<strong>リモート アクセス管理</strong> をクリックします。

2.  <strong>構成</strong> ウィンドウで <strong>Web アプリケーション プロキシ</strong> をクリックします。

3.  <strong>リモート アクセス管理</strong> コンソールの中央のウィンドウで、<strong>Web アプリケーション プロキシの構成ウィザードを実行する</strong> をクリックします。

4.  Web アプリケーション プロキシの構成ウィザードの <strong>ようこそ</strong> ダイアログ ボックスで、<strong>次へ</strong> をクリックします。

5.  <strong>フェデレーション サーバー</strong> ページで、次の操作を行ってから、<strong>次へ</strong> をクリックします。
    
      - <strong>フェデレーション サービス名</strong> ボックスに、AD FS サーバーの完全修飾ドメイン名 (FQDN) (例: **adfs.contoso.com**) を入力します。
    
      - <strong>ユーザー名</strong> および <strong>パスワード</strong> ボックスに、AD FS サーバーのローカル管理者アカウントの資格情報を入力します。

6.  <strong>AD FS プロキシ証明書</strong> ダイアログ ボックスで、Web アプリケーション プロキシ サーバーに現在インストールされている証明書の一覧から、Web アプリケーション プロキシが AD FS プロキシ機能のために使用する証明書を選択して、<strong>次へ</strong> を入力します。ここで選択する証明書は、サブジェクト名 (例: **adfs.contoso.com**) がフェデレーション サービス名になっているものである必要があります。

7.  <strong>確認</strong> ダイアログ ボックスで、設定の内容を確認します。必要であれば、Windows PowerShell コマンドレットをコピーして、追加のインストールを自動化することができます。<strong>構成</strong> をクリックします。

8.  <strong>結果</strong> ダイアログ ボックスで、構成が成功したことを確認してから、<strong>閉じる</strong> をクリックします。

次の Windows PowerShell コマンドレットは、上記の手順と同じ操作を実行します。

```powershell
Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com
```  

## ステップ 6: Web アプリケーション プロキシを使用して Outlook Web App と EAC を発行する (省略可能)

ステップ 3 では、Outlook Web App と EAC の要求の証明書利用者信頼を作成しました。次にこれらのアプリケーションの両方を発行することが必要です。ただし、この操作を行う前に、これらの証明書利用者信頼が作成されていること、および Web アプリケーション プロキシ サーバー上に Outlook Web App と EAC に適合する証明書があることを確認します。Web アプリケーション プロキシによって発行する必要のあるすべての AD FS エンドポイントについては、AD FS 管理コンソールで、エンドポイントを <strong>プロキシ有効</strong> に設定する必要があります。

Web アプリケーション プロキシを使用して Outlook Web App 発行するには、以下の手順を実行してください。EAC についても、以下の手順を繰り返します。ただし、EAC を発行するときには、名前、外部 URL、外部証明書、およびバックエンド URL を変更する必要があります。

Web アプリケーション プロキシを使用して Outlook Web App および EAC を発行するには、以下の手順を実行します。

1.  Web アプリケーション プロキシ サーバーの <strong>リモート アクセス管理</strong> コンソールで、<strong>ナビゲーション</strong> ウィンドウの <strong>Web アプリケーション プロキシ</strong> をクリックしてから、<strong>タスク</strong> ウィンドウの <strong>発行</strong> をクリックします。

2.  新しいアプリケーションの発行ウィザードの <strong>ようこそ</strong> ページで、<strong>次へ</strong> をクリックします。

3.  <strong>事前認証</strong> ページで、<strong>Active Directory フェデレーション サービス (AD FS)</strong> をクリックしてから、<strong>次へ</strong> をクリックします。

4.  <strong>証明書利用者</strong> ページで、証明書利用者の一覧から発行するアプリケーションの証明書利用者を選択してから、<strong>次へ</strong> をクリックします。

5.  <strong>発行の設定</strong> ページで、次の操作を行ってから、<strong>次へ</strong> をクリックします。
    
    1.  <strong>名前</strong> ボックスに、このアプリケーションのフレンドリ名を入力します。この名前は、<strong>リモート アクセス管理コンソール</strong> の発行されたアプリケーションの一覧でのみ使用されます。**OWA** や **EAC** という名前を使用できます。
    
    2.  <strong>外部 URL</strong> ボックスに、このアプリケーションの外部 URL を入力します。たとえば、Outlook Web App に対しては **https://external.contoso.com/owa**、EAC に対しては **https://external.contoso.com/ecp** などです。
    
    3.  <strong>外部証明書</strong> リストで、サブジェクト名が外部 URL のホスト名と一致する証明書を選択します。
    
    4.  <strong>バックエンド サーバー URL</strong> ボックスに、バックエンド サーバーの URL を入力します。なお、この値は、外部 URL を入力した時点で自動的に入力されます。バックエンド サーバーの URL が異なる場合にのみこの値を変更してください。たとえば、Outlook Web App に対しては **https://mail.contoso.com/owa**、EAC に対しては **https://mail.contoso.com/ecp** などです。
    

    > [!NOTE]
    > Web アプリケーション プロキシは、URL に含まれるホスト名を変換できますが、パスは変換できません。したがって、別のホスト名を入力できますが、同じパスを入力する必要があります。たとえば、外部 URL として <EM>https://external.contoso.com/app1/</EM> を入力し、バックエンド サーバー URL として <EM>https://mail.contoso.com/app1/</EM> を入力することができます。しかし、外部 URL として <EM>https://external.contoso.com/app1/</EM> を入力し、バックエンド サーバー URL として <EM>https://mail.contoso.com/internal-app1/</EM> を入力することはできません。



6.  <strong>確認</strong> ページで設定内容を確認し、<strong>発行</strong> をクリックします。Windows PowerShell コマンドをコピーしておけば、発行された追加のアプリケーションをセットアップできます。

7.  <strong>結果</strong> ページでアプリケーションが正常に発行されたことを確認してから、<strong>閉じる</strong> をクリックします。

次の Windows PowerShell コマンドレットは、Outlook Web App に対する上記の手順と同じ作業を実行します。

```powershell
Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'
```  

次の Windows PowerShell コマンドレットは、EAC に対する上記の手順と同じ作業を実行します。

```powershell
Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'
```  

これらの手順を完了すると、Web アプリケーション プロキシは Outlook Web App クライアントと EAC クライアントの AD FS 認証を実行し、これらに代わって Exchange への接続をプロキシ処理します。AD FS 認証用に Exchange 自体を構成する必要はないため、ステップ 10 に進んで構成をテストします。

## ステップ 7: AD FS 認証を使用するように Exchange 2013 を構成する

Exchange 2013 内の Outlook Web App および EAC でクレームベース認証を使用するように AD FS を構成している場合は、対象の Exchange 組織に対して AD FS を有効にする必要があります。[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\)) コマンドレットを使用して組織に対して AD FS の設定を構成する必要があります。

  - AD FS の発行者を **https://adfs.contoso.com/adfs/ls/** に設定します。

  - AD FS の URI を **https://mail.contoso.com/owa/** および **https://mail.contoso.com/ecp/** に設定します。

  - 証明書の拇印を署名するには、AD FS サーバーのWindows PowerShell を使用し`Get-ADFSCertificate -CertificateType "Token-signing"`を入力して、AD FS トークンを検索します。示されているトークン署名証明書の拇印を割り当てます。AD FS トークン署名証明書の有効期限が切れた場合は、 [Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))コマンドレットを使用して、新しい AD FS トークン署名証明書のサムプリントを更新しなければなりません。

Exchange 管理シェルで次のコマンドを実行します。

```powershell
$uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"
```  


> [!NOTE]
> これらのシナリオでは、 <EM>-AdfsEncryptCertificateThumbprint</EM>パラメーターはサポートされていません。



詳細と構文については、「[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))」および「[Get-ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706)」を参照してください。

## ステップ 8: OWA と ECP の仮想ディレクトリ上で AD FS 認証を有効にする

OWA および ECP の仮想ディレクトリについては、唯一の認証方式として AD FS 認証を有効にし、他のすべての形式の認証は無効にしてください。


> [!NOTE]
> OWA 仮想ディレクトリを構成する前に、ECP 仮想ディレクトリを構成する必要があります。



ECP 仮想ディレクトリを構成するには、Exchange 管理シェルを使用します。シェル ウィンドウで次のコマンドを実行します。

```powershell
Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false
```  

OWA 仮想ディレクトリを構成するには、Exchange 管理シェルを使用します。シェル ウィンドウで次のコマンドを実行します。

```powershell
Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false
```  


> [!NOTE]
> 上記の Exchange 管理シェル コマンドは、組織内のすべてのクライアント アクセス サーバーで OWA と ECP の仮想ディレクトリを構成します。すべてのクライアント アクセス サーバーにこれらの設定を適用しない場合は、 <EM>-Identity</EM>パラメーターを使用し、クライアント アクセス サーバーを指定します。インターネットには、組織内のクライアント アクセス サーバーにのみこれらの設定を適用したいと思われますが直面しています。



詳細と構文については、「[Get-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/aa998588\(v=exchg.150\))」と「[Set-OwaVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb123515\(v=exchg.150\))」、または「[Get-EcpVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dd351058\(v=exchg.150\))」と「[Set-EcpVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dd297991\(v=exchg.150\))」を参照してください。

## ステップ 9: インターネット インフォメーション サービス (IIS) を再起動またはリサイクルする

Exchange 仮想ディレクトリに変更を加えることを含め、必要なすべてのステップを完了した後、インターネット インフォメーション サービスを再起動する必要があります。これを行うには、以下のいずれかの方法を使用します。

  - Windows PowerShell を使用:
    
    ```powershell
    Restart-Service W3SVC,WAS -noforce
    ```

  - コマンド ラインを使用: <strong>スタート</strong> ボタンをクリックし、<strong>ファイル名を指定して実行</strong> をクリックします。次に、「`IISReset /noforce`」と入力し、<strong>OK</strong> をクリックします。

  - インターネット インフォメーション サービス (IIS) マネージャーを使用: <strong>サーバー マネージャー</strong> \> <strong>IIS</strong> で、<strong>ツール</strong> をクリックして、<strong>インターネット インフォメーション サービス (IIS) マネージャー</strong> をクリックします。<strong>インターネット インフォメーション サービス (IIS) マネージャー</strong> ウィンドウで、<strong>サーバーの管理</strong> の下にあるアクション ウィンドウから <strong>再起動</strong> をクリックします。

## ステップ 10: Outlook Web App と EAC の AD FS 要求をテストする

Outlook Web App の AD FS 要求をテストするには、次の手順を実行します。

  - Web ブラウザーで Outlook Web App (例: **https://mail.contoso.com/owa**) にサインインします。

  - ブラウザー ウィンドウで証明書エラーが表示されても、そのまま Outlook Web App の Web サイトに進みます。ADFS のサインイン ページまたは資格情報の入力を要求する ADFS のプロンプトにリダイレクトされます。

  - ユーザー名 (ドメイン\\ユーザー) とパスワードを入力して、<strong>サインイン</strong> をクリックします。

Outlook Web App がウィンドウにロードされます。

EAC に対して AD FS 要求をテストするには、以下の手順を実行します。

1.  Web ブラウザーで、**https://mail.contoso.com/ecp** にアクセスします。

2.  ブラウザー ウィンドウで証明書エラーが表示されても、そのまま ECP の Web サイトに進みます。ADFS のサインイン ページまたは資格情報の入力を要求する ADFS のプロンプトにリダイレクトされます。

3.  ユーザー名 (ドメイン\\ユーザー) とパスワードを入力して、<strong>サインイン</strong> をクリックします。

4.  EAC がウィンドウにロードされるはずです。

## 把握しておくとよい補足情報

**多要素認証**

Exchange 2013 SP1 の社内展開の場合、要求を使用して Active Directory フェデレーション サービス (AD FS) 2.0 を展開して構成すると、Exchange 2013 SP1 内の Outlook Web App および EAC が証明書ベース認証、認証トークンまたはセキュリティー トークン、および指紋認証などの多要素認証方式をサポートできるようになります。2 要素認証は、しばしば他の形式の認証と混同されます。多要素認証では、3 つの認証要素のうち 2 つを使用する必要があります。その要素は次のとおりです。

  - ユーザーだけが知っているもの (たとえば、パスワード、PIN、またはパターン)

  - ユーザーだけが持っているもの (たとえば、ATM カード、セキュリティ トークン、スマート カード、または携帯電話)

  - ユーザーだけがもつ状態 (たとえば、指紋などのバイオメトリクス特性)

Windows Server 2012 R2 での多要素認証の詳細については、「[機密性の高いアプリケーションの追加の多要素認証に伴うリスクを管理します。](https://go.microsoft.com/fwlink/?linkid=392707)」および「[チュートリアル ガイド: 機密性の高いアプリケーションの追加の多要素認証に伴うリスクを管理します。](https://go.microsoft.com/fwlink/?linkid=392708)」を参照してください。

Windows Server 2012 R2 AD FS 役割サービスでは、フェデレーション サービスがセキュリティ トークン サービスとして機能し、要求で使用されるセキュリティ トークンを提供するため、多要素認証をサポートできます。フェデレーション サービスは、提示された資格情報に基づいてトークンを発行します。アカウント ストアがユーザーの資格情報を検証した後、信頼ポリシーの規則に従ってそのユーザーに対する要求が生成され、それがセキュリティ トークンに追加されてクライアントに発行されます。要求の詳細については、「[要求とは](https://go.microsoft.com/fwlink/?linkid=392709)」を参照してください。

**他のバージョンの Exchange との共存**

組織内に展開された Exchange のバージョンが複数ある場合、Outlook Web App と EAC の AD FS 認証を使用することができます。このシナリオは Exchange 2010 と Exchange 2013 の展開でのみサポートされます。またすべてのクライアントが Exchange 2013 サーバー **および** を介して接続していて、それらの Exchange 2013 サーバーに AD FS 認証が構成されてる場合のみサポートされます。

Exchange 2010 サーバー上にメールボックスを持つユーザーは、AD FS 認証用に構成された Exchange 2013 サーバーを介してメールボックスにアクセスできます。Exchange 2013 サーバーへの最初のクライアント接続では、AD FS 認証が使用されます。ただし、Exchange 2010 サーバーへのプロキシ接続では Kerberos が使用されます。AD FS を直接認証するよう Exchange Server 2010 を構成する方法はサポートされていません。

