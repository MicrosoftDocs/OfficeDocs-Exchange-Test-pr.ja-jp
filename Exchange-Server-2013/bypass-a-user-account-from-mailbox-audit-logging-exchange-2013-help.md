---
title: 'メールボックス監査ログからユーザー アカウントをバイパスする: Exchange 2013 Help'
TOCTitle: メールボックス監査ログからユーザー アカウントをバイパスする
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 49896382
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックス監査ログからユーザー アカウントをバイパスする

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2013-05-21_

メールボックスのメールボックス監査ログを有効にすると、指定されたメールボックス アクセス イベント (フォルダーまたはメッセージへのアクセス、メッセージの完全な削除など) がログに記録されます。ただし、サード パーティのツールで使用されるアカウントや、法令に基づく監視に使用されるアカウントなどの承認されたアカウントによるアクセスは、大量のメールボックス監査ログ エントリを作成する可能性がある上、組織にとって興味がないものである可能性があります。

メールボックス監査ログをバイパスするようにユーザーまたはコンピューター アカウントを構成して、そのユーザーまたはアカウントがメールボックスに対して行った操作がログに記録されないようにすることができます。メールボックスに頻繁にアクセスする必要がある信頼されたユーザーまたはコンピューター アカウントをバイパスすることで、メールボックス監査ログのノイズを減少できます。


> [!NOTE]
> メールボックス監査ログを使用してメールボックスへのアクセスと操作を監査する場合は、メールボックス監査バイパス アソシエーションを定期的に監視する必要があります。あるアカウントに対してメールボックス監査バイパス アソシエーションが追加された場合、そのアカウントは、アクセス許可が割り当てられている組織内の任意のメールボックスにアクセスでき、こうしたアクセスや実行された操作 (メッセージの削除など) に対してメールボックス監査ログ エントリが作成されることはありません。



メールボックス監査ログに関連する追加の管理タスクについては、「[メールボックス監査ログの手順](mailbox-audit-logging-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」トピックの「メールボックス監査ログ」エントリ。

  - メールボックス監査ログをバイパスするようにアカウントが構成されると、そのアカウントによるすべてのメールボックスへのアクセスがログに記録されなくなります。特定のメールボックスへのアクセスのログをバイパスするようにアカウントを構成することはできません。

  - Exchange 管理センター (EAC) を使用してアカウントのメールボックス監査ログのバイパスを有効または無効にすることはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## シェルを使用してアカウントのメールボックス監査ログのバイパスを有効または無効にする

アカウントに対するメールボックス監査ログのバイパスを有効にする方法については、「[Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/ja-jp/library/ff696758\(v=exchg.150\))」の「[Examples](https://technet.microsoft.com/ja-jp/ff696758\(exchg.150\)#examples)」で例を参照できます。

アカウントに対するメールボックス監査ログのバイパスを無効にする方法については、「[Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/ja-jp/library/ff696758\(v=exchg.150\))」の「[Examples](https://technet.microsoft.com/ja-jp/ff696758\(exchg.150\)#examples)」で例を参照できます。

## 正常な動作を確認する方法

メールボックス監査ログからユーザー アカウントをバイパスした後に、[Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/ja-jp/library/ff696741\(v=exchg.150\)) コマンドレットを実行して、バイパス設定を確認できます。

メールボックス監査バイパス関連付けを確認する方法の例については、「[Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/ja-jp/library/ff696741\(v=exchg.150\))」の「[Examples](https://technet.microsoft.com/ja-jp/ff696741\(exchg.150\)#examples)」を参照してください。

