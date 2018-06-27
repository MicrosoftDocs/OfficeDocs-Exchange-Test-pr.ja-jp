---
title: 'オフライン アドレス帳を削除する: Exchange Online Help'
TOCTitle: オフライン アドレス帳を削除する
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 49896500
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オフライン アドレス帳を削除する

 

_**適用先:**Exchange Online, Exchange Server 2013_

このトピックでは、オフライン アドレス帳 (OAB) を削除する方法について説明します。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md) の「オフライン アドレス帳」。

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_AddressListRole\_EXOnOP)

  - ユーザーまたはメールボックス データベースにリンクされた OAB を削除した後、そのユーザーに対して新しい OAB を割り当てるまで、受信者は既定の OAB をダウンロードします。既定の OAB を削除する場合は、別の OAB を既定の OAB として割り当てる必要があります。既定の OAB を変更する手順については、「[既定のオフライン アドレス帳を変更する](change-the-default-offline-address-book-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して OAB を削除する

この例では、MY OAB という OAB を削除します。

    Remove-OfflineAddressBook -Identity "My OAB"

「**Y**」と入力して OAB を削除することを確認し、Enter キーを押します。

構文およびパラメーターの詳細については、「[Remove-OfflineAddressBook](https://technet.microsoft.com/ja-jp/library/bb123594\(v=exchg.150\))」を参照してください。

