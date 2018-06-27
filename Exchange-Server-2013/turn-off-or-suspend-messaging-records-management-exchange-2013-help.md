---
title: 'メッセージング レコード管理を無効化または中断する: Exchange 2013 Help'
TOCTitle: メッセージング レコード管理を無効化または中断する
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52057819
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メッセージング レコード管理を無効化または中断する

 

_**適用先:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**トピックの最終更新日:**2013-02-14_

個々の要件、IT 要件、またはビジネス要件を満たすため、個々のユーザーまたはメールボックス サーバーのメッセージング レコード管理 (MRM) を無効にするか、一時的に中断することが必要となる場合があります。次のような理由によって、MRM を無効にしたり、中断したりする必要性が生じます。

  - メールボックス ユーザーが会社にいない場合、または別の理由で電子メールにアクセスできない場合は、メールボックスの保存機能を有効にすることで、メールボックスの MRM を一時的に無効にすることができます。メールボックスの保存機能を有効にすると、メールボックスが管理フォルダー アシスタントで処理されなくなります。メールボックス ユーザーが戻るか、メールボックスに再度アクセスできるようになったときに、メールボックスから保存機能を削除できます。

  - パフォーマンスに関する問題をテストまたはトラブルシューティングする必要がある場合は、管理フォルダー アシスタントのスケジュールをクリアすることで、そのサーバー上の MRM を一時的に無効にすることができます。

  - メールボックスから保持タグを削除する必要がある場合 (メールボックスにそのタグが適用されたアイテム保持ポリシーがある場合) は、ポリシーからタグを削除できます。

  - アイテム保持ポリシーまたは管理フォルダー メールボックス ポリシーのメールボックスへの適用を中止する場合は、メールボックスからポリシーを削除できます。

  - 組織で MRM 機能を使用しないことにした場合は、組織全体で MRM を完全に無効にすることができます。後で MRM を展開する場合、その操作を実行できます。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分

  - このトピックの手順には、特定のアクセス許可が必要です。アクセス許可情報については、各手順を参照してください。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 必要な作業

## メールボックスの保存機能を有効にする

メールボックスの保存機能を有効にして、MRM を一時的に無効にすることができます (ユーザーが休暇中の場合など)。これにより、保存機能を無効にするまで、そのメールボックスのアイテム保持ポリシーの処理が中断されます。これは、メールボックスをインプレース保持または訴訟ホールドに置くこととは異なります。

メールボックスの保存機能を有効にする方法の詳細については、「[メールボックスの保存機能を有効にする](place-a-mailbox-on-retention-hold-exchange-2013-help.md)」を参照してください。

インプレース保持と訴訟ホールドの詳細については、「[インプレース保持と訴訟ホールド](in-place-hold-and-litigation-hold-exchange-2013-help.md)」を参照してください。

## メールボックスから保持タグを削除する

メールボックスから保持タグを削除するには、アイテム保持ポリシーからタグのリンクを解除します。既定フォルダーのアイテム保持ポリシー タグ (RPT) のリンクを解除すると、既定メールボックス タグがそのフォルダー内のすべてのアイテムに適用されます。個人タグのリンクを解除すると、ユーザーが使用できなくなります。既存のメッセージに適用されるタグは、Exchange 組織からタグを削除しない限り、引き続き処理されます。

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

このシェルの例では、保持タグ Delete - 3 Days のリンクをアイテム保持ポリシー Corp-Users から解除します。

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

構文およびパラメーターの詳細については、「[Get-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd298086\(v=exchg.150\))」と「[Set-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd335196\(v=exchg.150\))」を参照してください。

## メールボックスからアイテム保持ポリシーを削除する

この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「アイテム保持ポリシーを適用する」。

メールボックス ユーザーのプロパティからアイテム保持ポリシーを削除することで、ポリシーのメールボックスへの適用を停止できます。

このシェルの例では、メールボックス jpeoples からアイテム保持ポリシーを削除します。

    Set-Mailbox jpeoples -RetentionPolicy $null.

このシェルの例では、Exchange 組織内のすべてのメールボックスからアイテム保持ポリシーを削除します。

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

このシェルの例では、アイテム保持ポリシー Corp-Finance が適用されているすべてのメールボックス ユーザーからポリシーを削除します。

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」と「[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))」を参照してください。

## 組織全体で MRM を完全に無効にする

組織の MRM をオフにするには、Exchange セットアップで作成した ArbitrationMailbox ポリシーを除くすべての保持タグとアイテム保持ポリシーを削除します。これが完了すると、アイテム保持ポリシーは適用されなくなります。


> [!NOTE]
> また、アイテム保持ポリシーには、メッセージをユーザーのアーカイブ メールボックスに移動する [アーカイブに移動する] タグが含まれています。[アーカイブに移動する] タグがあるアイテム保持ポリシーを削除すると、そのポリシーが適用されたユーザーのメッセージは、管理フォルダー アシスタントによってアーカイブに移動されなくなります。<BR>これを防ぐには、[削除して回復を許可する] タグおよび [完全に削除] タグのみを組織から削除して、[アーカイブに移動する] タグがあるポリシーを適用し続けます。または、有効なアーカイブがあるユーザーは、Outlook または Outlook Web App を使用してアイテムを手動でアーカイブ メールボックスに移動することもできます。<BR>保持タグまたはアイテム保持ポリシーを削除する前に、削除するタグの設定を確認することをお勧めします。[アーカイブに移動する] 保持処理があるタグは削除しないでください。



この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。


> [!NOTE]
> 次のコマンドに <EM>WhatIf</EM> スイッチを含めると、コマンドによって実行される操作をシミュレートできます。



この例では、Exchange セットアップによって作成された ArbitrationMailbox ポリシーで使用される、\[削除しない\] タグを除くすべての削除タグを Exchange 組織から削除します。

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

この例では、\[削除しない\] タグを除くすべての保持タグを削除します。

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

このコマンドでは、Exchange 組織から Corp-Users 保持ポリシーが削除されます。

    Remove-RetentionPolicy Corp-Users

構文およびパラメーターの詳細については、以下のトピックを参照してください。

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/ja-jp/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/ja-jp/library/dd297962\(v=exchg.150\))

