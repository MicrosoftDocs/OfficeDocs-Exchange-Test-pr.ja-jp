---
title: 'クライアント アクセスの役割がローカル サイトで検出されない_ClientAccessRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: クライアント アクセスの役割がローカル サイトで検出されない_ClientAccessRoleNotPresentInSite
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 48269955
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# クライアント アクセスの役割がローカル サイトで検出されない\_ClientAccessRoleNotPresentInSite

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-06-05_

このトピックの内容は、Microsoft Exchange Server 2013 向けに更新されていません。まだ更新されていませんが、そのままで Exchange 2013 にも適用できる可能性があります。ヘルプが必要な場合は、以下のコミュニティ リソースを確認してください。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 セットアップ プログラムは、ローカルの Active Directory® ディレクトリ サービス サイトで既存のクライアント アクセスの役割を検出できない場合にこの警告を表示します。

Active Directory サイトにクライアント アクセスの役割のインスタンスをインストールする前に、メールボックス サーバーの役割をインストールすることを選択しています。

クライアント アクセス サーバーの役割では、さまざまなクライアントから Exchange 2007 サーバーへの接続を受け付けます。Microsoft Outlook Express や Eudora などのソフトウェア クライアントは、POP3 接続または IMAP4 接続を使用して Exchange サーバーと通信します。モバイル デバイスなどのハードウェア クライアントは、ActiveSync、POP3、または IMAP4 を使用して Exchange サーバーと通信します。

ユーザーが Microsoft Office Outlook® 以外のクライアントを使用して受信トレイにアクセスする場合は、Exchange 組織にクライアント アクセス サーバーの役割をインストールする必要があります。

ユーザーは Outlook を使用して自分のメールボックスにログオンできますが、ローカル Active Directory サイトにクライアント アクセスの役割がインストールされるまでは、Outlook Web Access やモバイル デバイスを使用して同一のメールボックスにアクセスすることはできません。

