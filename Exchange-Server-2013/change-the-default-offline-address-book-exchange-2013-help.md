---
title: '既定のオフライン アドレス帳を変更する: Exchange Online Help'
TOCTitle: 既定のオフライン アドレス帳を変更する
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 49896280
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 既定のオフライン アドレス帳を変更する

 

_**適用先:**Exchange Online, Exchange Server 2013_

既定では、メールボックス サーバーの役割をインストールすると、"既定のオフライン アドレス帳" という名前の Web ベースの既定のオフライン アドレス帳 (OAB) が作成されます。既定の OAB として、Exchange 組織内の任意の OAB を設定できます。この新しい既定の OAB は、新たに作成されるすべてのメールボックス データベースに関連付けられます。既定の OAB は組織内で 1 つしか設定できません。既定の OAB を削除しても、MicrosoftExchange によって別の OAB が既定として自動的に割り当てられることはありません。手動で、別の OAB を既定として指定する必要があります。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「オフライン アドレス帳」。

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_AddressListRole\_EXOnOP)

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して既定の OAB を変更する

この例では、My OAB という名前の OAB を既定の OAB として設定します。

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

構文およびパラメーターの詳細については、「[Set-OfflineAddressBook](https://technet.microsoft.com/ja-jp/library/aa996330\(v=exchg.150\))」を参照してください。

