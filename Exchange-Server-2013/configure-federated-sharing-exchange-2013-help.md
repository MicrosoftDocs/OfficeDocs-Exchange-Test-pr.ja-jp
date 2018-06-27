---
title: 'フェデレーション共有の構成: Exchange 2013 Help'
TOCTitle: フェデレーション共有の構成
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 49896423
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# フェデレーション共有の構成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-07_

Exchange Server 2013 のフェデレーション共有を使用して、ユーザーは外部のフェデレーション組織の受信者と情報を共有することができます。これには、スケジューリングのための空き時間（または「予定表の空き時間」）情報の共有や、業務上の関係性に応じてより詳細な予定表情報の共有などが含まれます。フェデレーション共有の詳細については、「[共有](sharing-exchange-2013-help.md)」を参照してください。


> [!IMPORTANT]
> Exchange Server 2013 のこの機能は、中国で 21Vianet によって運用される Office 365 との完全な互換性を備えておらず、いくつかの機能制限が適用される場合があります。詳細については、「<A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet が運用している Office 365 について</A>」を参照してください。



## 始める前に把握しておくべき情報

  - このタスクの予想所要時間:1 時間。

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 実行方法

## 手順 1:フェデレーション信頼を作成・構成します。

フェデレーション信頼は Exchange 2013 組織と Azure Active Directory 認証システムの間に信頼関係を確立し、フェデレーション共有の要件ともなります。

詳細な手順については、「[フェデレーション信頼の構成](configure-a-federation-trust-exchange-2013-help.md)」を参照してください。

## 手順 2:組織の関係を作成する

組織上の関係を使用すると、Exchange 組織内のユーザーは、他の Exchange フェデレーション組織とのフェデレーション共有の一部として予定表の空き時間情報を共有することができます。フェデレーション共有は、2 つの Exchange 2013 フェデレーション組織間、または 1 つの Exchange 2013 フェデレーション組織と複数の Exchange 2010 フェデレーション組織との間で構成できます。

詳細な手順については、「[組織の関係を作成する](create-an-organization-relationship-exchange-2013-help.md)」を参照してください。

## 手順 3:共有ポリシーの作成

共有ポリシーを使用すると、ユーザーが指定したユーザー同士の方法により、予定表情報をさまざまな種類の外部ユーザーと共有できます。これにより、外部フェデレーション組織、外部の非フェデレーション組織、およびインターネットへのアクセスが可能な個人との予定表情報や連絡先情報の共有がサポートされます。ユーザー同士または連絡先共有（組織レベルでの共有のみ）を構成する必要がない場合、共有ポリシーの構成は必要ありません。

詳細な手順については、「[共有ポリシーの作成](create-a-sharing-policy-exchange-2013-help.md)」を参照してください。

## 手順 4:自動検出のパブリック DNS レコードを構成する

エイリアスの正規名 (CNAME) リソース レコードを、インターネットに接続された DNS に追加する必要があります。新しい CNAME レコードは、インターネットに接続された自動検出サービスを実行している Exchange 2013 クライアント アクセス サーバーを指し示す必要があります。

CNAME レコードの追加方法に関する詳細な説明は、パブリック DNS レコードのホストサービスを参照してください。通常、これはドメイン Web サイトもホストしているインターネットベースのサービスです。

