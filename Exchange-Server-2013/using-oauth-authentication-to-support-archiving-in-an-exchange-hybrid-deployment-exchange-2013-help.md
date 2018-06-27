---
title: 'OAuth 認証を使用する Exchange ハイブリッド展開での Archiving のサポート: Exchange 2013 Help'
TOCTitle: OAuth 認証を使用する Exchange ハイブリッド展開での Archiving のサポート
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62247354
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# OAuth 認証を使用する Exchange ハイブリッド展開での Archiving のサポート

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Exchange 2013 ハイブリッド展開で Exchange Online Archiving (EOA) を Exchange Server のために使用する場合、Exchange 2013 Cumulative Update 5 (CU5) にアップグレードした後に、社内組織と Exchange Online 組織との間に OAuth 認証を構成する必要があります。EOA によって、社内メールボックスのあるユーザー用にクラウド ベースのアーカイブを持つことができます。このシナリオでは、社内メールボックス サーバーのメッセージング レコード管理 (MRM) アシスタントがアーカイブ ポリシーを適用して、メッセージをユーザーのメールボックスからユーザーのクラウド ベースのアーカイブに自動的に移動します。Exchange 2013 CU5 では、OAuth 認証が使用されます。

OAuth 認証を構成する詳細な手順については、「[Exchange と Exchange Online 組織の間の OAuth 認証の構成](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)」を参照してください。

## OAuth 認証とは何ですか

OAuth 認証は、アプリケーションが互いに認証するために使用できるサーバー間の認証プロトコルです。OAuth 認証を使用すると、コンピューター間でユーザー資格情報とパスワードの受け渡しが行われません。代わりに、認証と承認は、セキュリティ トークンの交換に基づくものとなります。これにより、特定のリソースのセットに対する特定の期間のアクセスを許可します。

OAuth 認証には、通常、次の 3 つのものが関係します。それは、1 つの認証サーバーと、互いに通信する必要のある 2 つの領域です。セキュリティ トークンは、認証サーバー (セキュリティ トークン サーバー) によって、通信する必要のある 2 つの領域に対して発行されます。それらのトークンにより、1 つの領域からの通信をもう一方の領域が信頼すべきかどうかが検証されます。オンプレミスの Exchange 組織と Exchange Online の間で OAuth 認証を使用するとき、認証サーバーの機能は、Office 365 組織内の Azure Active Directory アクセス制御サービス (ACS) によって提供されます。たとえば、社内外にまたがる電子情報開示検索の際、Azure Active Directory ACS によりトークンが発行され、そのトークンによって Exchange オンプレミス組織の管理者または法令遵守担当者が Exchange Online 組織にあるメールボックスにアクセスできるようになり、その逆も可能になります。

## Archiving をサポートするように OAuth 認証を構成する

前述のように、Exchange ハイブリッド展開で Archiving をサポートするように OAuth 認証を構成する方法については、「[Exchange と Exchange Online 組織の間の OAuth 認証の構成](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)」を参照してください。

OAuth が Exchange ハイブリッド展開のために構成されていない場合は、社内組織にあるユーザーのプライマリ メールボックスから Exchange Online にあるユーザーのクラウド ベースのアーカイブにアイテムを自動的に移動するアーカイブ ポリシーを使用できません。

## 詳細情報

  - さらに、単一の電子情報開示検索によって社内メールボックスとクラウド ベースのメールボックスで社内外にまたがる電子情報開示検索を実行するための、OAuth 認証を構成する必要があります。「[Exchange ハイブリッド展開において電子情報開示をサポートするための OAuth 認証の使用](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)」を参照してください。

  - さらに、SharePoint 2013 や Lync Server 2013 などの他のアプリケーションを Exchange 2013 に対して認証できるように OAuth 認証を構成することもできます。詳細については、「[SharePoint 2013 および Lync 2013 との OAuth 認証の構成](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 と SharePoint 2013 の間にサーバー間の認証を構成して、管理者とコンプライアンス担当者が SharePoint 2013 の電子情報開示センターを使用して Exchange 2013 メールボックスを検索できるようにすることができます。詳細については、「[SharePoint の電子情報開示センター用の Exchange の構成](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)」を参照してください。

  - Exchange 2013 のハイブリッド構成ウィザードを使用して、Exchange ハイブリッド展開を構成できます。カスタマイズされた、ハイブリッド展開の構成の詳細なチェックリストについては、「[Exchange Server 展開アシスタント](https://go.microsoft.com/fwlink/p/?linkid=277105)」を参照してください。

