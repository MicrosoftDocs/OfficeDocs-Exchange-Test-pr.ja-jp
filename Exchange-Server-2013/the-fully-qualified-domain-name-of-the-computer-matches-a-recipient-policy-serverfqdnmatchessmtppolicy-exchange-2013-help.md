---
title: 'コンピューターの完全修飾ドメイン名と受信者ポリシーが一致している_ServerFQDNMatchesSMTPPolicy: Exchange 2013 Help'
TOCTitle: コンピューターの完全修飾ドメイン名と受信者ポリシーが一致している_ServerFQDNMatchesSMTPPolicy
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 48270241
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# コンピューターの完全修飾ドメイン名と受信者ポリシーが一致している\_ServerFQDNMatchesSMTPPolicy

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2016-12-09_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

ローカル コンピューターの完全修飾ドメイン名 (FQDN) が受信者ポリシーの SMTP (Simple Mail Transfer Protocol) アドレスと一致するため、Microsoft® Exchange Server 2007 セットアップ プログラムを続行できません。

Microsoft Exchange セットアップ プログラムを実行するには、Exchange 組織内にあるサーバーの FQDN が、同じ Exchange 組織内で設定されている受信者ポリシーのいずれの SMTP アドレスとも異なっている必要があります。

コンピューターの FQDN が受信者ポリシーの SMTP アドレスと一致すると、SMTP を介したメールの転送に失敗し、MTA キューに保持される可能性があります。

この問題を解決するには、ローカル コンピューターの名前を変更するか、または受信者ポリシーを削除するか名前を変更し、Microsoft Exchange セットアップ プログラムを再実行します。

**ローカル コンピューターの名前を変更するには、次の操作を行います。**

1.  **\[コントロール パネル\]** の **\[システム\]** を開きます。

2.  \[**コンピューター名**\] タブで、\[**変更**\] をクリックします。

3.  **\[コンピューター名\]** ボックスにそのコンピューターの新しい名前を入力し、**\[OK\]** をクリックします。ドメイン内でそのコンピューターの名前を変更するためのユーザー名とユーザー パスワードを入力するよう求められます。

4.  **\[OK\]** をクリックして、**\[システムのプロパティ\]** ダイアログ ボックスを閉じます。コンピューターを再起動して変更を適用するよう求められます。


> [!IMPORTANT]
> 名前を変更するコンピューターがドメイン コントローラーの場合は、ドメイン コントローラーの名前の変更についてのページ (<A href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</A>) を参照してください (このサイトは英語の場合があります)。



**受信者ポリシーの SMTP アドレスを変更するには、次の操作を行います。**

1.  Exchange システム マネージャーを起動します。

2.  **\[組織\]** をクリックし、**\[受信者\]** をクリックします。次に、**\[受信者ポリシー\]** をクリックします。

3.  変更するポリシーをダブルクリックします。

4.  **\[電子メール アドレス\]** タブをクリックし、目的の SMTP アドレスを変更します。

受信者ポリシーの名前付けに関する問題の詳細については、Microsoft サポート技術情報の文書番号 288175「\[XCON\] 受信者ポリシーは組織のサーバーの FQDN とは異なる必要がある (5.4.8 NDR)」([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052&kbid=288175)) を参照してください。

