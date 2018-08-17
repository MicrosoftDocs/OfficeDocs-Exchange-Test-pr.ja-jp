---
title: 'メールボックスの保存機能を有効にする: Exchange Online Help'
TOCTitle: メールボックスの保存機能を有効にする
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 49895314
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# メールボックスの保存機能を有効にする

 

_**適用先:** Exchange Online, Exchange Server 2013_

メールボックスの保存機能を有効にすると、該当するメールボックスのアイテム保持ポリシーまたは管理フォルダー メールボックス ポリシーの処理が中断されます。 保存機能は、休暇中や出張中などの状況に対応するためのものです。

保存機能が有効化されている間は、ユーザーは自分のメールボックスにログオンして、アイテムを変更または削除することができます。 メールボックス検索を実行した場合、削除済みアイテムの保存期間が過ぎた削除済みアイテムは検索結果には返されません。 ユーザーが変更または削除したアイテムを法的情報保留シナリオで保持するようにするには、メールボックスを法的情報保留にする必要があります。 詳細については、「[インプレース保持を作成または削除する](create-or-remove-an-in-place-hold-exchange-2013-help.md)」(英語) を参照してください。

保存機能を有効にしたメールボックスの保持コメントを含めることもできます。 保持コメントは、サポートするバージョンの Microsoft Outlook に表示されます。

メッセージング レコード管理 (MRM) に関連する追加の管理タスクについては、「[メッセージング レコード管理の手順](messaging-records-management-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 1 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

  - Exchange 管理センター (EAC) ではメールボックスの保存機能を有効にすることはできません。シェルを使用する必要があります。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## シェルを使用してメールボックスの保存機能を有効にする

この例では、Michael Allen のメールボックスの保存機能を有効にします。

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## シェルを使用してメールボックスの保存機能を削除する

この例では、Michael Allen のメールボックスから保存機能を削除します。

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

メールボックスの保存機能を正しく有効にできたことを確認するには、[Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\)) コマンドレットで、そのメールボックスの *RetentionHoldEnabled* プロパティを取得します。

このコマンドは Michael Allen のメールボックスの *RetentionHoldEnabled* プロパティを取得します。

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

このコマンドは、Exchange 組織の全メールボックスを取得して、保存機能が有効なメールボックスをフィルター処理し、それぞれに適用された保持ポリシーとともに一覧にします。


> [!IMPORTANT]
> <EM>RetentionHoldEnabled</EM> は、Exchange 2013 ではフィルター処理できるプロパティではないので、<EM>Filter</EM> パラメーターを <STRONG>Get-Mailbox</STRONG> コマンドレットで使用してサーバー側で保存機能を有効にしたメールボックスをフィルター処理することはできません。 このコマンドは、シェル セッションで実行しているクライアントのすべてのメールボックスとフィルターの一覧を取得します。 メールボックスが何千もある大規模な環境では、このコマンドは完了までに時間がかかることがあります。



    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

