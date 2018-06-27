---
title: 'SMTP アドレス指定形式はサポートされていない_SMTPAddressLiteral: Exchange 2013 Help'
TOCTitle: SMTP アドレス指定形式はサポートされていない_SMTPAddressLiteral
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 48269971
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# SMTP アドレス指定形式はサポートされていない\_SMTPAddressLiteral

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

指定された受信者ポリシーが、サポートされていない SMTP (Simple Mail Transfer Protocol) アドレス形式を使用しているため、Microsoft Exchange Server 2007 および Exchange Server 2010 のセットアップ プログラムを続行できません。

Exchange 2007 および Exchange Server 2010 のセットアップ プログラムを実行するには、電子メール アドレス ポリシーに使用されるすべての SMTP アドレスに、*user@\[10.10.1.1\]* などの IP アドレス リテラルが含まれていないことが必要です。

この問題を解決するには、受信者ポリシー内の SMTP アドレスの値を、IP アドレス リテラルを含まないように変更します。IP アドレス リテラルの角かっこ (\[\]) と数字 (10.10.1.1) を、*user@contoso.com* のようなドメイン ネーム システム (DNS) の名前の形式に置き換えます。

Exchange Server 2007 における受信者ポリシーの管理の詳細については、電子メール アドレス ポリシーの管理についてのページ ([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653)) を参照してください (このサイトは英語の場合があります)。

Exchange Server 2010 における受信者ポリシーの管理の詳細については、電子メール アドレス ポリシーの管理についてのページ ([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519)) を参照してください (このサイトは英語の場合があります)。

