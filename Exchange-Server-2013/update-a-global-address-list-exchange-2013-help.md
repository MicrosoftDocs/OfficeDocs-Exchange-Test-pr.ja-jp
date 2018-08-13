---
title: 'グローバル アドレス一覧の更新: Exchange 2013 Help'
TOCTitle: グローバル アドレス一覧の更新
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 49895292
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# グローバル アドレス一覧の更新

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2014-12-16_

シェルを使用してグローバル アドレス一覧 (GAL) を更新できます。GAL とは、MicrosoftExchange が実装されている組織内のすべてのグループ、ユーザー、連絡先のエントリが含まれているディレクトリのことです。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス一覧」。

  - Exchange Online の既定では、アドレス一覧の役割はどの役割グループにも割り当てられません。アドレス一覧の役割を必要とするコマンドレットを使用するには、その役割を役割グループに追加してください。詳細については、トピック「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して GAL を更新する

この例では、Fourth Coffee 会社の GAL を更新します。


> [!NOTE]
> このコマンドを実行すると、更新処理が開始されるだけです。GAL が更新されるまで数時間かかる場合があります。



    Update-GlobalAddressList -Identity "Fourth Coffee"

構文およびパラメーターの詳細については、「[Update-GlobalAddressList](https://technet.microsoft.com/ja-jp/library/aa998806\(v=exchg.150\))」を参照してください。

