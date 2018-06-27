---
title: 'SharePoint 2013 および Lync 2013 との OAuth 認証の構成: Exchange 2013 Help'
TOCTitle: SharePoint 2013 および Lync 2013 との OAuth 認証の構成
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 49896476
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# SharePoint 2013 および Lync 2013 との OAuth 認証の構成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2014-03-03_

Exchange Server 2013 では、他のアプリケーションで OAuth を使用して Exchange への認証を行えます。Exchange 2013 のパートナー アプリケーションとして、アプリケーションを構成する必要があります.

Exchange 2013 では、パートナー アプリケーション (SharePoint 2013、Lync Server 2013など) による OAuth の構成は、`Configure-EnterpriseApplication.ps1` スクリプトの使用によってのみサポートされます。スクリプトを使用してタスクを自動化することにより、パートナー アプリケーションとの認証の構成がより簡単になり、構成エラーが低減されます。スクリプトは、次のタスクを実行します。

1.  OAuth トークンを自己発行するエンタープライズ パートナー アプリケーションを構成して、Exchange への認証を正常に行います。

2.  役割ベースのアクセス制御(RBAC) の役割をパートナー アプリケーションに割り当てて、特定の Exchange Web サービス API の呼び出しを行う権限を付与します。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - パートナー アプリケーションは Exchange 2013 の認証メタデータを公開して、このアプリケーションに対する直接の信頼を確立し、認証要求を受け入れる必要があります。

  - このトピックの例では、`\Scripts` ディレクトリの次の既定の場所 (`C:\Program Files\Microsoft\Exchange Server\V15\Scripts`) を使用します。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パートナー アプリケーション - 構成」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## パートナー アプリケーションとの OAuth 認証を構成する

この手順では、`Configure-EntepririseApplication.ps1` スクリプトを使用して、パートナー アプリケーションとの OAuth 認証を構成します。リソースへのアクセスは、パートナー アプリケーションまたは RBAC の使用により偽装したユーザー (あるいは両方) に割り当てられた権限に依存します。

Exchange から OAuth 認証を構成した後には、パートナー アプリケーションは Exchange 2013 リソースを使用できます。Exchange 2013 もまた、パートナー アプリケーションによって提供されたリソースにアクセスする必要がある場合は、パートナー アプリケーションにおいても OAuth 認証を構成する必要があります。

この例では、SharePoint 2013 の OAuth 認証が構成されます。

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint

この例では、Lync Server 2013 の OAuth 認証が構成されます。

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync

## 正常な動作を確認する方法

エンタープライズ パートナー アプリケーションによる Exchange 2013 への認証が正常に構成されたことを確認するには、シェルで [Get-PartnerApplication](https://technet.microsoft.com/ja-jp/library/jj218721\(v=exchg.150\)) コマンドレットを実行して構成を取得します。また、[Test-OAuthConnectivity](https://technet.microsoft.com/ja-jp/library/jj218623\(v=exchg.150\)) コマンドレットを実行して、ユーザーのパートナー アプリケーションとの OAuth 接続をテストすることもできます。

## 詳細情報

  - ハイブリッド展開では、社内 Exchange 2013 組織と Exchange Online 組織の間で OAuth 認証を使用できます。詳細については、「[Exchange ハイブリッド展開において電子情報開示をサポートするための OAuth 認証の使用](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)」を参照してください。

  - 社内展開では、Exchange 2013 と SharePoint 2013 の間でサーバー対サーバーの認証を構成して、管理者や法令遵守担当者が SharePoint 2013 で電子情報開示センターを使用して Exchange 2013 のメールボックスを検索できるようにすることが可能です。詳細については、「[SharePoint の電子情報開示センター用の Exchange の構成](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)」を参照してください。

