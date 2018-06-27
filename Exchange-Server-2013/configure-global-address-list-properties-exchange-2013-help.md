---
title: 'グローバル アドレス一覧のプロパティを構成する: Exchange Online Help'
TOCTitle: グローバル アドレス一覧のプロパティを構成する
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 49896275
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# グローバル アドレス一覧のプロパティを構成する

 

_**適用先:**Exchange Online, Exchange Server 2013_

ここでは、グローバル アドレス一覧 (GAL) の設定を変更する方法について説明します。

アドレス一覧に関連する追加の管理タスクについては、「[アドレス一覧の手順](address-list-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md)」の「アドレス一覧」。

  - Exchange Online の既定では、アドレス一覧の役割はどの役割グループにも割り当てられません。アドレス一覧の役割を必要とするコマンドレットを使用するには、その役割を役割グループに追加してください。詳細については、トピック「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - 既定の GAL の設定は編集できません。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して GAL のプロパティを構成する

この例は、GUID が 96d0c505-eba8-4103-ad4f-577a1bf4ad7b である GAL に FourthCoffee という新しい名前を割り当てます。

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee


> [!NOTE]
> 既定の条件付きフィルター プロパティを使用している場合、<EM>IncludedRecipients</EM> パラメーターの値を空白にすることはできません。



この例では、Fourth Coffee グローバル GAL に含まれる受信者を、所属する会社が Fourth Coffee に設定されている受信者に変更します。

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

構文およびパラメーターの詳細については、「[Set-GlobalAddressList](https://technet.microsoft.com/ja-jp/library/bb123877\(v=exchg.150\))」を参照してください。

