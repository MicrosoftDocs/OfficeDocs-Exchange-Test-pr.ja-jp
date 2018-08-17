---
title: 'オフライン アドレス帳の更新: Exchange Online Help'
TOCTitle: オフライン アドレス帳の更新
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 49896224
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# オフライン アドレス帳の更新

 

_**適用先:** Exchange Server 2013_

OAB の作成後または OAB 設定の変更後は、OAB 生成 (OABGen) プロセスが完了するまでユーザーはその変更を使用できません。

OAB に関連するその他の管理タスクについては、「[オフライン アドレス帳の手順](offline-address-book-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。[電子メール アドレスおよびアドレス帳のアクセス許可](email-address-and-address-book-permissions-exchange-2013-help.md) の「オフライン アドレス帳」。

  - Exchange 管理センター (EAC) を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して OAB を更新する

この例では、My OAB という名前の OAB を更新します。

    Update-OfflineAddressBook -Identity "My OAB"

構文とパラメーターの詳細については、「[Update-OfflineAddressBook](https://technet.microsoft.com/ja-jp/library/aa995979\(v=exchg.150\))」を参照してください。

