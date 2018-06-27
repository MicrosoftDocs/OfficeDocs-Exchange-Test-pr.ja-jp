---
title: '役割のスコープを削除する: Exchange 2013 Help'
TOCTitle: 役割のスコープを削除する
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 49896413
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 役割のスコープを削除する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-02_

管理役割スコープによって、ユーザーがどのオブジェクトを使用できるかが決定します。その後、ユーザーは自らに割り当てられているコマンドレットとパラメーターを使用して、それらのオブジェクトを変更できます。 スコープを使用しなくなった場合は、スコープを削除できます。Microsoft Exchange Server 2013 での管理役割スコープの詳細については、「[管理役割スコープについて](understanding-management-role-scopes-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[役割管理のアクセス許可](role-management-permissions-exchange-2013-help.md)」の「管理スコープ」。

  - これらの手順を実行するには、シェルを使用する必要があります。

  - スコープを削除する前に、そのスコープを使用している可能性のあるすべての管理役割の割り当てから、スコープを削除する必要があります。 役割の割り当てからスコープを削除する方法の詳細については、「[役割の割り当てを変更する](change-a-role-assignment-exchange-2013-help.md)」を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してスコープを削除する

スコープを削除するには、次の構文を使用します。

    Remove-ManagementScope <scope name>

たとえば、"Dublin Servers" スコープを削除するには、次のコマンドを使用します。

    Remove-ManagementScope "Dublin Servers"

