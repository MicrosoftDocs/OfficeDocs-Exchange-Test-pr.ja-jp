---
title: 'オフライン アドレス帳の作成: Exchange Online Help'
TOCTitle: オフライン アドレス帳の作成
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 49896428
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: HT
---

# オフライン アドレス帳の作成

 

_**適用先:** Exchange Online, Exchange Server 2013_

Exchange Server 2013 のオフライン アドレス帳 (OAB) は、アドレス帳のダウンロードされたコピーであり、Outlook のユーザーがサーバーに接続していないときでも情報にアクセスできます。Exchange 管理者は、オフラインで作業するユーザーが利用できるようにするアドレス帳を決定できます。また、アドレス帳の配布方法 (Web ベースの配布またはパブリック フォルダー配布) を構成することもできます。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 [電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md) の「オフライン アドレス帳」。

  - Exchange Online の既定では、アドレス一覧の役割はどの役割グループにも割り当てられません。アドレス一覧の役割を必要とするコマンドレットを使用するには、その役割を役割グループに追加してください。詳細については、トピック「[役割グループの管理](manage-role-groups-exchange-2013-help.md)」の「役割グループに役割を追加する」を参照してください。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して Web ベースの配布で OAB を作成する

この例では、既定の仮想ディレクトリを使用して、Outlook 2007 以降のクライアントに Web ベースの配布を使用する OAB\_Contoso という OAB を作成します。

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

構文およびパラメーターの詳細については、「[New-OfflineAddressBook](https://technet.microsoft.com/ja-jp/library/bb123692\(v=exchg.150\))」を参照してください。

