---
title: 'ストレージ グループ ドライブの仕様が見つからない_MailboxLogDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: ストレージ グループ ドライブの仕様が見つからない_MailboxLogDriveDoesNotExist
ms:assetid: fe210f29-60cb-4d34-877e-1356a21dc02a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.mailboxlogdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 48270286
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ストレージ グループ ドライブの仕様が見つからない\_MailboxLogDriveDoesNotExist

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

このサーバーの以前のインストールで使用されたストレージ グループ データベース ドライブの仕様にアクセスできないため、Microsoft® Exchange Server 2007 障害回復セットアップ プログラムを続行できません。

Microsoft Exchange 障害回復セットアップ プログラムを実行するには、以前このサーバーに対して使用したものと同じストレージ グループ データベース ドライブの仕様が、復元時に使用できる必要があります。

この問題を解決するには、ドライブを元の論理ドライブ構成に一致するように構成した後、Microsoft Exchange 障害回復セットアップ プログラムを再実行します。

**ドライブ文字の割り当てまたは変更**

1.  <strong>コンピューターの管理(ローカル)</strong> を開きます。

2.  コンソール ツリーで、<strong>コンピューターの管理 (ローカル)</strong> をクリックし、<strong>記憶域</strong> をクリックします。次に、<strong>ディスクの管理</strong> をクリックします。

3.  パーティション、論理ドライブ、またはボリュームを右クリックし、<strong>ドライブ文字とパスの変更</strong> をクリックします。

4.  次のいずれかの手順を実行します。
    
      - ドライブ文字を割り当てるには、<strong>追加</strong> をクリックします。次に、使用するドライブ文字をクリックし、<strong>OK</strong> をクリックします。
    
      - ドライブ文字を変更するには、そのドライブ文字をクリックし、<strong>変更</strong> をクリックします。次に、使用するドライブ文字をクリックし、<strong>OK</strong> をクリックします。

ドライブ文字を割り当てる方法の詳細については、ドライブ文字の割り当て、変更、または削除についてのページ ([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764)) を参照してください (このサイトは英語の場合があります)。

