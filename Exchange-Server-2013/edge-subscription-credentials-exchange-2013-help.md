---
title: 'エッジ サブスクリプション資格情報: Exchange 2013 Help'
TOCTitle: エッジ サブスクリプション資格情報
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61180552
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# エッジ サブスクリプション資格情報

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-03-09_

このトピックでは、エッジ サブスクリプション プロセスで EdgeSync 同期プロセスのセキュリティ保護を支援するために使用される資格情報を準備する方法と、EdgeSync でそれらの資格情報を使用して Exchange 2013 メールボックス サーバーとエッジ トランスポート サーバー間のセキュア LDAP 接続を確立する方法について説明します。エッジ サブスクリプション プロセスの詳細については、「[エッジ サブスクリプション](edge-subscriptions-exchange-2013-help.md)」を参照してください。

**目次**

エッジ サブスクリプション プロセス

EdgeSync レプリケーション アカウント

最初のレプリケーションを認証する

スケジュールされた同期セッションを認証する

EdgeSync レプリケーション アカウントを更新する

## エッジ サブスクリプション プロセス

エッジ トランスポート サーバーを Active Directory サイトにサブスクライブすることによって、Active Directory サイト内のメールボックス サーバーとサブスクライブしたエッジ トランスポート サーバー間の同期関係が確立されます。エッジ サブスクリプション プロセス中に準備される資格情報は、境界ネットワーク内のメールボックス サーバーとエッジ トランスポート サーバー間の LDAP 接続をセキュリティで保護するために使用されます。

エッジ トランスポート サーバー上で **New-EdgeSubscription** コマンドレットを実行すると、ローカル サーバー上の Active Directory ライトウェイト ディレクトリ サービス (AD LDS) ディレクトリに EdgeSync ブートストラップ レプリケーション アカウント (ESBRA) 資格情報が作成され、エッジ サブスクリプション ファイルに書き込まれます。これらの資格情報は、最初の同期を確立するためにのみ使用され、エッジ サブスクリプション ファイルの作成後 24 時間で有効期限が切れます。エッジ サブスクリプション プロセスが 24 時間以内に完了しなかった場合は、再度 **New-EdgeSubscription** コマンドレットを実行して、新しいエッジ サブスクリプション ファイルを作成する必要があります。エッジ サブスクリプション XML ファイルには、エッジ サブスクリプションに関する構成データが保存されます。

エッジ サブスクリプション XML ファイルに保存されるデータを次の表に示します。

### エッジ サブスクリプション ファイルの内容

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>サブスクリプション データ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerName</strong></p></td>
<td><p>エッジ トランスポート サーバーの NetBIOS 名。エッジ サブスクリプションの Active Directory 名がこの名前と一致します。</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServerFQDN</strong></p></td>
<td><p>エッジ トランスポート サーバーの完全修飾ドメイン名 (FQDN)。サブスクライブ先の Active Directory サイト内のメールボックス サーバーは、DNS を使用して FQDN を解決することによって、エッジ トランスポート サーバーを検出できる必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeCertificateBlob</strong></p></td>
<td><p>エッジ トランスポート サーバーの自己署名証明書の公開キー。</p></td>
</tr>
<tr class="even">
<td><p><strong>ESRAUsername</strong></p></td>
<td><p>ESBRA に割り当てられる名前。ESBRA アカウントは、次の形式に従います。ESRA.<em>エッジ トランスポート サーバー名</em>。ESRA は EdgeSync レプリケーション アカウントの略です。ESBRA (初期ブートストラップ レプリケーション アカウント) と ESRA の違いに注意してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ESRAPassword</strong></p></td>
<td><p>ESBRA に割り当てられたパスワード。このパスワードは、乱数ジェネレーターを使用して生成され、クリア テキストでエッジ サブスクリプション ファイルに保存されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>EffectiveDate</strong></p></td>
<td><p>エッジ サブスクリプション ファイルの作成日。</p></td>
</tr>
<tr class="odd">
<td><p><strong>期間</strong></p></td>
<td><p>これらの資格情報が有効期限切れになるまでの時間。ESBRA アカウントは、24 時間のみ有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>AdamSslPort</strong></p></td>
<td><p>Active Directory から AD LDS にデータを同期するときに EdgeSync がバインドするセキュア LDAP ポート。既定では、これは TCP ポート 50636 です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProductID</strong></p></td>
<td><p>エッジ トランスポート サーバーのライセンス情報。エッジ サブスクリプションを作成する前に、エッジ トランスポート サーバーをライセンス認証する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>VersionNumber</strong></p></td>
<td><p>エッジ サブスクリプション ファイルのバージョン番号。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SerialNumber</strong></p></td>
<td><p>エッジ トランスポート サーバーの Exchange バージョン。</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> ESBRA 資格情報は、クリア テキストでエッジ サブスクリプション ファイルに書き込まれます。このファイルはサブスクリプション プロセスを通して保護する必要があります。エッジ サブスクリプション ファイルを Exchange 組織にインポートしたら、エッジ トランスポー トサーバー、Exchange&nbsp;組織にファイルをインポートするために使用したネットワーク共有、およびすべてのリムーバブル メディアから、エッジ サブスクリプション ファイルを直ちに削除する必要があります。



ページのトップへ

## EdgeSync レプリケーション アカウント

EdgeSync レプリケーション アカウント (ESRA) は、EdgeSync セキュリティの重要な部分です。ESRA の認証と承認は、エッジ トランスポート サーバーとメールボックス サーバー間の接続をセキュリティで保護するために使用されるメカニズムです。

エッジ サブスクリプション ファイルに保存された ESBRA は、最初の同期中にセキュア LDAP 接続を確立するために使用されます。エッジ サブスクリプション ファイルをエッジ トランスポート サーバーのサブスクライブ先である Active Directory サイト内のメールボックス サーバーにインポートすると、エッジ トランスポート サーバーとメールボックス サーバーのペアごとに追加の ESRA アカウントが Active Directory に作成されます。最初の同期時に、新しく作成された ESRA 資格情報が AD LDS へレプリケートされます。これらの ESRA 資格情報は、以後の同期セッションをセキュリティで保護するために使用されます。

各 EdgeSync レプリケーション アカウントに、次の表に示すプロパティが割り当てられます。

### Ms-Exch-EdgeSyncCredential のプロパティ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ名</th>
<th>種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>String</p></td>
<td><p>これらの資格情報を承認するエッジ トランスポート サーバー。</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>文字列</p></td>
<td><p>これらの資格情報を提供するメールボックス サーバー。資格情報がブートストラップ資格情報の場合、この値は空です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>この資格情報の使用を開始する日時。</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>この資格情報の使用を停止する日時。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>文字列</p></td>
<td><p>認証に使用されるユーザー名。</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>Byte</p></td>
<td><p>認証に使用されるパスワード。パスワードは、<strong>ms-Exch-EdgeSync-Certificate</strong> を使用して暗号化されます。</p></td>
</tr>
</tbody>
</table>


以降のセクションでは、EdgeSync 同期プロセス中に、ESRA 資格情報を準備して使用する方法について説明します。

## EdgeSync ブートストラップ レプリケーション アカウントを準備する

**New-EdgeSubscription** コマンドレットがエッジ トランスポート サーバーで実行されるとき、ESBRA は次のように準備されます。

  - 自己署名証明書 (Edge-Cert) が、エッジ トランスポート サーバーで作成されます。秘密キーはローカル コンピューター ストアに格納され、公開キーはエッジ サブスクリプション ファイルに書き込まれます。

  - ESBRA アカウントが AD LDS で作成され、その資格情報がエッジ サブスクリプション ファイルに書き込まれます。

  - エッジ サブスクリプション ファイルはリムーバブル メディアにコピーすることによってエクスポートされます (エッジ サーバーは Active Directory 内に存在しないため、ファイルのエクスポートに共有フォルダーを使用できません)。これで、ファイルをメールボックス サーバーにインポートする準備ができました。

## Active Directory で EdgeSync レプリケーション アカウントを準備する

エッジ サブスクリプション ファイルをメールボックス サーバーにインポートするときに、Active Directory でエッジ サブスクリプションのレコードを設定し、追加の ESRA 資格情報を準備するための次の手順が実行されます。

1.  Active Directory でエッジ トランスポート サーバー構成オブジェクトが作成されます。Edge-Cert 証明書は、このオブジェクトに属性として書き込まれます。

2.  サブスクライブ先の Active Directory サイト内のすべてのメールボックス サーバーが、新しいエッジ サブスクリプションが登録されたことを示す Active Directory 通知を受け取ります。通知を受信するとすぐに、各メールボックス サーバーは ESRA.edge アカウントを取得し、Edge-Cert 公開キーを使用してそのアカウントを暗号化します。暗号化された ESRA.edge アカウントは、エッジ トランスポート サーバー構成オブジェクトに書き込まれます。

3.  メールボックス サーバーごとに、自己署名証明書 (TransportService-Cert) が作成されます。秘密キーはローカル コンピューター ストアに保存され、公開キーは Active Directory 内のメールボックス サーバー構成オブジェクトに保存されます。

4.  各メールボックス サーバーは、独自の TransportService 証明書の公開キーを使用して ESRA.edge アカウントを暗号化し、独自の構成オブジェクトに保存します。

5.  各メールボックス サーバーは、Active Directory 内の既存のエッジ トランスポート サーバー構成オブジェクトごとに ESRA (ESRA.edge. *Mailboxname.\#*) を生成します。
    
    例 : ESRA.edge.Example.0
    
    ESRA.edge 用のパスワードは、乱数ジェネレーターによって生成され、TransportService-Cert 証明書の公開キーを使用して暗号化されます。パスワードは、Windows Server に対して許可された最大長で生成されます。

6.  各 ESRA.edge.*Mailboxname.\#* アカウントは、Edge-Cert 証明書の公開キーを使用して暗号化され、Active Directory 内のエッジ トランスポート サーバー構成オブジェクトに保存されます。

次のセクションでは、EdgeSync 同期中のこれらのアカウントの使用方法について説明します。

ページのトップへ

## 最初のレプリケーションを認証する

最初の ESBRA アカウントは、最初の同期の確立時にのみ使用されます。最初の EdgeSync 同期中に、追加の ESRA アカウントである ESRA.edge.*Mailboxname.\#* が AD LDS にレプリケートされます。これらのアカウントは、以降の EdgeSync 同期セッションの認証に使用されます。

最初のレプリケーションを実行するメールボックス サーバーはランダムに決定されます。トポロジ スキャンを実行して新しいエッジ サブスクリプションを検出する Active Directory サイト内の最初のメールボックス サーバーが最初のレプリケーションを実行します。この検出はトポロジ スキャンのタイミングに基づいているため、サイト内のすべてのメールボックス サーバーが最初のレプリケーションを実行する可能性があります。

EdgeSync がメールボックス サーバーからエッジ トランスポート サーバーへのセキュア LDAP セッションを開始します。エッジ トランスポート サーバーが自己署名証明書を提示し、メールボックス サーバーがその証明書が Active Directory 内のエッジ トランスポート サーバー構成オブジェクトに保存されている証明書と一致することを確認します。エッジ トランスポート サーバーの ID が確認されると、メールボックス サーバーが ESRA.edge.*Mailboxname.\#* アカウントの資格情報をエッジ トランスポート サーバーに提供します。エッジ トランスポート サーバーは、その資格情報を AD LDS に保存されているアカウントと照合します。

その後で、メールボックス サーバー上の EdgeSync サービスが、トポロジ、構成、および受信者データを Active Directory から AD LDS にプッシュします。Active Directory 内のエッジ トランスポート サーバー構成オブジェクトに対する変更は、AD LDS にレプリケートされます。AD LDS が新しく追加された ESRA.edge.*Mailboxname.\#* エントリを受信し、Microsoft Exchange Credential Service が対応する AD LDS アカウントを作成します。これらのアカウントは、以降のスケジュールされた EdgeSync 同期セッションの認証に使用できます。

## Microsoft Exchange Credential Service

Microsoft Exchange Credential Service は、エッジ サブスクリプション プロセスの一部です。この資格情報サービスはエッジ トランスポート サーバー上でのみ動作します。このサービスが AD LDS で双方向の ESRA アカウントを作成し、EdgeSync 同期を実行するためにメールボックス サーバーがエッジ トランスポート サーバーで認証を受けることができるようにします。EdgeSync は、Microsoft Exchange Credential Service と直接通信しません。Microsoft Exchange Credential Service は AD LDS と通信し、メールボックス サーバーが ESRA 資格情報を更新するたびに、その情報をインストールします。

ページのトップへ

## スケジュールされた同期セッションを認証する

初期 EdgeSync 同期が完了すると、EdgeSync 同期スケジュールが設定され、変更されたすべての Active Directory データが定期的に AD LDS で更新されます。メールボックス サーバーが、エッジ トランスポート サーバー上の AD LDS インスタンスとのセキュア LDAP セッションを開始します。AD LDS は、自己署名証明書を提示することによって、そのメールボックス サーバーに身元を証明します。メールボックス サーバーは、その ESRA.edge 資格情報を AD LDS に提供します。ESRA.edge パスワードは、メールボックス サーバーの自己署名証明書の公開キーを使用して暗号化されます。その特別なメールボックス サーバーだけがそれらの資格情報を使用して AD LDS に対して認証されます。

ページのトップへ

## EdgeSync レプリケーション アカウントを更新する

ESRA アカウントのパスワードは、ローカル サーバーのパスワード ポリシーに従っている必要があります。パスワード更新プロセスで一時的な認証エラーが発生しないようにするために、最初の ESRA.edge アカウントが有効期限切れになる 7 日前に 2 つ目の ESRA.edge アカウントが作成されます。その有効期限は、最初の ESRA の有効期限の 3 日前です。2 つ目の ESRA.edge アカウントが有効になるとすぐに、EdgeSync が最初のアカウントの使用を停止し、2 つ目のアカウントの使用を開始します。最初のアカウントが有効期限に達すると、それらの ESRA 資格情報は削除されます。この更新処理は、エッジ サブスクリプションが削除されるまで継続されます。

ページのトップへ

