---
title: 'アドレス帳ポリシーの設定の変更: Exchange Online Help'
TOCTitle: アドレス帳ポリシーの設定の変更
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 49896442
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アドレス帳ポリシーの設定の変更

 

_**適用先:**Exchange Online, Exchange Server 2013_

アドレス帳ポリシー (ABP) を作成したら、名前および割り当てられたグローバル アドレス一覧 (GAL)、オフライン アドレス帳 (OAB)、会議室一覧、およびアドレス一覧を表示または変更することができます。

ABP に関連する追加の管理タスクについては、「[アドレス帳ポリシーの手順](address-book-policy-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス帳ポリシー」。

  - 組織の ABP の作成は、計画を必要とする複数ステップのプロセスです。詳細については、「[シナリオ: アドレス帳ポリシーの展開](scenario-deploying-address-book-policies-exchange-2013-help.md)」を参照してください。

  - Exchange 管理センター (EAC) を使用して ABP を構成することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

  - 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 必要な作業

## ABP の OAB、会議室一覧、および GAL を変更する

この例では、「All Fabrikam ABP」という名前の ABP を割り当てられたメールボックス ユーザーが使用する OAB、会議室一覧、および GAL を変更します。

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## ABP のアドレス一覧を置き換える

既存の ABP に指定したアドレス一覧は、ABP 内のすべてのアドレス一覧を置き換えます。

この例では、既存のアドレス一覧を、「Government Agency A」という名前の ABP のアドレス一覧「GovernmentAgencyA-Atlanta」および「GovernmentAgencyA-Moscow」と置き換えます。

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## ABP にアドレス一覧を追加する

ABP で既に定義されているアドレス一覧を保持するには、ABP に新しい一覧を追加するときに既にあるアドレス一覧を指定する必要があります。

次の例では、「Contoso-Chicago」という名前のアドレス一覧を「ABP Contoso」という ABP に追加します。この ABP は、「Contoso Seattle」というアドレス一覧を使用するように既に構成されています。

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## ABP からアドレス一覧を削除する

ABP で既に定義されているアドレス一覧を削除するには、保持するアドレス一覧を指定する必要があります。

たとえば、「ABPFabrikam」という名前の ABP が「Fabrikam-HR」および「Fabrikam-Finance」という名前のアドレス一覧を使用しているとします。ABP から「Fabrikam-HR」アドレス一覧を削除するには、保持する「Fabrikam-Finance」アドレス一覧を指定します。

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## 詳細情報

構文およびパラメーターの詳細については、「[Set-AddressBookPolicy](https://technet.microsoft.com/ja-jp/library/hh529945\(v=exchg.150\))」を参照してください。

