---
title: 'アドレス一覧を移動する: Exchange 2013 Help'
TOCTitle: アドレス一覧を移動する
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 49896470
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アドレス一覧を移動する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-14_

ここでは、既存のアドレス一覧をルート アドレス一覧の下の新しいコンテナーに移動する方法について説明します。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス一覧」。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してアドレス一覧を移動する

この例では、アドレス一覧の GUID を使用して、アドレス一覧を「All Users\\Sales」コンテナーにある「Building 4」というコンテナーに移動します。

    Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"

「**Y**」と入力してこのアドレス一覧を移動することを確認し、Enter キーを押します。

構文およびパラメーターの詳細については、「[Move-AddressList](https://technet.microsoft.com/ja-jp/library/bb124520\(v=exchg.150\))」を参照してください。

