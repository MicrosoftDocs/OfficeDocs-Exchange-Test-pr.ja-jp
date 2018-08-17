---
title: 'オフライン アドレス帳でのアドレス一覧の追加または削除: Exchange Online Help'
TOCTitle: オフライン アドレス帳でのアドレス一覧の追加または削除
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 49896346
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オフライン アドレス帳でのアドレス一覧の追加または削除

 

_**適用先:** Exchange Online, Exchange Server 2013_

シェルを使用して、オフライン アドレス帳 (OAB) にアドレス一覧を追加したり、またはオフライン アドレス帳 (OAB) からアドレス一覧を削除したりすることができます。既定では、グローバル アドレス一覧 (GAL) を含む、"既定のオフライン アドレス帳" という名前の OAB が用意されています。OAB は、その OAB に含まれるアドレス一覧に基づいて生成されます。ユーザーがダウンロードできるカスタムの OAB を作成するために、OAB にアドレス一覧を追加したり、OAB からアドレス一覧を削除したりすることができます。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md) の「オフライン アドレス帳」。

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_AddressListRole\_EXOnOP)

  - アドレス一覧に対する変更は、そのアドレス一覧が含まれる OAB が生成されるまでは、クライアントのダウンロード内容には反映されません。詳細については、「[オフライン アドレス帳の更新](update-an-offline-address-book-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用して OAB にアドレス一覧を追加する

*AddressLists* パラメーターを使用すると、現在存在するアドレス一覧が上書きされます。既存のアドレス一覧をそのまま含む OAB を生成するには、*AddressLists* パラメーターにそれらの既存のアドレス一覧を含める必要があります。この例では、AddressList1 と AddressList2 に、AddressList3 を追加します。

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

構文およびパラメーターの詳細については、「[Set-OfflineAddressBook](https://technet.microsoft.com/ja-jp/library/aa996330\(v=exchg.150\))」を参照してください。

## シェルを使用して OAB からアドレス一覧を削除する

OAB からアドレス一覧を削除するには、単純にアドレス一覧のリストからそのアドレス一覧を省略します。この例は、AddressList1、AddressList2、AddressList3 から AddressList3 を削除します。

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

構文およびパラメーターの詳細については、「[Set-OfflineAddressBook](https://technet.microsoft.com/ja-jp/library/aa996330\(v=exchg.150\))」を参照してください。

