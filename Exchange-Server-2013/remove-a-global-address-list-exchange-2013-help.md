---
title: 'グローバル アドレス一覧を削除する: Exchange Online Help'
TOCTitle: グローバル アドレス一覧を削除する
ms:assetid: 65d75b69-641b-4a37-a63c-47cf018f5f22
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232077(v=EXCHG.150)
ms:contentKeyID: 49896287
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# グローバル アドレス一覧を削除する

 

_**適用先:** Exchange Online, Exchange Server 2013_

グローバル アドレス一覧 (GAL) は、Exchange 組織内のすべてのグループ、ユーザー、および連絡先のエントリが含まれているディレクトリです。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス一覧」。

  - Exchange Online の既定では、アドレス一覧の役割はどの役割グループにも割り当てられません。アドレス一覧の役割を必要とするコマンドレットを使用するには、その役割を役割グループに追加してください。詳細については、トピック「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - 既定の GAL は削除できません。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して GAL を削除する

この例では、ドメイン コントローラー ad-server.fourthcoffee.com から GAL Fourth Coffee を削除します。

    Remove-GlobalAddressList -Identity "Fourth Coffee" -DomainController ad-server.fourthcoffee.com

「**Y**」と入力して GAL を削除することを確認し、Enter キーを押します。

構文およびパラメーターの詳細については、「[Remove-GlobalAddressList](https://technet.microsoft.com/ja-jp/library/bb124368\(v=exchg.150\))」を参照してください。

