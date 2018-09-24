---
title: 'AD LDS の構成を変更する: Exchange 2013 Help'
TOCTitle: AD LDS の構成を変更する
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61180555
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# AD LDS の構成を変更する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2015-04-08_

**ConfigureAdam.ps1** スクリプト ($env:ExchangeInstallPath\\Scripts に配置) を使用すれば、エッジ トランスポート サーバーを Exchange 組織にサブスクライブする前に、エッジ トランスポート サーバー上の既定の Active Directory ライトウェイト ディレクトリ サービス (AD LDS) 構成を変更できます。


> [!IMPORTANT]
> <STRONG>ConfigureAdam.ps1</STRONG> スクリプトは、<STRONG>dsdbutil</STRONG> コマンドを呼び出して AD&nbsp;LDS のレジストリ設定を変更します。<STRONG>dsdbutil</STRONG> コマンドは経験豊富な管理者のみを対象とした AD&nbsp;LDS 管理ツールです。AD&nbsp;LDS 構成を変更する場合は、<STRONG>ConfigureAdam.ps1</STRONG> の使用をお勧めします。



**ConfigureAdam.ps1** スクリプトには、次の表内のパラメーターを使用できます。これらのパラメーターのいずれか、すべて、または特定の組み合わせを使用して AD LDS を変更できます。

### ConfigureAdam.ps1 スクリプトに使用可能なパラメーター

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>LDAP 通信に使用されるポートを変更します。エッジ トランスポート サーバーは、既定で標準以外のポート 50389 を使用します。</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>セキュア LDAP 通信に使用されるポートを変更します。エッジ トランスポート サーバーは、既定で標準以外のポート 50636 を使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>ログ ファイルの場所を変更します。既定で、エッジ トランスポート サーバーはログ ファイルを %ExchangeInstallPath%Transport Roles\Data\adam パスに作成します。</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>ディレクトリ データベース ファイルの場所を変更します。既定で、エッジ トランスポート サーバーはディレクトリ データベースを %ExchangeInstallPath%Transport Roles\Data\adam パスに保存します。</p></td>
</tr>
</tbody>
</table>


## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「エッジ トランスポート サーバー」。

  - エッジ トランスポート サーバーの AD LDS 構成を変更する必要がある場合は、エッジ トランスポート サーバーを Exchange 組織にサブスクライブする前に実行します。サブスクライブしたエッジ トランスポート サーバーの AD LDS 構成を変更した場合は、エッジ トランスポート サーバーを Exchange 組織にサブスクライブし直す必要があります。

  - レジストリ設定を変更するときは、必ず、スクリプトを使用してください。AD LDS 構成のレジストリを手動で変更すると、AD LDS インスタンスが使用できなくなる可能性があります。

  - AD LDS で使用される LDAP ポートまたは SSL ポートを変更する必要がある場合は、まず、選択したポートが他のアプリケーションで使用されていないことを確認します。エッジ トランスポート サーバーで使用中のポートを確認するには、**netstat** コマンドを使用します。

  - この手順を実行するには、シェルを使用する必要があります。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## エッジ トランスポート サーバー上の AD LDS 構成を変更する

この例では、AD LDS で使用される LDAP ポートを 5000 に変更します。アンパサンド (&) はコマンド構文の一部です。

  ```powershell
  & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000
  ```

この例では、AD LDS 構成に次のような変更を加えます。アンパサンド (&) はコマンド構文の一部です。パラメーターとその値の間に使用されているコロン (:) に注意してください。

  - LDAP ポートを 5000 に変更する

  - SSL ポートを 500 に変更する

  - ログ パスを D:\\Exchange Server\\Data\\ADLDS に変更する

  - データ パスを D:\\Exchange Server\\Data\\ADLDS に変更する

<!-- end list -->

  ```powershell
  & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"
  ```

