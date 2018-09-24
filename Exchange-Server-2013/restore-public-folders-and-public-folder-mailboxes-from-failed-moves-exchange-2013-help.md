---
title: '失敗した移動からパブリック フォルダーとパブリック フォルダー メールボックスを復元する: Exchange 2013 Help'
TOCTitle: 失敗した移動からパブリック フォルダーとパブリック フォルダー メールボックスを復元する
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52057807
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 失敗した移動からパブリック フォルダーとパブリック フォルダー メールボックスを復元する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2013-02-13_

パブリック フォルダーまたはパブリック フォルダー メールボックスの移動要求が失敗した場合は、次の条件に当てはまるときに限り、フォルダーまたはメールボックスを復元できます。

  - **パブリック フォルダー移動の失敗**   回復可能な削除によって削除されたパブリック フォルダーのコピーが元のパブリック フォルダー メールボックスに存在し、保存期間内にある。

  - **パブリック フォルダー メールボックス移動の失敗**   回復可能な削除によって削除されたパブリック フォルダー メールボックスのコピーが元のメールボックス データベースに存在し、メールボックス保存期間内にある。

メールボックス保存期間が過ぎると、それぞれのパブリック フォルダー メールボックスをバックアップから回復できるようになります。その後、復元されたメールボックスからデータを抽出して、ターゲット フォルダーにコピーするか、別のメールボックスと結合することができます。詳細については、「[回復用データベースを使用してデータを復元する](restore-data-using-a-recovery-database-exchange-2013-help.md)」を参照してください。

パブリック フォルダーに関するその他の管理タスクについては、「[パブリック フォルダーの手順](public-folder-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「メールボックス復元要求」。

  - EAC を使用してこの手順を実行することはできません。シェルを使用する必要があります。

  - 復元要求を作成するには、回復可能な削除によって削除されたパブリック フォルダー メールボックス用に、*DisplayName*、*LegacyDN*、または *MailboxGUID* パラメーターに値を指定する必要があります。

  - 既定では、収集フォルダーは通常のフォルダーと共に復元されます。これは、*ExcludeDumpster* パラメーターを使用して回避できます。

  - パブリック フォルダー メールボックスの復元は通常のメールボックスの復元とは異なり、フォルダーは、対象のメールボックス内に存在しない場合作成されません。見つからないフォルダーは、復元要求の最後に警告メッセージに表示されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 回復可能な削除によって削除されたパブリック フォルダーを復元する

この例では、パブリック フォルダー \\Dev\\CustomerEnagagements が対象のパブリック フォルダー メールボックス Development01 に復元されます。

  ```powershell
  New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements
  ```

構文およびパラメーターの詳細については、「[New-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829875\(v=exchg.150\))」を参照してください。

## 回復可能な削除によって削除されたパブリック フォルダー メールボックスを復元する

この例では、パブリック フォルダー メールボックス PF\_Singapore が新しいパブリック フォルダー メールボックス PF\_Singapore\_Restore に復元されます。

  ```powershell
  New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch
  ```

構文およびパラメーターの詳細については、「[New-MailboxRestoreRequest](https://technet.microsoft.com/ja-jp/library/ff829875\(v=exchg.150\))」を参照してください。

