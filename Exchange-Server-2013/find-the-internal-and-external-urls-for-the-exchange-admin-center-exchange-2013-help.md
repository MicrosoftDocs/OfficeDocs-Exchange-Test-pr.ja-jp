---
title: 'Exchange 管理センターの内部 URL および外部 URL を検索する: Exchange 2013 Help'
TOCTitle: Exchange 管理センターの内部 URL および外部 URL を検索する
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 49896217
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 管理センターの内部 URL および外部 URL を検索する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2013-02-04_

Exchange 管理センター (EAC) は Exchange Server 2013 の Web ベースの管理コンソールであるため、Web ブラウザーの ECP 仮想ディレクトリの URL を使用してこれにアクセスします。このトピックでは、ECP 仮想ディレクトリの URL を見つける方法を説明します。


> [!NOTE]
> ECP は、Exchange Server 2010 用に開発された Web ベースのユーザー インターフェイスです。仮想ディレクトリ用の EAC のコマンドレットでは、名前に "ECP" がまだ使用されており、これらのコマンドレットを使用して Exchange 2010 および Exchange 2013 ECP 仮想ディレクトリを管理できます。



EAC の詳細については、「[Exchange 2013 の Exchange 管理者センター](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - EAC を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[Exchange およびシェル インフラストラクチャのアクセス許可](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)」の「Exchange 管理センター接続」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して ECP 仮想ディレクトリ用の内部および外部 URL を検索する

この例では、ECP 仮想ディレクトリ名、内部 URL、外部 URL を書式付きのリストで返します。

    Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL

コマンドの実行が終了したら、Web ブラウザー内の *InternalURL* または *ExternalURL* の値を使用して EAC を起動します。

構文およびパラメーターの詳細については、「[Get-EcpVirtualDirectory](https://technet.microsoft.com/ja-jp/library/dd351058\(v=exchg.150\))」を参照してください。

