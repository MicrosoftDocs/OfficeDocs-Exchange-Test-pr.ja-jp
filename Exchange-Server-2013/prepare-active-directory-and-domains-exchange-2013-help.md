---
title: 'Active Directory とドメインを準備する: Exchange 2013 Help'
TOCTitle: Active Directory とドメインを準備する
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 48270268
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory とドメインを準備する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange Server 2013 をインストールする前に、Active Directory フォレストおよびそのドメインを準備する必要があります。Exchange では、ユーザーのメールボックスおよび組織内の Exchange サーバーの構成に関する情報を格納できるように Active Directory を準備する必要があります。Active Directory フォレストまたはドメインについてあまり理解していない場合、「[Active Directory ドメイン サービスの概要](https://go.microsoft.com/fwlink/p/?linkid=399226)」を参照してください。


> [!NOTE]
> 環境に Exchange を初めてインストールする場合でも、以前のバージョンの Exchange Server を既に実行中の場合でも、Active Directory for Exchange 2013 を準備する必要があります。Exchange 2013 で Active Directory に追加された新しいスキーマ クラスとスキーマ属性 (Service Pack (SP) および累積的な更新プログラム (CU) によって作成されたものも含む) の詳細については、「<A href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Exchange 2013 Active Directory スキーマの変更</A>」で確認できます。



Exchange の Active Directory を準備する方法はいくつかあります。1 つの方法は、Exchange 2013 セットアップ ウィザードを使用して準備する方法です。規模の大きい Active Directory が展開されておらず、Active Directory を管理する独立したチームが存在しない場合、このウィザードを使用することをお勧めします。使用するアカウントは Schema Admins と Enterprise Admins の両方のセキュリティ グループのメンバーである必要があります。セットアップ ウィザードを使用する方法の詳細については、「[セットアップ ウィザードを使用した Exchange 2013 のインストール](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)」を参照してください。

規模の大きい Active Directory を展開しているか、または独立したチームが Active Directory を管理している場合、このトピックが役立ちます。このトピックの続く手順を使用すれば、準備の各段階は非常に制御しやすくなります。また、だれが各手順を実行できるかも示されています。たとえば、Exchange の管理者には、Active Directory スキーマを拡張するために必要なアクセス許可がない場合があります。

始める前に把握しておくべき情報

1\. Active Directory スキーマを拡張する

2\. Active Directory を準備する

3\. Active Directory ドメインを準備する

正常な動作を確認する方法

Exchange 用に Active Directory を準備しているときに起こり得る問題については、「[Exchange 2013 をインストールしたときの Active Directory の変更内容](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 ～ 15 分またはそれ以上 (Active Directory レプリケーションを含みません) で、組織の規模や子ドメインの数によって変わります。

  - これらの手順を実行するために使用するコンピューターは、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」を満たしている必要があります。また、Active Directory フォレストは、「[Exchange 2013 のシステム要件](exchange-2013-system-requirements-exchange-2013-help.md)」の「ネットワークおよびディレクトリ サービス」セクションに記載されている要件を満たしている必要があります。

  - 組織に複数の Active Directory ドメインが存在している場合、以下のこと行うようお勧めします。
    
      - すべてのドメインについて、Active Directory サーバーが存在する Active Directory サイトから以下の手順を実行します。
    
      - すべてのドメインについて、書き込み可能なグローバル カタログ サーバーを使用して Active Directory サイトに最初の Exchange サーバーをインストールします。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 1\. Active Directory スキーマを拡張する

Exchange 2013 を使用できるように組織を準備する最初の手順は、Active Directory スキーマの拡張です。Exchange は多くの情報を Active Directory に格納しますが、それを行うには、事前にクラス、属性、その他のアイテムの追加と更新が必要です。スキーマを拡張する際に変更する対象については、「[Exchange 2013 Active Directory スキーマの変更](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)」を参照してください。

スキーマを拡張する前に、以下の点に注意してください。

  - ログインするアカウントは Schema Admins と Enterprise Admins のセキュリティ グループのメンバーである必要があります。

  - スキーマを拡張するためにコマンドを実行するコンピューターは、スキーマ マスターと同じ Active Directory ドメインおよびサイトに配置する必要があります。

  - *DomainController* パラメーターを使用する場合、スキーマ マスターであるドメイン コントローラーの名前を使用していることを確認してください。

  - Exchange のスキーマを拡張する方法は、このトピックの手順を使用するか、または Exchange 2013 セットアップを使用する方法しかありません。その他のスキーマを拡張する方法はサポートされていません。


> [!TIP]
> Active Directory スキーマを管理する独立したチームを持たない場合、この手順を省略して直接「Active Directory を準備する」に進むことができます。手順 1 でスキーマが拡張されない場合、手順 2 のコマンドでスキーマを拡張します。手順 1 を省略する場合でも、上記の注意事項の情報は適用されます。



準備が整ったら、以下の手順を実行して Active Directory スキーマを拡張します。複数の Active Directory フォレストが存在する場合、適切なフォレストにログインしていることを確認してください。

1.  コンピューターで Exchange 2013 セットアップを実行する準備が整っていることを確認します。セットアップを実行するために必要な事柄を確認するには、「[Exchange 2013 の前提条件](exchange-2013-prerequisites-exchange-2013-help.md)」の「[Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md)」セクションを参照してください。

2.  Windows のコマンド プロンプト ウィンドウを開き、Exchange インストール ファイルをダウンロードした場所に移動します。

3.  次のコマンドを実行して、スキーマを拡張します。
    
        Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms

セットアップでスキーマの拡張が終了したら、Active Directory が変更をすべてのドメイン コントローラーにレプリケートするまで待機している必要があります。レプリケートの進行状況を確認する場合は、`repadmin` ツールを使用することができます。`Repadmin` は、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 の Active Directory ドメイン サービス ツール機能の一部として組み込まれています。Repadmin の使用方法の詳細については、「[Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)」を参照してください。

## 2\. Active Directory を準備する

ここまでで Active Directory スキーマは拡張されました。Exchange 2013 用の Active Directory のその他の部分を準備することができます。この手順の間、Exchange は、情報を格納するために使用する Active Directory にコンテナー、オブジェクト、およびその他のアイテムを作成します。Exchange のコンテナー、オブジェクト、属性などすべてを総称して「*Exchange 組織*」と呼びます。

Exchange 用の Active Directory を準備する前に、以下の点に注意してください。

  - ログインするアカウントは Enterprise Admins セキュリティ グループのメンバーである必要があります。*PrepareAD* コマンドでスキーマを拡張するために手順 1 を省略した場合、使用するアカウントは Schema Admins セキュリティ グループのメンバーである必要もあります。

  - コマンドを実行するコンピューターは、スキーマ マスターと同じ Active Directory ドメインおよびサイトに配置する必要があります。また、TCP ポート 389 上でフォレストのすべてのドメインと通信する必要もあります。

  - 手順 1 で加えた変更をすべてのドメイン コントローラーに Active Directory がレプリケートするまで、この手順を開始しないでください。

Exchange 用の Active Directory を準備するため以下のコマンドを実行する際、Exchange 組織に名前を付ける必要があります。この名前は Exchange によって内部的に使用され、通常、ユーザーには表示されません。多くの場合、Exchange をインストールする会社の名前がこの組織名に使用されます。使用する名前は、Exchange の機能に影響することも、電子メールに使用する事柄を決定することもありません。以下の注意点に従う限り、これには任意の名前を指定できます。

  - A から Z まで大文字または小文字のいずれも使用できます。

  - 0 から 9 まで数字を使用できます。

  - 名前の先頭または末尾でない限り、スペースを含めることができます。

  - 名前にハイフンまたはダッシュを使用できます。

  - 名前は 64 文字まで指定できますが、ブランクにはできません。

  - この名前は設定したら変更できません。

準備が整ったら、以下の手順を実行して Exchange 用の Active Directory を準備します。使用する組織名にスペースが含まれる場合は、二重引用符 (") で名前を囲む必要があります。

1.  Windows のコマンド プロンプト ウィンドウを開き、Exchange インストール ファイルをダウンロードした場所に移動します。

2.  次のコマンドを実行します。
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

セットアップで Exchange 用の Active Directory の準備が終了したら、Active Directory が変更をすべてのドメイン コントローラーにレプリケートするまで待機している必要があります。レプリケートの進行状況を確認する場合は、`repadmin` ツールを使用することができます。`repadmin` は、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 の Active Directory ドメイン サービス ツール機能の一部として組み込まれています。このツールの使用方法の詳細については、「[Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879)」を参照してください。

## 3\. Active Directory ドメインを準備する

Exchange 用に Active Directory を準備するための最後の手順は、Exchange がインストールされる、またはメールが有効なユーザーを配置する各 Active Directory ドメインを準備することです。この手順では、追加のコンテナーおよびセキュリティ グループを作成し、Exchange がそれらにアクセスできるようにアクセス許可を設定します。

Active Directory フォレストに複数のドメインがある場合、ドメインを設定する方法にはいくつかの選択肢があります。実行する内容に合わせてオプションを選択してください。ドメインが 1 つだけの場合は、手順 2 の *PrepareAD* コマンドで既にドメインを準備しましたので、この手順を飛ばすことができます。

## Active Directory フォレストにすべてのドメインを準備する

すべての Active Directory ドメインを準備するには、セットアップを実行する際に *PrepareAllDomains* パラメーターを使用できます。セットアップによって、Active Directory フォレストに Exchange 用のすべてのドメインが準備されます。

Active Directory フォレストにすべてのドメインを準備する前に、以下の点に注意してください。

  - 使用するアカウントは Enterprise Admins セキュリティ グループのメンバーである必要があります。

  - 手順 2 で実行した変更をすべてのドメイン コントローラーに Active Directory がレプリケートするまで待機してください。待機しないと、ドメインの準備の試行時にエラーが発生する可能性があります。

準備が整ったら、以下を実行して Exchange 用の Active Directory フォレストにすべてのドメインを準備します。

1.  Windows のコマンド プロンプト ウィンドウを開き、Exchange インストール ファイルをダウンロードした場所に移動します。

2.  次のコマンドを実行します。
    
        Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms

## 準備する Active Directory ドメインを選択する

準備する Active Directory ドメインを選択する場合、セットアップの実行時に *PrepareDomain* パラメーターを使用できます。*PrepareDomain* パラメーターを使用する場合、準備するドメインの完全修飾ドメイン名 (FQDN) を含める必要があります。

Active Directory フォレストにドメインを準備する前に、以下の点に注意してください。

  - ドメインが作成されたタイミングに応じて、使用するアカウントにアクセス許可が必要になります。
    
      - **PrepareAD を実行する前に作成されたドメイン**   ドメインが上記の手順 2 で *PrepareAD* コマンドを実行する**前**に作成された場合、使用するアカウントは、準備するドメインの Domain Admins グループのメンバーである必要があります。
    
      - **PrepareAD を実行した後に作成されたドメイン**   ドメインが上記の手順 2 で *PrepareAD* コマンドを実行した**後**に作成された場合、使用するアカウントは、1) Organization Management 役割グループのメンバーであり、かつ 2) 準備するドメインの Domain Admins グループのメンバーである必要があります。

  - 手順 2 で実行した変更をすべてのドメイン コントローラーに Active Directory がレプリケートするまで待機してください。待機しないと、ドメインの準備の試行時にエラーが発生する可能性があります。

  - Exchange サーバーがインストールされるすべてのドメインを準備する必要があります。また、電子メールが有効なユーザーを含むドメインは Exchange サーバーが含まれていなくても、それらのドメインすべてを準備する必要があります。

  - *PrepareAD* が実行されたドメインでは、*PrepareDomain* コマンドを実行する必要はありません。*PrepareAD* コマンドはそのドメインを自動的に準備します。

準備が整ったら、以下のことを実行して Exchange 用の Active Directory フォレストの個々のドメインを準備します。

1.  Windows のコマンド プロンプト ウィンドウを開き、Exchange インストール ファイルをダウンロードした場所に移動します。

2.  次のコマンドを実行します。準備するドメインの FQDN を含めます。コマンドを実行しているドメインを準備する場合は、FQDN を含める必要はありません。
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  Exchange サーバーをインストールする、または電子メールが有効なユーザーを配置する各 Active Directory ドメインに対してこれらの手順を繰り返します。

## 正常な動作を確認する方法

上記の手順をすべて実行したら、すべてが円滑に実行されていることを確認できます。この確認を行うには、Active Directory サービス インターフェイス エディター (ADSI エディター) と呼ばれるツールを使用します。ADSI エディターは、Active Directory ドメイン サービス ツール機能の一部として、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 に含まれています。詳細については、「[ADSI エディター (adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644)」を参照してください。


> [!WARNING]
> Microsoft サポートからの指示がない限り、ADSI エディターで値は変更しないでください。ADSI エディターで値を変更すると、回復困難な障害が Exchange 組織および Active Directory に発生する恐れがあります。



Exchange によって Active Directory スキーマを拡張し、Exchange 用に Active Directory の準備を行った後、いくつかのプロパティが更新され、準備が整ったことが示されます。以下のリストの情報を使用して、それらのプロパティに適切な値が設定されていることを確認します。それぞれのプロパティは、以下に示されている、インストールしている Exchange 2013 のリリースの値と一致しなければなりません。

  - **\[スキーマ\]** 名前付けコンテキストで、**ms-Exch-Schema-Verision-Pt** の **rangeUpper** プロパティが、「Exchange 2013 Active Directory のバージョン」の表に示された Exchange 2013 のバージョンの値に設定されていることを確認します。
    
     

  - **\[構成\]** 名前付けコンテキストで、CN=\<*your organization*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domain*\> コンテナーの **objectVersion** プロパティが、「Exchange 2013 Active Directory のバージョン」の表に示された Exchange 2013 のバージョンの値に設定されていることを確認します。
    
     

  - **\[既定\]** 名前付けコンテキストで、DC=\<*root domain*の下にある **Microsoft Exchange System Objects** コンテナーの **objectVersion** プロパティが、「Exchange 2013 Active Directory のバージョン」の表に示された Exchange 2013 のバージョンの値に設定されていることを確認します。
    
     

また、Exchange のセットアップ ログをチェックして、Active Directory の準備が正常に完了していることを確認することもできます。詳細については、「[Exchange 2013 のインストールの確認](verify-an-exchange-2013-installation-exchange-2013-help.md)」を参照してください。トピック「[Exchange 2013 のインストールの確認](verify-an-exchange-2013-installation-exchange-2013-help.md)」で説明する **Get-ExchangeServer** コマンドレットは、Active Directory サイトで少なくとも 1 つのメールボックス サーバーの役割およびクライアント アクセス サーバーの役割のインストールがそれぞれ完了するまでは、使用できません。

## Exchange 2013 Active Directory のバージョン

以下の表には、新しいバージョンの Exchange 2013 をインストールするたびに更新される Active Directory の Exchange 2013 オブジェクトが示されています。表示されるオブジェクト バージョンを以下の表の値と比較することにより、インストールした Exchange 2013 のバージョンが、インストール中に Active Directory を正常に更新したことを確認できます。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Exchange のバージョン</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>名前付けコンテキスト</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>コンテナー</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Microsoft Exchange システム オブジェクト</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 以降</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>

