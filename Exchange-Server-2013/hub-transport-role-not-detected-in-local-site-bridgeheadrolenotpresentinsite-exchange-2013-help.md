---
title: 'ハブ トランスポートの役割がローカル サイトで検出されない_BridgeheadRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: ハブ トランスポートの役割がローカル サイトで検出されない_BridgeheadRoleNotPresentInSite
ms:assetid: f318c947-81a8-4c18-975a-0f1e7868042a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.bridgeheadrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 48270237
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ハブ トランスポートの役割がローカル サイトで検出されない\_BridgeheadRoleNotPresentInSite

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2012-06-05_

Microsoft® Exchange Server 2007 セットアップ プログラムは、ローカルの Active Directory® ディレクトリ サービス サイトで既存のハブ トランスポート サーバーの役割を検出できなかった場合にこの警告を表示します。

Active Directory サイトにハブ トランスポートの役割のインスタンスをインストールする前に、メールボックス サーバーの役割をインストールすることを選択しています。

Exchange 2007 ハブ トランスポート サービスは、組織の Active Directory 内に展開されます。ハブ トランスポート サービスは、組織内におけるすべてのメール フローを処理し、組織のメール フローに関するルーティング規則を適用して、受信者のメールボックスにメッセージを配信する役割を果たします。

ユーザーは自分のメールボックスにはログオンできますが、ハブ トランスポートの役割がインストールされるまで、このメールボックス サーバーとの間でメールの送受信を行うことはできません。

