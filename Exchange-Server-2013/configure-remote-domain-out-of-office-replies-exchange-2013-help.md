---
title: 'リモート ドメインの不在時の応答の構成: Exchange 2013 Help'
TOCTitle: リモート ドメインの不在時の応答の構成
ms:assetid: 0c1e56be-7a29-4294-9762-600f9f788741
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ657713(v=EXCHG.150)
ms:contentKeyID: 49895233
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# リモート ドメインの不在時の応答の構成

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-08_

Exchange 管理シェルを使用して、リモート ドメイン経由で電子メールを送受信する方法を構成できます。次に、Exchange 管理シェルを使用して Exchange が不在時の返信の操作方法を構成する手順を示します。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 10 分

  - この手順を実行するには、シェルを使用する必要があります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メール フローのアクセス許可](mail-flow-permissions-exchange-2013-help.md)」の「リモート ドメイン」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して不在時の返信を構成する

リモート ドメインのプロパティを構成するには、**Set-RemoteDomain** コマンドレットを使用できます。

この例では、Contoso という名前のリモート ドメインの不在メッセージを無効にします。

    Set-RemoteDomain Contoso -AllowedOOFType None

この例では、外部向けの不在メッセージのみを許可します。

    Set-RemoteDomain Contoso -AllowedOOFType External

