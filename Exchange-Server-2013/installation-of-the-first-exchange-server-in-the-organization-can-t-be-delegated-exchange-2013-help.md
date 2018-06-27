---
title: '組織の最初の Exchange サーバーのインストールを委任できない: Exchange 2013 Help'
TOCTitle: 組織の最初の Exchange サーバーのインストールを委任できない
ms:assetid: bd1dbf09-5465-40fa-8668-ef99f753ba45
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.delegatedbridgeheadfirstinstall(v=EXCHG.150)
ms:contentKeyID: 48269999
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織の最初の Exchange サーバーのインストールを委任できない

 

_**適用先:**Exchange Server_

_**トピックの最終更新日:**2014-11-05_

ログオン ユーザーが、組織に最初の Exchange 2013 サーバーをインストールするために必要なアカウントのアクセス許可を持っていないため、Microsoft Exchange Server 2013 セットアップ プログラムを続行できません。

Exchange 2013 セットアップ プログラムでは、2 番目以降のサーバーの役割のインストールに委任を使用できますが、組織内で最初の Exchange 2013 サーバーをインストールするときには、ログオン ユーザーが Enterprise Admins Windows セキュリティ グループのメンバーであることを必要とします。これが必要なのは、インストール中に Exchange 2013 セットアップ プログラムが Active Directory の Exchange Organization コンテナー内にオブジェクトを作成して構成するためです。


> [!NOTE]
> Exchange 2013 用の Active Directory スキーマをまだ準備していない場合は、ログオン ユーザーが Schema Admins Windows セキュリティ グループのメンバーであることも必要です。別の方法として、まず Schema Admins Windows グループのメンバーであるユーザーが Active Directory スキーマを準備した後で、Exchange 2013 をインストールすることもできます。



この問題を解決するには、ログオン ユーザーを Enterprise Admins セキュリティ グループのメンバーとして追加します。または、Enterprise Admins セキュリティ グループのメンバーであるアカウントにログオンします。その後、Exchange 2013 セットアップ プログラムを再度実行します。

問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

