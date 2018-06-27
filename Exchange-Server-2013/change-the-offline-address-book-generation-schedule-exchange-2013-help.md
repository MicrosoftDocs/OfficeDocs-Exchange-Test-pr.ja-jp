---
title: 'オフライン アドレス帳の生成スケジュールを変更する: Exchange 2013 Help'
TOCTitle: オフライン アドレス帳の生成スケジュールを変更する
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 49896492
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: MT
---

# オフライン アドレス帳の生成スケジュールを変更する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-12-05_

オフライン アドレス帳 (OAB) はダウンロードしたアドレス帳のコピーであり、Outlook ユーザーはサーバーに接続していないときでもアドレス帳の情報にアクセスできます。Set-MailboxServer コマンドレットで *OABGeneratorWorkCycle* パラメーターと *OABGeneratorWorkCycleCheckpoint* パラメーターを使用して、OAB を生成する頻度を構成できます。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。 [電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md) の「オフライン アドレス帳」。

  - Exchange 管理センター (EAC) を使用してこの手順を実行できません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して OAB プロパティを構成する

この例では、メールボックス サーバー MBXServer01 上で、オフライン アドレス帳が毎日 6 時間ごとに生成されます。

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

構文およびパラメーターの詳細については、「[Set-OfflineAddressBook](https://technet.microsoft.com/ja-jp/library/aa996330\(v=exchg.150\))」を参照してください。

