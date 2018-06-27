---
title: 'SharePoint の電子情報開示センター用の Exchange の構成: Exchange 2013 Help'
TOCTitle: SharePoint の電子情報開示センター用の Exchange の構成
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 49129543
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# SharePoint の電子情報開示センター用の Exchange の構成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange Server 2013 には、*パートナー アプリケーション*と呼ばれる、Microsoft SharePoint Server 2013 および Microsoft Lync Server 2013 と連携動作する機能が含まれています。これらのパートナー アプリケーションがお互いのリソースにアクセスできるようにするには、サーバー間認証を構成する必要があります。

このトピックでは、Exchange 2013 と SharePoint 2013 間のサーバー間認証を構成して、ユーザーが SharePoint 2013 の電子証拠開示センターを使用して、Exchange Server 2013 メールボックスのコンテンツを検索できるようにする方法を示します。この機能を完全に有効にするには、SharePoint 2013 で追加の手順を完了する必要があります。詳細については、「[SharePoint 2013 での電子証拠開示の構成](https://go.microsoft.com/fwlink/?linkid=257727)」を参照してください。

## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:30 分。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - 別のドメインまたはフォレストへの Exchange 2013 と SharePoint 2013 のインストールがサポートされています。Exchange フォレストと SharePoint フォレスト間の Windows 信頼関係は必要ありません。これは、その環境では、Exchange と SharePoint が OAuth 2.0 プロトコルを通して相互に信頼するためです。

  - SharePoint 2013 サイトは、SSL (Secure Sockets Layer) を使用するように構成する必要があります。

  - [Exchange Web Services Managed API](https://go.microsoft.com/fwlink/?linkid=257726) は、SharePoint 2013 を実行しているすべてのサーバーにインストールする必要があります。インストール後に Internet Information Server (IIS) をリセットします。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:SharePoint Server 2013 を実行しているサーバー上で Exchange 2013 のサーバー間認証を構成する

次のコマンドを実行して、Exchange 2013 を SharePoint 2013 内の信頼できるセキュリティ トークン発行者として作成します。

    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1

## 手順 2:Exchange 2013 を実行しているサーバー上で SharePoint 2013 のサーバー間認証を構成する

Exchange 2013 サーバー上でこの手順を実行します。この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[共有とコラボレーションのアクセス許可](sharing-and-collaboration-permissions-exchange-2013-help.md)」の「パートナー アプリケーション - 構成」。

このコマンドを実行して、SharePoint パートナーのアプリケーションを構成します。

    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint

## 手順 3:承認されたユーザーを "Discovery Management/検出の管理" 役割グループに追加する

SharePoint 2013 を使用して電子証拠開示検索を実行する必要があるユーザーを、Exchange 2013 内の "Discovery Management/検出の管理" 役割グループに追加します。詳細については、「[Exchange の電子情報開示のアクセス許可を割り当てる](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> ユーザーを "Discovery Management/検出の管理" 役割グループに追加すると、ユーザーはインプレースの電子証拠開示を使用して、すべての Exchange 2013 メールボックスを検索し、ユーザー メールボックス内の機密性の高い電子メール コンテンツにアクセスできるようになります。既定では、このアクセス許可は、"Organization Management/組織の管理" 役割グループのメンバーを含むすべてのユーザーに割り当てられていません。このアクセス許可をユーザーに割り当てる前に、組織の法務部門または人事部門に確認してください。


