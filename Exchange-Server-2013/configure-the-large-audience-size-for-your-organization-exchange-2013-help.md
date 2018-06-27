---
title: '組織の大きなオーディエンス サイズの構成: Exchange Online Help'
TOCTitle: 組織の大きなオーディエンス サイズの構成
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 49896352
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の大きなオーディエンス サイズの構成

 

_**適用先:**Exchange Online, Exchange Server 2013_

Exchange 管理シェルを使用して、組織でメール ヒントを使用する方法を定義することができます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「メール ヒント」。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して組織の大きな対象サイズを構成する

**Set-OrganizationConfig** コマンドレットを使用して組織の大きな対象サイズを構成します。送信者が構成したサイズより多い受信者にメッセージを送信した場合、配信対象が大きい場合のメール ヒントが表示されます。大きな対象サイズは既定で 25 に設定されています。この例では、組織内で大きな対象サイズを 50 に構成します。

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

構文およびパラメーターの詳細については、「[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))」を参照してください。

