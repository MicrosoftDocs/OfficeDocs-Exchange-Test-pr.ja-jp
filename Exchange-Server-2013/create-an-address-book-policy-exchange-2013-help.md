---
title: 'アドレス帳ポリシーの作成: Exchange Online Help'
TOCTitle: アドレス帳ポリシーの作成
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 49896283
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# アドレス帳ポリシーの作成

 

_**適用先:**Exchange Online, Exchange Server 2013_

アドレス帳ポリシー (ABP) によって、ユーザーを特定のグループに分割し、組織のグローバル アドレス一覧 (GAL) をカスタマイズ表示することができます。ABP の作成時には、GAL、オフライン アドレス帳 (OAB)、会議室一覧、1 つ以上のアドレス一覧をポリシーに割り当てます。次に ABP をメールボックス ユーザーに割り当て、カスタマイズされた GAL にメールボックス ユーザーが Outlook と Outlook Web App でアクセスできるようにします。目標は、複数の GAL を必要とする社内組織で GAL セグメンテーションを完成するメカニズムを単純にすることです。ABP について詳しくは、「[アドレス帳ポリシー](address-book-policies-exchange-2013-help.md)」をご覧ください。

ABP に関連する追加の管理タスクについては、「[アドレス帳ポリシーの手順](address-book-policy-procedures-exchange-2013-help.md)」を参照してください。

この手順を使用するシナリオについては、「[シナリオ: アドレス帳ポリシーの展開](scenario-deploying-address-book-policies-exchange-2013-help.md)」をご覧ください。

## 始める前に把握しておくべき情報

  - 予想所要時間: 5 分未満。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス帳ポリシー」。

  - Exchange Online の既定では、アドレス一覧の役割はどの役割グループにも割り当てられません。アドレス一覧の役割を必要とするコマンドレットを使用するには、その役割を役割グループに追加してください。詳細については、トピック「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - 組織の ABP の作成は、計画を必要とする複数ステップのプロセスです。詳しくは、「[シナリオ: アドレス帳ポリシーの展開](scenario-deploying-address-book-policies-exchange-2013-help.md)」をご覧ください。

  - Exchange 管理センター (EAC) を使用して ABP を作成することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

  - 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## シェルを使用して ABP を作成する

この例では、次の設定で ABP を作成します。

  - **名前:** Fabrikam ABP のすべて

  - **GAL:** Fabrikam のすべて

  - **OAB:** Fabrikam の OAB のすべて

  - **会議室一覧:** Fabrikam 会議室のすべて

  - **アドレス一覧:** Fabrikam のすべて、Fabrikam のメールボックスのすべて、Fabrikam DL のすべて、Fabrikam の連絡先のすべて

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

構文およびパラメーターの詳細については、「[New-AddressBookPolicy](https://technet.microsoft.com/ja-jp/library/hh529913\(v=exchg.150\))」を参照してください。

## 詳細情報

[メール ユーザーへのアドレス帳ポリシーの割り当て](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

