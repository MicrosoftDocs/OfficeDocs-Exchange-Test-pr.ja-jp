---
title: 'Exchange ハイブリッド展開において電子情報開示をサポートするための OAuth 認証の使用: Exchange 2013 Help'
TOCTitle: Exchange ハイブリッド展開において電子情報開示をサポートするための OAuth 認証の使用
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61292376
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ハイブリッド展開において電子情報開示をサポートするための OAuth 認証の使用

 

_**適用先:** Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

Exchange 2013 ハイブリッド組織で社内外にまたがる電子情報開示検索を正常に行うには、社内の Exchange と Exchange Online 組織間で OAuth (Open Authorization) 認証を構成する必要があります。これにより、社内およびクラウド ベースのメールボックスの検索に、インプレース電子情報開示を使用できるようになります。OAuth 認証は、Exchange ハイブリッド展開で以下の電子情報開示シナリオをサポートします。

  - クラウド ベースのアーカイブ メールボックスに Exchange Online Archiving を使用する社内メールボックスを検索する。

  - 同じ電子情報開示検索で社内およびクラウド ベースのメールボックスを検索する。

電子情報開示をサポートするように OAuth 認証を構成するための段階的な手順については、「[Exchange と Exchange Online 組織の間の OAuth 認証の構成](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)」を参照してください。

## OAuth 認証とは何ですか

OAuth 認証は、アプリケーションが互いに認証するために使用できるサーバー間の認証プロトコルです。OAuth 認証を使用すると、コンピューター間でユーザー資格情報とパスワードの受け渡しが行われません。代わりに、認証と承認はセキュリティ トークンの交換に基づいて行われ、それらのトークンによって、特定の期間、特定のリソースの集合に対するアクセス権が付与されます。

OAuth 認証には、通常、次の 3 つのものが関係します。それは、1 つの許可サーバーと、互いに通信する必要のある 2 つの領域です。セキュリティ トークンは、認証サーバー (セキュリティ トークン サーバー) によって、通信する必要のある 2 つの領域に対して発行されます。それらのトークンにより、1 つの領域からの通信をもう一方の領域が信頼すべきかどうかが検証されます。社内 Exchange 組織と Exchange Online との間で OAuth 認証を使用すると、Office 365 組織において許可サーバーの機能が Microsoft Azure Active Directory Access Control Services (ACS) によって提供されます。例えば、社内外にまたがる電子情報開示検索の際、Azure ACS によりトークンが発行され、そのトークンによって Exchange 社内組織の管理者または法令遵守担当者が Exchange Online 組織にあるメールボックスにアクセスできるようになり、その逆も可能になります。

## ハイブリッド展開における電子情報開示シナリオ

次の表に、OAuth 認証が必要な Exchange ハイブリッド展開における電子情報開示シナリオを示します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>電子情報開示シナリオ</th>
<th>OAuth 認証の必要性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 社内組織から開始された同一の電子情報開示検索において、Exchange 社内メールボックスと Exchange Online メールボックスを検索する。例えば、一度の情報開示検索で、組織内にあるすべてのメールボックスを検索する場合などです。</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p>クラウド ベースのアーカイブ メールボックスで Exchange Online Archiving を使用する Exchange 社内メールボックスを検索する。インプレース電子情報開示を使用する場合、プライマリ メールボックスとアーカイブ メールボックスの両方が検索されます。</p></td>
<td><p>○</p></td>
</tr>
<tr class="odd">
<td><p>管理者または法令遵守担当者が Exchange 社内組織から開始した電子情報開示検索により Exchange Online メールボックスを検索する。</p></td>
<td><p>○</p></td>
</tr>
<tr class="even">
<td><p>管理者または法令遵守担当者が Exchange 社内組織から開始した電子情報開示検索により、社内メールボックスを検索する。</p></td>
<td><p>X</p>

> [!NOTE]
> 既に取り上げたように、クラウド ベースのアーカイブ メールボックスを使用して社内メールボックスが構成されている場合には、OAuth 認証が必要になります。


</td>
</tr>
<tr class="odd">
<td><p>Office 365 テナント管理者、または Office 365 ユーザー アカウントにサインインした法令遵守担当者が Exchange Online または SharePoint Online の電子情報開示センターから開始した電子情報開示検索により、Exchange Online メールボックスを検索する。</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## 電子情報開示をサポートするよう OAuth 認証を構成する

Exchange ハイブリッド展開において電子情報開示をサポートするように OAuth 認証を構成するための説明については、前述の「[Exchange と Exchange Online 組織の間の OAuth 認証の構成](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)」を参照してください。

ご使用の Exchange ハイブリッド展開において OAuth が構成されていない場合には、電子情報開示を使用して、同一の電子情報開示で Exchange 社内メールボックスと Exchange Online メールボックスを検索することはできません。社内組織から開始された電子情報開示検索によって社内メールボックスを検索する必要があります。同様に、Exchange Online メールボックスの検索を実行できるのは、Exchange Online 組織から開始された電子情報開示検索、または SharePoint Online の電子情報開示センターを使用して開始された電子情報開示検索に限られます。また、社内のプライマリ メールボックスに対応するアーカイブ メールボックスが Exchange Online または Exchange Online Archiving 組織にある場合には、そうしたプライマリ メールボックスを検索することはできません。

## 詳細情報

  - OAuth 認証を使用すると、SharePoint 2013 および Lync Server 2013 などの他のアプリケーションが Exchange 2013 への認証を行うこともできます。詳細については、「[SharePoint 2013 および Lync 2013 との OAuth 認証の構成](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 と SharePoint 2013 の間でサーバー間の認証を構成し、管理者および法令遵守担当者が SharePoint 2013 の電子情報開示センターを使用して Exchange 2013 メールボックスを検索できるようにすることができます。詳細については、「[SharePoint の電子情報開示センター用の Exchange の構成](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 のハイブリッド構成ウィザードを使用して、Exchange ハイブリッド展開を構成できます。カスタマイズされた、ハイブリッド展開の構成の詳細なチェックリストについては、「[Exchange Server 展開アシスタント](https://go.microsoft.com/fwlink/p/?linkid=277105)」を参照してください。

