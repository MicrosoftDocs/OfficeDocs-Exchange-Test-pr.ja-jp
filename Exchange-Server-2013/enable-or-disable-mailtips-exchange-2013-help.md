---
title: 'メール ヒントの有効化または無効化: Exchange 2013 Help'
TOCTitle: メール ヒントの有効化または無効化
ms:assetid: 11ad3848-f303-4ad5-a21d-9b0883db4bda
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ649321(v=EXCHG.150)
ms:contentKeyID: 49895258
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メール ヒントの有効化または無効化

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

Exchange 管理シェルを使用すると、組織内でメール ヒントを使用する方法を定義する各種設定を構成できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「メール ヒント」。

  - この手順を実行するには、シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してメール ヒントを有効または無効にする

組織でメール ヒントを有効または無効にするには、**Set-OrganizationConfig** コマンドレットを使用します。新しい Exchange 組織をインストールするとメール ヒントが既定で有効になります。この例では、組織内でメール ヒントを有効にする方法を示します。

    Set-OrganizationConfig -MailTipsAllTipsEnabled $true

構文およびパラメーターの詳細については、「[Set-OrganizationConfig](https://technet.microsoft.com/ja-jp/library/aa997443\(v=exchg.150\))」を参照してください。

