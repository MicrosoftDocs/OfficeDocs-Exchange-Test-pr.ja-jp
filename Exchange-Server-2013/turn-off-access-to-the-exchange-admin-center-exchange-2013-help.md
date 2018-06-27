---
title: 'Exchange 管理センターへのアクセスをオフにする: Exchange 2013 Help'
TOCTitle: Exchange 管理センターへのアクセスをオフにする
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 49129416
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 管理センターへのアクセスをオフにする

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2013-05-20_

セキュリティを強化するため、組織がインターネット経由でアクセスしてくるユーザーに対して、Exchange 管理センター (EAC) へのアクセスを制限できる場合があります。ここで説明する手順では、EAC へのアクセスをオフにする方法を示します。この手順を実行しても、ユーザーは Outlook Web App の \[オプション\] にアクセスできなくなるわけではありません。


> [!NOTE]
> この手順は、ステップが適用される CAS サーバー上で EAC 管理者アクセスを完全に無効にします。内部ユーザーに対して EAC 管理者を有効にする場合は、別の CAS サーバーをインストールして、それを次のコマンドを使用して内部要求のみを処理するように構成する必要があります。<BR><CODE>Set-ECPVirtualDirectory -Identity "InternalCAS\ecp (default web site)" -AdminEnabled $True</CODE>




> [!NOTE]
> この手順は、Exchange Server 2013 の社内展開にしか適用されません。



## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「Exchange 管理センター接続」。

  - EAC を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して EAC へのインターネット アクセスをオフにする

この例では、サーバー CAS01 の EAC へのアクセスをオフにします。

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

構文およびパラメーターの詳細については、「[Set-EcpVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dd297991\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

EAC へのアクセスが正常にオフになったことを確認するには、次の手順を実行します。

1.  インターネット ブラウザーを使用して、Outlook Web App へのアクセスに使用する組織の内部または外部 URL を入力します。ただし、**/owa** ID を **/ecp** に置き換えます。たとえば、Outlook Web App へのアクセスに使用する組織の外部 URL が https://primary.tailspintoys.com/owa の場合は、https://primary.tailspintoys.com/ecp を使用します。

2.  アクセスがオフになっていると、**\[404 – Web サイトが見つかりません\]** というエラーが発生します。

