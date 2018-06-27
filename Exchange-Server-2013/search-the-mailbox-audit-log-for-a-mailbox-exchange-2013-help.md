---
title: 'メールボックスのメールボックス監査ログを検索する: Exchange 2013 Help'
TOCTitle: メールボックスのメールボックス監査ログを検索する
ms:assetid: 5b518a08-3b51-4ba3-bfbd-0e35cc5ff374
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff461930(v=EXCHG.150)
ms:contentKeyID: 49896271
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスのメールボックス監査ログを検索する

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2012-10-03_

メールボックスのメールボックス監査ログのエントリを同期的に検索して、検索結果をシェルに表示できます。

複数のメールボックスに対してメールボックス監査ログを検索し、結果を指定したアドレスにメールで送信する場合は、メールボックス監査ログの検索を代わりに作成する必要があります。詳細については、「[メールボックス監査ログの検索を作成する](create-a-mailbox-audit-log-search-exchange-2013-help.md)」を参照してください。

メールボックス監査ログに関連する追加の管理タスクについては、「[メールボックス監査ログの手順](mailbox-audit-logging-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「メールボックス監査ログ」エントリ。

  - 既定では、すべてのメールボックスに対してメールボックス監査ログは無効になっています。 監査するメールボックスそれぞれについて監査ログを有効にし、監査を行うメールボックスの所有者、代理人、または管理者の操作を指定する必要があります。詳細については、「[メールボックスのメールボックス監査ログを有効または無効にする](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)」を参照してください。

  - EAC を使用して、メールボックスのメールボックス監査ログを検索することはできません。 ただし、EAC を使用して所有者以外のメールボックス アクセス レポートを実行または検索およびエクスポートできます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用して、メールボックスのメールボックス監査ログを検索する

シェルを使用してメールボックスのメールボックス監査ログを検索する方法の例は、「[Search-MailboxAuditLog](https://technet.microsoft.com/ja-jp/library/ff522360\(v=exchg.150\))」の「[Examples](https://technet.microsoft.com/ja-jp/ff522360\(exchg.150\)#examples)」を参照してください。

