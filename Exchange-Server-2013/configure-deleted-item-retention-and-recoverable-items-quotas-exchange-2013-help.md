---
title: '削除済みアイテムの保存期間と回復可能なアイテムのクォータを構成する: Exchange 2013 Help'
TOCTitle: 削除済みアイテムの保存期間と回復可能なアイテムのクォータを構成する
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50555885
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 削除済みアイテムの保存期間と回復可能なアイテムのクォータを構成する

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

ユーザーが Delete キー、Shift + Delete キー、または <strong>削除済みアイテム フォルダーを空にする</strong> 操作を使用して \[削除済みアイテム\] の既定フォルダーからアイテムを削除すると、アイテムは **Recoverable Items\\Deletions** フォルダーに移動します。削除済みアイテムがこのフォルダーに残される期間は、メールボックス データベースまたはメールボックスに対して構成された削除済みアイテムの保存期間の設定に基づきます。既定では、メールボックス データベースは削除済みアイテムを 14 日間保存するように構成され、回復可能なアイテムの警告クォータおよび回復可能なアイテムのクォータはそれぞれ 20 GB (ギガバイト) と 30 GB に設定されます。


> [!NOTE]
> 削除済みアイテムの保存期間が経過する前に、Microsoft Outlook および Microsoft OfficeOutlook Web App ユーザーは、削除済みアイテムの回復機能を使用して削除済みアイテムを回復することができます。この機能の詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=198206">削除済みアイテムを復元する</A>」(Outlook) または「<A href="https://go.microsoft.com/fwlink/p/?linkid=198207">削除済みアイテムの復元</A>」(Outlook Web App) を参照してください。



シェルを使用して、メールボックスまたはメールボックス データベースに対し、削除済みアイテムの保存期間の設定と回復可能なアイテムのクオータを構成することができます。メールボックスがインプレース保持または訴訟ホールドの対象となっている場合、削除済みアイテムの保存期間設定は無視されます。

削除済みアイテムの保存期間、\[回復可能なアイテム\] フォルダー、インプレース保持および訴訟ホールドの詳細については、「[\[回復可能なアイテム\] フォルダー](recoverable-items-folder-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 推定完了時間: 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「メッセージング レコード管理」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 削除済みアイテムの保存期間をメールボックス用に構成する

**EAC を使用してメールボックスの削除済みアイテムの保存期間を構成する**

1.  <strong>受信者</strong> \> <strong>メールボックス</strong> に移動します。

2.  リスト ビューで、メールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  メールボックス プロパティ ページで、<strong>メールボックスの使用状況</strong> をクリックし、次に <strong>追加オプション</strong> をクリックして、次のいずれかを選択します
    
      - <strong>メールボックス データベースの既定の保存期間設定を使用する</strong>   メールボックス データベースについて構成された削除済みアイテムの保存期間設定を採用する場合は、この設定を使用します。
    
      - <strong>このメールボックスの設定をカスタマイズする</strong>   メールボックスの削除済みアイテムの保存期間設定を構成する場合は、この設定を使用します。
        
        <strong>削除済みアイテムの保存期間 (日)</strong>   このボックスには、削除済みアイテムが永久に消去され、ユーザーが復元できなくなるまで保持される時間が表示されます。メールボックスが作成される場合、この値はメールボックスのデータベース用に構成される削除済みアイテムの保存期間の設定に基づきます。既定により、メールボックス データベースは、削除済みアイテムを 14 日間保持するよう構成されます。このプロパティの値の範囲は 0 から 24,855 日です。
    
      - <strong>データベースをバックアップするまでアイテムを完全に削除しない</strong>   メールボックスが存在するメールボックス データベースがバックアップされるまでメールボックスと電子メール メッセージが削除されないようにするには、このチェック ボックスをオンにします。

**シェルを使用してメールボックスの削除済みアイテムの保存期間を構成する**

この例では、April Stewart のメールボックスの削除済みアイテムを 30 日間保存するように構成します。

    Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30

構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## シェルを使用してメールボックスの回復可能なアイテムのクォータを構成する


> [!NOTE]
> EAC を使用してメールボックスの回復可能なアイテムのクォータを構成することはできません。



この例では、April Stewart のメールボックスの回復可能なアイテムの警告クォータを 12 GB に、回復可能なアイテムのクォータを 15 GB に構成します。

    Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false


> [!NOTE]
> 格納されているメールボックス データベースとは異なる回復可能なアイテムのクオータを使用するようにメールボックスを構成するには、<EM>UseDatabaseQuotaDefaults</EM> パラメーターを <CODE>$false</CODE> に設定する必要があります。



構文およびパラメーターの詳細については、「[Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))」を参照してください。

## シェルを使用してメールボックス データベースの削除済みアイテムの保存期間を構成する


> [!NOTE]
> EAC を使用してメールボックス データベースの削除済みアイテムの保存期間を構成することはできません。



この例では、メールボックス データベース MDB2 の削除済みアイテムの保存期間を 10 日間に構成します。

    Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10

構文およびパラメーターの詳細については、「[Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\))」を参照してください。

## シェルを使用してメールボックス データベースの回復可能なアイテムのクォータを構成する


> [!NOTE]
> EAC を使用してメールボックス データベースの回復可能なアイテムのクォータを構成することはできません。



この例では、メールボックス データベース MDB2 の回復可能なアイテムの警告クォータを 15 GB に、回復可能なアイテムのクォータを 20 GB に構成します。

    Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB

構文およびパラメーターの詳細については、「[Set-MailboxDatabase](https://technet.microsoft.com/ja-jp/library/bb123971\(v=exchg.150\))」を参照してください。

