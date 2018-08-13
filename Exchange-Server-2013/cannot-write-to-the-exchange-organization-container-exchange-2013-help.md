---
title: 'Exchange 組織コンテナーに書き込めない: Exchange 2013 Help'
TOCTitle: Exchange 組織コンテナーに書き込めない
ms:assetid: 17c4667b-7db1-4e0a-b824-1f6d51d980a9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/ms.exch.setupreadiness.globalserverinstall(v=EXCHG.150)
ms:contentKeyID: 48269211
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 組織コンテナーに書き込めない

 

_**適用先:** Exchange Server_

_**トピックの最終更新日:** 2014-11-05_

ログオン ユーザーが Active Directory ディレクトリ サービス内の組織コンテナーに書き込むために必要なアカウントのアクセス許可を持っていないため、Microsoft Exchange Server 2013 セットアップ プログラムを続行できません。

セットアップを行うには、Exchange 2013 のインストール時にログオンしているユーザーが、Active Directory のオブジェクトを作成および変更するアクセス許可を持っている必要があります。組織において Exchange 2013 セットアップを初めて実行する場合は、使用するアカウントが Schema Admins グループおよび Enterprise Admins グループのメンバーである必要があります。セットアップを初めて実行するときに Exchange 2013 の Active Directory が準備されるため、これらのアクセス許可が必要になります。Active Directory が準備された後に、追加の Exchange 2013 サーバーをインストールするために使用するアカウントは、Organization Management 管理役割グループのメンバーである必要があります。

この問題を解決するには、ログオン ユーザーに適切なアクセス許可を与えるか、またはこれらのアクセス許可を持つアカウントを使用してログオンした後、Exchange 2013 セットアップを再度実行します。


> [!IMPORTANT]
> Exchange 2013 のフォレストをまたいだインストールはサポートされていません。Exchange 2013 をインストールしようとしている Active Directory フォレストのメンバーであるアカウントを使用してください。



問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542)、 または [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

探しているものは見つかりましたか？検索したい情報に関する[フィードバックを送信](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback)してください。

