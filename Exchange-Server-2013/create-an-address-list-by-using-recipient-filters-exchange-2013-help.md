---
title: '受信者フィルターを使用したアドレス一覧の作成: Exchange 2013 Help'
TOCTitle: 受信者フィルターを使用したアドレス一覧の作成
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 49896361
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 受信者フィルターを使用したアドレス一覧の作成

 

_**適用先:**Exchange Online, Exchange Server 2013_

_**トピックの最終更新日:**2014-12-16_

このトピックでは、受信者フィルターを使用してアドレス一覧を作成する方法について説明します。アドレス一覧の詳細については、「[アドレス一覧](address-lists-exchange-2013-help.md)」を参照してください。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス一覧」。

  - Exchange Online の既定では、アドレス一覧の役割はどの役割グループにも割り当てられません。アドレス一覧の役割を必要とするコマンドレットを使用するには、その役割を役割グループに追加してください。詳細については、トピック「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - *RecipientFilter* パラメーターを使用してカスタム フィルターを作成するには、フィルターの文字列を指定する必要があります。シェルでは、フィルター構文に OPATH を使用します。OPATH は、オブジェクト データ ソースをクエリするために設計されたクエリ言語です。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用し、受信者フィルターを使用してアドレス一覧を作成する

この例では、Exchange メールボックスを持ち、住所がワシントンまたはオレゴンのすべてのユーザーのアドレス一覧を作成します。

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

この例では、Exchange メールボックスがあって、*CustomAttribute15* パラメーターの値が `AgencyB` になっているすべてのユーザーのアドレス一覧が作成されます。

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

構文およびパラメーターの詳細については、「[New-AddressList](https://technet.microsoft.com/ja-jp/library/aa996912\(v=exchg.150\))」を参照してください。

