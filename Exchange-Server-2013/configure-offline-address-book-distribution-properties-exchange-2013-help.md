---
title: 'オフライン アドレス帳配布のプロパティの構成: Exchange Online Help'
TOCTitle: オフライン アドレス帳配布のプロパティの構成
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 49896356
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: HT
---

# オフライン アドレス帳配布のプロパティの構成

 

_**適用先:** Exchange Online, Exchange Server 2013_

Exchange のオフライン アドレス帳 (OAB) 配布ポイントごとに、2 つの URL を構成できます。1 つは、内部の企業ネットワークからのみアクセスできる内部 URL で、もう 1 つは、インターネットからアクセスできる外部 URL です。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md) の「オフライン アドレス帳」。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して OAB 配布プロパティを構成する

この例では、OAB 仮想ディレクトリ (既定の Web サイト) 上の OAB 配布ポイントのポーリング間隔を 6 時間に設定します。

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

この例では、既定の OAB 仮想ディレクトリ OAB (既定の Web サイト) 用の https://contoso.com/OAB に OAB 配布ポイントを設定します。

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

構文およびパラメーターの詳細については、「[Set-OabVirtualDirectory](https://technet.microsoft.com/ja-jp/library/bb124707\(v=exchg.150\))」を参照してください。

## 詳細情報

[オフライン アドレス帳](offline-address-books-exchange-2013-help.md)

