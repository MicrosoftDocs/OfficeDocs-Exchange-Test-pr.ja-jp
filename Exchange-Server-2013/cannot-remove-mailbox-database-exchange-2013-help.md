---
title: 'メールボックス データベースを削除できない: Exchange 2013 Help'
TOCTitle: メールボックス データベースを削除できない
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 48269529
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス データベースを削除できない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2012-11-08_

ローカル サーバーからユーザー メールボックス データベースを削除するとデータが失われる可能性があるため、Microsoft Exchange Server 2013 セットアップ プログラムは作業を続行できません。

Exchange 2013 セットアップ プログラムは、メールボックス サーバーの役割を削除する前に、サーバーからすべてのメールボックス データベースが削除されているかどうかを判断します。ただし、ユーザーのメールボックスがまだサーバーに残っている可能性があります。

この問題を解決するには、サーバー上のメールボックスを別の Exchange サーバーに移動します。また、メールボックスとメールボックスに含まれているデータが必要ない場合は、メールボックスを無効にします。その後、Exchange 2013 セットアップ プログラムを再度実行します。

  - データベースでメールボックスを識別する方法の詳細については、「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」を参照してください。

  - メールボックスを移動する方法の詳細については、「[Exchange 2013 でのメールボックスの移動](mailbox-moves-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - メールボックスを無効にする方法の詳細については、「[Disable-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997210\(v=exchg.150\))」を参照してください。

  - メールボックス データベースを削除する方法の詳細については、「[Exchange 2013 のメールボックス データベースの管理](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

