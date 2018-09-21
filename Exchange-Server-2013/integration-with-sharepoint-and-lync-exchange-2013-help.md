---
title: 'SharePoint および Lync との統合: Exchange 2013 Help'
TOCTitle: SharePoint および Lync との統合
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 48269134
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# SharePoint および Lync との統合

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

MicrosoftExchange Server 2013 には、Microsoft SharePoint 2013 および Microsoft Lync 2013 と統合した多くの機能が含まれています。同様に、これらの製品は、サイト メールボックスの使用を可能にする、企業の電子情報開示やコラボレーションなどのシナリオを作成する一連の機能を提供します。

## アーカイブ、保持、および電子情報開示

電子メールおよびドキュメントを、アーカイブすること、規制遵守およびビジネス要件を満たすために必要な期間保存すること、迅速に検索して電子情報開示の要求を実現する機能は、大部分の組織で不可欠です。Exchange 2013、SharePoint 2013、および Lync Server 2013 は統合されたアーカイブ、保持、および電子情報開示機能を共に提供し、Exchange メールボックス、SharePoint ドキュメントおよび Web サイト、およびアーカイブされた Lync コンテンツの間で重要データをインプレースに保存できます。SharePoint 2013 の電子情報開示センターを利用すると、承認された検出マネージャーがこれらのストア間でコンテンツに対して電子情報開示検索を実行し、検索結果をプレビューし、法務レビューのためにデータをエクスポートできます。

## Lync Server 2013 コンテンツを Exchange 2013 にアーカイブする

Exchange 2013 と共に組織に展開された Lync Server 2013 を使用すると、共有プレゼンテーションまたはドキュメントなどインスタント メッセージングおよびオンライン会議コンテンツをユーザーの Exchange 2013 メールボックスにアーカイブするよう Lync を構成できます。Lync データを Exchange 2013 にアーカイブすることにより、保持ポリシーをそれに適用できます。アーカイブされた Lync コンテンツもあらゆる電子情報開示検索に表示されます。Lync アーカイブとその展開方法の詳細については、以下のトピックを参照してください。

  - [Lync Server 2013 のアーカイブの計画](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [Lync Server 2013 でのアーカイブの展開](https://go.microsoft.com/fwlink/p/?linkid=265006)

## SharePoint 2013 電子情報開示センターを使用して Exchange、SharePoint、および Lync のデータを検索する

Exchange 2013 を使用すると、SharePoint 2013 がフェデレーション検索 API を使用して Exchange メールボックス コンテンツを検索できます。SharePoint 2013 は電子情報開示センターを備えており、承認された担当者に電子情報開示の実行を許可します。Microsoft Search Foundation では、Exchange 2013 と SharePoint 2013 の両方に共通インデックス処理および検索インフラストラクチャが備えられ、両方のアプリケーションで同じクエリ構文を使用できます。これは、SharePoint 2013 で実行された電子情報開示検索は、Exchange 2013 でインプレースの電子情報開示を使用して実行された検索と同じ Exchange 2013 コンテンツを返すことを保証します。SharePoint 2013 電子情報開示センターを使用すると、Exchange 2013 コンテンツを PST ファイルにエクスポートするなど、電子情報開示検索で返されたコンテンツをエクスポートできます。

詳細については、以下のトピックを参照してください。

  - [インプレース電子情報開示 (eDiscovery)](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)

  - [インプレース保持と訴訟ホールド](https://docs.microsoft.com/ja-jp/exchange/security-and-compliance/in-place-and-litigation-holds)

  - [電子情報開示を構成する (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [SharePoint Server 2013 での電子情報開示の新機能](https://go.microsoft.com/fwlink/?linkid=275091)

  - [SharePoint の電子情報開示センター用の Exchange の構成](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## サイト メールボックス

多くの組織では、情報が 2 つの異なるストア (電子メールは Microsoft Exchange、ドキュメントは SharePoint) に存在し、2 つの異なるインターフェイスでそれらにアクセスします。これにより、ユーザーの操作性がばらばらになり、効果的なコラボレーションが妨げられます。サイト メールボックスを使用すると、ユーザーが Exchange 電子メールと SharePoint ドキュメントをまとめて一緒にすることによって効果的に共同作業を実施できます。ユーザーにとって、サイト メールボックスは集中ファイル キャビネットとして機能し、サイト メンバーのみがアクセスおよび編集できるプロジェクトの電子メールとドキュメントを整理する場所を提供します。サイト メールボックスは Outlook 2013 で表示され、ユーザーは重要なプロジェクトの電子メールとドキュメントに簡単にアクセスできます。さらに、同じ一連のコンテンツに、SharePoint サイト自体から直接アクセスできます。

サイト メールボックスでは、実際のコンテンツは元の場所に保持されます。Exchange は電子メールを保存するため、ユーザーは、自分のメールボックスで毎日使用しているビューと同じメッセージ ビューで電子メール スレッドを表示できます。SharePoint は、ドキュメントの共同編集およびバージョン管理を表にして、ドキュメントを保存します。Exchange は Outlook でドキュメント ビューを作成するのに十分なメタデータ (ドキュメント タイトル、最終変更日、最終変更者、サイズなど) だけを、SharePoint から同期します。

サイト メールボックスは、SharePoint 2013 から準備され、管理されます。詳細については、以下のトピックを参照してください。

  - [サイト メールボックス](site-mailboxes-exchange-2013-help.md)

  - [サイト メールボックスを構成する (SharePoint Server 2013)](https://go.microsoft.com/fwlink/p/?linkid=258264)

## 統合連絡先ストア

統合連絡先ストア (UCS) は、Microsoft Office 製品間で一貫した連絡先を用意する機能です。この機能により、ユーザーがすべての連絡先情報を Exchange 2013 メールボックスに保存できるので、Lync、Exchange、Outlook、および Outlook Web App 全体にわたって同じ連絡先情報を使用できます。

Lync Server 2013 が Exchange 2013 の環境にインストールされ、両者の間にサーバー間認証を構成した後、ユーザーは既存の連絡先の Lync Server 2013 から Exchange 2013 への移行を開始できます。詳細については、「[Lync Server 2013 での統合連絡先ストアの計画と展開](https://go.microsoft.com/fwlink/p/?linkid=275092)」を参照してください。

## ユーザーの写真

ユーザーの写真は、Outlook、Outlook Web App、SharePoint 2013、Lync 2013、およびモバイル電子メール クライアントなど、クライアント アプリケーションによってアクセスできる Exchange 2013 に高解像度のユーザーの写真を保存できる機能です。低解像度の写真も Active Directory に保存されます。統合連絡先ストアと同様に、ユーザーの写真を使用すると、組織はクライアント アプリケーションによって使用できる一貫したユーザー プロファイル写真を保持することができ、各アプリケーションがユーザーの写真を保持して写真を追加および管理する方法を自前で持つ必要がありません。ユーザーは、自分の写真を Outlook Web App、SharePoint 2013、または Lync 2013 によって管理できます。Outlook Web App で写真を管理する詳細については、「[Outlook Web App で写真とアカウント情報を更新する](https://go.microsoft.com/fwlink/p/?linkid=269646)」を参照してください。

## Outlook Web App での Lync の存在

Lync Server 2013 がインストールされた Exchange 2013 環境では、ユーザーが Outlook Web App でプレゼンス情報を確認できるように環境を構成できます。ユーザーは、それらのインスタント メッセージング連絡先およびグループを Outlook Web App のナビゲーション ウィンドウで確認し、Outlook Web App からインスタント メッセージング セッションへの応答またはセッション開始を行い、それらのインスタント メッセージング連絡先およびグループを管理できます。

## OAuth 認証

Exchange 2013、SharePoint 2013、および Lync Server 2013 は、サーバー間認証に OAuth 認証プロトコルを使用して前述の豊富な製品間機能を提供します。同じ認証プロトコルの使用により、これらのアプリケーションがセキュリティで保護されてシームレスに相互認証できます。認証機構は、アクセス要求がユーザー コンテキストで行われるリンクされたアカウントとユーザー偽装のコンテキストを使用して、認証をアプリケーションとしてサポートします。

OAuth は多数の Web サイトおよび Web サービスによって使用される標準認証プロトコルです。これを使用すると、クライアントがリソース サーバーによって提供されるリソースにユーザー名およびパスワードを入力することなくアクセスできます。認証は、リソース所有者が信頼する認証サーバーによって実行され、アクセス トークンをクライアントに提供します。トークンが特定のリソース セットに指定された期間のアクセス許可を付与します。Exchange 2013 の OAuth 実装の詳細については、「[\[MS-XOAUTH\]:OAuth 2.0 認証プロトコルの拡張](https://go.microsoft.com/fwlink/p/?linkid=275093)」を参照してください。

**社内展開での OAuth**

社内展開の中では、Exchange 2013、SharePoint 2013、および Lync Server 2013 は、認証サーバーでトークンを発行する必要がありません。これらの各アプリケーションは、自己署名付きトークンを発行して、他のアプリケーションから提供されるリソースにアクセスします。リソースへのアクセスを提供するアプリケーションは、たとえば Exchange 2013 など、呼び出し元アプリケーションによって提供される自己署名付きトークンを信頼する必要があります。信頼は、呼び出し元アプリケーションの ApplicationID、証明書、および AuthMetadataUrl を含む呼び出し元のアプリケーションの*パートナー アプリケーション*構成を作成することによって確立されます。Exchange 2013、SharePoint 2013、および Lync Server 2013 は、それらの認証メタデータ ドキュメントを既知の URL で公開します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>サーバー</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Exchange 2013 Server Auth Certificate**

Exchange 2013 セットアップは、フレンドリ名 Microsoft Exchange Server Auth Certificate で自己署名付き証明書を作成します。証明書は、Exchange 2013 組織内のすべてのフロントエンド サーバーに複製されます。証明書の拇印は、Exchange 2013 の認証構成でそのサービス名、社内の Exchange 2013 を表す既知の GUID と共に指定されます。Exchange は、認証構成を使用して、その認証メタデータ ドキュメントを公開します。


> [!IMPORTANT]
> Exchange 2013 で作成された既定の Server Auth Certificate は、5 年間有効です。認証構成に現在の証明書が含まれることを確認する必要があります。



Exchange 2013 がパートナー アプリケーションから Exchange Web サービス (EWS) 経由でアクセス要求を受信すると、https 要求の `www-authenticate` ヘッダーを解析します。ヘッダーには、呼び出し元サーバーがそのプライベート キーを使用して署名したアクセス トークンが含まれます。認証モジュールは、パートナー アプリケーション構成を使用してアクセス トークンを検証します。続いて、アプリケーションに付与された RBAC アクセス許可に基づいて、アクセスをリソースに付与します。アクセス トークンがユーザーに代わる場合、ユーザーに付与された RBAC アクセス許可が確認されます。たとえば、ユーザーが SharePoint 2013 の電子情報開示センターを使用して電子情報開示検索を実行する場合、Exchange はユーザーが "Discovery Management/探索管理" 役割グループのメンバーであるか、"Mailbox Search/メールボックス検索" 役割を割り当て済みであるかを確認し、検索しているメールボックスが RBAC 役割割り当ての範囲内にあるかを確認します。詳細については、「[アクセス許可](permissions-exchange-2013-help.md)」を参照してください。

## OAuth 認証の管理

Exchange 2013 で、OAuth 認証用にパートナー アプリケーションによって管理する必要がある構成オブジェクトが 2 つあります。

  - **AuthConfig**   AuthConfig は、Exchange 2013 セットアップによって作成され、認証メタデータの公開に使用されます。認証構成を管理する必要は、既存の証明書の有効期限が近付いたときに新しい証明書を用意する場合以外にありません。この場合、既存の証明書を更新して、新しい証明書を AuthConfig 内の次の証明書としてその有効日で構成できます。新しい証明書は組織内の他の Exchange 2013 に自動的に複製され、認証メタデータ ドキュメントは新しい証明書の詳細で更新され、AuthConfig が有効日に新しい証明書に切り替わります。

  - **パートナー アプリケーション**   パートナー アプリケーションを有効にして Exchange 2013 からアクセス トークンを要求するには、パートナー アプリケーション構成を作成する必要があります。Exchange 2013 では `Configure-EnterprisePartnerApplication.ps1` スクリプトが提供され、これにより、パートナー アプリケーション構成を簡単かつ迅速に作成して構成エラーを最小限に抑えることができます。詳細については、「[SharePoint 2013 および Lync 2013 との OAuth 認証の構成](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)」を参照してください。

